
UiPath RE-Framework(Refinement-Enhanced Framework)는 로봇 프로세스 자동화(RPA)를 위한 강력한 템플릿입니다. 이 프레임워크는 다양한 비즈니스 프로세스를 안정적으로 자동화하고 관리하는 데 필요한 모범 사례와 구조를 제공합니다. RE-Framework의 주요 특징은 다음과 같습니다:

1. **모듈화된 구조**: RE-Framework는 4개의 주요 상태로 구성됩니다: Initialization, Get Transaction Data, Process Transaction, End Process. 이러한 모듈화된 구조 덕분에 각 단계에서 로직을 쉽게 추가하거나 수정할 수 있습니다.
    
2. **강력한 예외 처리**: 예외 처리 메커니즘이 잘 구축되어 있어 예상치 못한 오류가 발생했을 때 이를 효율적으로 처리하고 재시도할 수 있습니다.
    
3. **로그 및 모니터링**: 프레임워크는 자동화된 작업의 로그를 체계적으로 관리하여 문제 발생 시 신속하게 원인을 파악하고 대응할 수 있게 해줍니다.
    
4. **재시도 메커니즘**: 트랜잭션이 실패할 경우 재시도를 통해 안정성을 높이고, 일정 횟수 이상 실패 시 이를 로깅하고 프로세스를 종료합니다.
    
5. **구성 파일 및 설정**: Config 파일을 통해 환경 설정과 변수들을 쉽게 관리할 수 있습니다. 이는 다양한 환경에서 동일한 프로세스를 유연하게 실행할 수 있게 합니다.
    
6. **데이터 및 큐 통합**: UiPath Orchestrator와의 통합을 통해 큐 기반으로 데이터를 처리할 수 있습니다. 이를 통해 대량의 트랜잭션을 효과적으로 관리할 수 있습니다.
    

RE-Framework는 이러한 기능들을 통해 복잡한 비즈니스 프로세스를 안정적으로 자동화할 수 있도록 설계되었습니다. 이를 통해 개발자는 보다 신뢰할 수 있는 자동화 솔루션을 빠르게 구축할 수 있습니다.


# [구조 및 설명] 
# (Entry -> Exit > Transition)
# [Initialization]
@ If first run, read local configuration file
- InitAllSettings - 딕셔너리 셋팅 (Name , Value)
- KillAllProcesses - 열린프로그램 종료
- Mail 계정 / 경로 설정 / 카피 파일
- Add Log Fields (for debug)  
- 01_TransactionDT생성
(InitAllSettings / Initialization(처음에 딱한번) - *어디에 처리할지 정하기) 

@ If maxConsecutiveSystemExceptions exceeded 
- MaxConsecutiveSystemExceptions (excel value)

@ InitiAllApplications - place holder 

(Cataches)
@ Assign SystemException

(Tracnsition)
successful -> Get Transation Data 
System Exception (failed initialization) -> End Process 

# [Get Transaction Data]
// TransactionItem - DataRow

@ Check Stop Signal - Orchestrator 통신
@ GetTransactionData - in_TransactionNumber(default 1)/*io_dt_TransactionData(row=3)
// in_TransactionNumber<=io_dt_TransactionData.RowCount -> (than io_dt_TransactionData(in_TransactionNumber-1)
-> out_TransactionItem -> [Process Transaction]

(Tracnsition)
New Transaction -> Get Transaction Data
No Data (TransactionItem = Nothin)  -> End Process

# [Process Transaction]
@ Process (*주로이부분만 건든다) 
> 02_Chrome_ExctactShoppingDT.xaml
> 03_Excel_WriteShoppingDT.xaml

@ SetTransactionStatus (Success) - flow chat

(Tracnsition)
System Exception -> [Initialization] / RetryNumber+1
Business Exception -> [Get Transaction Data] > 1번아이템이 실패해도 다음 아이템 실행 
Success(System/Business Exception = Nothing)  > [Get Transaction Data] *다음 item
(io_TransactionNumber +1)

# [End Process]
@ SendMail - 인수화 


![image](https://github.com/jaegyuyoo/automation/assets/57005741/1cd2c7f0-fa71-4629-a974-72aba1778c12)
