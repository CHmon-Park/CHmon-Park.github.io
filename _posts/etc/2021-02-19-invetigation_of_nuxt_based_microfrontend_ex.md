---
title: "Investigation of Nuxt based Microfrontend Example(from Qiankun)"
excerpt: "Difference among let, var, const"
excerpt_separator: "<!--more-->"
categories:
  - Etc
tags:
  - Code Investigation
  - Qiankun
  - Nuxt
  - Microfrontend
last_modified_at: 2021-02-19T10:10:00
---
<!--more-->

<br>

## 필요한 요소들(Main App)

### ● layouts > default.vue

##### 역할

  * DOM이 mount되는 단계에서 registerMicroApps, start 메소드를 사용하여 App들을 등록하고 프로젝트를 시작한다.
  * 이후 App 데이터에 들어간 내용을 바탕으로 화면에 이름을 출력하고, 이름이 클릭되면 해당하는 App이 출력되도록 nuxt-link 처리를 한다.
  * App이 출력되는 부분은 'default_subapp'이라는 id의 div이며, 이는 store > index.js 파일과 연동되어 있다. 
  
##### 코드

```vue
[template]

    <div class="menu-wrap">
      <ul>
        <li v-for="app in apps" :key="app.name">
          <nuxt-link :to="app.activeRule">{{ app.name }}</nuxt-link>
        </li>
      </ul>
    </div>

    <div id="default_subapp" class="bg-red-300"></div>
```

```vue
<script>
import { mapState } from 'vuex'
import { registerMicroApps, start } from 'qiankun'
export default {
  data() {
    return {
      value: '',
    }
  },
  computed: {
    ...mapState(['apps', 'sdk']),
  },
  mounted() {
    this.init()
  },
  methods: {
    async init() {
      // 注册所有子应用 <- 모든 하위 응용 프로그램 등록
      await registerMicroApps(this.apps)

      // 启动 <- 시작
      await start()
    },

    handleChange() {
      this.sdk.globalState.setGlobalState({
        name: this.value,
      })
    },
  },
}
</script>
```

### ● pages > 404.vue

##### 역할

  * 404 오류가 출력될 때 나오게 되는 페이지이다.
  * store > index.js 에서 위 페이지를 지정하고 있다.

##### 코드

```vue
<template>
  <div class="page-404">
    page 404
    <button @click="$router.replace('/')">返回首页</button>
  </div>
</template>

<script>
export default {
  layout: 'empty'
}
</script>

<style>
.page-404 {
  text-align: center;
}
</style>
```

### ● pages > index.vue

##### 역할

  * mounted 단계에서 init을 통해 registerMicroApps, setDefaultMountApp, start라는 메소드들을 실행하는 vue이다.
  * 여기에서 setDefaultMountApp 메소드는 처음 페이지에 나올 App을 지정하는 메소드인데, 원 코드와 같이 설정하게 되면 처음부터 App이 켜진 상태로 시작되기에 현재는 주석화 하여 첫 페이지를 메인 부분만 출력하도록 설정하였다. 

##### 코드

```vue
<template></template>

<script>
import { mapState } from 'vuex'
import {
  MicroAppStateActions,
  registerMicroApps,
  start,
  setDefaultMountApp,
} from 'qiankun'
export default {
  mounted() {
    this.init()
  },
  computed: {
    ...mapState(['apps']),
  },
  methods: {
    async init() {
      // 注册所有子应用 <- 모든 하위 응용 프로그램 등록
      registerMicroApps(this.apps)

      // 设置默认 active 的子应用 -> 기본 활성 하위 응용 프로그램 설정
      // setDefaultMountApp(this.apps[0].activeRule)

      // 启动
      start()
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

#subapp {
  min-height: 100vh;
}
</style>
```

### ● plugins > element-ui.js

##### 역할

  * element-ui를 사용하여 Nuxt에서 동적 요소를 사용할 수 있도록 한다.

##### 코드

```js
import Vue from 'vue'
import Element from 'element-ui'
import locale from 'element-ui/lib/locale/lang/en'

Vue.use(Element, { locale })
```

### ● plugins > resolveApps.js

##### 역할

  * getMenus라는 action을 통해 store에 명시되어 있는 App들을 store 변수 apps에 넣는 작업을 한다.
  * plugins에 포함되어 있기에 메인 App이 인스턴스 화 되기 전에 실행되어 전역적으로 구성 요소를 등록하고 함수 또는 상수를 삽입한다.

