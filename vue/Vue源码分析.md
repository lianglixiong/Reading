# Vue源码分析

## 为Vue prototype 原型添加方法

## initMixin为Vue prototype添加_init方法,Vue构造函数实例化对象时候就会调用该方法

## stateMixin为Vue prototype添加 set，$delete，$watch方法

## eventsMixin为事件初始化，为Vue prototype添加$on，$once ，$off，$emit方法

## lifecycleMixin方法是，为Vue prototype添加_update，$forceUpdate，$destroy方法

## renderMixin 渲染方法，为Vue prototype添加_o,_n,_s,_l,_t,_q,_i,_m,_f,_k,_b,_v,_e,_u,_g ， $nextTick ，_render方法

## 此时Vue prototype 原型中已经含有_init， set，$delete，$watch，$on，$once ，$off，$emit，update，$forceUpdate，$destroy,_o,_n,_s,_l,_t,_q,_i,_m,_f,_k,_b,_v,_e,_u,_g ， $nextTick ，_render的方法，在在一万多行中又添加了__patch__和$mount方法

## Vue初始化函数，未new Vue的时候

## initGlobalAPI为Vue添加静态方法和属性

## defineProperty  监听‘config’设置配置改值不可以修改

## 添加 Vue.util 工具类，但是这不是公共api 外部用户最好不要用

## 添加Vue.set 静态方法 用于更新视图

## 添加 Vue.delete 静态方法 用于删除数据

## 添加Vue.nextTick静态方法 用于更新视图后回调递归

## 添加Vue.options静态属性，并且在该对象中添加components,directives,filters静态对象 记录静态组件

## initUse方法为Vue添加 Vue.use静态方法 安装插件

## initMixin$1方法为Vue添加 Vue.mixin静态方法 合并参数

## initExtend为方法Vue添加 Vue.extend 继承使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。

## initAssetRegisters方法为Vue添加component，directive，filter 静态方法 定义组件，指令 过滤器

## 此时Vue静态方法有set，delete，nextTick，use，mixin，extend，component，directive，filter 

## new Vue实例化对象

## 调用_init方法传options进去，创建vm._uid

## 该为组件调用initInternalComponent初始化组件需要的参数

## 调用mergeOptions合并options参数

## 调用resolveConstructorOptions合并vm.constructor构造函数的属性options，就是当用户用了vue的静态方法拓展了一些组件或者参数

## 最终集合在  vm.$options

## initProxy 代理监听Vue 获取值，或者是添加观察者模式key判断 为vm实例化对象添加了_renderProxy 方法

## initLifecycle初始化生命周期标志此时vm构造对象添加了$root，$children ，$refs，_watcher，_inactive， _directInactive，_isMounted，_isBeingDestroyed等属性和标志

## initEvents初始化组件事件

## updateComponentListeners 更新组件事件，删除旧的事件，添加新的事件

## updateListeners更新事件

## add 添加事件

## 调用$once 只执行一次函数就解绑

## initRender 初始化渲染 为vm实例化的对象添加_vnode，_staticTrees，renderContext，$slots，$scopedSlots等属性或者对象，更重要的是添加了_c和$createElement这两个渲染方法，并且把$attrs属性和$listeners事件属性添加到defineReactive观察者中，监听此数据只能只读，如果修改则发出警告

## vue响应式双数据绑定从这里开始，defineReactive 过defineProperty的set，get方法监听数据变化，实例化dep对象

## 判断property.get是否存在，如果存在则说明该数据已经添加过 defineProperty 则使用 property.get 否则直接获取值

## 判断property.set是否存在，如果存在则说明该数据已经添加过 defineProperty 则使用 property.set 否则直接设置值

## observe方法 参数 value必需是对象 ，如果不是对象或者value对象属性configurable为假的是否则退出函数，所以递归跳出条件在这里，实例化 dep对象,获取dep对象  为 value添加__ob__ 属性，返回 new Observer 实例化的对象

## Observer为value添加dep对象，vmCount标记，如果value为对象并且值是{msg:'hello'} 此时value数据变成这样{value:{__ob__:{value:value, dep:new Dep(),vmCount:0}}}   __ob__  即Observer构造实例化的对象，__ob__ 对象prototype 还包含两个方法  walk和 observeArray

## observeArray 循环value把数组拆分调用observe，如果多层数据是数组则会递归下去

## Watcher中的addDep 添加dep对象

## walk 遍历对象 调用defineReactive  形成递归

## Watcher构造函数实例化时候把对象添加到vm中，添加id与记录渲染方式，如果lazy为假的时候，调用get方法，把Watcher实例化对象添加到targetStack队列中，并且标记 Dep.target静态属性等于Watcher实例化对象，关键参数第二个参数可能是更新view试图函数，也能是获取值函数，也能是用户自定义函数，第三个参数及是回调把值传给用户函数

## $on添加事件 把事件推进队列去vm._events[event]

## get方法。如果lazy为假的时候，调用get方法，get方法 调用pushTarget把Watcher实例化对象添加到targetStack队列中，标志Dep.target位Watcher实例化对象，调用getter方法获取值，则是expOrFn传进来的参数，获取值返回出去

## _traverse 为seenObjects set对象深度收集value含有__ob__属性的值把depId的key，收集到seenObjects对象中

## addDep为Watcher实例化对象中添加dep对象，当调用Dep.prototype.depend的时候就会调用该方法

## Dep构造函数，主题对象Dep构造函数  主要用于添加发布事件后，用户更新数据的 ，添加实例化id，添加subs队列，此队列是存放Watcher实例化对象存储

## addSub为subs队列，添加一个Watcher实例化对象 

## removeSub删除为subs队列中的一个Watcher实例化对象 

## depend为Watcher实例化对象添加一个Dep实例化对象

## notify更新数据，调用Watcher实例化对象中的update

## cleanupDeps清理观察者依赖项集合，调用dep的removeSub从dep的subs队列中，全部删除当前watcher实例化的对象

## update更新数据根断lazy 根据lazy是否需要更新数据

## run更新数据，更新cb回调函数，包括响应View试图，虚拟dom等

## 可能为多个观察者调用queueWatcher，queueWatcher为queue队列添加Watcher实例化对象，调用flushSchedulerQueue方法

## flushSchedulerQueue，改变queue队列排序，根据Watcher实例化对象id排序，循环调用Watcher观察者的run函数更新数据

## nextTick为callbacks队列收集异步函数，根据pending状态是否更新异步队列函数

## callHook，参数2位钩子函数的key，根据key值获取钩子函数队列数组，循环队列触发钩子函数，如果是 hook: 开头的标记为vue vue系统内置钩子函数 比如vue 生命周期函数等，如果_hasHookEvent为真则触发父组件钩子函数hook:+key

