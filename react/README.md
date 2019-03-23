# React

리액트는 Node JS와 함께 SSR(Server-Side Rendering)로 많이 사용된다. CSR은 SEO 하기가 불편하지만 SSR은 그런 문제가 없어서 토이프로젝트가 아니면 
대부분 Node JS와 SSR(Next.js)을 선호하는 추세이다.
특히 소규모 스타트업같이 인력이 부족한 회사들도 JS로 React-NodeJS-React Native-MongoDB 스택을 사용하는 사람들도 많다.
다만 개발할때 SSR을 염두에 두고 개발해야 한다.

리액트의 주요 특징 중 하나는 Virtual DOM을 사용하는 것이다. Virtual DOM을 사용하면 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 자바스크립트 객체를 구성하여 사용한다.

리액트에서 데이터가 변하여 웹 브라우저에 실제 DOM을 업데이트할 때는 다음 세 가지 절차를 밟는다.
1. 데이터를 업데이트하면 전체 UI를 Virtual DOM에 렌더링한다.
1. 이전 Virtual DOM에 있던 내용과 현재 내용을 비교한다.
1. 바뀐 부분만 실제 DOM에 적용한다.


* 서버사이드 렌더링이란?
  - http://webframeworks.kr/tutorials/react/server-side-rendering/

* 왜 서버사이트 렌더링이 필요할까?
  - https://subicura.com/2016/06/20/server-side-rendering-with-react.html

* Next.js - 서버 사이드 렌더링 프레임워크
  - https://blog.kesuskim.com/2017/06/next-js-react-server-side-rendering-framework/

## why React??
React는 다음 3가지의 중요한 특징을 지니고 있습니다. 이 요소들은 분리된 것이 아니라 서로 연결되면서 React를 지탱합니다.
### Component
Component는 UI를 구성하는 개별적인 뷰 단위입니다. React로 개발을 한다는 것은 마치 블럭을 조립해 성을 만드는 것과 같습니다. 전체 앱은 각 Component들이 결합해서 만들어 지게 되죠. 무엇보다 각 Component들은 앱의 다른 부분, 또는 다른 앱에서 쉽게 재사용이 가능합니다. Redux의 창시자이며, 현재는 Facebook React Core팀의 일원인 Dan Abramov는 React의 목표가 성능보다는 유지가능한 앱을 만드는 것에 있다고 설명한적이 있습니다.

### JSX
JSX는 React를 위해 태어난 새로운 자바스크립트 문법으로, 과거 페이스북이 만들었던 PHP의 개량판 XHP에 그 기원을 두고 있습니다. (참조)React.js Conf 2015 Keynote
```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
ReactDOM.render(<HelloMessage name="John" />, mountNode)
```
이 코드는 “Hello, John”라는 div를 생성하는 컴포넌트입니다. ES6를 공부하신 분들이라면, class를 이용한 method 상속 패턴 자체에는 익숙하실 겁니다. 그러나 아마 React를 처음 접하신 분들에게는 낯선 곳이 두군데 있습니다. 바로 render 함수의 return 값과 ReactDOM.render함수의 첫번째 argument죠. 뭔가 html처럼 보이긴 하는데 스트링으로 감싸진 것도 아닌 정체불명의 녀석들입니다.

React는 작성한 코드를 컴파일하는 과정을 꼭 거쳐야 합니다. 대부분 사실상 자바스크립트 표준이 되어가고 있는 Babel을 사용하죠. Babel의 React 플러그인을 통해 위의 코드를 컴파일하면 다음과 같은 모습이 됩니다.

```
class HelloMessage extends React.Component {
  render() {
    return React.createElement(
      "div",
      null,
      "Hello ",
      this.props.name
    );
  }
}
```
ReactDOM.render(React.createElement(HelloMessage, { name: "John" }), mountNode);
이제 그냥 보통 자바스크립트 코드가 되었죠? React는 Babel과 같은 트랜스파일러를 꼭 써야하기 때문에 Webpack 등을 통한 꽤 까다로운 초기 세팅이 필수적입니다. 그렇다면 왜 굳이 이런 번거로움을 들여가며, JSX를 사용하는 것일까요?

물론 JSX를 사용하지 않고 바로 위의 코드처럼 직접 순수한 자바스크립트 코드를 작성하여 React를 사용할 수도 있습니다. 그러나 실제로 그렇게 사용하는 경우는 거의 없을 뿐 아니라, React를 사용하는 중요한 이유 중 하나를 포기하는 셈이 되죠.

