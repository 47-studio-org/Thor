## 常见问题

### [HTTPS 证书无法信任]()

iOS10 开始由于系统原因，不能直接跳转到系统设置的二级界面，所以需要手动打开『证书信任』界面开启信任：

`设置 > 通用 > 关于本机 > 证书信任设置`：注意安装证书到系统的描述文件那里是『已验证』，并不是最终的『已信任』。


### [Thor 1.2.2 以后内置筛选器设置]()

Thor 1.2.2 以后实现了更加灵活强大的筛选器配置，可以自己定义并持久化保存。

定义自己的筛选器，生成之前版本的『文本』、『音视频』、『安装包』等内置筛选器时，只用选数据类型相关选项即可，别的条件不用选。


### [如何在过滤器中设置更全面的参数]()

过滤器的目的是减少不必要的流量抓取，要得到更精确的结果就需要配合筛选器（漏斗）灵活使用，得益于 Thor 全实时抓包的优势，可以用筛选器强化过滤器的效果：

`选取过滤器 > 启动抓包 > 选择并配置筛选器（漏斗） > 抓取数据`


### [越狱设备抓包秒断]()

越狱机容易出现 Thor 秒断的问题

由于 iOS 的系统限制，NE 扩展类应用最多只允许使用 6MB 的内存，在非越狱系统下基本上 Thor 不会触发此限制。然而在越狱系统下，由于各类插件的插入，会导致 Thor 的内存用量大增，直接无法启动或变得很不稳定。
以下方法可以解除系统的内存限制，让 Thor 能够稳定运行（这将彻底关闭系统内存限制机制，请谨慎）
使用 `iFile` 等文件管理工具，找到`/System/Library/LaunchDaemons/com.apple.jetsamproperties.{Model}.plist` 文件，将其改名为 `.bak`。（如有多个全部要改）

部分设备在越狱后可能会破坏 Thor 的部分权限，导致无法启动，重新安装 Thor 即可解决。

以上如果不能解决问题，参考（只有此唯一解法）：
* 这个问题的根源是：越狱后开了太多的耗内存的插件。导致 NE 框架分不到足够多的内存，被系统杀掉了。
* 所以唯一的解法是：排查所启动的插件中，耗内存大户，用控制变量法试出是哪个插件的问题。
* 如果是启动后过了几秒再断开，则可能是未知插件导致的闪退，应该用控制变量法排查插件的影响。

### [越狱设备无法通过收据验证]()

近期有越狱用户更新 Thor  后，验证报 3840 错误的，解决方法：

『狱越设备』安装过『内购、商店相关』或者别的未知插件，使 App 从商店环境变为沙盒环境，导致商店环境下的收据验证异常，甚至闪退。

请在停用相关插件（曾经安装过相关插件留有残留未清理干净的，即使重新入獄也会影响，需重装后正常删除）或者退出狱越后重试。

（可能重启设备生效，能成功识别正版的前提是系统商店基础设施未被损坏）

总结：正版辩认需要用收据数据向 iOS 系统发起询问，如果 app 获取收据，或者询问系统的任何环节被越狱后的一些插件破坏，此过程就无法成功，也就不知道是否正版。
并不能在购买过正版后，通过心灵感应告诉 app 它是正版。


同理越狱乱装了很多插件后，遇到每次启动（哪怕相隔几秒）都要验证的，参考上述原理，自行排除插件。

收据验证基于系统收据验证服务实现，有的越狱设备因为禁用了系统的收据子系统以达到破解商店或者内购的效果，进而造成 app 无法通过收据验证。

『狱越设备』如果安装了『内购、商店相关』或者别的未知插件，使 App 从商店环境变为沙盒环境，导致商店环境下的收据数据获取异常，甚至闪退。（商店环境的购买收据正确获取后才能继续验证）

请在停用相关插件（曾经安装相关插件留有残留未清理干净的，请重装后正常删除）或者退出狱越后重试。（验证需在系统商店基础设施未被破坏的情况下进行，也许重启设备生效）


### [越狱设备打开应用闪退]()

商店更新 Thor 1.3.9 后闪退或提示警告的越狱手机，关闭相关插件，然后删除所有类型针对 Thor 的补丁即可。
（注意，不是删插件，是删除补丁，不是关闭补丁，只关闭没用）

觉得自己没装的，就去搜索提示的关键字找到曾经装过的补丁残留文件删除。
即使删除了的插件，也有可能残留曾经装过的补丁文件

所有的商店上架 App 都是在非越狱环境下开发并调试的，各位越狱了又爱各种折腾的大神们，折腾 App 出问题后，请自行反推，排除解决，越狱加上乱折腾后，App 的运行环境变因太多，开发者也无法动用心灵感应找出问题所在，毕竟越狱环境不是 App 开发和正常运作的基础环境。