```c
#include <stdio.h>
#include <sqlite3.h>

/* 검색 결과 출력 함수 */
int callback(void *data, int argc, char **argv, char **colName)
{
    int i;

    for (i = 0; i < argc; i++)
    {
        printf("%s: %s\n",
            colName[i],
            argv[i] ? argv[i] : "NULL");
    }

    return 0;
}

int main(void)
{
    sqlite3 *db;
    char *errMsg = 0;
    char sql[200];
    int id;
    int result;

    /* 1. 데이터베이스 열기 */
    result = sqlite3_open("student.db", &db);

    if (result != SQLITE_OK)
    {
        printf("데이터베이스 열기 실패\n");
        return 1;
    }

    printf("데이터베이스 연결 성공!\n");

    /* 2. 테이블 생성 */
    result = sqlite3_exec(db,
        "CREATE TABLE IF NOT EXISTS Student ("
        "id INTEGER PRIMARY KEY, "
        "name TEXT, "
        "major TEXT);",
        0, 0, &errMsg);

    if (result != SQLITE_OK)
    {
        printf("테이블 생성 실패: %s\n", errMsg);
        sqlite3_free(errMsg);
        sqlite3_close(db);
        return 1;
    }

    /* 3. 학생 4명 저장 */
    result = sqlite3_exec(db,
        "INSERT OR IGNORE INTO Student VALUES"
        "(1, 'Kim', 'Computer'),"
        "(2, 'Lee', 'Design'),"
        "(3, 'Park', 'Math'),"
        "(4, 'Choi', 'English');",
        0, 0, &errMsg);

    if (result != SQLITE_OK)
    {
        printf("데이터 저장 오류: %s\n", errMsg);
        sqlite3_free(errMsg);
        sqlite3_close(db);
        return 1;
    }

    printf("학생 데이터 등록 완료!\n");

    /* 4. 학번 검색 */
    printf("\n검색할 학번을 입력하세요: ");
    scanf("%d", &id);

    sprintf(sql,
        "SELECT * FROM Student WHERE id = %d;", id);

    printf("\n[검색 결과]\n");

    result = sqlite3_exec(db, sql,
        callback, 0, &errMsg);

    if (result != SQLITE_OK)
    {
        printf("검색 오류: %s\n", errMsg);
        sqlite3_free(errMsg);
    }

    /* 5. 데이터베이스 닫기 */
    sqlite3_close(db);

    return 0;
}
```
