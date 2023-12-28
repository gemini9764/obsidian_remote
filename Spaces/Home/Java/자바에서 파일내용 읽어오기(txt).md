- **Http 통신을 활용해서 파일 내용 읽어오기**
	- MultipartHttpServletRequest multipartRequest = (MultipartHttpServletRequest) req;
        String fileName = multipartRequest.getParameter("fileName");
        
        MultipartFile mfile = multipartRequest.getFile(fileName);
        
        InputStream is = mfile.getInputStream();
        InputStreamReader isr = new InputStreamReader(is);
        BufferedReader bis = new BufferedReader(isr);
      
        String read = "";
		while ((read = bis.readLine()) != null) {
			System.out.println("################111   "+read);
		}
