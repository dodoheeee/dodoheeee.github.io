---
layout: single
title: 리액트 select option 태그 경고 해결하기
subtitle: 리액트에서 마크업을 하게 된다면 알아야할 점!
tags: [리액트, 삽질]
toc: true
toc_label: "목차"
toc_sticky: true
categories: React
author_profile: false
sitemap: true
header:
  teaser: /assets/images/0606/1.png
---

<br/>
<br/>

<p align="center"  style="color:#8E99AB; font-size :18px">안녕하세요! 도도히 입니다! <br/>
최근에 겪었던 리액트 warning 메세지에 대해서 알아보려고 합니다.<br/>
사실 그냥 경고메세지라 넘어가도 되는데 console창에 빨간글씨를 못 참는 편이기 때문에...😅 <br/>
블로그 타고타고 타고 다니다가 좀 바로 이해 되게 찾아본 블로그는 없어서 직접 정리해보았습니다!</p>

<br/>

---

<br/>

# ⚠️ 리액트 Select Option 태그 경고

내가 마주했던 에러는...<br/>

> Warning: Use the 'defaultValue' or 'value' props on select instead of setting 'selected' on option

대충 읽었을땐, 아 `select`에 defaultValue 값을 넣어줘야하는구나 싶어서 빈 스트링이라도 프로퍼티를 넣어줬다. 하지만 해결되지 않았다ㅎ

해석해보면 "경고: 'selected' 속성을 옵션에 설정하는 대신, `select` 요소에 'defaultValue' 또는 'value' props를 사용하세요."
라는 뜻이다.

![ex_screenshot](/assets/images/0606/1.png)

<br/>

```javascript
<select defaultValue={""} id="font">
  <option value="" disabled selected>
    Choose Font
  </option>
  <option value="Comic Sans MS, Comic Sans, cursive">Font 1</option>
  <option value="Arial Narrow, sans-serif">Font 2</option>
  <option value="Chalkduster, fantasy">Font 3</option>
</select>
```

리액트에서는 `select` 요소를 렌더링할 때, 옵션을 선택하기 위해 'selected' 속성을 사용하는 대신에, 'defaultValue' 또는 'value' props를 사용해야한다.

'selected' 속성을 사용하면 초기 렌더링 시 옵션을 선택하는 것은 가능하지만, 사용자가 다른 옵션을 선택할 때 `select` 요소의 값이 변경되지 않는 문제가 발생할 수 있기 때문이다.

그래서 내 코드에 문제점은,
코드에 defalutValue가 빈 스트링인 상태이고,
첫번째 `option`안에 value도 빈 스트링인데
첫번째 `option`값이 'selected'로 선택됨 상태로 되어있는게 문제 인 것 같았다.

<br/>

# 💡 해결

```javascript
<select defaultValue={"Choose Font"} id="font">
  <option value="Choose Font" disabled>
    Choose Font
  </option>
  <option value="Comic Sans MS, Comic Sans, cursive">Font 1</option>
  <option value="Arial Narrow, sans-serif">Font 2</option>
  <option value="Chalkduster, fantasy">Font 3</option>
</select>
```

<br/>

원인을 파악한 후에,

1. 첫번째 `select` 태그는 당연히 첫번째 `option`이랑 같게 할 목적이었으니까 defalutValue를 첫번째 옵션값으로 지정해줬다.
2. 첫번째 `option`값의 value를 defalutValue와 똑같이 설정해두었다.
3. select에 defalutValue를 설정해줬으니까, `option` 태그에 selected 프로퍼티는 빼줘도 되서 빼줬다.

그랬더니, 경고메세지는 뜨지 않았다! 오예!!ㅎㅎㅎㅎ

<br/>
<br/>
<br/>
<br/>

<p align="center"  style="color:#8E99AB; font-size :18px">블로그까지 찾아와주신 분들에게 도움이 되었음 좋겠습니다!🙇‍♀️ </p>

<br/><br/>
