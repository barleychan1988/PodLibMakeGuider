		CocoaPods Lib制作 
CocoaPods Lib开发的核心是podspec描述文件。
创建开源库
创建仓库主要是为了保存此次需要共享的Pod库，仓库名称必须与Pod库名称一致。创建github库过程在此不做叙述，创建的时候需要选取license。
Clone 仓库
通过命令git clone https://github.com/EadkennyChan/testPodLib.git下载到本地
提交源码
将创建的Pod库源码上传到git仓库。
git add -A && git commit -m 'Release 0.1.0'
git push origin master
打上标签
git tag 0.0.1
git push –tags
创建podspec描述文件
1.	在当前项目文件目录打开终端并执行
pod spec create testPodLib
2.	执行成功后会生成testPodLib.podspec文件。该文件描述了pod项目的一些属性。
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
3.	在上面指定的文件目录下添加相应功能的源码和资源
4.	提交资源和源码到github仓库
5.	验证podspec文件是否正确
pod spec lint YourProject.podspec
验证成功会显示：
-> testPodLib (1.0)
Analyzed 1 podspec.
testPodLib.podspec passed validation.
提交Pod Trunk
1.	注册Trunk
$ pod trunk register [邮箱] '[name]' --description='[mac]'
执行成功后会显示
[!] Please verify the session by clicking the link in the verification email that has been sent to youmail@gmail.com
去邮箱点击验证链接
2.	提交pods
pod trunk push testPodLib.podspec
注意：如果你没有翻墙，可能会需要的时候比较久，我用了大概2分钟提交完毕
成功后会显示：
-> testPodLib (1.0)
Updating spec repo `master`
-Data URL: https://raw.githubusercontent.com/CocoaPods/Specs/xxx/ testPodLib.podspec.json
  - Log messages:
    - May 31st, 21:54: Push for ` testPodLib 0.1.0' initiated.
- May 31st, 21:54: Push for `testPodLib 0.1.0' has been pushed (2.903283301 s).
ok。到此就成功了。
pod trunk me
可以查看自己的pod账号信息
至此一个开源的CocoaPod库就开发完成了。


