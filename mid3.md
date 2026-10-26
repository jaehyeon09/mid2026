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
