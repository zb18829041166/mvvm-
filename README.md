# mvvm

mvvm实现原理介绍：
1 单向绑定：
  我们使用的基本原理是观察者模式。该模式下，由data的各个属性，比如name属性作为主题，那么观察者是html中的{{name}}
  在mvvm对象初始化的过程中，{{name}}会去订阅name主题，当name 发生变化的时候，会通知所有订阅该主题的观察者更新内容。
  这一步的实现是依靠Object.defineProperty(data, 'name', {...})）方法实现，从而达到了改变name的值，就足以改变
  {{name}}的值

2 双向绑定：
  在单向绑定的基础上，我们给html 增加一个input，通过input来改变name属性，从而改变{{name}}，实现双向绑定。原理依旧
  是观察者模式，我们给html模版添加了 v-model=“name” 属性，在解析模版的时候，将该属性解析出来，并将name属性作为观察
  者，此处的name属性也会去订阅data中的name变量。除此之外给该模版绑定oniput事件，该事件触发vm的name的改变，从而达到
  通知{{name}}更新的目的，也就是双向绑定。
  