## initInjections 调用resolveInject，resolveInject循环父组件，把父组件的provide值抽出来，返回去，initInjections获取到父组件的provide值加入观察者中，如果有修改到provide父组件的值则发出警告

## get方法对象描述，调取值的getter方法获取值，判断Dep.target是否为真，如果为真，或者childOb为真则调用dep的depend函数。

## set方法对象描述，调用值的setter方法设置值，然后调用dep的notify函数更新数据

## initState初始化状态，为Vue实例化对象vm添加_watchers观察者队列

## initProps初始化props，调用validateProp验证props数据是否规范，循环propsOptions的key

##   validateProp *验证支柱  验证 prosp 是否是规范数据 并且为props 添加 value.__ob__  属性，把prosp添加到观察者中
     *  校验 props 参数 就是组建 定义的props 类型数据，校验类型
     *
     * 判断prop.type的类型是不是Boolean或者String，如果不是他们两类型，调用getPropDefaultValue获取默认值并且把value添加到观察者模式中
    

## getTypeIndex 判断expectedTypes 中的函数和 type 函数是否有相等的如有有则返回索引index 如果没有则返回-1，检查是布尔型还是字符串等检查方法数据类型

## getPropDefaultValue获取props默认值，获取值返回去

## mustUseProp校验属性

## getTagNamespace判断 tag 是否是svg或者math 标签

## isSVG判断svg 标签，包括svg子元素标签

## isReservedTagr保留标签 判断是不是真的是 html 原有的标签 或者svg标签

## isHTMLTag 函数，验证是否是html中的原始标签

## isReservedAttr验证属性是不是style,class

## assertProp判断props是否是必填的，判断type是否存在，type 必须是String|Number|Boolean|Function|Symbol 构造函数 simpleCheckRE.test(expectedType)才为真，expectedTypes为收集type 为输出日志

## getType检查函数是否是函数声明  如果是函数表达式或者匿名函数是匹配不上的

## assertType检测type的类型是什么，返回类型值

## loop 校验props的key，调用validateProp方法校验key，把props的value调用defineReactive方法添加到观察者里面，回调函数是警告禁止修改的日志

## initMethods初始化事件，校验事件的key有没有和props属性一样的，如果一样，或者事件为空，或者事件是$或者_开头的字母，则警告，然后把事件放在vm中，这样this就可以调用到，然后绑定事件

## bind 绑定事件

## polyfillBind bin不存在使用apply或者call

## nativeBind绑定事件fn.bind(ctx)

## initData初始化数据，判断数据data是不是方法，循环校验data的key不能和methods对象与props属性对象中的kye一样，如果一样则发出警告。

## getData，直接调用data() 返回data

## proxy添加观察者，比如 name 只能在Odata.data.name 获取到数据，执行 proxy(Odata,'data','name')之后可以Odata.name 获取值

## initComputed初始化属性计算，在vm中中创建_computedWatchers 监听者对象，循环computed属性并且，判断属性key是否在vm中。

## defineComputed根据shouldCache判断是否是浏览器调用createComputedGetter 为_computedWatchers 收集观察者，为watcher添加dep

## createComputedGetter为_computedWatchers 收集观察者，为watcher添加dep

## initWatch循环遍历options中的watch调用createWatcher

## createWatcher 转义handler 并且为数据 创建 Watcher 观察者

## $watch实例化Watcher 观察者,判断是否是对象 如果是对象则调用createWatcher递归 深层转义handler直到它不是一个对象的时候才会跳出递归

## 调用 Vue.prototype.$watch

## initProvide方法是为provide 选项应该是一个对象或返回一个对象的函数。该对象包含可注入其子孙的属性，用于组件之间通信。

## 触发钩子函数created

## $mount() 手动地挂载一个未挂载的实例，调用1万3千多行的$mount()挂载实例。该方法是判断options.template 是否存在，如果没有则从el中找el的innerHTML，或者是template第一个如果是id则获取dom中的innerHTML，如果template.nodeType存在则是一个真实的dom则直接获取innerHTML等 获取到html。调用compileToFunctions

## createCompilerCreator编译器创建的创造者 返回一个createCompiler编译函数，函数柯里化编程 ，缓存baseCompile基本的编译函数

## 执行createCompiler创建编译器,把baseOptions参数传进去。缓存baseOptions。执行createCompileToFunctionFn函数，传compile函数进去。缓存compile函数。  返回一个对象，含有compile和compileToFunctions属性，

## createCompileToFunctionFn，创建一个缓存对象cache记录模板字符串函数，函数科里化方式，缓存compile函数

## compile克隆对象Object.create(baseOptions)，把baseOptions的方法挂在到finalOptions.__proto__中，把options参数合并到finalOptions的构造属性中。此时finalOptions原型中有baseOptions方法，和构造属性有 shouldDecodeNewlines，shouldDecodeNewlinesForHref， delimiters，comments ，warn日志输出函数。 然后 调用createCompilerCreator(function baseCompile(){  调用到这里函数 })

## baseOptions为虚拟dom添加基本需要的属性包含这些属性 expectHTML: true,
        modules: modules$1,
        directives: directives$1,
        isPreTag: isPreTag,
        isUnaryTag: isUnaryTag,
        mustUseProp: mustUseProp,
        canBeLeftOpenTag: canBeLeftOpenTag,
        isReservedTag: isReservedTag,
        getTagNamespace: getTagNamespace,
        staticKeys: genStaticKeys(modules$1)

## modules$1 属性包含 klass$1,  style$1,model$2属性，为虚拟dom添加staticClass，classBinding，staticStyle，styleBinding，for，alias，iterator1，iterator2，addRawAttr ，type ，key， ref，slotName或者slotScope或者slot，component或者inlineTemplate ，      plain，if ，else，elseif 属性


## klass$1属性包含 staticKeys: ['staticClass'],
        transformNode: transformNode,
        genData: genData

## transformNode获取 class 属性和:class或者v-bind的动态属性值，并且转化成字符串 添加到staticClass和classBinding 属性中，为虚拟dom添加staticClass，classBinding属性

## getAndRemoveAttr移除传进来的属性name，并且返回获取到 属性的值

## getBindingAttr获取 :属性 或者v-bind:属性，或者获取属性 移除传进来的属性name，并且返回获取到 属性的值

## genData 转换class，返回转换数据。       //el.staticClass 比如我们设置样式是这样  class="classA classB" 此时将数据变成   staticClass:classA classB,                   //el.staticClass 比如我们设置样式是这样  class="classC classD" 此时将数据变成   class:classC classD,

