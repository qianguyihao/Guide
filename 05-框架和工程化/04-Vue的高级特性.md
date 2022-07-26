# 前言 

Vue的高级特性包括：

- 自定义 v-model

- $nextTick、refs

- slot 插槽
- 动态组件
- 异步组件
- keep-alive
- mixin



## 自定义 v-model

父组件：

```html
<CustomVModel v-model="text1"/> 
```

子组件：

```html
<template>
    <!-- 例如：vue 颜色选择 -->
    <input type="text"
        :value="text1"
        @input="$emit('change1', $event.target.value)"
    >
    <!--
        1. 上面的 input 使用了 :value 而不是 v-model
        2. 上面的 change1 和 model.event1 要对应起来
        3. text1 属性对应起来
    -->
</template>

<script>
export default {
    model: {
        prop: 'text1', // 对应 props text1
        event: 'change1'
    },
    props: {
        text1: String,
        default() {
            return ''
        }
    }
}
</script>
```

## $nextTick

Vue组件更新后，如何获取最新的DOM？

- Vue 是异步渲染框架
- data改变之后，DOM不会立即渲染，而是异步渲染
- $nextTick会在DOM渲染之后被触发，以获取最新的DOM节点

语法：

```js
this.$nextTick(() => {
	// 具体语法
})
```

代码举例：

```html
<template>
  <div id="app">
    <ul ref="ul1">
        <li v-for="(item, index) in list" :key="index">
            {{item}}
        </li>
    </ul>
    <button @click="addItem">添加一项</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
      return {
        list: ['a', 'b', 'c']
      }
  },
  methods: {
    addItem() {
        this.list.push(`${Date.now()}`)
        this.list.push(`${Date.now()}`)
        this.list.push(`${Date.now()}`)

        // 异步渲染，$nextTick 待 DOM 渲染完再回调
        // 页面渲染时会将 data 的修改做整合，多次 data 修改只会渲染一次。比如，上面的 data修改有三次，但页面知会渲染一次， nextTick也只会触发一次
        this.$nextTick(() => {
          // 获取 DOM 元素
          const ulElem = this.$refs.ul1
          // eslint-disable-next-line
          console.log( ulElem.childNodes.length )
        })
    }
  }
}
</script>
```

## slot 插槽

父组件往子组件里插入内容。

### 基本使用

父组件：

```html
<SlotDemo :url="website.url">
            {{website.title}}
</SlotDemo> 
```

子组件：

```html
<template>
    <a :href="url">
        <slot>
            默认内容，即父组件没设置内容时，这里显示
        </slot>
    </a>
</template>

<script>
export default {
    props: ['url'],
    data() {
        return {}
    }
}
</script>
```







### 作用域插槽



### 具名插槽

## 动态组件

如果组件类型、组件数量不确定，则可以用动态组件。

语法：

```html
:is	= "my-component-name"
```

代码举例：

```html
<div v-for="(item, key) in DataList" :key="key1">
  <component is = 'item.name' />
</div>

dataList: [
	{key: 1,
	name: 'a'
	},
	{key: 2,
	name: 'b'
	}
]
```



## 异步组件（很常用）

- 按需加载，异步加载大组件。什么时候用到，再什么时候加载，避免影响首页打开性能。
- 语法：import() 函数。普通的 import是同步加载，而异步加载是通过 import()函数。

代码举例：

```html
<!-- 异步组件 -->
<FormDemo v-if="showFormDemo"/>
<button @click="showFormDemo = true">show form demo</button>

components: {
  // 异步加载组件
	FormDemo: () => import('../FormDemo'),
},
```



## keep-alive：缓存组件

使用场景：该组件频繁切换，不需要重复渲染。 比如tab切换场景。

使用 keep-alive缓存组件后，该组件不会被销毁。

代码举例：

```html
<keep-alive> <!-- tab 切换 -->
  <KeepAliveStageA v-if="state === 'A'"/>
  <KeepAliveStageB v-if="state === 'B'"/>
  <KeepAliveStageC v-if="state === 'C'"/>
</keep-alive>
```



## mixin

多个组件有相同数据和逻辑时，可以通过  mixin 抽离出来。

语法：

```js
import myMixin from './mixin'

export default {
    mixins: [myMixin], // 可以添加多个，会自动合并起来
    data() {}
    },
    methods: {
    },
    mounted() {
    }
}
```

备注：一个组件可以引用多个 mixin，多个组件可以共用一个 mixin。这是一对多、多对多的关系。

mixin并不是完美的解决方案，会有一些问题。Vue3的 Composition API 可以解决这个问题。

mixin的问题：

- 变量来源不明确，不利于阅读

- 多 mixin 可能会造成命名冲突

- mixin和组件可能出现多对多的关系，复杂度较高。









