```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>HTML Image</title>
    </head>
        <body>
            <a href="index.html">인덱스 페이지</a>
            
            <h1>이미지 태그</h1>
            
            <!--같은 웹 서버에 포함된 이미지 넣기 -->
            <img src="images/197-300x300.jpg" alt="기찻길" />
            <img src="images/481-300x300.jpg" alt="호수" />
            
            <!-- 외부 서버에 있는(웹 상에 있는) 이미지 넣기 -->
            <img src="https://picsum.photos/300" alt="Lorem Picsum" />
            
            <h1>이미지 링크</h1>
            <!-- 이미지를 클릭하면 다음(Daum) 홈페이지로 이동 -->
            <a href="https://www.daum.net">
                <img src="images/daum_logo.png" alt="다음" style="width: 100px;" />
            </a>
            
            <!-- 이미지를 클릭하면 네이버(Naver) 홈페이지로 이동 -->
            <a href="https://www.naver.com">
                <img src="images/naver_logo.png" alt="네이버" style="width: 100px;" />
            </a>
            
        </body>
</html>
```