## style$1属性包含   staticKeys: ['staticStyle'],
        transformNode: transformNode$1,
        genData: genData$1

## transformNode$1获取 style属性和:style或者v-bind的动态属性值，并且转化成字符串 添加到staticStyle和styleBinding属性中为虚拟dom添加staticStyle，styleBinding属性

## parseStyleText把style 字符串 转换成对象 比如'width:100px;height:200px;' 转化成 {width:100px,height:200px}

## genData 转换class，返回转换数据。       //比如staticStyle的值是  {width:100px,height:200px} 转换成 staticStyle:{width:100px,height:200px},
                          //比如styleBinding的值是  {width:100px,height:200px} 转换成 style:(width:100px,height:200px),
         

## model$2把attrsMap与attrsList属性值转换添加到el   ast虚拟dom中为虚拟dom添加for，alias，iterator1，iterator2，addRawAttr ，type ，key， ref，slotName或者slotScope或者slot，component或者inlineTemplate ， plain，if ，else，elseif 属性


## preTransformNode把attrsMap与attrsList属性值转换添加到el   ast虚拟dom中为虚拟dom添加for，alias，iterator1，iterator2，
addRawAttr ，type ，key， ref，slotName或者slotScope或者slot，component或者inlineTemplate ， plain，if ，else，elseif 属性


## cloneASTElement克隆ast元素

## createASTElement创建ast元素， //转换属性，把数组属性转换成对象属性，返回对象 AST元素

## processFor检测是否有v-for指令判断获取v-for属性是否存在如果有则转义 v-for指令 把for指令添加到虚拟dom中

## parseFor转换v-for属性，//转换 for指令 获取 for中的key  返回一个res对象为{for:data字符串，alias：value字符串，iterator1:key字符串，iterator2:index字符串}
   

## addRawAttr添加原始dom attr(在预转换中使用)

## processElement 校验属性的值，为el 虚拟dom添加muted， events，nativeEvents，directives，  key， ref，slotName或者slotScope或者slot，component或者inlineTemplate 标志 属性
                

## processKey获取属性key值，校验key 是否放在template 标签上面 为el 虚拟dom添加 key属性

## processRef获取ref 属性，并且判断ref 是否含有v-for指令 为el虚拟dom 添加 ref 属性

## processSlot  检查插槽作用域 为el虚拟dom添加 slotName或者slotScope或者slot

## processComponent判断虚拟dom 是否有 :is属性，是否有inline-template 内联模板属性 如果有则标记下

## processAttrs  检查属性，为虚拟dom属性转换成对应需要的虚拟dom vonde数据 为el虚拟dom 添加muted， events，nativeEvents，directives
     

## addHandler   为虚拟dom添加events 事件对象属性，如果添加@click='clickEvent' 则此时 虚拟dom为el.events.click.value="clickEvent"
或者虚拟dom添加nativeEvents 事件对象属性，如果添加@click.native='clickEvent' 则此时 虚拟dom为el.nativeEvents.click.value="clickEvent"

## genAssignmentCode创赋值代码返回 key"=" value
     * 或者 $set(object[info],key,value)

## parseModel   转义字符串对象拆分字符串对象  把后一位key分离出来
两种情况分析1 如果数据是object.info.name的情况下 则返回是 {exp: "object.info",key: "name"}
如果数据是object[info][name]的情况下 则返回是 {exp: "object[info]",key: "name"}

## addProp添加props属性

## addAttr添加普通的属性 在attrs属性中

## addDirective为虚拟dom 添加一个 指令属性 对象

## checkForAliasModel检查指令的命名值 不能为for 或者 for中的遍历的item

## directives$1对象有     {
        model: model, 
        text: text,
        html: html
    }  根据判断虚拟dom的标签类型是什么？给相应的标签绑定 相应的 v-model 双数据绑定代码函数，为虚拟dom添加textContent 属性，为虚拟dom添加innerHTML 属性

## model根据判断虚拟dom的标签类型是什么？给相应的标签绑定 相应的 v-model 双数据绑定代码函数    

## genComponentModel为虚拟dom添加model属性，属性对象为value: ("(" + value + ")"), // 绑定v-model 的值
            expression: ("\"" + value + "\""), //绑定v-model 的值
            //函数  $set(object[info],key,$$v) //$set更新值函数
            callback: ("function (" + baseValueExpression + ") {" + assignment + "}")   回调函数是 $set(object[info],key,$$v) //$set更新值函数

## genSelect 为虚拟dom添加change 函数 ，change函数调用 set 去更新 select选中数据的值

##   genCheckboxModel 为input type="checkbox" 虚拟dom添加 change 函数 ，根据v-model是否是数组，调用change函数，调用 set 去更新 checked选中数据的值
 

## genRadioModel为虚拟dom  inpu标签 type === 'radio' 添加change 事件 更新值  

## genDefaultModel如果虚拟dom标签是  'input' 类型不是checkbox，radio 或者是'textarea' 标签的时候，获取真实的dom的value值调用 change或者input方法执行set方法更新数据
   

## text为虚拟dom添加textContent 属性

## html为虚拟dom添加innerHTML 属性

## isPreTag判断标签是否是pre

## isUnaryTag匹配标签是否是 'area,base,br,col,embed,frame,hr,img,input,isindex,keygen, link,meta,param,source,track,wbr'

## mustUseProp 校验属性
        /*
         * 1. attr === 'value', tag 必须是 'input,textarea,option,select,progress' 其中一个 type !== 'button'
         * 2. attr === 'selected' && tag === 'option'
         * 3. attr === 'checked' && tag === 'input'
         * 4. attr === 'muted' && tag === 'video'
         * 的情况下为真
         * */

## canBeLeftOpenTag判断标签是否是 'colgroup,dd,dt,li,options,p,td,tfoot,th,thead,tr,source'    

## getTagNamespace判断 tag 是否是svg或者math 标签

## genStaticKeys 把数组对象[{ staticKeys:1},{staticKeys:2},{staticKeys:3}]连接数组对象中的 staticKeys key值，连接成一个字符串 str=‘1,2,3’
    

## baseCompile基本的编译函数, //把html变成ast模板对象，然后再转换成 虚拟dom 渲染的函数参数形式。
  // 返回出去一个对象
  // {ast: ast, //ast 模板
// render: code.render, //code 虚拟dom需要渲染的参数函数
 //staticRenderFns: code.staticRenderFns } //空数组

