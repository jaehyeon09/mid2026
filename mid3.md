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
