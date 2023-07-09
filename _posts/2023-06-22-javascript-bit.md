---
layout: single
title: 자바스크립트 비트 연산자 알고 쓰기!
subtitle: 무심코 썼던 것들을 다시 익혀보자!
tags: [자바스크립트]
toc: true
toc_label: "목차"
categories: Javascript
author_profile: false
sitemap: true
toc: true
header:
  teaser: https://miro.medium.com/v2/resize:fit:1400/1*ahpxPO0jLGb9EWrY2qQPhg.jpeg

---

<br/>
<br/>

<p align="center"  style="color:#8E99AB; font-size :18px">안녕하세요! 도도히 입니다! <br/>회사에서 필터 기능을 만들때마다 아주 자주 다뤘던 연산자인데<br/>
제대로 익히지 않고 쓰다보니, 오랜만에 보니까 물어봤을때 "어..? 뭐더라" 하고 설명을 못해버렸어요😞<br/>
자바스크립트에서 꽤나 중요한 부분이라 이건 블로그감이다! 하고 블로그를 쓰러 찾아왔습니다😋</p>

<br/>

---

<br/>

먼저 비트 연산자를 알아보기 전에! 과연 우리는 비트에 대해서 잘 알고 있을까?

# 📌 비트 (bit)

> 컴퓨터에서 사용하는 가장 작은 데이터 단위.<br/> 하나의 비트는 2진수 1 또는 0으로 표현되어 데이터를 처리, 저장, 전송 할 때 사용된다.

bit는 binart digit의 약자이다.<br/>
컴퓨터는 전자 스위치로 구성된 전기 장치라서,<br/>
전자식 스위치를 이용해서 데이터를 전달하는 것이 기본적이다.<br/>
컴퓨터는 단순 전기적 신호에 대해서만 반응하기 때문에 on / off (1 또는 0) 으로 해석할 수 있다.

그래서! 컴퓨터는 의사소통을 할때, 두가지의 상태 2진수의 0 과 1 형태만 이해하고 사용할 수 있다.<br/>
이 형태를 2진수라고 부르거나, 비트(Bit)라고 부른다.<br/>

<br/>

# 📌 비트 연산자

> 비트 연산자(bitwise operator)는 논리 연산자와 비슷하지만, 비트(bit) 단위로 논리 연산을 수행합니다.

## 비트 연산자 종류

![ex_screenshot](/assets/images/0626/1.png)

### AND 연산자(&)

> A, B 값이 둘다 1이어야 1을 출력.

비트 AND 연산자는 대응되는 두 비트가 모두 1일 때만 1을 반환하며, 다른 경우는 모두 0을 반환한다.

![ex_screenshot](/assets/images/0626/2.png)

### OR 연산자(|)

> A, B 값이 둘 중 하나가 1이면 1을 출력.

비트 OR 연산자는 대응되는 두 비트 중 하나라도 1이면 1을 반환하며, 두 비트가 모두 0일 때만 0을 반환한다.

![ex_screenshot](/assets/images/0626/3.png)

### XOR 연산자(^)

> A, B 값이 서로 다르면 1을 출력.

비트 XOR 연산자는 대응되는 두 비트가 서로 다르면 1을 반환하고, 서로 같으면 0을 반환한다.