## compileToFunctions函数把 template, //模板字符串和options参数 {
                        shouldDecodeNewlines: shouldDecodeNewlines, //flase //IE在属性值中编码换行，而其他浏览器则不会
                        shouldDecodeNewlinesForHref: shouldDecodeNewlinesForHref, //true chrome在a[href]中编码内容
                        delimiters: options.delimiters, //改变纯文本插入分隔符。修改指令的书写风格，比如默认是{{mgs}}  delimiters: ['${', '}']之后变成这样 ${mgs}
                        comments: options.comments //当设为 true 时，将会保留且渲染模板中的 HTML 注释。默认行为是舍弃它们。
                    },传进去 到执行compile函数

## parse 将HTML字符串转换为AST。

## parseHTML函数     while (html)  循环html,查找截取tag标签，tag属性，指令，组件等。通过advance函数去截取每次匹配过的标签属性等。通过baseOptions里面的函数去转义成ast对象模板，挂载在root中

## advance//截取字符串重新循环  while 跳出循环就是靠该函数，每次匹配到之后就截取掉字符串，知道最后一个标签被截取完没有匹配到则跳出循环

## comment   //把text添加到属性节点或者添加到注释节点，ast模板数据

## parseStartTag   //获取开始标签的名称，收集属性集合，开始位置和结束位置，并且返回该对象
                                                                

## handleStartTag         //把数组对象属性值循环变成对象，这样可以过滤相同的属性
         //为parseHTML 节点标签堆栈 插入一个桟数据
        //调用options.start  为parse函数 stack标签堆栈 添加一个标签

## isNonPhrasingTag 判断标签是否是
                'address,article,aside,base,blockquote,body,caption,col,colgroup,dd,' +
                'details,dialog,div,dl,dt,fieldset,figcaption,figure,footer,form,' +
                'h1,h2,h3,h4,h5,h6,head,header,hgroup,hr,html,legend,li,menuitem,meta,' +
                'optgroup,option,param,rp,rt,source,style,summary,tbody,td,tfoot,th,thead,' +
                'title,tr,track'

## parseEndTag  //查找parseHTML的stack栈中与当前tagName标签名称相等的标签，
        //调用options.end函数，删除当前节点的子节点中的最后一个如果是空格或者空的文本节点则删除，
        //为stack出栈一个当前标签，为currentParent变量获取到当前节点的父节点

## options.start 函数   //标签开始函数， 创建一个ast标签dom，  判断获取v-for属性是否存在如果有则转义 v-for指令 把for，alias，iterator1，iterator2属性添加到虚拟dom中
                                                        //获取v-if属性，为el虚拟dom添加 v-if，v-eles，v-else-if 属性
                                                        //获取v-once 指令属性，如果有有该属性 为虚拟dom标签 标记事件 只触发一次则销毁
                                                        //校验属性的值，为el添加muted， events，nativeEvents，directives，  key， ref，slotName或者slotScope或者slot，component或者inlineTemplate 标志 属性
                                                        // 标志当前的currentParent当前的 element
                                                        //为parse函数 stack标签堆栈 添加一个标签

## options.end函数， //删除当前节点的子节点中的最后一个如果是空格或者空的文本节点则删除，
                                                    //为stack出栈一个当前标签，为currentParent变量获取到当前节点的父节点
                                                  

## processPre检查标签是否有v-pre 指令 含有 v-pre 指令的标签里面的指令则不会被编译

## decodeAttr //替换html 中的特殊符号，转义成js解析的字符串,替换 把   &lt;替换 <  ， &gt; 替换 > ， &quot;替换  "， &amp;替换 & ， &#10;替换\n  ，&#9;替换\t
   

## options.chars //把text添加到属性节点或者添加到注释节点，ast模板数据

## optimize//optimize 的主要作用是标记标签是不是静态节点，

## generate   //初始化扩展指令，on,bind，cloak,方法， dataGenFns 获取到一个数组，数组中有两个函数genData和genData$1
    //genElement根据el判断是否是组件，或者是否含有v-once，v-if,v-for,是否有template属性，或者是slot插槽，转换style，css等转换成虚拟dom需要渲染的参数函数
  

## markStatic$1循环递归虚拟node，标记不是静态节点

## markStaticRoots第二步:标记静态根。 //根据node.static或者 node.once 标记staticRoot的状态

## pluckModuleFunction   //循环过滤数组或者对象的值，根据key循环 过滤对象或者数组[key]值，如果不存在则丢弃，如果有相同多个的key值，返回多个值的数组
  

## dataGenFns获取到一个数组，数组中有两个函数genData和genData$1

## CodegenState    //生成状态添加options构造属性就是baseOptions对象，包含html转ast的方法，
    // *  扩展指令，为directives构造属性添加on,bind，cloak,方法。添加warn构造属性，
    // *  添加dataGenFns构造属性 获取到一个数组，数组中有两个函数genData和genData$1

## genElement//根据el判断是否是组件，或者是否含有v-once，v-if,v-for,是否有template属性，或者是slot插槽，转换style，css等转换成虚拟dom需要渲染的参数函数，类似于这样的函数(function (function anonymous(
                 ) {
                   
                      with(this){return _c('div',{attrs:{"id":"app"}},[_c('input',{directives:[{name:"info",rawName:"v-info"},{name:"data",rawName:"v-data"}],attrs:{"type":"text"}}),_v(" "),_m(0),_v(" "),_c('div',[_v("\n        "+_s(message)+"\n    ")])])}
                 })
  

## genStatic将子节点导出虚拟dom 渲染函数的参数形式。静态渲染，返回虚拟dom渲染需要的参数格式

## genOnce，onceProcessed标志已经处理过的

## genIf判断标签是否含有if属性

## 循环父节点回调调用genElement

## genFor将子节点导出虚拟dom 渲染函数的参数形式。for渲染，返回虚拟dom渲染需要的参数格式

## 返回一个vnode 虚拟dom需要渲染的函数，回调回调genElement函数，获取该需要的code

## genIfConditions解析 if指令中的参数 并且返回 虚拟dom需要的参数js渲染函数

## genTernaryExp返回一个vnode 虚拟dom需要渲染的函数

## genChildren返回虚拟dom vonde渲染调用的函数

## getNormalizationType     //确定子数组所需的标准化。
                                      如果children.length==0 就返回0，如果如果有for属性存在或者tag等于template或者是slot 则问真就返回1，如果是组件则返回2

## needsNormalization如果for属性存在或者tag等于template或者是slot 则问真

## genNode根据node.type 属性不同调用不同的方法,得到不同的虚拟dom渲染方法

## genComment返回虚拟dom vonde渲染调用的函数

## genText返回虚拟dom vonde渲染调用的函数

## transformSpecialNewlines     \u2028	 	行分隔符	行结束符
     \u2029	 	段落分隔符	行结束符
     这个编码为2028的字符为行分隔符，会被浏览器理解为换行，而在Javascript的字符串表达式中是不允许换行的，从而导致错误。
     把特殊字符转义替换即可，代码如下所示：
     str = str.Replace("\u2028", "\\u2028");

