---
title: UnsatisfiedLinkError异常
categories: android
tags:
  - android
  - bug
abbrlink: c5a8ca53
date: 2024-10-17 13:05:13
---

很长时间没有做三方的so库导入了，今天项目需要导入三方库。按照以前的经验，引入libs、创建jniLibs、功能开发，一切准备就绪。运行时却出现了错误`java.lang.UnsatisfiedLinkError: dalvik.system.DexClassLoader` 报找不到`.so`文件。于是又去检查了一下配置，不应该啊，配置完全没有问题啊，这是为什么呢？于是开始排查问题三部曲，百度、google、尝试。
网上基本都是说架构适配原因的，没什么用。
## 检查APK
网上找不到原因，于是我便去查看打包的APK有什么问题。解压APK，看到解压目录下，导入的`.so`文件都存在
![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241017/112024400-20241017112012-2f23e.png)
这没问题，那么安装后呢？
于是找到安装后的目录查看
![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241017/112246226-20241017112237-ffc76.png)
可以看到这里确实没有任何`.so`文件
![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241017/112518302-20241017112514-fd9ee.png)

到这里我就搞不懂了，于是继续google，不过google方向调整了下，于是我便看到了`android:extractNativeLibs`，在`AndroidManifest.xml` 的 `<application>`标签里添加`android:extractNativeLibs="true"`，于是我去尝试了下，终于成功了，那么`extractNativeLibs`有什么作用呢？
于是便去官网查了查
	![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241017/113157370-20241017113150-a82da.png)
## extractNativeLibs
### extractNativeLibs不同版本的默认值
- 若`minSdkVersion < 23 或 Android Gradle plugin < 3.6.0`，打包时`android:extractNativeLibs=true`；
- 若`minSdkVersion >= 23 并且 Android Gradle plugin >= 3.6.0`，打包时`android:extractNativeLibs=false`；
### extractNativeLibs不同设置的表现
当设置`android:extractNativeLibs=true`时，打包时，工程中的`.so`库会被压缩，那么生成的apk的体积也会减少，但是安装时，需要解压缩到`/data/app/`那么安装的时间就会变长，而且同一个 so 文件就会有两份，一份在 apk 中压缩存储，一份在 /data/app/ 中未压缩存储，导致多占用了空间。
当设置为`false`则安装apk时 `.so`文件不会从apk中解压出来，同时修改`System.loadLibrary` 直接打开调用 `apk` 中的 `so` 文件。
### 官方建议 
从 AGP 4.2.0 开始，DSL 选项[`useLegacyPackaging`](https://developer.android.com/build/releases/past-releases/agp-4-2-0-release-notes?hl=zh-cn#compress-native-libs-dsl)取代了`extractNativeLibs`清单属性。建议使用`useLegacyPackaging` 来配置原生库的压缩行为。

```groovy
android {
    packagingOptions {
        jniLibs {
            useLegacyPackaging true
        }
    }
}
```