JSX는 보통 선언적이라고 번역되는, Declarative한 개발을 도와주는 도구입니다. 간단하게 말해 한눈에 이해하기 쉬운 개발을 만들어 줍니다. JSX는 그 형태가 마치 html과 같습니다. 유저에게 보여주고 싶은 최종적인 View라고 할 수 있죠. 개발자는 JSX를 통해 결과물에 직관적으로 도달할 수 있습니다. 이는 예측가능한 개발을 만들어줄 뿐 아니라 유지보수, 협업 등에서도 엄청난 강점을 발휘합니다.

### Vitual DOM
결국 위의 모든 것을 가능하게 만들어주는 것, 그리고 React의 가장 큰 특징이자 뜨거운 논쟁을 불러일으키는 대상, 그것이 바로 Virtual DOM입니다.

DOM은 웹 개발자들의 영원한 숙제입니다. DOM은 웹의 핵심으로써, 브라우저가 화면을 그리기 위한 정보가 담겨있는 문서입니다. 웹은 원래 인터넷을 통해 공유되는 문서의 규격으로써 탄생했죠. 문제는 이 DOM을 효과적으로 다루는 것이 꽤나 힘들다는 것입니다. 그래서 DOM이 성능이 좋지 않다느니 하는 말도 나오지만 사실 DOM 자체보다는 해석 과정에 문제가 있는 경우가 대부분입니다. 브라우저별로 이 DOM을 가지고 화면을 만드는 방식이 다르기도 하구요.

## React vs React Native

* React
  - 사용자 인터페이스(UI)를 만들기 위한 자바스크립트(JavaScript)라이브러리로서 구조가 MVC, MVW(Model-View Whatever)등인 프레임워크와 달리 오직V(View)만 신경쓰는 
* React Native
  - 리액트 네이티브는 네이티브 모바일 앱을 만들 수 있게 도와주는 라이브러리로서 Objective-C, Java 또는 Swift를 사용하여 만든 앱과 구별 할 수없는 실제 모바일 앱을 만들 수 있다.  React Native는 일반 iOS 및 Android 앱과 동일한 기본 UI 빌딩 블록을 사용한다. JavaScript와 React를 사용하여 이러한 빌딩 블록을 함께 모으는 것이다. (React Native는 자바스크립트 코드와 네이티브 코드를 별도의 스레드로 분리하여 둘 사이의 통신을 비동기식으로 만들어 느려지는 현상이 없다)

## 렌더링
* 사용자 화면에 뷰를 보여 주는 것을 렌더링이라고 한다.
  ### 초기 렌더링
  * 리액트에서 다루는 render(){...} 함수는 컴포넌트가 어떻게 생겼는지 정의하는 역할을 한다. 이 함수는 html형식의 문자열을 반환하지 않고 뷰가 어떻게 생겼고 어떻게 작동하는지 정보를 지닌 객체를 반환한다. 컴포넌트 내부에는 또 다른 컴포넌트들이 들어갈 수 있다. 이때 render 함수를 실행하면 그 내부에 있는 컴포넌트들도 재귀적으로 렌더링한다. 이렇게 최상위 컴포넌트의 렌더링 작업이 끝나면 지니고 있는 정보들을 사용하여 HTML 마크업을 만들고, 이를 우리가 정하는 실제 페이지의 DOM 요소 안에 주입한다.

## Node.js와 npm
* Node.js는 크롬 V8 자바스크립트 엔진으로 빌드한 자바스크립트 런타임이다. 이것으로 웹 브라우저 환경이 아닌 곳에서도 자바스크립트를 사용하여 연산할 수 있다. Node.js를 출시한 이후 자바스크립트는 웹 브라우저 영역 외에 웹 서버는 물론, 모바일 애플리케이션, 데스크톱 애플리케이션 영역에서도 활약 중이다.
* npm은 Node.js 패키지 매니저로 수많은 개발자가 만든 모듈(재사용 가능한 코드)을 설치하고 해당 모듈 버전을 관리하는 도구이다.

## Redux
리덕스는 상태관리의 로직을 컴퓨넌트 밖에서 처리한다. 리덕스를 사용하면 스토어라는 객체 내부에 상태를 담게 되는데 이를 사용하면 다음 구조로 프로젝트를 관리할 수 있다.
리덕스는 리액트에서 사용하려고 만든 상태 관리 라이브러리지만, 리액트에 의존하지는 않는다. 즉, 리액트를 사용하지 않더라도 리덕스를 사용할 수 있다.
###  리덕스의 세 가지 규칙
1. 스토어는 단 한개
1. state는 읽기 전용
1. 변화는 순수 함수로 