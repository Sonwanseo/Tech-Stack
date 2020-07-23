# Recoil

## 등장 배경
복잡한 React 웹 앱에서는 상태 관리가 개발자의 주요 과제이자 어려운 작업으로 여겨진다.
어떤 하나의 상태 변경이 하나 이상의 다른 컴포넌트에 영향을 끼칠 수 있기 때문이다.

그래서 페이스북 소프트웨어 엔지니어 Dave McCabe와 그의 동료들은 복잡한 UI를 대상으로 전역 상태 관리를 위한 최적화 방법을 찾으려고 하였으나 성능 및 효율성이라는 장벽에 부딪혔다.
그리고 이 문제를 해결할 가장 좋은 방법은 직접 라이브러리를 만드는 것이라고 결정하였다.

기존에 있던 상태관리 라이브러리(Redux와 MobX 등)은 제공하는 API가 단순하지 않았고, 근본적으로 React에서 사용하기 위해 나온 것이 아니다. 
(react-redux 혹은 mobx-react와 같이 React 전용 wrapper 라이브러리가 있긴 하다.)
그렇다고 React만으로 해결하려고 하니 그것도 쉬운 일이 아니었다.

또한, store는 "외부요인"으로 취급되는 것이기 때문에 React의 내부 스케줄러에 접근할 수 없다.
지금까지는 중요하지 않았지만 동시성 모드가 등장하며 상황이 바뀌었다.
React와 동시성 모드를 손쉽게 사용할 수 있는 해결방안이 필요하였을 것이다.
(Recoil은 내부적으로 React의 상태를 사용하고 있으며, 동시성 모드에 대한 지원도 곧 추가될 것이다.)

일부 라이브러리는 강력한 기능을 제공하긴 하지만, 기본적인 store 구성을 위해 많은 보일러 플레이트와 장황한 코드를 작성해야 한다.
또한 비동기 데이터 처리 또는 계산된 값, 캐시와 같은 중요한 기능은 라이브러리의 기능이 아니며, 이를 해결하기 위해 또 다른 라이브러리를 사용해야 한다.

이러한 이유로 Recoil 개발자들은 API와 동작 방식을 가능한 React스럽게(Reactish) 가져가면서 현상을 해결하려고 Recoil을 제작했다고 한다.

아직 개발 초기 단계인 것 같다.

#### _React 내부 스케줄러_
?

#### _동시성 모드_
(Concurrent Mode), 많은 작업을 한번에, 그들의 우선순위를 바꿔가면서 동작할 수 있게 한다.
참고(https://ideveloper2.tistory.com/170, https://reactjs.org/blog/2018/11/27/react-16-roadmap.html#react-16x-q2-2019-the-one-with-concurrent-mode)

#### _보일러 플레이트_
최소한의 변경으로 여러곳에서 재사용되며, 반복적으로 비슷한 형태를 띄는 코드를 말한다.
참고(https://medium.com/@charlezz/%EB%B3%B4%EC%9D%BC%EB%9F%AC%ED%94%8C%EB%A0%88%EC%9D%B4%ED%8A%B8-%EC%BD%94%EB%93%9C%EB%9E%80-boilerplate-code-83009a8d3297)

## 핵심 개념
Recoil은 Atom이라는 하나의 상태로부터 시작해서 Selector를 거쳐 React 컴포넌트까지 전달되는 하나의 Data-Flow Graph를 만들게 한다.
Atom은 컴포넌트들이 구독(subscribe) 할 수 있는 단위이고, Selector는 동기적 혹은 비동기적으로 상태를 변환한다.
이 두 가지 핵심 개념으로 이루어진 라이브러리이다.

## 장점
- atom/selector라는 단위를 통해 derived state를 효과적으로 처리하고 상태의 '코드 분할'이 가능하게 한다.
- 기존 상태관리 라이브러리보다 훨씬 단순한 API를 제공하고, Concurrent Mode를 통합하는 것까지 목표로 한다.

## 참고
- https://ui.toast.com/weekly-pick/ko_20200616/
- https://recoiljs.org/
- https://velog.io/@ansrjsdn/%EC%83%88%EB%A1%9C%EC%9A%B4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-Recoil
- https://medium.com/humanscape-tech/recoil-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-285b29135d8e