![ex_screenshot](http://www.tcpschool.com/lectures/img_php_bitwise_xor.png)

### NOT 연산자(~)

> 비트 값이 0이면 1을 출력. 1이면 0을 출력.

비트 NOT 연산자는 해당 비트가 1이면 0을 반환하고, 0이면 1을 반환한다.

![ex_screenshot](http://www.tcpschool.com/lectures/img_php_bitwise_not.png)

<br/>

# 💡 비트연산자로 다중 선택 filter 구현하기!

나는 일반 1개만 클릭하는 필터일땐, 비트연산자를 활용해서 필터를 구현하지 않는 편이다.<br/>
그런데, 다중 선택일 경우엔 비트 연산자 방법을 한번만 익히면 활용하기 편리하고 쉽다.<br/>
다만 비트와,비트연산자에 대해서 잘 모른다면 방법이 조금 까다로울 수 있다.<br/>

**⚠️ 주의 ⚠️**<br/>
서버가 필터 타입을 number로 관리할때 사용하기 편리하다!<br/>
서버가 string 타입으로 필터를 관리한다면, 이 방법은 좋지 않을수도?!

## 1. 필터타입을 정의해준다.

나는 타입스크립트를 사용해서 개발을 했기 때문에<br/>
타입스크립트의 `enum` 기능을 사용해서<br/>
각 필터 타입에 이진수 값을 기반으로 한 숫자값을 정의해줬다.<br/>

```javascript
export enum FilterType {
    NONE = 0, //아무것도 선택 안됐을때,
    COMPLETION = 1, //완료
    INCORRECT = 2, //금액이 맞지 않음
    NOTISSUED = 4, // 미완료
    ALL = 7, // 전체 선택 (COMPLETION,INCORRECT,NOTISSUED 합산 값)
}
```

## 2. view에 다중필터를 만들어준다.

체크박스의 state값의 조건식을 clickFilter에서 구현했던 식 그대로 사용하고,<br/>
체크박스를 클릭했을때의 함수실행시에 Argument값에 (클릭한 필터 값)을 넣어주면 된다!<br/>

```html
<UI.Widgets.Filter.BasicFilter filterOptions={[ { value: "완료", state:
(filterStatus & FilterType.COMPLETION) === FilterType.COMPLETION, onClick: () =>
clickFilter(FilterType.COMPLETION), }, { value: "금액 상이", state:
(filterStatus & FilterType.INCORRECT) === FilterType.INCORRECT, onClick: () =>
clickFilter(FilterType.INCORRECT), }, { value: "미발행", state: (filterStatus &
FilterType.NOTISSUED) === FilterType.NOTISSUED, onClick: () =>
clickFilter(FilterType.NOTISSUED), }, ]} />
```

## 3. 필터를 관리할 함수를 만들어준다.

```javascript
 clickFilter: (clickedFilterType: FilterType) => {
    if ((filteredStatus & clickedFilterType) === clickedFilterType) {
        setFilteredStatus(filteredStatus - clickedFilterType)
    } else {
        setFilteredStatus(filteredStatus + clickedFilterType)
    }
},
```

`clickFilter` 함수를 살펴보면, Parameter 값으로 클릭한 `filterType`이 들어온다.

`if ((filteredStatus & clickedFilterType) === clickedFilterType)` 조건을 해석해야 필터를 구현할 수 있다.

지금 내가 쓴 코드에선 비트연산자 중에 AND 연산자를 사용한 것이다.<br/>
현재 filterStatus 의 초기값이 7 (ALL 전체선택) 이고,<br/>
클릭한 필터의 값을 1 (COMPLETION 완료) 를 눌렀다고 예시를 들어보자.<br/>

### 🎙 해석

만약 `7 & 1 === 1` 이라면 <br/>
현재 `필터타입 - 클릭한 필터타입` 으로 필터 state값을 변경해주고,<br/>
아니라면, `필터타입 + 클릭한 필터타입` 으로 필터 state값을 변경해줘.<br/>

### ✏️ 이진법 계산

일단 계산을 할때 2진수의 자리마다의 값이 의미하는 것을 알아야한다.

![ex_screenshot](https://mblogthumb-phinf.pstatic.net/MjAyMDA2MTBfMzUg/MDAxNTkxNzg3NTE5OTA4.qeyWttB5ROGwxjIVn_IWU-qzldk8hlzBF-eI0Lw8ZTIg.hy2tt_G040Xv9AbmuhcSosklJVqgyFDqaS4UDnUNvYkg.PNG.skyboy7863/image.png?type=w800)

10진수를 이진수로 표현하면 아래 값 처럼 나온다. <br/>

A : 7 => 111 <br/>
B : 1 => 001 <br/>

자 이제 우리가 위에서 배웠던 AND 연산자대로 계산을 한다면 <br/>
**001이 출력**된다.

001을 2진수 자리가 뜻하는 대로 계산을 해보면<br/>
왼쪽 부터 첫번째 1 , 두번째 0 , 세번째 0<br/>
**합산하면 1**이다.<br/>

## 4. 결과

처음 초기값이 모두 선택된 All 상태일때,<br/>
1개의 필터값을 선택하게 된다.<br/>
필터값에 대한 state값이 변경되면,<br/>
뷰는 변한 state값으로 체크뱍스의 상태값을 그려주게 된다.<br/>

![ex_screenshot](/assets/images/0626/5.png)

<br/>
<br/>

---

> [참고자료1](http://www.tcpschool.com/javascript/js_operator_bitwise)<br/>
> [참고자료2](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1%ED%8E%B8-Bit-%EC%99%80-Byte-%EC%B0%A8%EC%9D%B4%EC%A0%90)<br/>
> [참고자료3](https://devtry.tistory.com/entry/%EB%B9%84%ED%8A%B8-%EC%97%B0%EC%82%B0%EC%9E%90AND-OR-XOR-NOT)

<p align="center"  style="color:#8E99AB; font-size :18px">블로그까지 찾아와주신 분들에게 도움이 되었음 좋겠습니다!🙇‍♀️ </p>

<br/><br/>
