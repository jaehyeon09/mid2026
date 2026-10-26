***3번 답안***
***프롬프트 : [문제 1] 숫자야구 판정 로직 (기초 입출력 및 조건문)
- 평가 범위: 1주차 (변수, 연산자, 조건문)
- 문제: 정답 숫자 3개(중복 없음)와 사용자가 입력한 숫자 3개가 주어질 때, 볼(Ball)과 스트라이크(Strike) 개수를 계산하여 출력하는 프로그램을 작성하시오.
- 조건:
- 숫자와 위치가 모두 맞으면 Strike, 숫자는 맞지만 위치가 다르면 Ball입니다.
- 3 Strike일 경우 "HOMERUN"을 추가로 출력합니다.
- 입력 예시: 1 2 3 (정답) / 1 3 5 (입력)
- 출력 예시: 1 Strike, 1 Ball 이 코드를 시험문제여서 작성해야하는데 visual studio에서 실행 할 수 있어야하고 C언어로 작성해야해***
```c
#include <stdio.h>

int main(void)
{
    int answer[3] = {1, 2, 3};
    int input[3];
    int strike = 0, ball = 0;
    int i, j;

    printf("숫자 3개를 입력하세요: ");
    scanf_s("%d %d %d", &input[0], &input[1], &input[2]);

    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
        {
            if (answer[i] == input[j])
            {
                if (i == j)
                    strike++;
                else
                    ball++;
            }
        }
    }

    printf("%d Strike, %d Ball\n", strike, ball);

    if (strike == 3)
        printf("HOMERUN\n");

    return 0;
}
```
<img width="281" height="119" alt="mid3 md" src="https://github.com/user-attachments/assets/05a3a9f7-87f3-4b27-b3d7-77a02bc88de2" />
<img width="297" height="96" alt="mid3-1 md" src="https://github.com/user-attachments/assets/fb07ee45-ab8e-4f9b-bad7-e08b4518a444" />
