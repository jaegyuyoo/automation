

![image](https://github.com/user-attachments/assets/1953dec5-b8bd-4a04-930c-8c17a7480c2e)
![image](https://github.com/user-attachments/assets/b545bca7-2a60-4e91-b831-d08292747518)
1. **하위 워크플로우 (`RethrowExample.xaml`)**:
    
    - `Try` 블록에서 `Throw` 활동을 사용하여 새로운 예외를 발생시킵니다. 예외 메시지는 "An error occurred"입니다.
    - `Catch` 블록에서 예외를 잡고, `WriteLine` 활동을 사용하여 "Exception caught!" 메시지를 로그에 기록합니다.
    - `Rethrow` 활동을 사용하여 예외를 다시 던집니다.
    - `Finally` 블록에서 `WriteLine` 활동을 사용하여 "Finally block executed." 메시지를 로그에 기록합니다.
2. **상위 워크플로우 (`Main.xaml`)**:
    
    - `Try` 블록에서 `InvokeWorkflowFile` 활동을 사용하여 `RethrowExample.xaml`을 호출합니다.
    - `Catch` 블록에서 예외를 잡고, `WriteLine` 활동을 사용하여 "Rethrow: " & exception.Message 메시지를 로그에 기록합니다.

### 실행 결과 확인

이제, 예제 워크플로우를 실행하면 다음과 같은 로그 메시지를 확인할 수 있어야 합니다:

1. 하위 워크플로우에서 `Throw` 활동에 의해 예외가 발생합니다.
2. 하위 워크플로우의 `Catch` 블록에서 예외가 잡히고 "Exception caught!" 메시지가 기록됩니다.
3. 하위 워크플로우의 `Finally` 블록이 실행되고 "Finally block executed." 메시지가 기록됩니다.
4. `Rethrow` 활동에 의해 예외가 다시 던져집니다.
5. 상위 워크플로우의 `Catch` 블록에서 예외가 잡히고 "Rethrow: An error occurred" 메시지가 기록됩니다.

이 과정을 통해 `Throw`와 `Rethrow` 활동이 제대로 작동하는지 확인할 수 있습니다.