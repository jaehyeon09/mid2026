### 2번 답안
### 프롬프트:SQLite를 활용한 간단한 DB를 설계하고 구현하시오(시나리오는 각자 만들어서 하시오, 반드시 3명 이상의 데이터를 넣고, 검색을 포함해야 합니다.) 이게 중간고사 문제인데 이걸 C언어로 작성하고 visual studio로 실행할 수 있어야해
```c
#include <stdio.h>
#include "sqlite3.h"

int main(void)
{
    sqlite3 *db;
    sqlite3_stmt *stmt;
    int result;
    int id;

    /* 1. 데이터베이스 열기 */
    result = sqlite3_open("student.db", &db);

    if (result != SQLITE_OK)
    {
        printf("데이터베이스 열기 실패\n");
        return 1;
    }

    printf("데이터베이스 연결 성공!\n");

    /* 2. 학생 테이블 만들기 */
    result = sqlite3_exec(db,
        "CREATE TABLE IF NOT EXISTS Student ("
        "id INTEGER PRIMARY KEY,"
        "name TEXT,"
        "major TEXT);",
        NULL, NULL, NULL);

    if (result != SQLITE_OK)
    {
        printf("테이블 생성 실패\n");
        sqlite3_close(db);
        return 1;
    }

    /* 3. 학생 4명 저장하기 */
    result = sqlite3_exec(db,
        "INSERT OR IGNORE INTO Student VALUES"
        "(1, 'Kim', 'Computer'),"
        "(2, 'Lee', 'Design'),"
        "(3, 'Park', 'Math'),"
        "(4, 'Choi', 'English');",
        NULL, NULL, NULL);

    if (result != SQLITE_OK)
    {
        printf("데이터 저장 실패\n");
        sqlite3_close(db);
        return 1;
    }

    printf("학생 데이터 등록 완료!\n");

    /* 4. 검색할 학번 입력 */
    printf("\n검색할 학번을 입력하세요: ");

    if (scanf("%d", &id) != 1)
    {
        printf("잘못된 입력입니다.\n");
        sqlite3_close(db);
        return 1;
    }

    /* 5. 학번으로 학생 검색 */
    result = sqlite3_prepare_v2(db,
        "SELECT * FROM Student WHERE id = ?;",
        -1, &stmt, NULL);

    if (result != SQLITE_OK)
    {
        printf("검색 준비 실패\n");
        sqlite3_close(db);
        return 1;
    }

    sqlite3_bind_int(stmt, 1, id);

    printf("\n[검색 결과]\n");

    result = sqlite3_step(stmt);

    if (result == SQLITE_ROW)
    {
        printf("학번: %d\n",
            sqlite3_column_int(stmt, 0));

        printf("이름: %s\n",
            sqlite3_column_text(stmt, 1));

        printf("전공: %s\n",
            sqlite3_column_text(stmt, 2));
    }
    else
    {
        printf("해당 학생을 찾을 수 없습니다.\n");
    }

    /* 6. 종료 */
    sqlite3_finalize(stmt);
    sqlite3_close(db);

    return 0;
}
```
<img width="372" height="225" alt="mid2 md" src="https://github.com/user-attachments/assets/0ad0e17c-b6a8-47f6-bfb9-076973bac6c6" />