## genSlot返回虚拟dom vonde渲染调用的函数

## genComponent返回虚拟dom vonde渲染调用的函数

## genData$2 转换class，style 数据转换成虚拟dom需要渲染的调用参数函数

## query函数html5 获取dom

## getOuterHTML获取 dom的html

## 获取到dom的html或者模板信息

## 调用1万1千多行的Vue.prototype.$mount

## mountComponent 调用Watcher _render函数，去创建vnode。虚拟dom，返回vm，new Vue 实例化的对象

## 声明updateComponent更新组件

## _render循环$slots，标志_rendered为false，未渲染过。调用render函数获取vnode，最终返回vnode。给_update函数 使用

## 调用render函数就是执行genElement函数的时候返回来的虚拟dom，需要执行编译的函数。类似于这样的函数(function (function anonymous(
                 ) {
                   
                      with(this){return _c('div',{attrs:{"id":"app"}},[_c('input',{directives:[{name:"info",rawName:"v-info"},{name:"data",rawName:"v-data"}],attrs:{"type":"text"}}),_v(" "),_m(0),_v(" "),_c('div',[_v("\n        "+_s(message)+"\n    ")])])}
                 }) 这里的_c 就是createElement创建虚拟dom vonde。 _s就是 toString; // 将对象或者其他基本数据 变成一个 字符串。 _v createTextVNode; //创建一个文本节点 vonde.  最终返回 vonde

## createElement创建虚拟dom vonde，判断标签节点的属性数据  如果是数组  或者是   是否是string，number，symbol，boolean。就把数据data = undefined，最终返回的是一个vnode 虚拟dom

## _createElement函数。判断标签属性数据是否有加入到响应式数据中，如果是则发出警告。并且创建一个空的虚拟节点。如果有is属性则标记tag是is。如果tag不存在则调用createEmptyVNode 创建一个虚拟dom空节点，如果tag === 'string' 可能是组件，调用resolveAsset方法检测是不是组件如果是组件则调用调用6000多行的createComponent  方法创建组件的vonde，如果不是组件创建一个正常的vonde。最后判断vnode是不是数组如果是直接返回出去，如果不是则调用applyNS方法判断是否是svg标签，如果定义有标签属性data 需要

## createEmptyVNode创建一个虚拟dom空节点

## normalizeChildren判断children的数据类型 而创建不同的虚拟dom vonde，返回vonde

## [createTextVNode(children)] 创建一个创建一个文本节点 虚拟dom vonde

## 判断children是否是数组

##    normalizeArrayChildren接收 2 个参数，
    //  children 表示要规范的子节点，nestedIndex 表示嵌套的索引，

    //  主要的逻辑就是遍历 children，获得单个节点 c，然后对 c 的类型判断，
    //  如果是一个数组类型，则递归调用 normalizeArrayChildren;
    //  如果是基础类型，则通过 createTextVNode 方法转换成 VNode 类型；
    //  否则就已经是 VNode 类型了，如果 children 
    //  是一个列表并且列表还存在嵌套的情况，则根据 nestedIndex 
    //  去更新它的 key。这里需要注意一点，在遍历的过程中，
    //  对这 3 种情况都做了如下处理：如果存在两个连续的 text 节点，
    //  会把它们合并成一个 text 节点。    
    //  因为单个 child 可能是一个数组类型。把这个深层的数组遍历到一层数组上面去。如果是深层数组则调用递.归 normalizeArrayChildren,返回单个单层数组的vonde 虚拟dom


## simpleNormalizeChildren 循环子节点children，把他连在一起，其实就是把伪数组变成真正的数组返回出去

## VNode 创建标准的vue vnode，虚拟dom，标记虚拟dom的各种属性。把'child'添加到观察者get中，如果访问'child' 就获取到  this.componentInstance

## 创建一个虚拟dom，vonde  = new VNode(
                                    config.parsePlatformTagName(tag), //返回相同的值 。当前tag的标签名称
                                    data, //tag标签的属性数据
                                    children, //子节点
                                    undefined,  //文本
                                    undefined, //*当前节点的dom */
                                    context // vm vue实例化的对象
                                );

##  isReservedTag判断标签是不是html 原有的标签

## 调用resolveAsset去检测components中查找是否有该标签，如果有则是组件

## 获取到sub类 构造函数是VueComponent 简写Ctor函数

## ASSET_TYPES.forEach var ASSET_TYPES = [
         //     'component',  //注册指令
         //     'directive', //注册定义指令 指令
         //     'filter'  //注册过滤器指令
         // ];

## Vue.component注册组件调用Vue.extend

## Vue.extend//使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。合并继承new 实例化中的拓展参数或者是用户直接使用Vue.extend 的拓展参数。把对象转义成组件构造函数。创建一个sub类 构造函数是VueComponent，合并options参数，把props属性和计算属性添加到观察者中。//如果组件含有名称 则 把这个对象存到 组件名称中, 在options拓展参数的原型中能获取到该数据Sub.options.components[name] = Sub 简称Ctor，返回该构造函数
            

## Vue.filter,Vue.directive 返回 自定义的拓展参数对像

## createComponent创建组件，Ctor如果是对象则调用Vue.extend函数把Ctor转化成构造函数，最终返回vnode虚拟dom

## resolveAsyncComponent解决异步组件 更新组建数据 根据判断factory函数即Ctor函数如果是promise函数则添加到promise中，用factory.contexts队列去记录当前组件的状态，定义forceRender函数为调用$forceUpdate 更新数据 观察者数据 调用 vm._watcher.update()

## isUndef//判断数据 是否是undefined或者null

## createAsyncPlaceholder创建简单的占位符 调用createEmptyVNode创建一个虚拟dom节，返回出去点

## resolveConstructorOptions解析new Vue constructor上的options拓展参数属性的 合并 过滤去重数据。如果Ctor.super 超类存在 有super属性，说明Ctor是Vue.extend构建的子类 继承的子类。resolveConstructorOptions(Ctor.super);//回调超类 表示继承父类 返回options //返回参数

## resolveModifiedOptions/解决修改options 转义数据 合并 数据，循环超类和子类的options对比。

## dedupe //转换判断最新的选项是否是数组，如果是数组则将他们拓展和最新还有自选项 转义成数组并且过滤相同的数组 合并数组返回数组。如果是对象直接返回最新的对象

## extend 浅拷贝合并参数，将Ctor.extendOptions对象和modifiedOptions对象合并，优先保留Ctor.extendOptions对象的数据

