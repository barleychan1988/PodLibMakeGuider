#<center>CocoaPods Lib 开发</center>
##CocoaPods是什么？
<p>当你开发iOS应用时，会经常使用到很多第三方开源类库，比如JSONKit，AFNetWorking等等。可能某个类库又用到其他类库，
所以要使用它，必须得另外下载其他类库，而其他类库又用到其他类库，“子子孙孙无穷尽也”，这也许是比较特殊的情况。
总之小编的意思就是，手动一个个去下载所需类库十分麻烦。另外一种常见情况是，你项目中用到的类库有更新，你必须得
重新下载新版本，重新加入到项目中，十分麻烦。如果能有什么工具能解决这些恼人的问题，那将“善莫大焉”。
所以，你需要 CocoaPods。
CocoaPods应该是iOS最常用最有名的类库管理工具了，上述两个烦人的问题，通过cocoaPods，只需要一行命令就可以完全解决，
当然前提是你必须正确设置它。重要的是，绝大部分有名的开源类库，都支持CocoaPods。所以，作为iOS程序员的我们，
掌握CocoaPods的使用是必不可少的基本技能了。

其中PodSpec描述文件是CocoaPods Lib的核心。

如果我们也想将自己写的组件或库开源出去，让别人也可以通过pod install命令安装自己的框架该怎么做呢？下面，我就教
大家一步一步的将自己的pods发布到CocoaPods 中。
</p>
##创建功能代码库
创建仓库主要是为了保存此次需要共享的Pod库，仓库名称必须与Pod库名称一致。创建github库过程在此不做叙述，
创建的时候需要选取license。
<p><img src="http://photo-zw.oss-cn-shanghai.aliyuncs.com/%E6%97%A0%E6%A0%87%E9%A2%98.png?Expires=1488165077&OSSAccessKeyId=TMP.AQE6sl7X7Fm--JQ7K-nXM58saIyaH0LXeMg1MHp6o4hkikLYSN75x48SPX7VADAtAhRVqGoHN_1K9v7NNsCX8fBuwQ7_bgIVAPWEFrPWDrEtoF43onbrub-Z0kVa&Signature=XXiud2vS9f%2BHK9xx1BCv8jqNYb0%3D" width= ><br>
</p>
Clone 仓库<br/>
通过命令```git clone https://github.com/EadkennyChan/testPodLib.git```下载到本地，然后在相应目录下加入功能代码
提交源码<br/>
将创建的Pod库源码上传到git仓库。
```
git add -A && git commit -m 'Release 0.1.0'
git push origin master
```
打上标签<br/>
```
git tag 0.0.1
git push –tags
```
##创建podspec描述文件
在当前项目文件目录打开终端并执行
```
pod spec create testPodLib
```
执行成功后会生成testPodLib.podspec文件。该文件描述了pod项目的一些属性。
```
Pod::Spec.new do |s|
  # 你的项目名称
  s.name         = " testPodLib "
  # 版本号，最后会指定到tag版本号
  s.version      = "0.1.0"
  # 简要描述 
  s.summary      = "a test pod lib"
  # 详细描述 
 s.description = <<-DESC 
           
                DESC
  # github仓库地址
  s.homepage     = "https://github.com/EadkennyChan/ testPodLib "
  # license协议
  s.license      = { :type => "MIT", :file => "LICENSE" }
  # 作者
  s.author       = { " EadkennyChan " => " EadkennyChan @gmail.com" }
  # 是否支持arc
  s.requires_arc = true

  #  对应的平台版本号
  s.ios.deployment_target = "8.0"
  # s.osx.deployment_target = "10.7"
  # s.watchos.deployment_target = "2.0"
  # s.tvos.deployment_target = "9.0"

  # 需要提供给pod的文件git地址
  s.source       = { :git => "https://github.com/EadkennyChan/ testPodLib.git", :tag => s.version }
  # 需要提供给pod的具体文件
  s.source_files  = "Classes ", "Classes/**/*.{h, m, swift}"
  # 如果有资源则指定，没有的话无需该条配置
  s.resources = "YourProject/YourProject.bundle"
  s.framework = "UIKit", "Foundation"
end
```
在上面指定的文件目录下添加相应功能的源码和资源<br>
提交资源和源码到github仓库<br>
验证podspec文件是否正确<br>
```
pod spec lint YourProject.podspec
```
验证成功会显示：
```javascript
-> testPodLib (1.0)
Analyzed 1 podspec.
testPodLib.podspec passed validation.
```
##提交Pod Trunk
注册Trunk
```
$ pod trunk register [邮箱] '[name]' --description='[mac]
'```
执行成功后会显示
```javascript
[!] Please verify the session by clicking the link in the verification email that has been sent to youmail@gmail.com
```
去邮箱点击验证链接
提交pods
```
pod trunk push testPodLib.podspec
```
注意：如果你没有翻墙，可能会需要的时候比较久，我用了大概2分钟提交完毕
成功后会显示:<br/>
```javascript
-> testPodLib (1.0)
Updating spec repo `master`
-Data URL: https://raw.githubusercontent.com/CocoaPods/Specs/xxx/ testPodLib.podspec.json
  - Log messages:
    - May 31st, 21:54: Push for ` testPodLib 0.1.0' initiated.
- May 31st, 21:54: Push for `testPodLib 0.1.0' has been pushed (2.903283301 s).
```
ok。到此就成功了。<br>
```
pod trunk me
```
可以查看自己的pod账号信息
至此一个开源的CocoaPod库就开发完成了。