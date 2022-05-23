### python 패키지 설치
- pytest
- JayDeBeApi
  - JPype1

net.ucanaccess.jdbc.UcanaccessDriver

### 설치
- DBeaver ([dbeaver.io](https://dbeaver.io))

### 참고사항
- jdbc를 이용한 접속은 ucanaccess 사용
- [ucanaccess.sourceforge.net](http://ucanaccess.sourceforge.net/site.html)
- DB 브라우저
  - DBeaver ([dbeaver.io](https://dbeaver.io))
  - intellij : 별도의 드라이버 설정이 필요


C:\Users\haroo\anaconda3\condabin\conda.bat activate IdeaProjects
C:\Users\haroo\anaconda3\condabin\conda.bat deactivate
### 조회 예제

```python
from sqlalchemy import create_engine
file_path = r"jdbc:ucanaccess://C:\Users\haroo\IdeaProjects\windows_agent\resource\test\PSM3000_SITE.MDB"
engine = create_engine(f'access+pyodbc://{file_path}')
```