## mergeOptions将两个对象合并成一个对象优先取Ctor.extendOptions 将两个对象合成一个对象 将父值对象和子值对象合并在一起，并且优先取值子值，如果没有则取子值，最终返回options参数
           

## checkComponents检验子组件，验证所有的组件

## validateComponentName 验证组件名称 必须是大小写，并且是-横杆

## normalizeProps 检查 props 数据类型，并把type标志打上。如果是数组循环props属性数组，如果val是string则把它变成驼峰写法  res[name] = {type: null}; 。如果是对象也循环props把key变成驼峰，并且判断val是不是对象如果是对象则    res[name] 是{type: val}否则    res[name] 是val。

## normalizeInject将所有注入规范化为基于对象的格式，如果inject是数组，则循环数组  // * 将数组转化成对象 比如 [1,2,3]转化成
            // * normalized[1]={from: 1}
            // * normalized[2]={from: 2}
            // * normalized[3]={from: 3}。如果是对象则循环对象如果val 是对象则   normalized[key] ={from: key，...val} 如果不是对象normalized[key] ={from: val}

## normalizeDirectives获取到指令对象值。循环对象指令的值，如果是函数则把它变成dirs[key] = {bind: def, update: def} 这种形式

## 如果有extendsFrom或者mixins则调用mergeOptions回调递归合并参数

##    strats类 有方法 el，propsData，data，provide，watch，props，methods，inject，computed，components，directives，filters 。 strats类里面的方法都是  合并数据 如果没有子节点childVal，就返回父节点parentVal，如果有子节点childVal就返回子节点childVal。

## strats.el = strats.propsData 判断vm是否有实例化如果没有则发出警告日志 调用 defaultStrat 如果没有子节点就返回父节点，如果有子节点就返回子节点

##  strats.data ，strats.provide

## mergeDataOrFn递归合并数据 深度拷贝。如果vm不存在，并且childVal不存在就返回parentVal。如果vm不存在并且parentVal不存在则返回childVal。如果vm不存在parentVal和childVal都存在则返回mergedDataFn。如果vm存在则返回 mergedInstanceDataFn函数

## mergeData判断to, from两个参数是否有同样的值，如果有同样的并且from还是对象或者数组的是否，深层递归，如果from对象中的key不存在了to值中则调用set方法

## set//如果是数组  并且key是数字 就更新数组
    //如果是对象则重新赋值
    //如果 (target).__ob__ 存在则表明该数据以前添加过观察者对象中  //通知订阅者ob.value更新数据 添加观察者  define  set get 方法
   

## strats.watch* 循环childVal。获取到子节点childVal的key如果在父亲节点上面有，则先获取到父亲节点的值，如果父亲节点的上没有值得获取子节点的值。 变成数组存在ret对象中。返回let对象
   

##  strats.props =
        strats.methods =
            strats.inject =
                strats.computed = 如果parentVal不存在则返回childVal调用extend 对象浅拷贝，参数（to, _from）循环_from的值，会覆盖掉to的值 把childVal和parentVal浅拷贝到 ret 对象中

## 循环LIFECYCLE_HOOKS， 为strats类添加 beforeCreate，created，beforeMount，mounted，beforeUpdate，updated，beforeDestroy，destroyed，activated，deactivated，errorCaptured方法为mergeHook

## mergeHook参数(
                        parentVal,
                        childVal
                        )   * 钩子和道具被合并成数组。
     * 判断childVal存在么？如果不存在 则返回parentVal
     * 如果childVal存在 则判断parentVal存在么。如果parentVal存在则返回 parentVal.concat(childVal)，如果不存在，则判断childVal是不是数组如果是数组直接返回去，
     * 如果不是数组把childVal变成数组在返回出去

## 循环ASSET_TYPES为strats类添加components，directives，filters方法为

## mergeAssets创建一个res对象，获取parentVal对象中的数据。如果parentVal存在则获取parentVal对象 的数据存在res中的  __props__ 中，如果没有则创建一个空的对象。
     * 如果childVal 存在，则用浅拷贝吧 childVal 合并到res中，返回res对象

## mergeField //获取到key 去读取strats类的方法
        // strats类 有方法 el，propsData，data，provide，watch，props，methods，inject，computed，components，directives，filters 。
        // strats类里面的方法都是  合并数据 如果没有子节点childVal，
        // 就返回父节点parentVal，如果有子节点childVal就返回子节点childVal。 如果starats类找不到方法就获取defaultStrat方法 执行strats类 的方法把返回的数据存到    options[key]中

## 调用 mergeOptions方法把参数vm.constructor合并到vm.$options参数中

## transformModel  //将标签含有v-model 信息属性转换为
    //获取options.model.prop属性  获取options.model.event 事件类型，
    // 把data.model.value 数据赋值到data.props.value中 如果value的key没有定义 则是input
    // 把事件  data.model.callback 添加到 data.on[event] 中  如果没有定义是input

## extractPropsFromVNodeData循环propOptions对象，把驼峰的key转换成横杠的key。校验props属性的key是否和attrs属性值相同，如果相同删除掉attrs属性的同样key的值。获取props属性的值添加搞res对象中，返回出去

## checkProp检查  属性  检查key和altKey 在hash属性对象中有没有，如果有则赋值给res对象

## createFunctionalComponent 通过检测 props 属性 然后合并options 拓展参数 之后创建 vond 虚拟dom，返回虚拟dom vonde

## mergeProps前拷贝合并 props属性 并且把 from 的key 由 - 写法变成 驼峰的写法。

##  *  添加虚拟dom 属性data，添加事件，添加props属性，添加parent 属性 添加injections属性
     *  添加slots插槽渲染方法 重写 this._c   createElement 函数 渲染vonde
     *  安渲染函数到FunctionalRenderContext.prototype原型中，这样该对象和 Vue有着同样的渲染功能
     *  installRenderHelpers(FunctionalRenderContext.prototype)

##  options.render这个其实就是用户定义组件时候在options参数上面传进来的，回调会调用_c编译函数，其实就是调用createElement 函数 创建vonde  之后

## 调用cloneAndMarkFunctionalResult 克隆一个vonde 并且返回出去

## cloneVNode 克隆节点  把节点变成静态节点 标记isCloned为真，如果vnode.children存在则递归，返回vonde

## 调用normalizeArrayChildren 创建一个规范的子节点 vonde

## 循环vnodes，调用cloneAndMarkFunctionalResult 克隆vonde标志静态 vonde，存在res数组中，然后res数组 vonde集合

## installComponentHooks把componentVNodeHooks对象里面的方法安装到vonde 的data.hook中

## componentVNodeHooks组件钩子函数

## init初始化组件

## prepatch更新组件

## insert 调用callHook 触发mounted钩子函数

## destroy销毁组件

