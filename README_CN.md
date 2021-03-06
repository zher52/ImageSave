# cordova-plugin-imagesave

保存照片到相册

支持平台

- IOS (>=8.0)
- Android (>=4.4)

## 特点

- 支持自定义相册
- 支持网络、本地图片
- Android 重复文件处理
- Android 上传完成通知系统扫描相册

## 用法

### 返回码定义

| Code | State | Message |
| --- | --- | --- |
| 100 | Success | 全部成功 |
| 101 | Success | 部分成功 && 部分失败 |
| 110 | Error | 全部失败 |
| 120 | Error | 权限错误(无法保存到相册) |
| 130 | Error | 其他异常 |


### 调用

参数

```
{
    // 图片数据
    imageList: imageList,
    // 自定义相册名称
    albumName: albumName,
    // 缓存目录
    cacheDirName: cacheDirName
}
```

示例:

```
var imageList = [
    {
        fileFullName: 'xxx.png',
        cacheFileName:'112ssq.png',
        imageUrl: 'http://xxx.png'
    }
];
var cacheDirName = 'cacheDir';
var albumName = 'Custom Album';

```


```
if (window.plugins && window.plugins.ImageSave) {
    window.plugins.ImageSave.saveToAlbum(JSON.stringify({
        imageList: imageList,
        albumName: albumName,
        cacheDirName: cacheDirName
        }), function (data) {
            // 保存成功，请到相册中查看
        }, function (error) {
            // 保存失败
        });
} else {
    console.log("未安装 相册插件");
}
```

## 回调

返回码请参考上面的表格

成功

```
function (data) {
    // data : {code: 100, message: 'xxxx'}
}
```


失败

```
function (error) {
    // error : {code: 120, message: 'xxxx'}
}
```

## IOS

鉴于IOS8以上市场已达到了95%以上，最低版本8.0 ，使用了8.0之后新增的 Photos.framework。
[官方数据](https://developer.apple.com/support/app-store/)
当用户手动到设置里关闭相册访问权限后，需要手动打开相册开关；

```
- (void)openSetting {
    NSURL *url = [NSURL URLWithString:UIApplicationOpenSettingsURLString];
    if ([[UIApplication sharedApplication] canOpenURL:url]) {
        [[UIApplication sharedApplication] openURL:url];
    }
}
```

### 缓存目录

项目使用了 [imgcachejs](https://github.com/chrisben/imgcache.js) [ion-image-cache](https://github.com/vitaliy-bobrov/ionic-img-cache),具体请根据说明文档进行配置

```
/application dir/Library/files/cacheDir/
```


## Android

### 缓存目录

```
/External Path/cacheDir/
```

## TODO

* [ ] Android - 适配6.0
* [ ] IOS - 相册重复处理


## 联系

如在使用过程中遇到问题，请提交[issues](https://github.com/SandLZ/ImageSave/issues)或邮件978949438@qq.com





