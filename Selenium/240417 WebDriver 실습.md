1. 크롬 드라이버 다운 
	https://chromedriver.chromium.org/downloads

2. WebDrive 실습
	```python
	from selenium import webdriver
	from selenium.webdriver.chrome.service import Service
	
	# ChromeOptions 객체 생성
	options = webdriver.ChromeOptions()
	options.add_argument('headless')
	options.add_argument("no-sandbox")
	options.add_argument('window-size=1920x1080')
	options.add_argument("disable-gpu")
	options.add_argument("lang=ko_KR")
	options.add_argument('user-agent=Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/61.0.3163.100 Safari/537.36')
	
	# Chrome 드라이버 경로 설정 및 드라이버 생성
	s = Service('./chromedriver.exe')
	driver = webdriver.Chrome(service=s, options=options)
	
	# 웹 페이지에 접근
	driver.get('https://naver.com')
	driver.implicitly_wait(3)
	driver.get_screenshot_as_file('capture_naver.png')
	
	# 드라이버 종료
	driver.quit()
```

3. 결과 - capture화면 생성
	![스크린샷 2024-04-17 171943](https://github.com/jaegyuyoo/myboard/assets/57005741/61733d27-3909-48fc-9a34-18244b82b680)