## 调用VNode创建虚拟dom，vonde

## registerDeepBindings如果vonde中的data即是标签属性，有data.style或者data.class 则调用traverse

## traverse 调用_traverse为 seenObjects 深度收集val 中的key

## Vue.prototype._update 更view试图函数。触发生命周期beforeUpdate函数。 prevVnode//如果这个prevVnode不存在表示上一次没有创建过vnode，这个组件或者new Vue 是第一次进来，获取到vonde参数之后调用__patch__函数渲染成真实的dom
           

## createPatchFunction 返回patch函数

## createPatchFunction传nodeOps对象和modules对象进去

## nodeOps对象   createElement: createElement$1, //创建一个真实的dom
        createElementNS: createElementNS, //创建一个真实的dom svg方式
        createTextNode: createTextNode, // 创建文本节点
        createComment: createComment,  // 创建一个注释节点
        insertBefore: insertBefore,  //插入节点 在xxx  dom 前面插入一个节点
        removeChild: removeChild,   //删除子节点
        appendChild: appendChild,  //添加子节点 尾部
        parentNode: parentNode,  //获取父亲子节点dom
        nextSibling: nextSibling,     //获取下一个兄弟节点
        tagName: tagName,   //获取dom标签名称
        setTextContent: setTextContent, //  //设置dom 文本
        setStyleScope: setStyleScope  //设置组建样式的作用域

## createElement$1创建一个真实的dom如果不是select标签则返回dom出去。//如果是select标签 判断是否设置了multiple属性。如果设置了则加上去

## createElementNS创建一个真实的dom svg方式

## createTextNode创建文本节点真是dom节点

## createComment创建一个真实的注释节点dom

## insertBefore 插入节点 在referenceNode  dom 前面插入一个节点

## removeChild删除子节点 真实dom

## appendChild//添加子节点 尾部

## parentNode获取父亲子节点dom

## nextSibling //获取下一个兄弟节点

## tagName获取dom标签名称

## setTextContent设置dom 文本

## setStyleScope设置组建样式的作用域

## modules对象是由于两个数组组成platformModules数组和baseModules数组连接成

## platformModules

## attrs包含两个方法create和update都是更新设置真实dom属性值

## events更新真实dom事件。有两个方法create 和update 不过函数都是updateDOMListeners 更新真实dom的事件

## domProps 更新真实dom的props属性。有两个方法create 和update 不过函数都是updateDOMProps 更新真实dom的props属性值

## updateAttrs  * 更新设置真实dom属性值，比较新的vnode和旧的oldVnode中的属性值，如果不相等则设置属性,就更新属性值，如果新的vnode 属性中没有了则删除该属性
   

## updateClass获取vonde中的data.staticClass和data.class，更新真实的dom的class值

##  genClassForVnode  *   class 转码
     * 将组件中的class 数据 转化成html 真实dom所需要的class 字符串格式。while循环 如果childNode.componentInstance 已经实例化过了或者 parentNode.parent存在则调用mergeClassData合并vonde中的class

## mergeClassData合并calss数据合并child.staticClass, parent.staticClass的class  和 child.class, parent.class。返回对象{staticClass,class}

## renderClassstringifyClass把vnode的对象class转义成真实dom中的calss再调用concat连接class，返回真实dom需要渲染的class

## concat连接class 返回 return a ?
                (   b ?
                    (a + ' ' + b) :
                                    a
                ):
                  (b || '')

## stringifyClass把vnode的对象class转义成真实dom中的calss

## stringifyArray数组变成字符串，然后用空格 隔开 拼接 起来变成字符串，返回字符串

## stringifyObject对象字符串变成字符串，然后用空格 隔开 拼接 起来变成字符串 返回字符串

## klass包含类包含两个方法create和update都是更新calss。其实就是updateClass方法。 设置真实dom的class

## updateDOMListeners更新dom事件，获取到真实的dom，存放在target$1中。更新完事件后把  target$1 = undefined;

## normalizeEvents 为事件 多添加 change 或者input 事件加进去

## updateListeners更新事件 并且为新的值 添加函数 旧的值删除函数等功能。循环vonde 中的on 事件存储对象

## add$1     //withMacroTask，为事件添加一个静态属性_withTask为红任务，则是执行fn的。
    // 判断once$$1是否存在，如果存在则调用createOnceHandler  返回一个直接调用函数的方法，调用完就删除事件
    // 为真实的dom添加事件

## withMacroTask，为事件添加一个静态属性_withTask为红任务，则是执行fn的。此时 事件类invoker有fns属性和_withTask属性，执行invoker._withTask 则调用invoker 在调用fns 真的的绑定的事件函数。当然也可以直接运行invoker

## createFnInvoker，如果事件只是个函数就为为事件添加多一个静态类， invoker.fns = fns; 把真正的事件放在fns。而 invoker 则是转义fns然后再运行fns

## createOnceHandler柯理化函数，返回一个直接调用函数的方法，调用完就删除事件

## remove$2删除真实dom的事件

## updateDOMProps 循环vonde中的data中的props，如果key是value的话把值转换成字符串重新赋值。如果key不是value那么直接重新赋值

## style 更新真实dom的style属性。有两个方法create 和update 不过函数都是updateStyle更新真实dom的style属性值

## updateStyle将vonde虚拟dom的css 转义成并且渲染到真实dom的css中

## normalizeStyleBinding  //将可能的数组/字符串值规范化为对象 //把style 字符串 转换成对象 比如'width:100px;height:200px;' 转化成 {width:100px,height:200px} 返回该字符串。
         

## parseStyleText   //把style 字符串 转换成对象 比如'width:100px;height:200px;' 转化成 {width:100px,height:200px}
         

## toObject 把数组转化成对象。  和并对象数组合并成一个对象

## getStyle循环子组件和组件的样式，把它全部合并到一个样式对象中返回 样式对象 如{width:100px,height:200px} 返回该字符串。

## normalizeStyleData在同一个vnode上合并静态和动态样式数据。返回样式对象 如{width:100px,height:200px} 返回该字符串。

## extend浅拷贝把两个对象合并to, _from， //对象浅拷贝，参数（to, _from）循环_from的值，会覆盖掉to的值

## setProp设置真实dom的style样式。并且加上前缀

## normalize给css加前缀。解决浏览器兼用性问题，加'Webkit', 'Moz', 'ms'前缀

## camelize横线-的转换成驼峰写法
     可以让这样的的属性 v-model 变成 vModel

## transition 动画过度有三个方法create创建，activate激活，remove删除

## resolveTransition 解析vonde中的transition属性获取到一个css过度对象类

