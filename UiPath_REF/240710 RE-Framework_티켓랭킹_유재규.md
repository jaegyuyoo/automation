

[Initialization]
- 템플릿 파일 복사하여, 결과 파일 생성 (티켓랭킹_오늘날짜_유재규)
- 수신한 메일에서 처리할 항목을 가져온다(오류 데이터 포함)
	mail subject(나중에 메일발송용-*수신메일의날짜사용), 추출데이터(DT추출용)  
	엑셀 전처리 (엑셀에 / 저장이안되어 _로 변환 작업)

[Process Transaction]
- 항목별 추출하여 각시트 기입 (DT방식)
- 본문에 처리 성공/실패 여부 기재

[End Process]
- 엑셀파일 첨부하여 메일발송 
- 제목에 본인이름 기재
- 메일 기재날짜는 수신 메일의 날짜 사용
- 제목과 본문은 String.Format을 활용
- 각 항목의 1위 데이터 취합 본문 테이블 삽입 
- 수행 성공/실패 항목 본문 기재
- 총 수행 건수 성공/실패 건수 입력 


# Process 부분 

<img width="212" alt="image" src="https://github.com/jaegyuyoo/automation/assets/57005741/de240169-68cf-4524-88b1-4a6257a6c6bd">

// 이중 for 문 - uielement를 통해 DT추출 

![[Pasted image 20240710160731.png]]

// 정규화를 통해 데이터 분리

startDate = System.Text.RegularExpressions.Regex.Match(info, "(\d{4}\.\d{2}\.\d{2})~").Groups(1).Value
endDate = System.Text.RegularExpressions.Regex.Match(info, "~(\d{4}\.\d{2}\.\d{2})").Groups(1).Value
location = System.Text.RegularExpressions.Regex.Match(info, "\d{4}\.\d{2}\.\d{2}\n(.+)").Groups(1).Value