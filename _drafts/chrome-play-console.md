

# https://developer.mozilla.org/en-US/docs/Web/API/Console

크롬 개발자도구에서 사용하는 console 을 정리해 보았어요 :)

보통 `console.log()`, `console.error()` 를 제일 많이 사용했지만 여러가지가 있다는 것을 알고 궁금해서 정리하게 되었어요. 'ㅅ'/

모든 예제는 MDN 에 나온 내용이에요. 자세한 내용은 제목의 링크를 타고 들어가서 확인해 주세요.

![List]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console01.png )

## [Assert](https://developer.mozilla.org/en-US/docs/Web/API/Console/assert){: target="_blank"}

if 문을 쓰지않고 assert 안에서 if 문처럼 사용할 수 있음.

```javascript
console.assert( assertion, ... );
```

- assertion

    bool 타입으로 거짓이면 console 에 다음 내용을 기록

- ...

    콤마(,) 로 구분지어서 string, int, array, object 모두 출력

> 예제
 
`number % 2 === 0` 이 아니라면 뒤의 내용들을 콘솔에 보여줌

```javascript
const errorMsg = 'the # is not even';
for (let number = 2; number <= 5; number += 1) {
    console.log( 'the # is ' + number );
    console.assert( number % 2 === 0, "test", 1234, {number: number, errorMsg: errorMsg} );
}
```

![Assert]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console02.png )

## [Clear](https://developer.mozilla.org/en-US/docs/Web/API/Console/clear){: target="_blank"}

console 내용을 모두 지움

```javascript
console.clear();
```

![Clear]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console03.png )

## [Count](https://developer.mozilla.org/en-US/docs/Web/API/Console/count){: target="_blank"}

호출 된 횟수를 출력

```javascript
console.count( a );
```

![Count]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console04.png )

![Count]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console05.png )

## [CountReset](https://developer.mozilla.org/en-US/docs/Web/API/Console/countReset){: target="_blank"}

호출 된 횟수를 리셋

```javascript
console.countReset( a );
```

## [Dir](https://developer.mozilla.org/en-US/docs/Web/API/Console/dir){: target="_blank"}

객체를 보기 편하게 보여줌

```javascript
console.dir( a );
```

![Dir]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console06.png )

```javascript
let test = { 1: 2, 3: 4 };
console.dir( test );
Object
    1: 2
    3: 4
    __proto__: Object
```

## [Error](https://developer.mozilla.org/en-US/docs/Web/API/Console/error){: target="_blank"}

에러를 출력

아래 예제는 같은 의미로 쓰임

```javascript
console.error( a );
console.exception( a );
```

![Error]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console07.png )

## [Group](https://developer.mozilla.org/en-US/docs/Web/API/Console/group){: target="_blank"}

```javascript
console.group();
console.warn();
console.groupEnd();
```

![Group]( {{ site.img_url }}/{{ page.categories }}/chrome-play-console08.png )

```javascript
console.log("This is the outer level");
console.group();
console.log("Level 2");
console.group();
console.log("Level 3");
console.warn("More of level 3");
console.groupEnd();
console.log("Back to level 2");
console.groupEnd();
console.log("Back to the outer level");
```