## autoCssTransition //  通过 name 属性获取过渡 CSS 类名   比如标签上面定义name是 fade  css就要定义  .fade-enter-active,.fade-leave-active，.fade-enter,.fade-leave-to 这样的class。返回一个css对象过度类
   return {
            enterClass: (name + "-enter"),
            enterToClass: (name + "-enter-to"),
            enterActiveClass: (name + "-enter-active"),
            leaveClass: (name + "-leave"),
            leaveToClass: (name + "-leave-to"),
            leaveActiveClass: (name + "-leave-active")
        }

## create创建，activate激活方法都是_enter。标志如果show不等于true的是否就进入enter

## enter进入或者激活过度动画。解析vonde中的transition的name属性获取到一个css过度对象类。注入动画钩子函数，执行动画钩子函数和执行动画。

## _enterCb 如果 data.css存在 就删除toClass和activeClass过度css的class 类或者cb.cancelled为真并且data.css存在 就删除startClass  css的静态class 类

## removeTransitionClass删除vonde的class类和删除真实dom的class类

## removeClass 删除真实dom的css类名

## mergeVNodeHook 合并vue vnode 钩子函数，       def[hookKey] = invoker; //把钩子函数用对象存起来

## createFnInvoker 创建一个调用程序 创建一个钩子函数createFnInvoker，如果事件只是个函数就为为事件添加多一个静态类， invoker.fns = fns; 把真正的事件放在fns。而 invoker 则是转义fns然后再运行fns

## addTransitionClass 为真实的dom标签添加class样式类

## nextFrame 下一帧  raf等于 //如果是浏览器如果浏览器支持requestAnimationFrame就用requestAnimationFrame，不支持就用setTimeout
   

## getHookArgumentsLength 检测钩子函数 fns 的长度检测钩子函数 fns 的长度
     数据必须是这样才返回真，也可以是n层fns只要规律是一样嵌套下去就行

## 判断动画时长是不是number类型

## setTimeout设置延迟动画然后执行_enterCb

## whenTransitionEnds获取动画的信息，执行动画_enterCb。

## getTransitionInfo //获取返回transition，或者animation 动画的类型，动画个数，动画执行时间  

## leave和enter动画代码其实差不多，区别就是leave没有安装insert钩子函数

## baseModules数组是由ref对象和directives对象组成。ref创建，更新 ， 销毁 函数。//directives自定义指令 创建 ，更新，销毁函数

## ref是由create，update，destroy组成

## registerRef注册ref或者删除ref。比如标签上面设置了ref='abc' 那么该函数就是为this.$refs.abc 注册ref 把真实的dom存进去

## update更新ref，先删除ref，再添加ref

## destroy删除销毁ref

## directives 有create，update，destroy 创建 更新 和销毁组件

## create，update，destroy都是updateDirectives方法

## _update  //更新指令 比较oldVnode和vnode，根据oldVnode和vnode的情况 触发指令钩子函数bind，update，inserted，insert，componentUpdated，unbind钩子函数
  

## normalizeDirectives$1规范化的指令，为指令属性修正变成规范的指令数据。返回指令数据集合

## callHook$1用于触发指令的钩子函数

##  vnode.componentInstance &&  !vnode.componentInstance._isDestroyed &&vnode.data.keepAlive为假的时候

## createComponentInstanceForVnode 调用VueComponent构造函数去实例化组件对象

##  vnode.componentInstance &&  !vnode.componentInstance._isDestroyed &&vnode.data.keepAlive为真的时候

## 生成完之后调用15500多行的 Vue.prototype.$mount 挂载模板

## updateChildComponent 更新子组件 循环调用validateProp把props 添加到观察者中 ，调用updateComponentListeners更新事件，如果有子节点判断是否有插槽，调用resolveSlots 收集插槽嗲用$forceUpdate  //更新数据 观察者数据

## queueActivatedComponent //添加活跃的组件函数 把活跃的vm添加到activatedChildren 中

## activateChildComponent  //判断是否有不活跃的组件 禁用他 如果有活跃组件则触发钩子函数activated

## $forceUpdate 更新观察者set方法 用于触发 vonde更新 然后更新view的 调用vm._watcher.update()

## 则调用Vue.prototype.$destroy  销毁组建周期函数

## deactivateChildComponent循环子组件 和父组件  判断是否有禁止的组件 如果有活跃组件则执行生命后期函数deactivated
               

## patch

## invokeDestroyHook    //组件销毁，触发销毁钩子函数

## createElm 创建真实的dom

## cloneVNode //克隆节点  把节点变成静态节点

## 调用8000多行的createComponent创建组件。   //如果组件已经实例化过了才会初始化组件，才会返回值为真

## 表示该vonde.hook中有componentVNodeHooks对象中的钩子函数init，prepatch，insert，destroy

## 触发componentVNodeHooks中的init安装组件

## initComponent 初始化组建，如果没有tag标签则去更新真实dom的属性，如果有tag标签，则注册或者删除ref 然后为insertedVnodeQueue.push(vnode);确保调用插入钩子如果vnode.data.pendingInsert为反正则也为insertedVnodeQueue插入缓存 vnode.data.pendingInsert

##  isPatchable判断组件是否定义有 tag标签

## invokeCreateHooks，循环cbs.create 钩子函数，并且执行调用，其实cbs.create 钩子函数就是platformModules中的attrs中 updateAttrs更新属性函数。如果是组件则调用componentVNodeHooks中的 create

## setScope 为有作用域的CSS设置作用域id属性。

## setStyleScope 设置组建样式的作用域 scopeId

## registerRef      //注册ref或者删除ref。比如标签上面设置了ref='abc' 那么该函数就是为this.$refs.abc 注册ref 把真实的dom存进去。

## reactivateComponent 激活组建。把vonde添加到parentElm中。如果是transition组件则 调用 transition中的activate就是_enter

## insert //插入一个真实的dom，如果ref$$1.parentNode等于parent是。ref$$1和elm他们是兄弟节点则插入ref$$1前面
        //如果ref$$1的ref$$1.parentNode不等于parent。那么elm就直接append到parent中

## vnode.elm为创建真实的dom

## nodeOps.createElementNS创建xml真实dom

## nodeOps.createElement创建真实的html dom

## createChildren，循环children，回调递归创建真实的dom

## checkDuplicateKeys  //检测key是否有重复，如果有则发出警告

## 如果children是数组

## 如果children不是数组

## isPrimitive判断数据类型是否是string，number，symbol，boolean

## nodeOps.appendChild创建一个真实的dom

## nodeOps.createTextNode//创建文本节点真是dom节点

## nodeOps.createComment 创建一个真实的注释节点

## nodeOps.createTextNode// 创建文本节点

*XMind: ZEN - Trial Version*