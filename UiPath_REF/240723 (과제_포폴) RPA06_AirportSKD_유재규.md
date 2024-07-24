
# 요구사항 및 초기설계 / 일정 

	**목표  (데이터가공) 데이터테이블을 쪼개고, 합치고**
	
	- 수신한 메일에서 처리 파일 다운로드
	다운로드 받을 파일 경로 : Data\Input\yyyyMMdd(메일 제목에 있는 날짜로 폴더 생성)
	- 양식 파일을 Copy하여 결과파일 생성
	 저장 경로 : Data\Output
	 파일명 : AirportSKD_(본인이름).xlsx

	- 각각의 파일을 불러와, 데이터를 가공하여 결과데이터를 생성한다
	가공1: 운항요일 컬럼 삭제
	가공2: 운항기간을 운항시작일과 운항종료일로 분리
	가공3: 목적지에 있는 3자리코드(Code_IATA)를 4자리(Code_ICAO)코드로 변경
	가공4: 터미널 종류에 따라 DT를 분리 (South Terminal = Cargo(S) / North Terminal = Cargo(N)) 
	가공5: North Terminal에는 운항시작일 컬럼을 남기고, South Terminal에는 운항종료일 컬럼을 남김

	(선택)
	메일을 읽어 올 때, 처리할 데이터가 없으면 End Process로 보낼 것
	Switch 액티비티를 사용해 볼 것
	FlowChart 액티비티를 사용해 볼 것
	메일 발송 시 성공, 실패 여부 로직 추가
# 워크플로우 구성(JOB)]
### Initialization
	01_TransactionDT_Generate
		- 반복 item생성 (SKD_SFO, SKD_MNL, SKD_SIN)
		- (R)양식 파일을 Copy하여 결과파일 생성
		저장 경로 : Data\Output
		 파일명 : AirportSKD_(본인이름).xlsx

	02_ReceiveMail_ExtractDate
		- 첨부다운(input), 저장(output), 파일명 지정
		- *메일읽어올떄 
		- (R)수신한 메일에서 처리 파일 다운로드
		다운로드 받을 파일 경로 : Data\Input\yyyyMMdd(메일 제목에 있는 날짜로 폴더 생성)
### Get Transaction Data

### Process Transaction 
	03_ExtractDT_Excel
		- item반복하여 엑셀 3개 하나씩 추출
		- (R)각각의 파일을 불러와, 데이터를 가공하여 결과데이터를 생성한다
		가공1: 운항요일 컬럼 삭제
		가공2: 운항기간을 운항시작일과 운항종료일로 분리
		가공3: 목적지에 있는 3자리코드(Code_IATA)를 4자리(Code_ICAO)코드로 변경
		가공4: 터미널 종류에 따라 DT를 분리 (South Terminal = Cargo(S) / North Terminal = Cargo(N)) 
		가공5: North Terminal에는 운항시작일 컬럼을 남기고, South Terminal에는 운항종료일 컬럼을 남김

	04_Excel_WriteDT
## End Process
	06_SMTP_SendMail
		- 추출날짜활용 + String.Format

# Feedback & Comment
