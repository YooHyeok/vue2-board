# *Vue Cli-init*
## *Install*
<details>
<summary>펼치기/접기</summary>
<br>

- ## NPM 방식
  - ### vue/cli-init 설치
    ```bash
    npm i -g @vue/cli-init
    ```

  - ### vue 프로젝트 추가
    ```bash
    vue init webpack {프로젝트명}
    ```
- ## YARN 방식
  - ### yarn 설치
    ```bash
    npm install -g yarn
    ```
  - ### vue 설치
    ```bash
    yarn global add vue
    ```
  - ### vue/cli-init 설치
    일종의 보일러플레이트로 vue.js 프로젝트의 환경 세팅을 자동으로 해준다.
    ```bash
    yarn global add @vue/cli-init
    ```

  - ### vue 프로젝트 추가
    ```bash
    vue init webpack {프로젝트명}
    ```

  - #### 설치 옵션 선택 및 설치 결과
    ```text/plain
    ? Project name {프로젝트명}
    ? Project description {프로젝트 상세설명}
    ? Author 닉네임 <깃허브 계정>
    ? Vue build standalone
    ? Install vue-router? Yes
    ? Use ESLint to lint your code? No
    ? Set up unit tests Yes
    ? Pick a test runner jest
    ? Setup e2e tests with Nightwatch? No
    ? Should we run `npm install` for you after the project has been created? (recommended) npm

      vue-cli · Generated "vue2-board".
      
    Run `npm audit` for details.

    # Project initialization finished!
    # ========================

    To get started:

      cd vue2-board
      npm run dev
    ```

</details>

# `v-for` 리스트 렌더링
### v-for로 엘리먼트에 배열 매핑
v-for 디렉티브를 사용하여 배열을 기반으로 리스트를 렌더링 할 수 있다.

```html
  <tr 
    v-for="(value) in data"
      >
      <td>{{value.writer}}</td>
      <td>{{value.title}}</td>
      <td>{{value.content}}</td>
  </tr>
```

```text/plain
Elements in iteration expect to have 'v-bind:key' directives.
```
Eslint에 의해 위와같은 오류가 발생한다.  
v-for을 사용할때, key값이 요구되기 때문이다.  
아래와 같이 index값을 key값으로 넣어 사용하자.  
(만약 Unique한 값이 존재한다면 해당 값을 사용하면 된다.)

```html
  <tr 
    :key="index"
    v-for="(value, index) in data"
      >
      <td>{{value.writer}}</td>
      <td>{{value.title}}</td>
      <td>{{value.content}}</td>
  </tr>
```

# 라우터 & 파라미터
`path: `속성에 : 콜론을 통해 파라미터를 변수를 지정해준다.  
(전달받을 만약 값이 없는 경우에도 정상적으로 작동하기 위해서는 변수명 끝에 ? 문자를 지정해준다.)
- router/`index.js`
  ```
  import Vue from 'vue'
  import Router from 'vue-router'
  import Read from '@/components/Read'
  import Create from '@/components/Create'
  import Detail from '@/components/Detail'

  Vue.use(Router)

  export default new Router({
    routes: [
      {
        path: '/',
        name: 'Read',
        component: Read
      },
      {
        path: '/create/:contentId?',
        name: 'Create',
        component: Create
      },
      {
        path: '/detail/:contentId',
        name: 'Detail',
        component: Detail
      }
    ]
  })
  ```
- 목록 컴포넌트
  
  `this.$router.push({path: /create/`\`${this.index}\``})`  
  위와 같이 $router.push()함수에 object타입 변수를 파라미터로 담아 컴포넌트를 변경한다.  
  object타입 변수의 path 프로퍼티에 url주소를 입력한다.  
  이때 파라미터는 url끝에 위처럼 동적으로 바인딩할 수 있다.  

  또 다른 방법은 name에 router에 등록한 name을 입력하고 params라는 property에 
  라우터 path에 명시한 변수명 그대로 선언하여 value값을 초기화해준다.
  ```vue
  <script>
  import data from '@/data'
  export default {
    name: 'Read',
    data () {
      return {
        index: 1
      }
    },
    methods: {
      create(index) {
        this.$router.push({
          path: `/create/${this.index}`
        })
      },
      detail(index) {
        this.$router.push({
          name: 'Detail',
          params: {
            contentId: index
          }
        })
      }
    }
  }
  </script>
  ```