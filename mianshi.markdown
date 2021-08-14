URL和URI的区别：
	1. URL是一种具体的URI，它是URI的一个子集


	1.  URI和URL都定义了资源是什么
	2. URL不仅唯一标识资源，而且还提供了定位该资源的信息。
	3. URI 是一种语义上的抽象概念，可以是绝对的，也可以是相对的，而URL则必须提供足够的信息来定位，是绝对的

href和src的区别：
	1. href是引用，表示当前页面和它相关联
	2. src是引入，是页面的一部分

rollup和webpack区别：webpack更适合打包组件库，应用程序之类的应用grollup更适合打包纯js的类库webpack拆分代码，按需加载rollup所有资源放在一个地方，一次性加载，利用tree-shake的特性来剔除项目中未使用的代码，减少冗余，但是webpack2也在逐渐支持tree-shake常见的状态码：
	1. 1xx：需要继续操作


	* 100：客户端继续请求
	* 101：服务端根据客户端请求切换协议


	1. 2xx：成功


	* 200：请求成功
	* 201：请求成功并创建了新的资源
	* 202：接收请求，但未处理完成
	* 204：服务器成功处理，但没有返回内容，在未更新网页的情况下，确保浏览器继续显示当前文档


	1. 3xx：重定向


	* 300：用户终端选择（资源特征与资源的列表）
	* 301：永久移动
	* 302：临时移动
	* 303：查看其他地址


	1. 4xx：客户端错误


	* 400：语法错误，服务器无法理解
	* 403：请求不允许
	* 404：请求资源找不到


	1. 5xx：服务端错误


	* 500：服务器内部错误
	* 501：服务器不支持请求功能

深拷贝实现的方式：浅拷贝只复制指向对象的指针，而不复制对象本身，新旧对象使用的是同一块内存深拷贝创建了另外一个一模一样的对象浅拷贝：var a = [1,2,3,4];var b = a;深拷贝：不可能拷贝原型跨域怎么解决：同源：如果两个URL的协议、端口、域名完全一致，那么这两个URL就是同源的跨域：两个URL不同源，但是一个URL可以访问另一个URL中的数据方法一：CORSresponse.setHeader("Access-Control-Allow-Origin", "http://localhost:9990");方法二：JSONP给不支持CORS跨域的浏览器使用，比如说IE。给它专门建一个js文件，我们通过构造src形如xxx.com/friends.json?callback=xxxx的<script>标签请求这个JS文件，会执行一个回调，回调里面就是想要的数据。
	* 优点就是兼容IE，可以跨域；
	* 缺点是由于是script标签，所以它读不到AJAX那么精确的状态，不知道状态码，响应头，只知道成功或者失败，只能发GET请求。

webpack中的loader和plugin的作用是什么webpack是一个模块打包器， 根据每个模块文件之间的依赖关系将所有的模块打包（bundle）起来loader就是加载器（用来load一个文件）plugin就是一个插件（就是用来加强功能的）loader一般情况下是一对一plugin一般是多对一，也有一对多的，但是比较少见
	1. 给webpack一个js文件，它通过一个内置的babel-loader的东西将这个js文件放到webpack中，然后webpack就会输出一个另外的js文件
	2. 同样也会引入一个css，它通过style-loader和css-loader两个loader将css文件变成一个style标签（这个标签也是JS生成的，所以在某种程度上来讲它也是一个JS），还有一种情况，它可以通过一个插件MIniCssExtractPlugin将n个CSS文件变成一个CSS文件
	3. HTML是0个或者一个HTML文件通过HtmlWebpackPlugin这个插件来生成一个新的Html文件，这个HTML文件和 之前的区别就是它自动引入了上面的css和js

函数防抖和函数节流：函数防抖：简单点来说就是带着一起做，一段时间内会等，然后带着一起做function debounce(fn,delay){    let timerId = null    return function(){        if(timerId){window.clearTimeout(timerId)}        timerId = setTimeout(()=>{            fn.apply(this,arguments)            timerId = null        },delay)    }}函数节流：就是一段时间执行完一次之后，就不会执行第二次function throttle(fn,delay){    let canUse = true    return function(){        if(canUse){            fn.apply(this,arguments)            canUse = false            setTimeout(()=>{                canUse = true            },delay)        }    }}原型链和继承：当访问一个对象的某个属性时，会先在这个对象本身属性上查找，如果没有找到，则会去它的__proto__隐式原型上查找，即它的构造函数的prototype，如果还没有找到就会再在构造函数的prototype的__proto__中查找，这样一层一层向上查找就会形成一个链式结构，我们称为原型链。对象.__proto__===其构造函数的.prototypeObject.prototype是所有对象的（直接或间接）的原型所有函数都是有Fuction构造的
	1. 基于原型的继承：

