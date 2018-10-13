# Getting Started

1. 当 Vue 组件从 store 取状态 (state) 时，如果 store 的状态变化了，Vue 组件将会是响应式的并会有效的更新。<!-- issu-1 -->

2. 你不能直接修改 store 的状态。修改 store 状态的唯一方式是明确地提交修改 (explicity comming mutations)。这使得每个状态变化可预测，并使得工具帮助我们更好地理解我们的应用程序。(这只是约定而已)

```js
const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        increment(state){
            state.count++
        }
    }
})

store.state.count // access store state
store.commit('increment')
store.state.count
```

在组件中使用 store 状态只是在计算属性中将他返回，因为 store 状态是响应式的。<!-- issue-1 clues -->

```jsx
import Vue from 'vue'
import store from './store'

class Counter extends Vue{
    get count(){
        return store.state.cout
    }
    render(){
        return (
            <div>{ this.count }</div>
        )
    }
}
```

当 `store.state.count` 变化时，他使得计算属性重新计算值，然后触发相关的 DOM 更新。// 不用计算属性应该不行

然而，这种模式使得组件依赖全局的 store 单例。当使用模块系统时，每个需要 store 的组件都要引入 store 状态。

Vuex 提供了一种从根组件以 `store` 选项将 store 注入所有子组件的机制 (使用 `Vuex.use(Vuex)`):  //?

```js
const app = new Vue({
    el: '#app',
    // provide the store using the "store" option
    // this will inject the store instance to all child components
    store,
    components: { Counter },
    template: `
        <div></div>
    `
})
```

通过向根实例提供 `store` 选项，store 将被注入到所有根组件的子组件中并在子组中使用 `this.$store` 可访问。

```jsx
import Vue from 'vue'

class Counter extends Vue{
    get count(){
        return this.$store.state.cout
    }
    render(){
        return (
            <div>{ this.count }</div>
        )
    }
}
```

`mapState`...

使用 Vuex 并不意味着你应该把状态都放在 Vuex 中。虽然把状态都放在 Vuex 中使得状态 (state) 修改更明确且可调度，但也使得代码更繁索而且不直接。做决定时权衡利蔽以适应你项目的开发需求。

# q禾金

Vue.use(Vuex)
