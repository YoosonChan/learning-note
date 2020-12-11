# 注册全局组件

## **```index.js```**
```js
// 导入vue
import Vue from 'vue'
// 导入所需组件
import Components from './components'
...

// 所有所需组件注册 install
Components.install = () => {
  Vue.component('组件名称', Components)
}
...

// 打包导出所有组件
export default {
  Components
  ...
}

```

## 使用组件

### 全局使用
**```main.js```**
```js
import Vue from 'vue'
// 导入组件注册文件index.js
import components from 'components/index.js'

// 使用组件
Vue.use(components)
```

### 单文件使用
**```page.vue```**
```html
<script>
import components from 'components/index.js'

export default {
  components: { ...componts }
}
</script>
```