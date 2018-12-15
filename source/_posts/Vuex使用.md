---
title: Vuex使用
date: 2018-07-21 22:30:55
tags:
- vue
---

Vuex 是一个专门为 Vue.js 应用所设计的集中式状态管理架构。暂时，我的理解是vue数据的管理中心，所有组件的数据都可以通过Vuex访问，修改。

不在需要父子组件之间的传递数据

### 安装

工程目录下

```
npm install vuex --save
```

### 在src目录下新建stroe/stroe.js

写入

```
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)

const state = {
  nowPage: 0
}

const mutations = {
  change (state, num) {
    state.nowPage = num
  }
}

export default new Vuex.Store({
  state,
  mutations
})
```

### main.js 文件

导入store.js

```
import storeConfig from './store/store.js'
```

应用

```
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>',
  router: router1,
  store: storeConfig
})
```

### 使用store下的数据

获取数据

```
this.$store.state.nowPage
```

修改数据

```
this.$store.commit('change', 0) 
// 修改nowPage的值为0
```

### 其他

其他更强大的功能优待试用