#### 基本原理
##### 1.初始化
    scheme注册，xml配置文件 Pull解析
    xml用来约定path（project和module）和action（actionType以及interceptor）匹配；
##### 2.路由
    分两种，URL路由和Context路由（App内部），通过URL或者IBridge生成BirdgeData（包含BirdgeEvent）
    通过BridgeEvent生成InterceptorQueue和IAction，先逐条Interceptor，如果InterceptorQueue整条链pass的话，走IAction；

#### 思考点
+ URL路由只能带String参数，不能带自定义参数（可以转成json格式的String）
+ 缺少回调（路由过程中各个阶段的状态回调，路由失败（未注册），拦截器状态（Pass，Intercepted，Blocked），IAction成功）；
+ 每次路由InterceptorQueue中Interceptor对象都是new，可以考虑缓存，尤其是全局Inteceptor；
+ 是否支持异步IAction
+ 现在是静态注册，是否支持动态注册和动态注销；
+ 各项目配置文件分module
