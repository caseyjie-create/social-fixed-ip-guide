# 🌐 美国住宅 IP 稳定访问方案

> **AI 时代,你的账号值得一个稳定的身份。**
>
> 通过 **Clash Verge + 自建 VPS 跳板 + 美国住宅 IP** 的三层链式代理,实现访问 Twitter、Instagram、TikTok、Claude、ChatGPT、Gemini 等网站时**永久使用同一个固定住宅 IP**,从此告别异常登录警告、验证码轰炸、账号被封。

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-lightgrey.svg)
![Clash](https://img.shields.io/badge/Clash%20Verge%20Rev-supported-green.svg)

---

## 😱 你遇到过这些吗?

- 🔒 Twitter / Instagram 账号刚注册就要手机验证,最后直接被封
- 🚫 ChatGPT 登录一直转圈,提示 `Unable to load site`
- 📧 Google 账号每天收到"异常登录"邮件,频繁要求二次验证
- 😮‍💨 TikTok 视频看两下就被限流,刷不出海外内容
- 💔 精心养的 Facebook 广告账号突然被禁用,申诉石沉大海

**这些问题的根源是同一个:你的 IP 不干净 + IP 经常变化。**

### 为什么普通机场节点解决不了?

| 问题 | 说明 |
|------|------|
| 💥 **IP 被大量滥用** | 机场节点 IP 被成百上千用户共用,早被 AI / 社媒平台拉黑 |
| 🔄 **IP 频繁变化** | 机场节点 IP 每 7-15 天轮换一次,账号登录地飘忽不定 |
| 🏢 **数据中心 IP 被识别** | 机场多为机房 IP,OpenAI / Netflix 等会直接拒绝服务 |
| 🇨🇳 **中国 IP 被硬封** | 很多海外服务对中国 IP 一刀切,哪怕你用代理也会被检测 |

### AI 和社媒平台的风控越来越严

**2024 年以来,OpenAI、Meta、Google、Anthropic 等都在加强 IP 风控**:

- **OpenAI**:检测机房 IP,非住宅 IP 几乎 100% 被拒
- **Anthropic(Claude)**:账号绑定 IP,频繁切换 IP 会触发安全验证
- **Meta(Facebook/Instagram)**:多账号关联检测,共享 IP 会把账号批量封杀
- **TikTok**:IP 变化 → 限流、隐形封禁
- **Twitter/X**:异常登录检测越来越敏感

### 真正的解决方案:美国住宅 IP

**住宅 IP(Residential IP)= 美国真实家庭宽带的 IP**。

对于平台而言:
- ✅ 这就是一个正常美国用户在家里上网
- ✅ IP 属于大型 ISP(Verizon、AT&T、Comcast 等)
- ✅ IP 干净、没有代理特征、不在黑名单里
- ✅ 长期固定不变,账号行为稳定

**把住宅 IP 固定下来,你的海外账号就像真正的美国本地用户一样稳定。**

---

## 💡 我自用的方案

经过反复测试,我选择了下面这套组合。**目前自己在用,稳定运行**,账号再也没有被风控过。

### 需要购买的 3 样东西

#### 1️⃣ 机场订阅(负责翻墙)

**我用的是 WgetCloud 全球加速**,Trojan 协议,稳定性好,美国节点对 AI 和社媒解锁支持不错。

👉 **[注册 WgetCloud](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf)**

*通过此链接注册可享新用户优惠*

> 💡 其实机场不限定,任何稳定能翻墙的机场都行。我选 WgetCloud 是因为节点稳、速度快、支持 Trojan 协议。你已经有机场的话跳过这一步。

#### 2️⃣ 美国 VPS(做固定跳板)

**我用的是 Racknerd 的特价 KVM VPS**,年付 $10-15,纽约/洛杉矶机房任选。配置 1GB 内存就够用,它只负责做中转,不吃资源。

👉 **[注册 Racknerd](https://my.racknerd.com/aff.php?aff=19430)**

*通过此链接注册,到特价页面(Black Friday Specials 或 Special Offers)即可选购 $10+ 年付套餐*

推荐原因:
- ✅ 便宜(一年不到 100 元人民币)
- ✅ IP 永久固定(这是整个架构的关键)
- ✅ 流量 2TB 够用,绰绰有余
- ✅ 可选多个美国机房(纽约、洛杉矶、西雅图等)

#### 3️⃣ 美国住宅 IP(最终出口)

**我用的是 Cliproxy 的静态长效 ISP 住宅 IP**,$3.8 起/月,IP 在有效期内固定不变,是真实住宅网络的 IP,质量纯净。

👉 **[Cliproxy 官网](https://share.cliproxy.com/share/l1bvl4pxt)**

*通过此链接注册可享邀请返利*

选择原因:
- ✅ 真正的住宅 IP,不是机房 IP 伪装
- ✅ 静态长效,一个 IP 用一个月不变
- ✅ 支持账密认证 + 白名单双重模式
- ✅ 支持 HTTP / HTTPS / SOCKS5 协议
- ✅ 价格亲民,适合个人用户

---

## 📖 目录

- [方案架构](#方案架构)
- [为什么需要三层代理](#为什么需要三层代理)
- [前置准备](#前置准备)
- [完整部署步骤](#完整部署步骤)
  - [第一步:购买 VPS](#第一步购买-vps)
  - [第二步:VPS 安装 SOCKS5 服务](#第二步vps-安装-socks5-服务)
  - [第三步:本地测试 VPS 连通性](#第三步本地测试-vps-连通性)
  - [第四步:住宅代理白名单配置](#第四步住宅代理白名单配置)
  - [第五步:Clash Verge 配置](#第五步clash-verge-配置)
  - [第六步:验证成功](#第六步验证成功)
- [完整配置示例](#完整配置示例)
- [规则语法说明](#规则语法说明)
- [添加更多网站](#添加更多网站)
- [常见问题](#常见问题)
- [安全建议](#安全建议)
- [成本估算](#成本估算)

---

## 方案架构

```
┌───────────────────────────────────────────┐
│   本地设备 (公网 IP 会变动)                │
│   Clash Verge Tun 模式接管所有流量         │
└──────────────────┬────────────────────────┘
                   │ 翻墙
                   ↓
┌───────────────────────────────────────────┐
│   机场美国节点                             │
│   (负责穿过 GFW, 节点 IP 会定期变化)       │
└──────────────────┬────────────────────────┘
                   │
                   ↓
┌───────────────────────────────────────────┐
│   自建 VPS (固定美国 IP)                   │
│   运行 gost SOCKS5 服务,端口 1080         │
│   这是整个架构的稳定枢纽                   │
└──────────────────┬────────────────────────┘
                   │
                   ↓
┌───────────────────────────────────────────┐
│   住宅代理 IP (永久固定)                   │
│   VPS IP 已加入住宅代理白名单              │
└──────────────────┬────────────────────────┘
                   │
                   ↓
┌───────────────────────────────────────────┐
│   目标网站 (Twitter/Claude/ChatGPT 等)     │
│   看到的访问 IP 永远是住宅 IP              │
└───────────────────────────────────────────┘
```

### 三层架构职责分工

| 层级 | 作用 | 是否可替换 |
|------|------|-----------|
| **机场节点** | 翻墙穿过 GFW | 可随时更换机场,节点 IP 变化无影响 |
| **自建 VPS** | 固定跳板 IP,用于代理服务白名单 | IP 永久固定,是核心枢纽 |
| **住宅代理** | 最终出口 IP,对外展示 | 可换 IP,但需同步更新配置 |

---

## 为什么需要三层代理

### 为什么不直接用机场节点?

机场节点 IP 会变。平台看到你今天从美国 A IP 登录,明天从美国 B IP 登录,会认为账号可能被盗,触发二次验证、短信验证,甚至直接封号。

### 为什么不直接连住宅代理?

大部分住宅代理服务对中国大陆 IP 做了**硬性封锁**,从国内直连会返回 `403 Mainland China IP banned`。

### 为什么要用 VPS 做跳板?

住宅代理通常用**白名单方式**授权访问。把 VPS 的固定 IP 加入白名单一次,永久有效。如果直接把机场节点 IP 加白名单,机场 IP 每 15 天变化,白名单天天失效,维护成本极高。

### 自建 VPS 成本高吗?

**极低**。选用 Racknerd 等低成本 VPS 商,1GB 内存、年付约 $10-15,**平均每月不到一杯咖啡钱**。

---

## 前置准备

### 你需要准备

- ✅ 一个**机场订阅**(用于翻墙的底层通道)→ [推荐 WgetCloud](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf)
- ✅ 一台**美国 VPS**(固定 IP,建议 Racknerd 特价套餐)
- ✅ 一个**美国住宅代理 IP**(静态长效 ISP)→ [推荐 Cliproxy](https://share.cliproxy.com/share/l1bvl4pxt)
- ✅ **Clash Verge Rev**(Mihomo 内核,支持 dialer-proxy)

### 推荐服务商

**机场(翻墙用)**:

- [WgetCloud 全球加速](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf) - Trojan 协议,IEPL 专线,稳定性佳

**VPS(做跳板用)**:

- [Racknerd](https://my.racknerd.com/aff.php?aff=19430) - 年付 $10-15 特价套餐,做跳板足够 ⭐ 个人自用推荐
- [Vultr](https://www.vultr.com) - $6/月,稳定可靠

**住宅代理(最终出口)**:

- [Cliproxy](https://share.cliproxy.com/share/l1bvl4pxt) - 静态长效 ISP,$3.8 起/月 ⭐ 个人自用推荐

**客户端**:

- [Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) - 必须使用这个版本,支持 `dialer-proxy`

---

## 完整部署步骤

### 第一步:购买 VPS

#### 选择配置

最低配置足矣,因为 VPS 只做轻量转发:

- **内存**:1GB
- **CPU**:1 核
- **硬盘**:25GB
- **流量**:2TB/月
- **带宽**:1Gbps
- **机房**:美国(洛杉矶、纽约、西雅图任选)
- **系统**:Ubuntu 22.04 LTS 64-bit

#### 购买流程

1. 访问 **[Racknerd 官网](https://my.racknerd.com/aff.php?aff=19430)**,进入 KVM VPS 页面
2. 选择 KVM VPS 特价套餐(Special Offers 或 Black Friday Specials 页面)
3. 机房选择美国任一机房
4. 系统选择 **Ubuntu 22.04 LTS 64-bit**(后续教程基于此系统)
5. 不购买任何增值服务(备份、额外 IP、IPv6 等全部不选)
6. 账单地址可使用 [fakenamegenerator.com](https://www.fakenamegenerator.com) 生成
7. 使用 PayPal 或信用卡付款
8. 等待 1-60 分钟内收到开通邮件,记下 **VPS IP** 和 **root 密码**

> 💡 **提示**:RackNerd 等服务商常年有特价,年付 $10-15 即可获得 1GB 配置。可在 LowEndBox 等论坛查找当前特价。

---

### 第二步:VPS 安装 SOCKS5 服务

本方案使用 **gost v3** 作为 SOCKS5 代理服务,稳定高效。

#### 2.1 SSH 登录 VPS

> ⚠️ **前置条件**:本地客户端需开启 Clash 并走美国节点,否则国内到 VPS 的 SSH 连接可能被运营商干扰或超时。

```bash
ssh root@<YOUR_VPS_IP>
```

粘贴 root 密码回车登录。

#### 2.2 下载并安装 gost

```bash
cd /root
wget https://github.com/go-gost/gost/releases/download/v3.0.0/gost_3.0.0_linux_amd64.tar.gz
tar -xzf gost_3.0.0_linux_amd64.tar.gz
mv gost /usr/local/bin/
chmod +x /usr/local/bin/gost
gost -V
```

若输出类似 `gost v3.0.0 (go1.23.4 linux/amd64)`,则安装成功。

##### 下载失败备用方案

若 GitHub 访问慢或返回小文件(< 2KB),使用镜像:

```bash
wget https://ghproxy.com/https://github.com/go-gost/gost/releases/download/v3.0.0/gost_3.0.0_linux_amd64.tar.gz
```

#### 2.3 创建 systemd 服务

```bash
cat > /etc/systemd/system/gost.service <<'EOF'
[Unit]
Description=GOST SOCKS5 Proxy
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/gost -L "socks5://YOUR_USER:YOUR_PASSWORD@:1080"
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF
```

> ⚠️ **重要**:
> - 将 `YOUR_USER` 替换为自定义用户名(如 `proxyuser`)
> - 将 `YOUR_PASSWORD` 替换为**强密码**(16 位以上,字母+数字组合)
> - 生成强密码命令:`openssl rand -hex 12`

#### 2.4 启动并验证服务

```bash
systemctl daemon-reload
systemctl enable gost
systemctl start gost
systemctl status gost
```

看到绿色 `active (running)` 则成功,按 `q` 退出。

#### 2.5 放行防火墙端口

```bash
ufw allow 1080/tcp 2>/dev/null || true
iptables -I INPUT -p tcp --dport 1080 -j ACCEPT
```

#### 2.6 VPS 本机测试 SOCKS5

```bash
curl -x socks5://YOUR_USER:YOUR_PASSWORD@127.0.0.1:1080 http://ifconfig.me
```

返回 VPS 自身 IP 即为成功。退出 VPS:

```bash
exit
```

---

### 第三步:本地测试 VPS 连通性

回到本地终端,测试 `本地 → Clash → VPS` 的链路:

```bash
curl -x "socks5h://YOUR_USER:YOUR_PASSWORD@<YOUR_VPS_IP>:1080" https://api.ipify.org
```

返回 VPS 的公网 IP 说明整条链路已通。

> 💡 **注意**:此处必须使用 `socks5h`(h 表示让 VPS 做 DNS 解析),否则可能触发 IPv6 解析导致 "Network unreachable" 错误。

---

### 第四步:住宅代理白名单配置

1. 登录住宅代理服务商控制台([Cliproxy Dashboard](https://dash.cliproxy.com))
2. 进入**白名单管理**或 **IP 授权**页面
3. 添加 VPS 的固定 IP
4. 保存(通常即时生效)

> 💡 **提示**:之后 VPS IP 不会变,白名单**只需加一次,永久有效**。如果之前加过机场节点 IP,可以删除(会变动,留着没用)。

---

### 第五步:Clash Verge 配置

#### 5.1 必须确认的基础设置

在 **Clash Verge → 设置** 中确认:

- ✅ **虚拟网卡模式 (Tun)**:开启
- ✅ **系统代理**:开启
- ✅ **IPv6**:**关闭**(关键!否则 Tun 只建立 IPv6 网卡,IPv4 流量不被接管)
- ✅ **服务模式**:已安装并运行中(macOS 上 Tun 必须安装此服务)
- ✅ **代理模式**:Rule(不要选 Global)

#### 5.2 配置 Script 覆写

> ⚠️ **重要**:Clash Verge 的 Merge 覆写在合并 `prepend-proxies` 字段时存在已知 Bug,会静默丢失节点定义。**必须使用 Script 覆写**(JavaScript 方式)确保配置完整注入。

1. Clash Verge → 订阅页面 → 点击「**全局扩展脚本**」卡片
2. `Cmd+A` 全选后删除现有内容
3. 粘贴下面的完整脚本(**记得替换占位符**)
4. `Cmd+S` 保存
5. 回订阅页面,点击订阅卡片的 **C 形刷新图标**

```javascript
function main(config) {
  // 1. VPS 跳板(SOCKS5)
  config.proxies = config.proxies || [];
  config.proxies.unshift({
    name: "US_VPS_Jump",
    type: "socks5",
    server: "YOUR_VPS_IP",          // 替换为你的 VPS IP
    port: 1080,
    username: "YOUR_USER",           // 替换为你的 SOCKS5 用户名
    password: "YOUR_PASSWORD",       // 替换为你的 SOCKS5 密码
    udp: true
  });

  // 2. 住宅代理(通过 VPS 前置)
  config.proxies.unshift({
    name: "Residential_ISP",
    type: "http",                    // 根据服务商协议调整: http/socks5
    server: "RESIDENTIAL_IP",        // 替换为你的住宅代理 IP
    port: 443,                       // 替换为对应端口
    username: "PROXY_USER",          // 替换为住宅代理账号
    password: "PROXY_PASSWORD",      // 替换为住宅代理密码
    "dialer-proxy": "US_VPS_Jump"   // 关键:指定通过 VPS 前置
  });

  // 3. 代理组
  config["proxy-groups"] = config["proxy-groups"] || [];
  config["proxy-groups"].unshift({
    name: "社媒固定IP",
    type: "select",
    proxies: ["Residential_ISP"]
  });

  // 4. 规则 —— 需要固定 IP 的所有域名
  const fixedIPRules = [
    // ======= Twitter / X =======
    "DOMAIN-SUFFIX,twitter.com,社媒固定IP",
    "DOMAIN-SUFFIX,x.com,社媒固定IP",
    "DOMAIN-KEYWORD,twitter,社媒固定IP",
    "DOMAIN-SUFFIX,twimg.com,社媒固定IP",
    "DOMAIN-SUFFIX,t.co,社媒固定IP",

    // ======= Instagram =======
    "DOMAIN-SUFFIX,instagram.com,社媒固定IP",
    "DOMAIN-SUFFIX,cdninstagram.com,社媒固定IP",

    // ======= Facebook =======
    "DOMAIN-SUFFIX,facebook.com,社媒固定IP",
    "DOMAIN-SUFFIX,fbcdn.net,社媒固定IP",
    "DOMAIN-SUFFIX,fb.com,社媒固定IP",

    // ======= TikTok =======
    "DOMAIN-SUFFIX,tiktok.com,社媒固定IP",
    "DOMAIN-SUFFIX,tiktokcdn.com,社媒固定IP",
    "DOMAIN-SUFFIX,tiktokv.com,社媒固定IP",
    "DOMAIN-SUFFIX,byteoversea.com,社媒固定IP",

    // ======= Claude / Anthropic =======
    "DOMAIN-SUFFIX,claude.ai,社媒固定IP",
    "DOMAIN-SUFFIX,claude.com,社媒固定IP",
    "DOMAIN-SUFFIX,anthropic.com,社媒固定IP",
    "DOMAIN-KEYWORD,anthropic,社媒固定IP",
    "DOMAIN-KEYWORD,claude,社媒固定IP",
    "DOMAIN-SUFFIX,claudeusercontent.com,社媒固定IP",

    // ======= OpenAI / ChatGPT =======
    "DOMAIN-SUFFIX,openai.com,社媒固定IP",
    "DOMAIN-SUFFIX,chatgpt.com,社媒固定IP",
    "DOMAIN-SUFFIX,oaistatic.com,社媒固定IP",
    "DOMAIN-SUFFIX,oaiusercontent.com,社媒固定IP",
    "DOMAIN-SUFFIX,sora.com,社媒固定IP",
    "DOMAIN-KEYWORD,openai,社媒固定IP",
    "DOMAIN-KEYWORD,chatgpt,社媒固定IP",
    "DOMAIN-SUFFIX,auth0.com,社媒固定IP",
    "DOMAIN-SUFFIX,algolia.net,社媒固定IP",

    // ======= Google Gemini =======
    "DOMAIN-SUFFIX,gemini.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,bard.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,aistudio.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,generativelanguage.googleapis.com,社媒固定IP",
    "DOMAIN-SUFFIX,makersuite.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,notebooklm.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,notebooklm.google,社媒固定IP",
    "DOMAIN-SUFFIX,deepmind.google,社媒固定IP",
    "DOMAIN-SUFFIX,labs.google,社媒固定IP",

    // ======= Cloudflare 验证(AI 服务需要)=======
    "DOMAIN-SUFFIX,challenges.cloudflare.com,社媒固定IP",

    // ======= IP 查询工具(调试用)=======
    "DOMAIN-SUFFIX,ipinfo.io,社媒固定IP",
    "DOMAIN-SUFFIX,ifconfig.me,社媒固定IP",
    "DOMAIN-SUFFIX,ipify.org,社媒固定IP",
    "DOMAIN-SUFFIX,ip.sb,社媒固定IP"
  ];
  config.rules = [...fixedIPRules, ...(config.rules || [])];

  return config;
}
```

---

### 第六步:验证成功

#### 方法 1:浏览器验证 IP

新开无痕窗口访问:

```
https://ipinfo.io/ip
```

应显示住宅代理的 IP。

#### 方法 2:Clash 连接页面查看链路

左侧「连接」页面,访问 ipinfo.io 后会出现两条连接:

| 主机 | 链路 | 说明 |
|------|------|------|
| `ipinfo.io:443` | `社媒固定IP / Residential_ISP` | 浏览器到 Clash 的连接 |
| `<VPS_IP>:443` | `US_VPS_Jump` | Clash 内部 dialer-proxy 链 |

两条连接都正常出现,说明三层链式代理完整工作。

#### 方法 3:终端验证

```bash
curl https://ipinfo.io/ip
```

应返回住宅代理 IP。

---

## 完整配置示例

### 典型使用场景的推荐域名列表

除了社媒和 AI 服务,你可能还想把以下网站加入固定 IP:

```javascript
// 跨境电商
"DOMAIN-SUFFIX,amazon.com,社媒固定IP",
"DOMAIN-SUFFIX,ebay.com,社媒固定IP",
"DOMAIN-SUFFIX,shopify.com,社媒固定IP",

// 开发者平台
"DOMAIN-SUFFIX,github.com,社媒固定IP",
"DOMAIN-SUFFIX,vercel.com,社媒固定IP",

// 办公协作
"DOMAIN-SUFFIX,notion.so,社媒固定IP",
"DOMAIN-SUFFIX,figma.com,社媒固定IP",

// 海外金融(仅限海外注册账号)
"DOMAIN-SUFFIX,paypal.com,社媒固定IP",
"DOMAIN-SUFFIX,wise.com,社媒固定IP",
```

---

## 规则语法说明

### DOMAIN-SUFFIX(后缀匹配)

匹配以指定字符串**结尾**的域名,精准安全。

| 域名示例 | `DOMAIN-SUFFIX,twitter.com` 是否命中 |
|----------|--------------------------------------|
| `twitter.com` | ✅ 命中 |
| `api.twitter.com` | ✅ 命中(子域名) |
| `mobile.twitter.com` | ✅ 命中 |
| `abs.twimg.com` | ❌ 不命中(后缀是 twimg.com) |
| `notwitter.com` | ❌ 不命中(非独立前缀) |

### DOMAIN-KEYWORD(关键词匹配)

匹配域名中**任意位置**包含关键词,覆盖广但可能误伤。

| 域名示例 | `DOMAIN-KEYWORD,twitter` 是否命中 |
|----------|-----------------------------------|
| `twitter.com` | ✅ 命中 |
| `api.twitter.com` | ✅ 命中 |
| `twittercdn.net` | ✅ 命中 |
| `fake-twitter-phishing.com` | ⚠️ 命中(误伤钓鱼网站) |

### 使用建议

- ✅ **优先使用 `DOMAIN-SUFFIX`**,99% 场景首选
- ✅ `DOMAIN-KEYWORD` 仅在域名变种多、关键词独特时用作兜底
- ❌ **严禁对 `google` / `api` / `www` 等通用词用 KEYWORD**,会大面积误伤

---

## 添加更多网站

### 操作方式

1. 打开 Clash Verge → 订阅 → 全局扩展脚本
2. 找到 `fixedIPRules` 数组
3. 追加新规则行:

```javascript
"DOMAIN-SUFFIX,example.com,社媒固定IP",
```

4. 保存 → 刷新订阅

### 建议固定 IP 的场景

- ✅ 社交媒体账号(Twitter/Instagram/TikTok/Facebook)
- ✅ AI 服务(Claude/ChatGPT/Gemini/Perplexity)
- ✅ 跨境电商账号(Amazon Seller/Shopify)
- ✅ 广告平台(Facebook Ads/Google Ads)
- ✅ 海外金融(PayPal/Wise,仅限海外注册账号)

### ⛔ 不建议固定 IP 的场景

- ❌ **国内银行/支付宝/微信支付**:美国 IP 访问会触发风控,账户可能冻结
- ❌ **Netflix/Disney+**:住宅代理 IP 常被识别,不如机场专用解锁节点
- ❌ **Gmail/YouTube 的整个 google.com**:会连累其他 Google 服务
- ❌ **国内网站(淘宝/京东/B 站)**:本来就应走直连
- ❌ **大流量视频下载**:住宅代理通常按流量计费,烧钱快

---

## 常见问题

<details>
<summary><b>Q: ipinfo.io 显示的不是住宅代理 IP</b></summary>

1. 检查 Clash「连接」页面链路是否显示 `社媒固定IP / Residential_ISP`
2. 确认住宅代理白名单里有 VPS IP
3. SSH 到 VPS 检查 gost 服务:`systemctl status gost`
4. 查看 gost 日志:`journalctl -u gost -n 50`
</details>

<details>
<summary><b>Q: Clash 的 Tun 模式不生效(终端不走代理)</b></summary>

1. 检查服务模式是否已安装(首页显示「服务模式」)
2. **关闭 IPv6**(设置 → Clash 设置 → IPv6 = 关闭)
3. 重启 Tun 模式:关 → 开 → 输密码授权
4. 验证:`ifconfig | grep -A 3 utun` 应能看到 `inet 198.18.0.1`
</details>

<details>
<summary><b>Q: curl 返回 "Mainland China IP banned"</b></summary>

说明 Clash 没把该网站域名路由到固定 IP 组,直接走国内 IP 被住宅代理拒绝:

1. 确认 Tun 模式已正确接管流量(`ifconfig` 能看到 utun 带 inet 198.18.0.1)
2. 在 Clash Script 的 `fixedIPRules` 里添加该网站域名
3. 保存并刷新订阅
4. 清除 Clash 连接页面的旧连接,强制刷新浏览器
</details>

<details>
<summary><b>Q: Claude/ChatGPT/Gemini 登录失败或转圈</b></summary>

Cloudflare 验证需要 `challenges.cloudflare.com` 域名也走固定 IP。脚本中已包含。

如果还是失败,可能是住宅代理 IP 被该服务标记:
1. 清除浏览器 cookie 和缓存
2. 新开无痕窗口尝试
3. 严重时联系代理服务商要求更换 IP
</details>

<details>
<summary><b>Q: Clash 运行时配置里搜不到 VPS 节点</b></summary>

1. 脚本没合并成功:重新保存 Script + 刷新订阅
2. 确认用的是 **Script 覆写**(不是 Merge 覆写)
3. 检查 Script 里的 JavaScript 语法(引号、逗号)
4. 打开订阅页面右上角的文档图标,查看合并后的运行时配置
</details>

<details>
<summary><b>Q: 如何实时查看 gost 收到了哪些连接</b></summary>

SSH 到 VPS 后运行:

```bash
journalctl -u gost -f
```

(按 `Ctrl+C` 退出)
</details>

<details>
<summary><b>Q: 如何重启 VPS 的 SOCKS5 服务</b></summary>

```bash
ssh root@<YOUR_VPS_IP>
systemctl restart gost
systemctl status gost
```
</details>

<details>
<summary><b>Q: 无论 Clash 主节点选什么,固定 IP 都不变吗?</b></summary>

**是的**。`US_VPS_Jump` 节点没有 `dialer-proxy` 字段,意味着 Clash 使用当前选中的主代理组去连 VPS。无论主节点是美国、日本、香港还是新加坡,通过 VPS 出去的 IP 永远固定,最终住宅代理返回的 IP 也永远不变。

这是链式代理的设计精髓:三层职责分离,替换任一环都不影响其他两环。
</details>

<details>
<summary><b>Q: 在路由器上也能这样配吗?</b></summary>

完全可以。建议在路由器上开启 **Guest Network(访客网络)**,配置 Clash 的 `SRC-IP-CIDR` 规则,让只有连接访客 WiFi 的设备走固定 IP,其他家庭设备(电视、家人电脑)走正常网络不受影响。
</details>

---

## 安全建议

### 🔐 VPS 安全

- **强密码**:SOCKS5 密码至少 16 位,字母+数字+符号混合
- **禁用 root 密码登录**(使用 SSH 密钥):
  ```bash
  sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
  systemctl restart ssh
  ```
- **修改 SSH 端口**(减少被扫):
  ```bash
  sed -i 's/^#*Port.*/Port 22022/' /etc/ssh/sshd_config
  systemctl restart ssh
  ufw allow 22022/tcp
  ```
- **启用防火墙**:只放行必要端口(1080、自定义 SSH 端口)

### 🔒 账号密码管理

- **所有密码用密码管理器管理**(1Password、Bitwarden、KeePass)
- **VPS 密码、住宅代理账号、Clash 配置**都属于敏感信息
- **不要把实际配置推到公开仓库**

### 📡 网络安全

- **关闭 IPv6**:避免 IPv6 泄露真实 IP
- **禁用 WebRTC**:浏览器装 WebRTC Control 扩展,防止泄露真实 IP
- **定期检查出口 IP**:访问 `ipinfo.io/ip` 确认还是固定 IP

---

## 成本估算

| 项目 | 费用 | 频率 | 年化成本 |
|------|------|------|----------|
| [机场订阅(WgetCloud)](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf) | ~$10-15 | 月 | ~$120-180 |
| [VPS(Racknerd 1GB)](https://my.racknerd.com/aff.php?aff=19430) | **$10-15** | **年** | **~$10-15** ⭐ |
| [住宅代理(Cliproxy 静态 ISP)](https://share.cliproxy.com/share/l1bvl4pxt) | $3.8+ | 月 | ~$45+ |
| **总计** | | | **~$175-240 / 年** |

> 💰 **每年不到 250 美元**,换来所有海外账号长期稳定运行,对于做社媒运营、跨境电商、AI 工具重度使用者来说,这笔投入回报率极高。

---

## 关键理解

### 核心原理

- **三层代理是必须的**,因为住宅代理通常不允许中国大陆 IP 直接访问
- **VPS 的 IP 必须永久不变**,这是整个架构的基石 —— 这就是不用机场节点做前置的原因(机场 IP 会轮换)
- **住宅代理白名单只需加 VPS IP 一次**,永久有效
- **目标网站看到的 IP 永远固定**,跨设备、跨网络、跨时间保持一致
- **Clash 主节点选什么无所谓**,只负责翻墙,最终出口 IP 始终由住宅代理决定

### 最常见的坑

- ❌ **IPv6 忘了关** → Tun 只建 IPv6 网卡,IPv4 流量不被接管
- ❌ **用 Merge 覆写写代理节点** → `prepend-proxies` 字段被 Clash Verge Bug 丢弃,必须用 Script 覆写
- ❌ **节点名含 emoji 手动敲入** → 🇺🇸 和 🇺🇲 看起来像但码点不同,要从代理页面复制粘贴
- ❌ **VPS 密码含特殊字符** → curl 命令解析失败,建议用纯字母数字密码
- ❌ **白名单加的是机场节点 IP** → 机场 IP 每 15 天变化,必须加 VPS IP 才能长期有效

---

## 常用验证命令

```bash
# 查看当前出口 IP
curl https://ipinfo.io/ip

# 查看详细 IP 信息(位置、运营商)
curl https://ipinfo.io/json

# 测试能否访问 Anthropic API
curl -I https://api.anthropic.com

# 测试能否访问 OpenAI
curl -I https://api.openai.com

# 一键测试所有关键服务
for url in https://ipinfo.io/ip https://claude.ai https://chatgpt.com https://gemini.google.com; do
  echo "Testing: $url"
  curl -o /dev/null -s -w "  HTTP %{http_code}  remote IP: %{remote_ip}\n" "$url"
done
```

---

## 🙏 致谢与链接

### 我自用的服务商

以下是我经过对比后选择自用的服务,通过我的链接注册可以获得优惠/返利,感谢支持 🙏:

- 🛰️ **机场(翻墙)**:[WgetCloud 全球加速](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf)
- 🏠 **美国住宅 IP**:[Cliproxy 静态长效 ISP](https://share.cliproxy.com/share/l1bvl4pxt)
- 🖥️ **VPS(跳板)**:[Racknerd](https://my.racknerd.com/aff.php?aff=19430)(到特价页找 $10-15 年付套餐即可)

### 开源项目致谢

- [Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) - 优秀的 Clash 客户端
- [Mihomo](https://github.com/MetaCubeX/mihomo) - 强大的 Clash 内核
- [gost](https://github.com/go-gost/gost) - 现代化的代理工具

---

## 贡献

欢迎提 Issue 和 PR。如有配置经验或踩坑心得,欢迎分享。

如果这份文档对你有帮助,请点个 ⭐ Star 支持一下!

---

## 许可证

MIT License - 自由使用、修改、分发

---

## ⚠️ 免责声明

本文档仅用于技术交流与学习。使用者应遵守所在地区法律法规,因使用本方案产生的任何后果由使用者自行承担。

文档中推荐的服务商均为个人自用评测,通过推广链接注册不会给你带来任何额外费用,反而会让你享受到新用户优惠或返利。如果不想走推广链接,也可以直接访问服务商官网。
