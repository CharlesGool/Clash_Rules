[中文](https://github.com/CharlesGool/Clash_Rules/edit/main/README.md) | [English](https://github.com/CharlesGool/Clash_Rules/edit/main/README_EN.md)

本Clash分流规则包括两个版本,一个是完整版(不带后缀的版本),一个是Lite版本. 完整版本主要为x64/高性能设备设计,需要大内存才能跑起来(我这里测试4G内存的设备没有问题,实测512M内存+512M Zram的设备启动时会爆内存,请使用更大内存的设备或者开启更大的Zram),Lite版设计为低内存设备,可以快速启动,代价是更少的可配置的分流规则.

完整版的分流特性如下:

1. 防DNS泄露(需要配合我的项目中的[Openclash配置文件](https://github.com/CharlesGool/Clash_Rules/blob/main/openclash_config_V181_final.txt))
2. 私有域名绕过,走直连(例如TPlink路由器的http://tplogin.cn/,数据来自GEOSITE)
3. 临时规则:
   1. 屏蔽Spotify更新
   2. Speedtest走直连
   3. PassNet提供的域名走直连
   4. DNS域名优化
   5. 禁用QUIC协议(更好检测流量)
4. 交易优化
   1. 国际可直连交易全部走直连,规则组包括: 🇦🇺澳大利亚银行/🇭🇰香港银行/🇸🇬新加坡银行/🇺🇸美国银行/🇬🇧英国银行/🇨🇦加拿大银行/🇩🇪德国银行/🇫🇷法国银行/🇯🇵日本银行/🇳🇱荷兰银行,以及虚拟银行Wise/Revolut/Monzo,以及Visa/MasterCard系统. 还有一些其他可能上面的rule没有收录的,自己进行了补全,包括: 澳新银行/汇丰银行/恒生银行/八达通/Paypal/盈透证券/Stripe/OCSP在线证书状态协议.
   2. 国际不可直连交易为单独的一个规则组,可手动选择,默认走新加坡纯净节点. 包括: 彭博社/路透社/欧易.
   3. 中国的交易也是一个单独的规则组,可手动选择,默认直连,包括：农业银行、中国银行、交通银行、建设银行、光大银行、广发银行、招商银行、工商银行、邮储银行、兴业银行、中国股票相关证券服务及中国银联
5. 📵去广告&反追踪规则组旨在提升网络隐私与安全性，默认丢弃拦截，涵盖：全类目广告屏蔽、第三方隐私行为跟踪防护、以及针对运营商或恶意劫持的专项防护。
6. 🔞NSFW的规则因为一些网站有风控,以及一些国家的法律保护,所以默认走的是美国纯净节点,也可以选择Reject拒绝(如果想要禁止访问的话)
7. 其他的规则主要按照逻辑: 独立公司/大厂公司,再对大厂进行细分的逻辑,大厂全部有自己的规则组,可以监控流量/一键断网. 优先级如下
   1. 全球独立不可直连社交平台,包括Telegram/Reddit/Discord/Pinterest/LinkedIn,考虑到Reddit/LinkedIn可能风控严一些,所以有单独的规则组,默认走新加坡纯净节点,其他默认走`全球网络-廉价流量-负载均衡-低延迟`
   2. 全球独立媒体平台,包括Netflix/Disney+/Twitch/Spotify/Anime1, Netflix/Disney+可能对IP要求比较高,所以有单独的规则组,默认走新加坡纯净节点,Anime1走直连
   3. 全球AI/代码平台,分为会风控(包括OpenAI/Claude/Perplexity)和不会风控的(包括GitLab/Docker/Ollama/Nvidia),会风控的有单独的策略组,不会风控的走`全球网络-廉价流量-负载均衡-低延迟`
   4. 全球可直连大厂,包括:🍎Apple/Microsoft, 其中Apple-AI/GitHub有自己单独的规则组,防止连接不稳定和解锁Apple-AI
   5. 全球不可直连大厂,包括:Google/Twitter/Meta/BytedanceGlobal,其中Gemini有自己单独的规则组,防止风控.
   6. 中国独立媒体平台,包括小红书/新浪微博/知乎/豆瓣,有自己单独的规则组,也可以用通过修改节点来修改显示的IP,也可以一键断网
   7. 中国独立社交平台,包括哔哩哔哩,有自己单独的规则组,也可以用通过修改节点来修改显示的IP,也可以一键断网
   8. 中国AI&代码平台,包括Gitee,走直连,也可以一键断网
   9. 中国手机品牌,包括小米,有自己单独的规则组,也可以用通过修改节点来修改显示的IP,也可以一键断网
   10. 中国其他,包括拓竹,走直连,也可以一键断网
   11. 中国大厂,包括腾讯/阿里巴巴/百度/字节跳动中国/网易,有自己单独的规则组,也可以用通过修改节点来修改显示的IP,也可以一键断网
   12. 兜底规则,使用GEOSITE的规则,所有的未分类的大陆流量为一个规则组,可以用通过修改节点来修改显示的IP,也可以一键断网

以及支持: 多机场/负载均衡/纯净廉价网络分离/多规则组一键断网/自建服务器等规则



如何使用?

1. 从你的机场下载订阅,找到`proxies`,复制到release中的配置文件替换`proxies`.

2. 打开任意一个AI,复制整个`proxies`输入以下内容

   ```
   proxies: 
   根据我的proxies,填入以下proxy-groups:
   # -------------------------------------
   # [🌏全球网络-廉价流量-负载均衡-低延迟]
   # -------------------------------------
   - { name: '🌏全球网络-廉价流量-负载均衡-低延迟', type: load-balance, strategy: round-robin, url: 'http://www.gstatic.com/generate_204', interval: 300, proxies: ['ProviderA-廉价节点-url-test', 'ProviderB-廉价节点-url-test'] }
   
   # -----------------------------
   # [🌏全球纯净网络-🇸🇬新加坡节点]
   # -----------------------------
   - { name: '🌏全球纯净网络-🇸🇬新加坡节点', type: select, proxies: ['REJECT'] }
   
   # ---------------------------
   # [🌏全球纯净网络-🇺🇸美国节点]
   # ---------------------------
   - { name: '🌏全球纯净网络-🇺🇸美国节点', type: select, proxies: ['REJECT'] }
   
   # ---------------------------
   # [🌏全球纯净网络-🇭🇰香港节点]
   # ---------------------------
   - { name: '🌏全球纯净网络-🇭🇰香港节点', type: select, proxies: ['REJECT'] }
   
   # ---------------------------
   # [🌏全球纯净网络-🇯🇵日本节点]
   # ---------------------------
   - { name: '🌏全球纯净网络-🇯🇵日本节点', type: select, proxies: ['REJECT'] }
   
   # -------------------
   # [自建服务器-Select]
   # -------------------
   - { name: '自建服务器-Select', type: select, proxies: ['REJECT'] }
   
   # ---------------------------
   # [🌏全球网络-节点供应商测试]
   # ---------------------------
   
   # [ProviderA-廉价节点-url-test]
   - { name: ProviderA-廉价节点-url-test, type: url-test, url: http://www.gstatic.com/generate_204, interval: 300, proxies: ['REJECT'] }
   # [ProviderB-廉价节点-url-test]
   - { name: ProviderB-廉价节点-url-test, type: url-test, url: http://www.gstatic.com/generate_204, interval: 300, proxies: ['REJECT'] }
   # [ProviderA-All]
   - { name: ProviderA-All, type: select, proxies: ['REJECT'] }
   # [ProviderB-All]
   - { name: ProviderB-All, type: select, proxies: ['REJECT'] }
   
   # [🌏全球网络-所有节点-select]
   - { name: '🌏全球网络-所有节点-select', type: select, proxies: ['REJECT'] }
   ```

3. 粘贴在proxy-groups的最后面即可,记得保持正确换行即可.

4. 如果你使用的是Openwrt和Openclash,可以下载[Openclash配置文件](https://github.com/CharlesGool/Clash_Rules/blob/main/openclash_config_V181_final.txt) 替换到Openwrt的`/etc/config/openclash`,可以有效防止DNS泄露

