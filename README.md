# blog

hugo 설치 후 hugo 폴더에 blog 와 handnew04.github.io를 받아서 사용할 각각의 폴더 필요<br>
<br>
지금 현재를 예로 들면<br>
<br>
Hugo 폴더 내에 myblog 폴더와 page 폴더가 있음<br>
myblog - blog.git<br>
page - handnew04.github.io.git<br>
<br>
포스트 생성시 my blog 터미널에서 hugo new post/제목.md<br>
포스트 확인시 myblog 터미널에서 hugo server 후 인터넷 localhost:1313 접속 <br>
실제 사이트 생성 myblog 터미널에서 hugo -d ../page -> page 폴더에 사이트 생성<br>
<br>
두 폴더의 내용 다 git push <br>
