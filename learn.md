什么是组件？
组件是vue的基本文件，格式为.vue
每个组件都包含：
    template：模板，类似于html，定义组件的结构
    script: js逻辑，定义组件属性和方法、逻辑
    style：即css，定义组件的样式
App.vue是根组件，所有组件最终都会被引入到App.vue中使用
main.js加载App.vue并进行渲染

常用的vue指令：
- v-bind(shorthand - :attribute_name)： This directive binds one or more attributes of an element to a JavaScript expression
- v-for： This directive iterates over a data array and renders an element for each item.
- v-model：This directive creates a two-way binding between a form input element and a data property.
- v-on(shorthand - @event_name)： This directive attaches event listeners to elements and triggers methods when events occur.
- v-if: This directive conditionally renders an element based on a truthy value.

父子组件
引用者是父组件，被引用者是子组件
组件常用结构：
    components：组件引用的其他组件，配合import语句使用
    props: 定义使用组件的参数，类似函数参数，父组件引用子组件时，需要传递子组件要求的参数
    methods：组件的script部分暴露的方法，供template部分调用
    data(): 组件的script部分暴露的变量，供template部分调用
    computed：不太理解
父子组件交互：
    子组件this.$emit("event_name", attribute)：向父组件传递事件和参数
    父组件@event_name="call_function(attribute)"：捕捉子组件事件和参数，并调用函数处理事件
    eg: 子组件某个输入框接收到新输入，抛出一个new_input事件和input_content参数
    父组件捕捉到new_input事件和参数，触发valid函数，校验input_content是否合规，不合规则抛错