# VideoCacheAndroid

<p dir='rtl' align='right'>کش کردن ویدیوها در اندروید</p>

# used:

<p dir='rtl' align='right'>اضافه کردن لایبرری زیر به gradle:</p>

```gradle
implementation 'com.danikula:videocache:2.7.1'
```

<p dir='rtl' align='right'>ایجاد کلاس اپلیکیشن و اضافه کردن کد زیر به این کلاس:</p>

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

<p dir='rtl' align='right'>سپس داخل اکتیویتی پلیر خود متد زیر را اضافه کنید:</p>

```java
public String cachingUrl(String urlPath) {

 return Applications.getProxy(this).getProxyUrl(urlPath, true);

}
```
<p dir='rtl' align='right'>و در انتها با صدا زدن این متد لینک ویدیو کش شده را دریافت کنید:</p>

```java
Uri mp4Uri = Uri.parse(cachingUrl(videoUrl));
```