function Parent(name1) {    this.name1 = name1}parent.prototype.pMethod = () => {    console.log(this.name1)}function Child(name1, name2) {    Parent.call(this, name1)    this.name2 = name2}Child.prototype.__proto__ = Parent.prototypeChild.prototype.cMethod = () => {    console.log(this.name2)}2. 基于class的继承：class Parent {    constructor(name1) {        this.name1 = name1    }    pMethod() {        console.log(this.name1)    }}class Child extends Parent {    constructor(name2, name1) {        super(name1)        this.name2 = name2    }    cMethod() {        console.log(this.name2)    }}不要使用 class，写一个 Person 构造函数function Person(name, age) {    this.name = name;    this.age = age;}Person.prototype.sayHi = function () {    console.log('你好，我叫' + this.name);}let person = new Person('frank', 18)person.name === 'frank' // trueperson.age === 18 // trueperson.sayHi() // 打印出「你好，我叫 frank」请用 class 再实现一次上面的功能class Person {    constructor(name, age) {        this.name = name;        this.age = age;    }    sayHi() {        console.log('你好，我叫' + this.name);    }}let person = new Person('frank', 18)person.name === 'frank' // trueperson.age === 18 // trueperson.sayHi() // 打印出「你好，我叫 frank」constructor 是一种用于创建和初始化class创建的对象的特殊方法。使用与运算符判断奇数还是偶数
	* 偶数&1 = 0
	* 奇数&1 = 1

使用~，>>,<<,>>>,|来取整
	* console.log(~~ 6.83)  //6 因为位运算符不支持小数
	* console.log(6.83 >> 0)  //6
	* console.log(6.83 << 0)  //6
	* console.log(6.83 | 0)  //6
	* console.log(6.83 >>> 0)  //6

使用^来交换a b的值
	* [a,b] = [b,a]
	* a = a^b

           b = b^a           a = a^b.join（）把数组转为字符串，通过括号中的内容进行分割数组排序：
	1. 使用递归

let sort = (numbers) => {    if (numbers.length > 2) {        let index = minIndex(numbers)        let min = numbers[index]        numbers.splice(index, 1)        return [min].concat(sort(numbers))    } else {        return numbers[0] < numbers[1] ? numbers : numbers.reverse()    }}let minIndex = (numbers) => numbers.indexOf(min(numbers))let min = (numbers) => {    if (numbers.length > 2) {        return min([numbers[0], min(numbers.slice(1))])    } else {        return Math.min.apply(null, numbers)    }}// 选择排序最终代码let sort = (numbers) => {    for (let i = 0; i < numbers.length - 1; i++) {        let index = minIndex(numbers.slice(i)) + i        if (index !== i) {            swap(numbers, index, i)        }    }    return numbers}let swap = (array, i, j) => {    let temp = array[i]    array[i] = array[j]    array[j] = temp}let minIndex = (numbers) => {    let index = 0    for (let i = 1; i < numbers.length; i++) {        if (numbers[i] < numbers[index]) {            index = i        }    }    return index}// 快速排序let quickSort = arr => {    if (arr.length <= 1) {        return arr;    }    let pivotIndex = Math.floor(arr.length / 2); //小于或等于指定数字的最大整数    let pivot = arr.splice(pivotIndex, 1)[0]; //基准拿出来    let left = [];    let right = [];    for (let i = 0; i < arr.length; i++) {        if (arr[i] < pivot) {            left.push(arr[i])        } else {            right.push(arr[i])        }    }    return quickSort(left).concat(        [pivot], quickSort(right))}// 归并排序（一半一半的排）let mergeSort = arr => {    let k = arr.length    if (k === 1) {        return arr    }    let left = arr.slice(0, Math.floor(k / 2))    let right = arr.slice(Math.floor(k / 2))    return merge(mergeSort(left), mergeSort(right))}let merge = (a, b) => {    if (a.length === 0) return b    if (b.length === 0) return a    return a[0] > b[0] ? [b[0]].concat(merge(a, b.slice(1))) : [a[0]].concat(merge(a.slice(1), b))}// 计数排序（先找出最大的和最小的，开辟长度为(max-min+1)的空间）let countSort = arr => {    let hashTable = {},        max = 0,        result = []    for (let i = 0; i < arr.length; i++) { // 遍历数组        if (!(arr[i] in hashTable)) {            hashTable[arr[i]] = 1        } else {            hashTable[arr[i]] += 1        }        if (arr[i] > max) {            max = arr[i]        }    }    for (let j = 0; j <= max; j++) { // 遍历哈希表        if (j in hashTable) {            for (let i = 0; i < hashTable[j]; i++) {                result.push(j)            }        }    }    return result}如何实现数组去重？
	1. 老方法：

