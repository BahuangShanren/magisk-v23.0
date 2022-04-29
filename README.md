## magisk-v23.0

> 本仓库只是[magisk-file](https://github.com/topjohnwu/magisk-files)的备份。

Magisk使用随机包名重新安装以隐藏自身，需要从[magisk-file](https://github.com/topjohnwu/magisk-files)这个仓库的`json`文件获取下载链接，然后下载安装包进行安装。

### 糟糕的状况

如果你使用的是使用[Magisk（version<=23.0)](https://github.com/topjohnwu/Magisk/releases/tag/v23.0)，那么将出现这种状况：

- 打不开刚刚安装的具有随机包名的Magisk。
- 原来的Magisk变成了未root的状态。卸载具有随机包名的Magisk，原来的Magisk又变回已root的状态。

### 原因

使用默认更新通道安装的是Magisk的新版本[(version>=24.0)](https://github.com/topjohnwu/Magisk/releases/tag/v24.0)，因为使用了Zygisk和其他一些特性，与Magisk旧版本[(version<=23.0)](https://github.com/topjohnwu/Magisk/releases/tag/v23.0)差别很大，于是新旧版本之间的冲突导致了上面的状况。

[magisk-file](https://github.com/topjohnwu/magisk-files)用于存储[Magisk](https://github.com/topjohnwu/Magisk/releases)软件的默认更新通道文件，比如这是[稳定版通道](https://github.com/topjohnwu/magisk-files/blob/master/stable.json)Magisk_`v24.3`的内容：

```json
{
  "magisk": {
    "version": "24.3",
    "versionCode": "24300",
    "link": "https://cdn.jsdelivr.net/gh/topjohnwu/magisk-files@24.3/app-release.apk",
    "note": "https://topjohnwu.github.io/Magisk/releases/24300.md"
  },
  "stub": {
    "versionCode": "27",
    "link": "https://cdn.jsdelivr.net/gh/topjohnwu/magisk-files@24.3/stub-release.apk"
  }
}
```

### 解决方法

参考[issue #5361](https://github.com/topjohnwu/Magisk/issues/5361#issuecomment-1027061705)，从之前的[commit](https://github.com/topjohnwu/magisk-files/tree/afe2c304e59f631280cc26ccc6d40a7cf04f7f37)中找到适用于Magisk_v23.0的`json`文件，复制其链接粘贴到自定义更新通道：

https://cdn.jsdelivr.net/gh/topjohnwu/magisk-files@afe2c304e59f631280cc26ccc6d40a7cf04f7f37/stable.json

之后再使用随机包名隐藏Magisk功能。

以下是适用于Magisk_v23.0的稳定版通道内容：

```json
{
  "magisk": {
    "version": "23.0",
    "versionCode": "23000",
    "link": "https://cdn.jsdelivr.net/gh/topjohnwu/magisk-files@23.0/app-release.apk",
    "note": "https://topjohnwu.github.io/Magisk/releases/23000.md"
  },
  "stub": {
    "versionCode": "21",
    "link": "https://cdn.jsdelivr.net/gh/topjohnwu/magisk-files@23.0/stub-release.apk"
  }
}
```

或者使用来自本仓库的链接：https://cdn.jsdelivr.net/gh/BahuangShanren/magisk-v23.0@master/magisk-v23.0.json