##### 코드

```js
export default async ({ store }, inject) => {
  await store.dispatch('getMenus')
}
```

### ● store > index.js

##### 역할

  * sub_app의 요소들을 main_app에서 등록할 수 있도록 데이터를 등록 및 관리하는 부분이다.

##### 코드

```js
import { Message } from 'element-ui'
import { initGlobalState } from 'qiankun'

const TYPES = {
  INIT_APPS: 'init_apps',
}

export const state = () => ({
  apps: [],
  name: 'femessage',
  sdk: null,
})

export const mutations = {
  [TYPES.INIT_APPS](state, apps) {
    // 初始化全局变量 <- 전역 변수 초기화
    const actions = initGlobalState({
      name: state.name,
    })

    // 使用 sdk 方式进行 父子应用通信, 这里大家可以根据自己项目进行增加删除
    // 자신의 프로젝트에 따라 추가 및 삭제할 수있는 상위-하위 애플리케이션 통신에 sdk 메서드를 사용합니다.
    const sdk = {
      globalState: actions,
      toast: (...args) => {
        Message(...args)
      },
      go2404: () => {
        this.$router.push('404')
      },
      name: state.name,
    }

    // 处理 apps 列表 <- 앱 목록 처리
    apps = apps.map((item) => ({
      ...item,
      container: '#default_subapp', // default.vue에서 subapp들이 들어갈 div의 id를 명시한 것.
      props: {
        sdk,
      },
    }))

    // 处理路由表 <- 라우팅 테이블 처리
    const routes = apps.map((item, i) => ({
      path: `${item.activeRule}(.*)`,
      name: `${item.name}-i`,
      component: () => import('@/pages/index.vue').then((m) => m.default || m),
    }))

    // 动态增加路由, 这里要注意 404 页面不能直接写在 pages 中
    // 라우팅을 동적으로 늘리십시오. 여기에서 404 페이지는 페이지에 직접 쓸 수 없습니다.
    // 不然匹配的时候会根据顺序匹配到 * 就直接返回了 从而匹配不到我们后续添加的动态路由
    // 그렇지 않으면 일치 할 때 순서에 따라 일치하고 직접 반환되므로 나중에 추가 할 동적 경로와 일치하지 않습니다.
    this.$router.addRoutes(
      [].concat(...routes, {
        path: `*`,
        name: `404`,
        component: () => import('@/pages/404.vue').then((m) => m.default || m),
      })
    )

    state.apps = apps
    state.sdk = sdk
  },
}

export const actions = {
  async getMenus({ commit }) {
    const { payload } = await getMenus()

    commit(TYPES.INIT_APPS, payload)
  },
}

function getMenus() {
  return {
    code: 0,
    payload: [
      {
        name: 'nuxt-app',
        activeRule: '/nux',
        entry: 'http://localhost:7102/',
      },
      {
        name: 'ggg-app',
        activeRule: '/gg',
        entry: 'http://localhost:7102/',
      },
    ],
    message: 'success',
  }
}
```

### ● nuxt.config.js

  * mode: 'spa'
  * target: 'server'
  * plugins: ['@/plugins/element-ui', '@/plugins/resolveApps']
  * modules에 추가: '@femessage/nuxt-micro-frontend'
  * build에 추가: transpile: [/^element-ui/]
  
### ● package.json

  * scripts > dev: "cross-env PORT=7100 nuxt"
  * dependencies에 추가: "@femessage/nuxt-micro-frontend": "^1.6.0", "element-ui": "^2.13.2", "qiankun": "^2.0.16"
  * devDependencies에 추가: "cross-env": "^7.0.2"
  
  
## 필요한 요소들(Sub App)

### ● layouts > default.vue
  
  * <Nuxt /> 태그 필요
  
### ● router > index.js

##### 역할

  * routes.js에서 sub_app이 출력해야 할 부분에 해당하는 주소, 이름, url 등을 받아 요청받은 페이지를 return 하는 역할을 한다. 

##### 코드

```js
import Router from 'vue-router'
import routes from './routes'

export function createRouter(ssrContext, createDefaultRouter, routerOptions) {
  const options = routerOptions
    ? routerOptions
    : createDefaultRouter(ssrContext).options

  return new Router({
    ...options,
    routes: fixRoutes(options.routes),
  })
}

function fixRoutes() {
  // default routes that come from `pages/`
  return [].concat(routes)
}
```

