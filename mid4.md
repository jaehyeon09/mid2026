***4번 문제 답안***
**프롬프트:4번문제는 [문제 2] 아스키 피라미드 패턴 출력 (중첩 반복문)
- 평가 범위: 2주차 (반복문, 패턴 그리기)
- 문제: 높이 N을 입력받아 중앙 정렬된 피라미드 형태의 문자 패턴을 출력하시오.
- 조건:
- 홀수 번째 행은 *, 짝수 번째 행은 #으로 출력합니다.
- 입출력 예시 (N=4):
   *
  ###
 *****
####### 이거인데 visual studio로 실행될 수 있어야 하고 C언어로 작성해야해 어렵지않게 작성해줘
```c
#include <stdio.h>

int main(void)
{
    int N, i, j;

    printf("높이 입력: ");
    scanf_s("%d", &N);

    for (i = 1; i <= N; i++)
    {
        for (j = 1; j <= N - i; j++)
            printf(" ");

        for (j = 1; j <= 2 * i - 1; j++)
        {
            if (i % 2 == 1)
                printf("*");
            else
                printf("#");
        }

        printf("\n");
    }

    return 0;
}
```
<img width="294" height="158" alt="mid4 md" src="https://github.com/user-attachments/assets/925f840d-d8f0-4584-927b-86820203593f" />
