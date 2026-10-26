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
