# hover시, 설명DIV가 뜨는 애니메이션

## 1. preview

<img src="https://j.gifs.com/P7k2y2.gif" />


## 2. 코드 분석

### 1) html


#### (1) item안에 img, caption을 자식요소로 둔다.

```html
<body>
    <div class="items">
      <div class="item">
        <img
          style="width:300px;"
          src=""
          alt=""
        />
        <div class="caption">
          
          <!--상세내용을 담는 공간  -->
          <h2>title</h2>
          <p>
            asdasdasdasdasdasdas dasdasdasdasdasdasd
          </p>
          <p>price : <s>$12</s> -> $10</p>    
          <a href="">상세보기</a>
        </div>
      </div>
    </div>
  </body>
```

<br/><br/>

### 2) css

#### (1) 화면 변동에 따라, 자식 요소의 위치를 절대 위치으로 유지시킨다.
- 부모요소의 `position : relative`로 하고, 자식요소의 `position : absolute`로 한다.
- 자식요소의 위치를 `top`, `left` 등을 이용하여 위치를 정한다. 
- 결과적으로 `img`태그 위에 `caption`태그가 항상 위에 있는 상태가 된다.
- 사용자가 `item`에 `hover`하면 `caption`의 `투명도가 0->1`이 되면서 설명이 보인다.

```css
      a {                         /*a 태그의 디자인*/
        color: #222;   
        text-decoration: none;
      }
      .items {                    /*item요소를 감싸는 부모요소*/
        border: 1px solid while;
        text-align: center;       /*내부 글자 배치를 중앙정렬*/
      }

      .item {                     /*내용을 담는 item요소*/
        display: inline-block;    /*여러 요소들을 일렬로 나열 */
        width: 300px;
        height: 300px;
        position: relative;       /*내부 요소의 고정 위치 설정(1)*/
      }
```

<br/>

#### (2) padding을 해도 크기 고정시키기와 이벤트 넣기
- 요소에 padding을 넣게 되면, 해당 padding값만큼 크기가 늘어난다.
- 이를 방지하기 위해 `box-sizing: border-box` 설정을 해준다.

- `transition: 0.5s`를 넣어 `caption`에 이벤트가 발생하여 0.5초 딜레이 후 발생시킨다.
- 투명도가 처음에는 0이었지만 어떤 이벤트가 발생하면 0.5초뒤에 1로 변한다.

```css
      .caption {
        width: 300px;
        height: 300px;
        background-color: #000;
        position: absolute;       /*내부 요소의 고정 위치 설정(2)*/
        top: 0;
        left: 0;
        color: #fff;
        padding: 20px;
        box-sizing: border-box;  /* 300x300 안에 padding이 적용되도록 함 */
        padding-top: 40px;
        opacity: 0;              /* 투명도가 처음에는 0이었지만 어떤 이벤트가 발생하면 0.5초뒤에 발생함*/
        transition: 0.5s;        /*caption에 이벤트가 발생하여 0.5초 딜레이 후 발생시킴*/
      }
 
      .item:hover .caption {    
        opacity: 1;
      }
      .caption a {
        color: #fff;
        background-color: teal;
        padding: 7px;
        border-radius: 3px;
      }
      .caption a:hover {
        background-color: #fff;
        color: #000;
      }

```




