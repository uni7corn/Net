## Net

<p align="center"><img src="https://i.imgur.com/YRdJdzG.jpg" width="50%"/></p>

<p align="center"><strong>不仅仅是网络请求的异步任务库</strong></p>

<p align="center"><a href="http://liangjingkanji.github.io/Net/">使用文档</a></p>

<p align="center"><img src="https://i.imgur.com/NFL3tTk.jpg" width="60%"/></p>

<p align="center">
<a href="https://jitpack.io/#liangjingkanji/Net"><img src="https://jitpack.io/v/liangjingkanji/Net.svg"/></a>
<img src="https://img.shields.io/badge/language-kotlin-orange.svg"/>
<img src="https://img.shields.io/badge/license-Apache-blue"/>
<a href="https://jq.qq.com/?_wv=1027&k=vWsXSNBJ"><img src="https://img.shields.io/badge/QQ群-752854893-blue"/></a>
</p>

<p align="center"><img src="https://i.imgur.com/aBe7Ib2.png" align="center" width="30%;" /></p>



Android上不是最强网络任务库, 创新式的网络请求库(针对[Kalle](https://github.com/yanzhenjie/Kalle)网络请求框架进行扩展), 支持协程高并发网络请求 <br>
<br>
我是目前Android上最简洁和功能最多的网络请求库, 也是扩展性最强的, 可以完美适应任何项目的后端要求, 并且还是一个异步任务库

<br>



Net 1.x 版本为RxJava实现 <br>
Net 2.x 版本为协程实现(开发者无需掌握协程也可以使用)



正在进行的任务

- OkHttp4.8 重构

<br>

主要新增特性

- 代码简洁(最少一行代码发起请求)
- 文档详细
- Kotlin
- 协程(不懂协程也可上手)
- 并发网络请求(马上优化网络速度!)
- 串行网络请求
- 切换线程
- DSL编程
- 全局日志记录器(完美解决日志过长展示不清晰数据加密问题, 比抓包更强大)
- 支持先强制读取缓存后网络请求二次刷新
- 并发请求返回最快请求结果(可返回不同响应数据)
- 方便的缓存处理
- 自动错误信息吐司
- 自动异常捕获
- 自动日志打印异常(任何网络错误可追踪到具体请求接口)
- 自动JSON解析(可解析List)
- 自动处理下拉刷新和上拉加载
- 自动处理分页加载
- 自动缺省页
- 自动处理生命周期
- 自动处理加载对话框
- 协程作用域支持错误和结束回调
- 内置超强轮循器(计时器)
- 解析JSON数组返回集合



同时完全不影响Kalle的特性

- 九种缓存模式
- 重试次数拦截器
- 重定向拦截器
- 数据库缓存
- 缓存加密
- 上传进度监听
- 下载进度监听
- 断点续传
- 下载文件策略
- 网络连接判断
- 自定义数据转换器
- 网络拦截器
- 重定向
- 自定义请求体
- 全局配置
- Cookie
- SSH证书



<br>

在项目根目录的 build.gradle 添加仓库

```groovy
allprojects {
    repositories {
        // ...
        maven { url 'https://jitpack.io' }
    }
}
```

在 module 的 build.gradle 添加依赖

```groovy
// 协程库(版本自定)
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.7'
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.7'

// 支持自动下拉刷新和缺省页的(可选)
implementation 'com.github.liangjingkanji:BRV:1.3.13'

implementation 'com.github.liangjingkanji:Net:2.3.3'
```

<br>

## Contribute

<p align="center">
<img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gaskr305czj30u00wjtcz.jpg" alt="jetbrains" width="15%" />
</p>
<p align="center">
<strong>The project is supported by <a href="https://www.jetbrains.com/">JetBrains</a></strong></p>



## License

```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
