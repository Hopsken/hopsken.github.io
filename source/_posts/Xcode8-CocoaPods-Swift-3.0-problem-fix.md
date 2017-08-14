---
layout: post 
title: Xcode8 中 CocoaPods 与 Swift 3.0 的适配问题
tags: 
- Swift
- CocoaPods
- Xcode
date: 2016-12-13
---

很多童鞋可能会遇到这样的问题：明明使用的 Swift 3 版本的库（比如 Alamofire 的 4.0.0 版本），但是使用 CocoaPods 安装之后打开 Xcode 仍然会提示 转换为 Swift 3，一路 Next 确认后各种报错。

有童鞋提出一种解决方法，就是在项目设置里把 “Use Legacy Swift Language Version” 改为 No。经本人测试后，发现有些时候这样改过之后就能编译通过了，但是有时候仍然会报错。怎么彻底解决这个问题呢？
<!--more-->

遂StackOverFlow之。原来在 CocoaPods 1.1.1 版本中已经解决了这个问题。

### 解决方案
更新CocoaPods
```
sudo gem install -n /usr/local/bin cocoapods --pre
```

在 Podfile 中添加如下内容：
```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```


运行 `pod install` 即可。

再次打开项目，这时候就能够顺利编译通过啦～


