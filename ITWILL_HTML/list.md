```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>HTML List</title>
    </head>
        <body>
            <a href="index.html">인덱스 페이지</a>
            
            <h1>Unordered List</h1> <!-- 순서가 없는 리스트(목록) -->
            <ul style="list-style: circle;"> <!-- unordered list -->
                <li>무빙</li> <!-- list item -->
                <li>이두나!</li>
                <li>마스크걸</li>
            </ul>
            
            <h1>Ordered List</h1> <!-- 순서가 있는 리스트(목록) -->
            <ol style="list-style: decimal;">
                <li>무빙</li>
                <li>이두나!</li>
                <li>마스크걸</li>
            </ol>
            
            <h1>Description List</h1> <!-- 사전식 리스트(목록). 용어와 설명을 갖는 목록. -->
            <dl>
                <dt>HTML</dt> <!-- description term: 용어. -->
                <dd>Hyper-Text Markup Language</dd> <!-- description definition: 설명, 정의. -->
                <dd>웹 페이지의 정적 컨텐츠를 작성하는 프론트엔드 개발 언어</dd>
                
                <dt>CSS</dt>
                <dd>Cascading Style Sheet</dd>
                <dd>웹 페이지의 스타일을 작성하는 프론트엔드 개발 언어</dd>
                
                <dt>JavaScript</dt>
                <dd>웹 페이지의 동적인 기능, 이벤트 처리 등을 담당하는 프론트엔드 개발 언어</dd>
            </dl>
            
        </body>
</html>
```