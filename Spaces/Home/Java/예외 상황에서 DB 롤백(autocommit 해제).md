/**
	 * 동일대체 저장
	 */
	@RequestMapping(value = "checkUpdateInsert.do")
	==@Transactional(rollbackFor = {Exception.class})==
	public NexacroResult ccsCurSave(@ParamDataSet(name = "ds_list") DataSet ds_list) throws Exception {
		NexacroResult result = new NexacroResult();
		List<DataResultMap> dsList = NexaComUtil.getDataResultMapList(ds_list);
		Map<String, Object> paramMap = new HashMap<String, Object>();
		//결과전송용 ds
		DataSet dsResult = new DataSet("ds_result");
		dsResult.addColumn("code", PlatformDataType.INT);
		dsResult.addColumn("deptNm", PlatformDataType.STRING);
		dsResult.addColumn("sbNm", PlatformDataType.STRING);
		int nRow = dsResult.newRow();
		
		==DefaultTransactionDefinition def = new DefaultTransactionDefinition();==
		==def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);==
		==TransactionStatus txStatus = txManager.getTransaction(def);==
		
		for(int i=0; i<dsList.size(); i++) {
			String strSbRelRcd = MapUtils.getString(dsList.get(i), "sbRelRcd");
			String strSaCd = MapUtils.getString(dsList.get(i), "spvsDeptCd");
			String strSbCd = MapUtils.getString(dsList.get(i), "sbCd");
			String strKeyDate = MapUtils.getString(dsList.get(i), "begDt");
			
			paramMap.clear();
			paramMap.put("strSbCd", strSbCd);
			paramMap.put("strKeyDate", strKeyDate);
			
			//동일, 선수 가능 여부 파악
			Map<String, Object> checkResult = this.selectOne(NAME_SPACE, "getStdCcsSubRelCheckCL10100023", paramMap);
			int checkCount = Integer.parseInt(MapUtils.getString(checkResult, "chkCount"));
				
			//동일, 선수 가능한 교과목이 아닐 때
			if(checkCount < 1) {
				dsResult.set(nRow, "code", 1);
				dsResult.set(nRow, "deptNm", MapUtils.getString(dsList.get(i), "spvsDeptNm"));
				dsResult.set(nRow, "sbNm", MapUtils.getString(dsList.get(i), "sbNm"));
				result.addDataSet(dsResult);
				break;
			}
			//데이터 관리자에게 문의하세요
			else if(checkCount > 1) {
				dsResult.set(nRow, "code", -1);
				dsResult.set(nRow, "deptNm", MapUtils.getString(dsList.get(i), "spvsDeptNm"));
				dsResult.set(nRow, "sbNm", MapUtils.getString(dsList.get(i), "sbNm"));
				result.addDataSet(dsResult);
				break;
			}
			//순환참조확인
			if(!("CL1010003".equals(strSbRelRcd) || "CL1010004".equals(strSbRelRcd))){
				try {
					this.insert(NAME_SPACE, "insert", dsList.get(i));
					paramMap.clear();
					paramMap.put("strSaCd", strSaCd);
					paramMap.put("strSbCd", strSbCd);
					paramMap.put("strKeyDate", strKeyDate);
					List<Map<String, Object>> loopCheck = this.selectList(NAME_SPACE, "loopRelationSubDataCheck", paramMap);
					txManager.commit(txStatus); //Exception이 없으면 commit
				}	
				catch(Exception e) {
					dsResult.set(nRow, "code", 0);
					dsResult.set(nRow, "deptNm", MapUtils.getString(dsList.get(i), "spvsDeptNm"));
					dsResult.set(nRow, "sbNm", MapUtils.getString(dsList.get(i), "sbNm"));
					result.addDataSet(dsResult);
					txManager.rollback(txStatus);	//Exception이 있으면 rollback
				}
			}	
		}
		return result;
	}