for (let i = 0; i < array.length - 1; i++) {    let item = array[i]    for (let j = i + 1; j < array.length - 1; j++) {        if (array[j] === item) {            array.splice(j, 1)            j--;        }    }}最大的缺点浪费性能，每一个元素都和其他的元素比较了一遍，时间复杂度不友好
	1. 使用Set

let item = [...new Set(array)] ...扩展运算符缺点：ES6毕竟是新出的，所以会考虑兼容问题
	1. 使用Map

function noRepeat(arr) {    let hashMap = new Map()    let result = new Array()    for (let i = 0; i < arr.length - 1; i++) {        if (hashMap.has(arr[i])) {            hashMap.set(arr[i], false)        } else {            hsahMap.set(arr[i], true)            result.push(arr[i])        }        return result    }}这种方法不但可以做到去重，还可以知道是哪些元素重复了缺点：不能过滤掉重复的Object创建对象的几种方式：
	1. new Object()
	2. 字面式创建：let person = {name:'kaku'}
	3. 工厂模式：上面两种方法在使用同一个接口创建多个对象的时候，会产生大量的重复代码     function createPerson(name,age,family) {
var o = new Object();o.name = name;o.age = age;o.family = family;o.say = function(){alert(this.name);}return o;}	4. 构造函数模式：function Person(name,age){this.name = name; this.age = age}
	5. 原型模式：function Person(){}   Person.prototype.name = 'lu';   Person.prototype.age = 22

new一个对象的时候发生了什么：
	1. 新生成一个对象
	2. 链接到原型obj.__proto__= Object.prototype
	3. 绑定this
	4. 返回新对象

function newGenerater(fn, ...args) {    const result = new Object();    result.__proto__ = fn.prototype;    const res = fn.call(result, ...args);    return (typeof res === 'object' && res !== null) ? res : result;}js中this的指向：
	1. fn()this => window/global
	2. obj.fn()this => obj
	3. fn.call(xx)this => xx
	4. fn.apply(xx)this => xx
	5. fn.bind(xx)this => xx
	6. new Fn()this => 新的对象
	7. fn = ()=> {}this => 外面的 this

HTTP和TCP的关系：TCP是传输层，而http是应用层http是要基于TCP连接基础上的，简单的说，TCP就是单纯建立连接，不涉及任何我们需要请求的实际数据，简单的传输。http是用来收发数据，即实际应用上来的。HTTP协议中的数据是利用TCP协议传输的，所以支持HTTP也就一定支持TCP      HTTP属于无状态协议(Stateless)。这表示每一个请求之间是没有相关性的。Cookie V.S. LocalStorage V.S. SessionStorage V.S. Session
	* Cookie V.S. LocalStorage

		1. 主要区别是 Cookie 会被发送到服务器，而 LocalStorage 不会
		2. Cookie 一般最大 4k，LocalStorage 可以用 5Mb 甚至 10Mb（各浏览器不同）
	* LocalStorage V.S. SessionStorage

		1. LocalStorage 一般不会自动过期（除非用户手动清除），而 SessionStorage 在回话结束时过期（如关闭浏览器）
	* Cookie V.S. Session

		1. Cookie 存在浏览器的文件里，Session 存在服务器的文件里
		2. Session 是基于 Cookie 实现的，具体做法就是把 SessionID 存在 Cookie 里

DocType的作用：声明位于文档最前面，告诉浏览器应该用什么样的方式来渲染页面严格模式：以浏览器支持的最高标准执行混杂模式：向后兼容，防止浏览器无法兼容页面数据库的事务概念以及特性：事务，简短的说就是一组操作要么全部完成，要么全部不做，绝不允许只做其中的一部分操作。
	* 原子性
	* 一致性
	* 隔离性：并发 【对于任意两个并发的事务A和B，在事务A看来，B要么在A开始之前就已经结束，要么在A结束之后才开始，这样每个事务都感觉不到有其他事务在并发地执行。】
	* 持久性：对数据库中的数据的改变就是永久性的

