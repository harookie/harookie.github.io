배포 환경별로 Nexus등 저장소가 별도로 구축되어 있을경우
환경별 저장소 url을 변경해줄수 있다.

1. 환경별 URL 설정 변수 추가
2. URL 태그내의 URL을 변수를 이용해 변경되도록 placeholder로 변경

pom.xml 내용중 필요한 내용만 발췌해 전후를 비교하면 아래와 같다.

![비교]

[비교]: ../img/_single_pic/2021-05-14-maven-프로파일별-repo-url지정.png