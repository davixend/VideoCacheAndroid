# VideoCacheAndroid
<p dir='rtl' align='right'>test</p>
کش کردن ویدیوها در اندروید


# used:

اضافه کردن لایبرری زیر به gradle:

```gradle
implementation 'com.danikula:videocache:2.7.1'
```

ایجاد کلاس اپلیکیشن و اضافه کردن کد زیر به این کلاس:

```java
private HttpProxyCacheServer proxy;

public static HttpProxyCacheServer getProxy(Context context) {
    Applications app = (Applications) context.getApplicationContext();
    return app.proxy == null ? (app.proxy = app.newProxy()) : app.proxy;
}

private HttpProxyCacheServer newProxy() {
    //return new HttpProxyCacheServer(this);
    return new HttpProxyCacheServer.Builder(this)
            .cacheDirectory(CacheUtils.getVideoCacheDir(this))
            .maxCacheFilesCount(40)
            .maxCacheSize(1024 * 1024 * 1024)
            .build();
}
```


سپس داخل اکتیویتی پلیر خود متد زیر را اضافه کنید:
```java
public String cachingUrl(String urlPath) {

 return Applications.getProxy(this).getProxyUrl(urlPath, true);

}
```
و در انتها با صدا زدن این متد لینک ویدیو کش شده را دریافت کنید:
```java
Uri mp4Uri = Uri.parse(cachingUrl(videoUrl));
```