Position有哪些取值：
	1. relative： 但其在文本流中的位置依然存在。
	2. absolute： 脱离文档流，但与relative的区别是其在正常流中的位置不再存在。 绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
	3. static(默认值)
	4. fixed： 相对于浏览器窗口进行定位。
	5. sticky：粘滞定位，兼容很差

vm = new Vue({data:myData})做了哪些事情
	1. 会让vm称为myData的代理（proxy）
	2. 会对myData的所有属性进行监控
	3. 监控就是为了防止myData的属性变了，vm不知道
	4. vm知道了之后就可以调用render(data）UI=render(data）

vue双向绑定是怎么实现的：vue实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty() 数据劫持，来劫持各个属性的setter，getter，在数据更新时发布消息给订阅者，触发相应监听回调。Vue的响应式原理：创建Vue实例时，将data中所有property遍历，通过Object.defineProperty把属性全部转为getter、setter，通过观察者模式（watcher），在调用setter时（修改数据时），通知依赖更新，但是Vue不能检测到对象属性的添加或者删除，这个时候要使用Vue.set和Vue.$set可以搞定
	1. 当一个值被读取时进行追踪， proxy 的 get 处理函数中 track 函数记录了该 property 和当前副作用。
	2. 当某个值改变时进行检测， 在 proxy 上调用 set 处理函数
	3. 重新运行代码来读取原始值，  trigger 函数查找哪些副作用依赖于该 property 并执行它们。
	4. target:要使用 Proxy 包装的目标对象（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）。
	5. handler:一个通常以函数作为属性的对象，各属性中的函数分别定义了在执行各种操作时代理 p 的行为。

我们使用了Proxy ，Proxy是一个对象，它包装了另一个对象，并允许你拦截对该对象的任何交互。const p = new Proxy(target, handler)VueRouter 你怎么用的？

		1. 背下文档第一句：Vue Router 是 Vue.js 官方的路由管理器。
		2. 说出核心概念的名字和作用：History 模式/导航守卫/路由懒加载
		3. 说出常用 API：router-link/router-view/this.$router.push/this.$router.replace/this.$route.paramsthis.$router.push('/user-admin')this.$route.params

路由守卫(导航守卫)是什么？路由跳转是一个大的过程，这个大的过程分为跳转前中后等等细小的过程，在每一个过程中都有一函数，这个函数能让你操作一些其他的事儿的时机，这就是导航守卫。
	* 全局前置守卫
	* 全局解析守卫
	* 全局后置钩子
	* 路由独享守卫
	* 组件内的守卫

路由懒加载怎么做：不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件import('./Foo.vue') //返回Promisewatch 和 computed 和 methods 区别是什么？
	1. computed 和 methods 相比，最大区别是 computed 有缓存：如果 computed 属性依赖的属性没有变化，那么 computed 属性就不会重新计算。methods 则是看到一次计算一次。
	2. watch 和 computed 相比，computed 是计算出一个属性（废话），而 watch 则可能是做别的事情（如上报数据）。

声明周期钩子：
	1. 要特别说明哪个钩子里请求数据，答案是 mounted

Vue 如何实现组件间通信？
	1. 父子组件：$emit('xxx',data)  $on('xxx',function(){})
	2. 爷孙组件：使用两次 v-on 通过爷爷爸爸通信，爸爸儿子通信实现爷孙通信
	3. 任意组件：使用 eventBus = new Vue() 来通信，eventBus.$on 和 eventBus.$emit 是主要API
	4. 任意组件：使用 Vuex 通信

Vuex 你怎么用的？

		1. 背下文档第一句：Vuex 是一个专为 Vue.js 应用程序开发的状态管理工具
		2. 说出核心概念的名字和作用：State/Getter/Mutation/Action/Module

state => 基本数据getters => 从基本数据派生的数据mutations => 提交更改数据的方法，同步！actions => 像一个装饰器，包裹mutations，使之可以异步。modules => 模块化Vuex这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。CSS语义化命名：header 头部/页眉；logo 标志；nav/sub_nav 导航/子导航；banner 横幅广告；main/content 主体/内容；container/con 容器；wrapper/wrap 包裹（类似于container）；menu 菜单；sub_menu/second_menu 子菜单/二级菜单；list 列表；section 分区/分块（类似于div）;article 文章；aside 侧边栏/广告；footer 页脚/底部；title/sub_title 标题/副标题；news 新闻；hot 热点；pro 产品（product）；company 公司；msg/info 信息（message）/消息；ads 广告（advertisements）;icon 小图标；copyright 版权；contact_us 联系我们；friend_link 友情链接；tel 联系电话（telephone）；address 地址；首先介绍一下HTTPHTTP 协议，全称Hyper Text Transfer Protocol，超文本传输协议，它是一种规范，完成从客户端到服务器端等一系列运作流程。HTTP不同版本特点
	* 0.9：请求方式只支持GET请求
	* 1.0：请求方式增加了post，put，options等，增加了状态码，用来明确错误类型
	* 1.1：头信息是二进制，数据可以是二进制也可以是文本，增加了持久链接和管道机制
	* 2.0：二进制传输，多路复用，头部压缩

请求的几种方式：
	* OPTIONS 返回服务器所支持的请求方法
	* GET 向服务器获取指定资源
	* HEAD 与GET一致，只不过响应体不返回，只返回响应头
	* POST 向服务器提交数据，数据放在请求体里
	* PUT 与POST相似，只是具有幂等特性，一般用于更新
	* DELETE 删除服务器指定资源
	* TRACE 回显服务器端收到的请求，测试的时候会用到这个
	* CONNECT 预留，暂无使用

POST 请求的过程：浏览器请求TCP连接（第一次握手）服务器答应进行 TCP 连接（第二次握手）浏览器确认，并发送 POST 请求头（第三次握手，这个报文比较小，所以 HTTP 会在此时进行第一次数据发送）服务器返回100 Continue响应浏览器发送数据服务器返回 200 OK响应GET 请求的过程：浏览器请求 TCP 连接（第一次握手）服务器答应进行 TCP 连接（第二次握手）浏览器确认，并发送 GET 请求头和数据（第三次握手，这个报文比较小，所以 HTTP 会在此时进行第一次数据发送）服务器返回 200 OK响应get和POST的区别：
	1. 本质上一样，只是http为了不同的分工而规定的两种请求方式，http的底层是TCP/IP，所以get和post的底层也是TCP/IP


	1. 作用不同：get多用于从服务器获取资源，post一般向服务端提交资源
	2. 参数传递方式不同：get提交的数据在地址栏中可以看见，post提交的数据可以在开发者工具中看到，放到了叫做from data中
	3. 安全性不同：get和post更不安全，它直接暴露在url上，从传输的角度来说，都不安全，因为http在网络上是明文传输的，只要抓包都能获取完整信息，想要安全只能加密传输也就是使用HTTPS
	4. 长度限制不同：get请求，http规范对url的长度没有限制，只是不同的浏览器对它做了限制（一般上url长度不要超过2kb就好）post请求也没有长度限制，限制它的是服务器的处理能力与存储大小，还有就是web容器的限制，比如Tomcat默认2M
	5. 参数数据类型不同：get只接受ASCII字符，post支持更多的编码类型
	6. 缓存机制不同：GET 请求会被浏览器主动cache，而 POST 不会，除非手动设置。GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留。GET 在浏览器回退时是无害的，而 POST 会再次提交请求。
	7. 时间消耗不同：get产生一个tcp数据包，post会产生两个数据包

浏览器输入url后，发生了什么：
	1. 解析url
	2. DNS解析
	3. 浏览器与网站建立TCP连接（三次握手）
	4. 请求和传输数据
	5. 浏览器渲染页面


	* 浏览器会解析html源码，然后创建一个 DOM树。
	* 浏览器解析CSS代码，计算出最终的样式数据，形成css对象模型CSSOM。
	* 利用DOM和CSSOM构建一个渲染树（rendering tree）。
	* 浏览器就根据渲染树直接把页面绘制到屏幕上。

http的报文格式：首部内容由以下数据组成：
	* 请求行：请求方法、请求URI、HTTP版本
	* 状态行：标明响应结果的的状态码，原因短语和HTTP版本。
	* 首部字段：一般是通用首部、请求首部、响应首部和实体首部。
	* 其他


	1. 报文首部

首部：在客户端和服务器处理时起重要作用的信息几乎都在这边主体：所需要的用户和资源的信息都在这边1.1 HTTP请求报文
	* 请求行：方法、URI、HTTP版本
	* 请求头：首部字段（请求首部字段、通用首部字段、实体首部字段）
	* 请求体：发送的数据

1.2 HTTP响应报文
	* 响应行：HTTP版本号、状态码、原因短语
	* 响应头：响应首部字段、通用首部字段、实体首部字段
	* 响应体：响应的数据

 报文主体和实体主体的差异
	* 报文是HTTP通信中的基本单位，由8位组字节流组成，通过HTTP通信传输。
	* 实体作为请求或相应的有效何在数据（补充项）被传输，其内容由实体首部和实体主体组成。

协议层数：
