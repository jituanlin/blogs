重复代码不是我们的敌人, 脆弱的抽象基础才是.

很多时候, 一个个 “小小的需求改动”, 之所以要弄很久, 不是我们需要复制粘贴改十遍, 而是我们改了一个地方, 其他九个地方出问题了.

如果所有的需求都能负责粘贴改就做完, 那么程序员也不会掉头发. 

vuex/redux 是用来放全局状态的, 如果一个数据是不是全局状态, 那么它不应该放在 vuex/redux 里.

**应当避免污染全局状态**, 这就是为什么我们不应当把很多东西都挂载在 window 对象上, 为什么 ES6 引入模块, 为什么用 var 声明变量已经被淘汰了的原因.

问:

但是组件 A 和组件 B 都依赖了数据 C, 如果不把数据放在全局状态里, 那么数据会请求两次.

答:

1. “但是组件 A 和组件 B 都依赖了数据C” 不等价于 “数据 C 是全局状态”, 只能说明数据 C **在某一个特定的范围内是共享的**. 
在确定了数据C的共享范围(比如组件 A 和组件 B都在共同父组件)之后, 可以将数据 C 的获取, 维护写在这个特定的范围内(React.Context).
2. 组件 A 和组件 B **都用到了**数据 C 不等价于 **都依赖** 了数据C. 
举个例子, 组件 A 和组件 B 都实用了 goods[id=1] 的数据, 单它们的 id, 不来自同一个变量, 只是在当前 **恰好** 值一样, 那么数据 C 不应该抽象为一个公共状态. 

在面向对象编程中, 一个常见的错误是将两个*相似*的东西抽象为一个基类. 

因为狗狗和汽车都借助 轮子/腿 走路, 于是`Dog extends Card`, 我们发明了狗狗车.

因为猫猫和毛毛虫都有毛, 所以我们发明了猫猫虫.

但其实继承不是说 A 像 B, 而是 A 是 B, `Dog extends Animal` 是因为狗是一种动物.

相似是脆弱的, 易变的, 不是所有的猫猫都有毛的, 在脆弱的基础上抽象, 最终我们得到的不是代码复用, 而是代码耦合.

耦合的代码最终导致了 “改了这个, 那个又不行了”.

**而全局状态, 便是一种最强的耦合.**

由于时间不足, 这个文章只是开个头, 这里先记下TODO:

1. 说明 将数据放在全局状态里, 不是真的复用, 要想复用, 还需要将这些数据与请求的参数(key)进行绑定, 并进行缓存过期管理, 并最终 “发明” 了 react-query.
2. 说明 React.Suspense 是如何用声明式的写法, 简化了数据 loading, error 的处理的.
3. 说明 为什么要选择 显式地声明, 而不是 隐式 的魔法, 并以 mixin 为例, 说明 mixin 这种为了复用而带来的 隐式 的魔法的危害, 并最终被 React 社区弃用.
4. 说明 什么是严谨的代码, 为什么我们应当在代码中基于 脆弱 的前提条件 把代码写死.