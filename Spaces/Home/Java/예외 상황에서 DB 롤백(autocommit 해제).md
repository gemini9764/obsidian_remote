**==@Transactional(roobackFor = {Exception.class})==**  //모든 예외상황에서 롤백(checked Exception)
public DataType functionName() throws Exception{
	--Codes--
	==DefaultTransactionDefinition def = new DefaultTransactionDefinition();==
	==def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);==
	==TransactionStatus txtStatus = txManager.getTransaction(def);==
	--Codes--
	//필요한 경우마다 commit과 rollback을 실행
	==txManager.commit(txStatus);==
	==txManager.rollback(txStatus);	==

}