### ● router > routes.js

##### 역할

  * 임의의 url로 접근을 요청받게 되었을 때 그 접근의 유효성을 검사하고, 검사를 통과할 시 해당하는 페이지의 정보를 전달한다.

##### 코드

```js
const BASE = window.__POWERED_BY_QIANKUN__ ? '/nux' : ''
const BASE2 = window.__POWERED_BY_QIANKUN__ ? '/gg' : ''

function dynamicImport(path) {
  return import(`~/views/${path}/index.vue`).then((m) => m.default || m)
}

const resolveRoute = (route) => ({
  ...route,
  component: () => dynamicImport(route.component),
})

function dynamicImportRoute(routes) {
  return routes.map((route) => ({
    ...resolveRoute(route),
    children: route.children ? route.children.map(resolveRoute) : [],
  }))
}

let routes = [
  {
    path: `${BASE}/about`,
    name: 'About',
    component: 'about',
  },
  {
    path: `${BASE}/home`,
    name: 'Home',
    component: 'home',
    alias: `${BASE}`,
  },
  {
    path: `${BASE2}/gg`,
    name: 'Home',
    component: 'home',
    alias: `${BASE2}`,
  },
]

export default dynamicImportRoute(routes)
```

### ● views > about > index.vue

##### 코드

```vue
<template>
  <div>
    <h2>About page</h2>
    <button @click="$router.back()">back</button>
  </div>
</template>

<script>
export default {}
</script>

<style></style>
```

### ● views > home > index.vue

##### 코드

```vue
<template>
  <div>
    <h1>haahahaa</h1>
    <h2>Home page</h2>
    <button @click="go2about">go2about</button>
    <button @click="toast">Toast</button>
  </div>
</template>

<script>
export default {
  methods: {
    go2about() {
      this.$router.push({ name: 'About' })
    },
    toast() {
      this.$sdk &&
        this.$sdk.toast({
          message: 'nuxt에 의해 트리거 된 토스트',
          type: 'success',
        })
    },
  },
}
</script>

<style></style>
```

### ● mfe.js

##### 역할

  * 조사 필요..

##### 코드

```js
import Vue from 'vue'

export default function(render) {
  if (!window.__POWERED_BY_QIANKUN__) {
    render()
  }
}

export function bootstrap() {}

export async function mount(render, props) {
  await render()
}

export async function update() {}

export function mounted(instance, props) {

  if (props.sdk) {
    Vue.prototype.$sdk = props.sdk
  }
}

export function beforeUnmount(instance) {}
export function unmount() {}
```

### ● nuxt.config.js

  * mode: 'spa'
  * target: 'server'
  * buildModules에 추가: ['@nuxtjs/router', { keepDefaultRouter: true, path: './router', fileName: 'index.js' }]
  * modules에 추가: '@femessage/nuxt-micro-frontend'
  * MFE: {force: true}

### ● package.json

  * scripts > dev: "cross-env PORT=7102 nuxt"
  * dependencies에 추가: "@nuxtjs/router": "^1.5.0"
  * devDependencies에 추가: "@femessage/nuxt-micro-frontend": "^1.5.0", "cross-env": "^7.0.2"
  
## 프로젝트 구동 과정

1. 각 App 별로 Server가 켜져 있어야 한다.

2. main app 의 url로 접속하게 되면 default.vue로 접속한다.

3. 이 때 mounted 단계에서 this.init이 실행된다.

4. init에는 registerMicroApps, start라는 메소드가 있는데, 이들은 모두 node_modules의 qiankun의 apis.js에서 import되었다.

5. registerMicroApps는 App을 등록하고, start에서 준비사항 점검 및 기능 시작 역할을 한다.

6. App들이 store 데이터에 들어가게 되면 이를 통해 default.vue에서 App들의 이름을 출력한다.

7. main_app 에서 sub_app들의 이름을 누르게 되면 해당하는 url에 request를 보내게 된다.

8. request를 받은 sub_app은 router에서 유효성 검사를 거쳐 request에 따라 vue 파일을 전달한다.

9. response를 받은 main_app은 해당 내용을 default.vue의 'default_subapp'이라는 id의 div에 출력한다.


## 분석 과정 중 이슈 사항

##### 1. 각 App 당 port 번호는 어떻게 지정하는가?

package.json > scripts > dev 부분에서 포트 번호를 지정할 수 있다. 이 때 필요한 모듈이 cross-env이다.
{: .notice--info}

