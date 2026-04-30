中文: https://github.com/CharlesGool/Clash_Rules/blob/main/Readme_CN.md
English Version: 

### **Advanced Custom Clash Ruleset: Feature Overview**

This ruleset is engineered for maximum privacy, precise traffic dispatching, and optimal network performance. It utilizes a modular architecture to decouple nodes from rules, ensuring a leak-proof and highly customizable proxy environment.

**1. Precision Traffic Dispatching (Tech Giants)**
*   **Granular Corporate Routing:** Achieves highly accurate, decoupled traffic separation for major global and Chinese tech giants. It individually targets services from Tencent, Alibaba (including Qianwen), Baidu, Bytedance (separating TikTok global from BytedanceCN), and NetEase.
*   **AI & Developer Optimization:** Dedicated rules for AI platforms (Apple Intelligence, Grok, Gemini, OpenAI, Claude) and developer tools (GitHub, GitLab, Docker), ensuring unhindered access without triggering regional risk controls.

**2. Zero-Leak Privacy & DNS Architecture**
*   **Strict DNS Leak Prevention:** Built on a Fake-IP enhanced mode using the `GeoIP Dat` database. It actively disables the QUIC protocol (`UDP/443` rejection) to force traffic through TCP, effectively neutralizing DNS leaks.
*   **Anti-Tracking & Hijacking Protection:** Integrates comprehensive rule providers to block intrusive trackers, telemetry (e.g., Datadog), and DNS hijacking, maintaining a clean and ad-free browsing experience.

**3. Financial-Grade Security & Kill Switch**
*   **Global & Local Banking Segregation:** Highly optimized routing for international banks (US, UK, SG, AU, etc.), virtual finance platforms (Revolut, Monzo), and Chinese domestic banks.
*   **"Kill Switch" for Undirectable Trades:** Features a strict "一键断网" (One-Click Disconnect/Reject) policy for unsupported global trading platforms (e.g., OKX, Bloomberg), preventing accidental direct connections and securing sensitive financial traffic.

**4. Smart Load Balancing & Regional Pinning**
*   **Automated Load Balancing:** Groups cost-effective and high-availability nodes into an automated `url-test` load balancer for general "cheap traffic," minimizing latency without manual intervention.
*   **App-Specific Regional Pinning:** Automatically forces region-locked applications to their optimal environments (e.g., locking Spotify entirely to US nodes, routing Xiaomi and Bambulab telemetry to Chinese networks).

**5. Social Media Location Spoofing (FakeLocation)**
*   **IP Masking for Chinese Platforms:** Integrates targeted "FakeLocation" rule providers that proxy IP-resolving traffic for major Chinese social networks (Bilibili, Douyin, Xiaohongshu, Weibo, Tieba), allowing deliberate control over the displayed IP location.

**6. Modular Architecture & Node Decoupling**
*   **Node Decoupling:** Completely separates underlying proxy nodes from routing logic, allowing seamless swapping of proxy providers without rewriting complex rule sets.
*   **Temporary Global Proxy:** Supports a flexible "temporary global mode" that allows traffic normally assigned to `DIRECT` to be forcefully routed through proxies when needed.
*   **Bilingual & Intuitive UI:** The control panel groups are designed with bilingual labels (e.g., `🇨🇳中国大厂`, `🍎Apple`) and logical hierarchies, creating a clean, manageable visual experience.
