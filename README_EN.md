[中文](https://github.com/CharlesGool/Clash_Rules/edit/main/README.md) | [English](https://github.com/CharlesGool/Clash_Rules/edit/main/README_EN.md)

1. These Clash split-tunneling rules include two versions: a Full version (the one without a suffix) and a Lite version. The Full version is primarily designed for x64/high-performance devices and requires significant memory to run (my tests show no issues on devices with 4GB RAM, but real-world tests on devices with 512M RAM + 512M Zram will result in out-of-memory errors during startup; please use a device with more memory or enable a larger Zram). The Lite version is designed for low-memory devices and can start up quickly at the cost of fewer configurable split-tunneling rules.

   Split-tunneling features of the Full version are as follows:

   1. DNS leak protection (requires use with the [Openclash configuration file]() in my project)
   2. Private domain bypass, using Direct connection (e.g., TPlink router's tplogin.cn, data from GEOSITE)
   3. Temporary rules:
      1. Block Spotify updates
      2. Speedtest via Direct connection
      3. Domains provided by PassNet via Direct connection
      4. DNS domain optimization
      5. Disable QUIC protocol (better for traffic detection)
   4. Transaction optimization
      1. All international direct-connectable transactions go through Direct connection. Rule groups include: 🇦🇺 Australian Banks / 🇭🇰 Hong Kong Banks / 🇸🇬 Singapore Banks / 🇺🇸 US Banks / 🇬🇧 UK Banks / 🇨🇦 Canadian Banks / 🇩🇪 German Banks / 🇫🇷 French Banks / 🇯🇵 Japanese Banks / 🇳🇱 Dutch Banks, as well as virtual banks Wise/Revolut/Monzo, and Visa/MasterCard systems. Some others that might not have been included in the rules above have been supplemented, including: ANZ Bank / HSBC / Hang Seng Bank / Octopus / Paypal / Interactive Brokers / Stripe / OCSP Online Certificate Status Protocol.
      2. International non-direct-connectable transactions are in a separate rule group and can be manually selected; the default is a Singapore clean node. Includes: Bloomberg / Reuters / OKX.
      3. Chinese transactions are also a separate rule group and can be manually selected; the default is Direct connection. Includes: Agricultural Bank of China, Bank of China, Bank of Communications, China Construction Bank, China Everbright Bank, China Guangfa Bank, China Merchants Bank, Industrial and Commercial Bank of China, Postal Savings Bank of China, Industrial Bank, Chinese stock-related securities services, and China UnionPay.
   5. 📵 Ad-blocking & Anti-tracking rule group aims to improve network privacy and security. The default is to drop/intercept. It covers: all categories of ad blocking, third-party privacy tracking protection, and specific protection against operators or malicious hijacking.
   6. 🔞 NSFW rules, due to risk control on some websites and legal protections in some countries, default to using a US clean node. You can also choose "Reject" (if you want to prohibit access).
   7. Other rules primarily follow the logic: Independent Companies / Big Tech Companies, and then further subdividing the Big Tech. All Big Tech companies have their own rule groups for traffic monitoring/one-click disconnection. The priority is as follows:
      1. Global independent non-direct-connectable social platforms, including Telegram/Reddit/Discord/Pinterest/LinkedIn. Considering Reddit/LinkedIn may have stricter risk control, they have separate rule groups defaulting to a Singapore clean node; others default to `🌏Global Network-Cheap Traffic-Load Balance-Low Latency`.
      2. Global independent media platforms, including Netflix/Disney+/Twitch/Spotify/Anime1. Netflix/Disney+ may have higher requirements for IPs, so they have separate rule groups defaulting to a Singapore clean node; Anime1 uses Direct connection.
      3. Global AI/Code platforms, divided into those with risk control (including OpenAI/Claude/Perplexity) and those without (including GitLab/Docker/Ollama/Nvidia). Those with risk control have separate policy groups; those without go through `🌏Global Network-Cheap Traffic-Load Balance-Low Latency`.
      4. Global direct-connectable Big Tech, including: 🍎 Apple/Microsoft. Among them, Apple-AI/GitHub have their own separate rule groups to prevent unstable connections and unlock Apple-AI.
      5. Global non-direct-connectable Big Tech, including: Google/Twitter/Meta/BytedanceGlobal. Among them, Gemini has its own separate rule group to prevent risk control.
      6. Chinese independent media platforms, including Xiaohongshu/Sina Weibo/Zhihu/Douban. They have their own rule groups; you can change the displayed IP by modifying the node, or use one-click disconnection.
      7. Chinese independent social platforms, including Bilibili. They have their own rule groups; you can change the displayed IP by modifying the node, or use one-click disconnection.
      8. Chinese AI & Code platforms, including Gitee, using Direct connection or one-click disconnection.
      9. Chinese mobile brands, including Xiaomi. They have their own rule groups; you can change the displayed IP by modifying the node, or use one-click disconnection.
      10. Other Chinese entities, including Bambu Lab, using Direct connection or one-click disconnection.
      11. Chinese Big Tech, including Tencent/Alibaba/Baidu/Bytedance China/NetEase. They have their own rule groups; you can change the displayed IP by modifying the node, or use one-click disconnection.
      12. Final fallback rules, using GEOSITE rules. All unclassified Mainland China traffic is one rule group; you can change the displayed IP by modifying the node, or use one-click disconnection.

   Also supports: multiple airports / load balancing / separation of clean and cheap networks / one-click disconnection for multiple rule groups / self-built servers, etc.

   How to use?

   1. Download the subscription from your airport, find `proxies`, and copy them into the configuration file in the release to replace `proxies`.
   2. Open any AI, copy the entire `proxies` section, and input the following:

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

2. Simply paste it at the very end of the `proxy-groups`, remembering to maintain correct line breaks.

3. If you are using Openwrt and Openclash, you can download the [Openclash configuration file]() and replace the one at `/etc/config/openclash` on Openwrt to effectively prevent DNS leaks.

