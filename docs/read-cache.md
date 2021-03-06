Net_v2基于[Kalle](https://github.com/yanzhenjie/Kalle)开发, 支持Kalle的9种缓存模式

缓存模式要求在初始化的时候开启
```kotlin
initNet("http://182.92.97.186/") {
    cacheEnabled() // 开启缓存
}
```

=== "请求缓存或网络"
    ```kotlin
    scopeNetLife {
        // 先读取缓存, 如果缓存不存在再请求网络
        tv_fragment.text = Get<String>("api", cache = CacheMode.READ_CACHE_NO_THEN_NETWORK).await()
        Log.d("日志", "读取缓存")
    }
    ```
=== "读取缓存然后请求网络"
    ```kotlin
    scopeNetLife {
        // 然后执行这里(网络请求)
        tv_fragment.text = Post<String>("api", cache = CacheMode.NETWORK_YES_THEN_WRITE_CACHE).await()
        Log.d("日志", "网络请求")
    }.preview {
        // 先执行这里(仅读缓存), 任何异常都视为读取缓存失败
        tv_fragment.text = Get<String>("api", cache = CacheMode.READ_CACHE).await()
        Log.d("日志", "读取缓存")
    }
    ```

预读模式本质上就是创建一个`preview`附加作用域, 里面的所有异常崩溃都会被静默捕捉(算作缓存失败), 会优先于`scope*`执行, 然后再执行scope本身,
而且一旦缓存读取成功(`preview`内部无异常)即使网络请求失败也可以不提醒用户任何错误信息(可配置)

<br>

!!! note
    `preview`并没有说只能用在网络缓存上, 也可以用于其他的处理场景

<br>

## 缓存模式

缓存模式属于`CacheMod`枚举, 建议开发者浏览缓存模式的源码和注释，有助于理解和更好的使用缓存模式。

1. `HTTP` Http标准模式；
<br>发起请求前如果本地已经有缓存，会检查缓存是否过期，如果没过期则返回缓存数据，如果过期则带上缓存头去服务器做校验。如果服务器响应304则返回缓存数据，如果响应其它响应码则读取服务器数据，并根据服务器响应头来决定是否缓存数据到本地。如果请求失败则是正常失败。

1. `HTTP_YES_THEN_WRITE_CACHE` 先Http标准协议再写入缓存；
<br>发起请求前如果本地已经有缓存则带缓存头，在有缓存的时候，服务器可能响应304，则返回缓存数据，如果服务器响应其它响应码，则读取服务器数据，并把请求成功后的数据缓存到本地。如果请求失败则是正常失败。

1. `NETWORK` 仅仅请求网络；
<br>发起请求前不管本地是否有缓存，都不会带上缓存头，请求成功后，不论服务器响应头如何，都不会缓存数据到本地。如果请求失败则是正常失败。

1. `NETWORK_YES_THEN_HTTP` 先仅仅网络再按照Http标准协议；
<br>发起请求前不管本地是否有缓存，都不会带上缓存头，请求成功后根据服务器响应头来决定是否缓存数据到本地。如果请求失败则是正常失败。

1. `NETWORK_YES_THEN_WRITE_CACHE` 先仅仅网络再写入缓存；
<br>发起请求前不管本地是否有缓存，都不会带上缓存头，请求成功后会把数据缓存到本地。如果请求失败则是正常失败。

1. `NETWORK_NO_THEN_READ_CACHE` 先仅仅网络，失败后读取缓存；
<br>发起请求前不管本地是否有缓存，都不会带上缓存头，请求成功后正常返回，请求失败后尝试读取缓存，如果缓存不存在则继续按照之前失败的流程走，如果缓存存在则正常返回缓存。

1. `READ_CACHE `仅仅读取缓存；
<br>只是去读取缓存，如果缓存不存在则会失败，如果缓存存在就返回缓存。

1. `READ_CACHE_NO_THEN_NETWORK` 先读取缓存，缓存不存在再请求网络；
<br>先尝试读取缓存，如果缓存存在就返回缓存，如果缓存不存在就请求网络，请求成功后不论服务器响应头如何都不存缓存数据。如果请求失败则是正常失败。

1. `READ_CACHE_NO_THEN_HTTP` 先读取缓存，缓存不存在再；
<br>先尝试读取缓存，如果缓存存在就返回缓存，如果缓存不存在就请求网络，请求成功后根据服务器响应头来决定是否缓存数据到本地。如果请求失败则是正常失败。

<br>
便于理解
<img src="https://i.imgur.com/sHnrzWX.png" width="100%"/>