##### 2. 처음 들어가면 localhost:7100/<name> 형식으로 url이 들어가지는데 정확히 메인페이지로 가게 하기 위해서는 메인 App으로 갈 수는 없을까?

이는 index.vue의 setDefaultMountApp의 영향인 것으로 확인되었다. setDefaultMountApp은 처음에 출력될 App을 지정하는 메소드로, 이것을 주석처리하여 url이 자동으로 바뀌지 않도록 하였다. 현재까지는 아무 오류도 발생하지 않았다.
{: .notice--info}

##### 3. nuxt-app과 sub-app 두 가지의 버튼이 있을 때, nuxt-app은 app을 정상적으로 출력하는 반면, sub-app은 같은 포트를 가리키더라도 페이지를 가지고 오지 못한다.

이름 자체의 문제나 주소의 문제가 아니었다. 추가로 들어갈 url의 문제로 보이는데.. /nuxt라는 것은 되는 것을 보면 어디에선가 등록이 된 것 같다.
{: .notice--info}

##### 4. sub_app의 첫 페이지가 무조건 home으로 뜨는데, 이것을 수정할 방향은 없는지, 그리고 default.vue나 index.vue의 영향은 전무한 것인지 아직 확인이 되지 않았다. 실제로 이전에는 vue 마크가 같이 출력되기도 했었는데 지금은 나오지 않는 상황이다.

sub app의 router > routes.js를 보면 routes 변수에 각 path들이 적혀 있는데, 이 부분에서 alias, 즉 가명을 설정할 수 있다. 이 가명을 `${BASE}`로 설정하게 되면 가장 먼저 해당 페이지가 나오는 것으로 보인다. 또한 이 alias 설정이 없으면 페이지 자체를 띄우지 못한다.
{: .notice--info}

sub app의 default.vue 파일에 <Nuxt> 태그를 넣어야 그곳에 views 내용이 들어간다. 즉, 그동안 vuejs 로고가 나오지 않았던 것은 <Logo> 태그가 없었기 때문이며, views의 내용만 나왔던 것은 <Nuxt> 태그가 존재했기 때문으로 풀이된다. 다만.. 그럼 <Nuxt> 태그에 무슨 의미가 따로 있는 것일까..
{: .notice--info}

alias 설정은 그와 같은 접속 path도 동일하게 취급하겠다는 의미이다.
{: .notice--info}

Nuxt 태그에 대한 내용은 nuxt.js에 있을 것으로 보인다. 검색 시 나오는 nuxt-child에 대한 내용도 명시되어 있고.. 그러나 보다 면밀한 조사가 필요하다. 우선은 기본적으로 nuxt.js에서 nuxt 태그가 부분 component들을 불러오는 통로로서 사용되도록 설정된 것으로 보이고, 해당 기능을 사용하기 위해서 다른 파일이 등록하는 기능을 할 것으로 예상된다. 즉, 그 다른 파일이라는 것을 찾으면 된다.
{: .notice--info}

##### 5. 그렇다면 router 없이 기본 default.vue만 나오게 하려면 어떻게 해야할까..?

sub app의 router > index.js 를 보면 fixRoutes() 라는 function이 존재한다. 이 부분이 routes.js에서 가져온 routes를 가지고 새로운 path를 만들어내고 있다. createRouter 부분의 return 부분을 주석화 하면 예상대로 default.vue가 출력된다.
{: .notice--info}

##### 6. main_app에서 activeRule이 '/nux'로 등록된 app의 경우에는 정상적으로 페이지를 받아오는 반면, 다른 내용으로 등록된 app들은 페이지를 받아오지 못한다. 특히 같은 sub_app을 가리키는 url을 적어두어도 같은 현상이다.
  
sub app 의 router > routes.js 에서 맨 윗 줄의 전역 변수를 보면 /nux를 BASE로 사용하고 있다. 즉, 아래의 routes들에 나오는 path의 `${BASE}`가 /nux인 것이다. '/nux' 부분이 어딘가에 등록된 것처럼 느껴졌던 것은 이쪽인 것 같다. 따라서 routes.js 파일에 새로운 전역 변수를 생성하고, 그것을 routes에서 기존과 같은 방식으로 사용하게 되면 적절한 효과를 볼 수 있다..!
{: .notice--info}

##### 7. 그럼 MFE는 무엇인가..?