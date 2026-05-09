# 🪟 Windows 系统部署指南
 
> 本指南详细介绍如何在 **Windows 10/11** 上部署「美国住宅 IP 三层链式代理」方案。
>
> 基于 [社媒固定 IP 部署指南](../README.md) 的 Windows 适配版本,所有架构和原理与主文档一致,只是客户端操作有差异。
 
---
 
## 💡 我自用的方案(Windows 也一样)
 
无论你用 Windows 还是 macOS,**底层架构和服务商完全一致**。我自用并推荐以下三个服务商,Windows 用户同样适用:
 
### 1️⃣ 机场订阅(翻墙)
 
**WgetCloud 全球加速** —— Trojan 协议,稳定性好,美国节点对 AI 和社媒解锁支持不错。
 
👉 **[注册 WgetCloud](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf)**
 
### 2️⃣ 美国 VPS(固定跳板)
 
**Racknerd 特价 KVM VPS** —— 年付 $10-15,1GB 配置足够做中转,IP 永久固定。
 
👉 **[注册 Racknerd](https://my.racknerd.com/aff.php?aff=19430)**
 
### 3️⃣ 美国住宅 IP(最终出口)
 
**Cliproxy 静态长效 ISP 住宅 IP** —— $3.8 起/月,IP 固定不变,真实住宅网络,Twitter/Claude/ChatGPT 全部稳定。
 
👉 **[注册 Cliproxy](https://share.cliproxy.com/share/l1bvl4pxt)**
 
> 💡 通过以上链接注册可享受新用户优惠。如不想走推广链接,可直接搜索官网。
 
---
 
## 📖 目录
 
- [前置准备](#前置准备)
- [Windows vs macOS 的关键差异](#windows-vs-macos-的关键差异)
- [完整部署步骤](#完整部署步骤)
  - [第一步:购买并初始化 VPS](#第一步购买并初始化-vps)
  - [第二步:Windows 上 SSH 到 VPS 安装 SOCKS5](#第二步windows-上-ssh-到-vps-安装-socks5)
  - [第三步:本地 Windows 测试 VPS 连通性](#第三步本地-windows-测试-vps-连通性)
  - [第四步:住宅代理白名单配置](#第四步住宅代理白名单配置)
  - [第五步:Clash Verge 配置](#第五步clash-verge-配置)
  - [第六步:验证成功](#第六步验证成功)
- [Windows 特有问题](#windows-特有问题)
- [验证命令速查](#验证命令速查)
- [推荐服务商](#推荐服务商)
---
 
## 前置准备
 
### 你需要
 
- ✅ Windows 10/11(管理员权限)
- ✅ 一个机场订阅 → 推荐 [WgetCloud](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf)
- ✅ 一台美国 VPS → 推荐 [Racknerd](https://my.racknerd.com/aff.php?aff=19430)
- ✅ 一个美国住宅 IP → 推荐 [Cliproxy](https://share.cliproxy.com/share/l1bvl4pxt)
- ✅ **Clash Verge Rev for Windows**
### 下载安装 Clash Verge Rev
 
访问 [Clash Verge Rev Releases](https://github.com/clash-verge-rev/clash-verge-rev/releases),下载对应你 Windows 架构的安装包:
 
- **64 位 Windows(主流)**:`Clash.Verge_x.x.x_x64-setup.exe`
- **ARM 架构(Surface Pro X 等)**:`Clash.Verge_x.x.x_arm64-setup.exe`
双击安装,选择「**所有用户**」(避免后期切换账户找不到配置)。
 
### 启用 Service Mode(服务模式)
 
**这一步在 Windows 上是必须的**,否则 Tun 模式无法接管系统流量。
 
1. 打开 Clash Verge → **设置**
2. 找到「**服务模式**」
3. 点击「**安装服务**」
4. UAC 弹窗确认 → 输入管理员密码
5. 等待 1-2 秒,显示「**服务已运行**」
---
 
## Windows vs macOS 的关键差异
 
| 操作 | macOS | Windows |
|------|-------|---------|
| **管理员权限** | sudo 输密码 | UAC 弹窗 |
| **Tun 模式** | 装服务模式后开关 | 装服务后开关(必须服务模式) |
| **SSH 工具** | 终端自带 | PowerShell 自带(Win10 1809+) |
| **DNS 缓存清理** | `sudo dscacheutil -flushcache` | `ipconfig /flushdns` |
| **环境变量** | `~/.zshrc` | 系统属性 → 高级 → 环境变量 |
| **代理变量临时设置** | `export HTTP_PROXY=...` | `$env:HTTP_PROXY = "..."` |
| **配置目录** | `~/Library/Application Support/io.github.clash-verge-rev.clash-verge` | `%APPDATA%\io.github.clash-verge-rev.clash-verge` |
| **打开终端** | Spotlight 搜「Terminal」 | Win+R → `powershell` |
| **复制文件路径** | Cmd+I 看「Where」 | Shift+右键 → 复制路径 |
 
---
 
## 完整部署步骤
 
### 第一步:购买并初始化 VPS
 
VPS 购买流程**与 macOS 完全一致**,推荐使用 [Racknerd 特价套餐](https://my.racknerd.com/aff.php?aff=19430)(年付 $10-15)。
 
详细参考主 README 的 [第一步:购买 VPS](../README.md#第一步购买-vps) 章节。
 
收到开通邮件后,记下 **VPS IP** 和 **root 密码**。
 
---
 
### 第二步:Windows 上 SSH 到 VPS 安装 SOCKS5
 
#### 2.1 用 PowerShell SSH 登录 VPS
 
> ⚠️ **前置条件**:Windows 上需先开启 Clash Verge 并走美国节点(不开机场代理直接 SSH 国内到美国,经常被运营商干扰超时)。
 
打开 **PowerShell**:
 
- 按 `Win + R`,输入 `powershell`,回车
- 或在开始菜单搜索「PowerShell」
执行:
 
```powershell
ssh root@<YOUR_VPS_IP>
```
 
第一次会提示是否信任主机,输入 `yes` 回车。
 
然后输入 root 密码登录。
 
> 💡 **如果 PowerShell 没有 ssh 命令**(Windows 10 1809 以下):
> 1. 安装 OpenSSH Client:**设置 → 应用 → 可选功能 → 添加功能 → OpenSSH 客户端**
> 2. 或者下载 [PuTTY](https://www.putty.org/) 替代
 
#### 2.2 在 VPS 上下载并安装 gost
 
(以下命令在 SSH 后的 VPS 终端里执行,与 macOS 版完全一致)
 
```bash
cd /root
wget https://github.com/go-gost/gost/releases/download/v3.0.0/gost_3.0.0_linux_amd64.tar.gz
tar -xzf gost_3.0.0_linux_amd64.tar.gz
mv gost /usr/local/bin/
chmod +x /usr/local/bin/gost
gost -V
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
 
⚠️ 把 `YOUR_USER` 和 `YOUR_PASSWORD` 替换为你自定义的强账号密码。
 
#### 2.4 启动并验证
 
```bash
systemctl daemon-reload
systemctl enable gost
systemctl start gost
systemctl status gost
```
 
看到 `active (running)` 即为成功,按 `q` 退出。
 
#### 2.5 放行防火墙端口
 
```bash
ufw allow 1080/tcp 2>/dev/null || true
iptables -I INPUT -p tcp --dport 1080 -j ACCEPT
```
 
#### 2.6 退出 VPS
 
```bash
exit
```
 
回到 Windows PowerShell。
 
---
 
### 第三步:本地 Windows 测试 VPS 连通性
 
PowerShell 自带 curl(实际是 Invoke-WebRequest 的别名,**语法与 Linux curl 不完全一致**)。建议用真正的 curl:
 
#### 方案 A:用 Windows 自带 curl.exe
 
Windows 10 1803+ 自带 curl.exe,**直接用 `curl.exe`(注意 `.exe` 后缀)**:
 
```powershell
curl.exe -x "socks5h://YOUR_USER:YOUR_PASSWORD@<YOUR_VPS_IP>:1080" https://api.ipify.org
```
 
返回 VPS 公网 IP 即为成功。
 
#### 方案 B:用 PowerShell 原生命令
 
```powershell
$proxy = New-Object System.Net.WebProxy "socks5://YOUR_USER:YOUR_PASSWORD@<YOUR_VPS_IP>:1080"
$client = New-Object System.Net.WebClient
$client.Proxy = $proxy
$client.DownloadString("https://api.ipify.org")
```
 
> 💡 PowerShell 原生不太支持 SOCKS5,推荐用 `curl.exe`。
 
---
 
### 第四步:住宅代理白名单配置
 
操作与 macOS 一致,以 [Cliproxy](https://share.cliproxy.com/share/l1bvl4pxt) 为例:
 
1. 浏览器登录 [Cliproxy 控制台](https://dash.cliproxy.com)
2. 进入**白名单管理**
3. 添加 VPS IP
4. 保存(通常即时生效)
> 💡 **提示**:VPS IP 永久不变,白名单**只需加一次**。如果之前加过机场节点 IP,可以删除(机场 IP 会变动,留着没用)。
 
---
 
### 第五步:Clash Verge 配置
 
#### 5.1 必须确认的基础设置
 
打开 Clash Verge,点击左侧「**设置**」:
 
- ✅ **TUN 模式**:开启(打开开关时会再次 UAC 确认)
- ✅ **服务模式**:已安装(显示「**服务已运行**」)
- ✅ **系统代理**:**关闭** ⚠️(Windows 上同样建议关闭,避免命令行工具被强制走代理)
- ✅ **代理模式**:Rule(规则模式)
> 💡 **如果 TUN 模式打不开,提示「需要管理员权限」**:
> 1. 退出 Clash Verge
> 2. 右键 Clash Verge 图标 → **以管理员身份运行**
> 3. 重新打开 Tun 模式
 
#### 5.2 IPv6 设置
 
在 Clash 配置里**关闭 IPv6**(避免 Tun 在 IPv6 路径上不稳定):
 
如果你用的是 Script 覆写(推荐),不需要管 IPv6,因为 Tun 默认只接管 IPv4。
 
如果出现 IPv6 泄露问题,在 Windows 网络适配器里手动关闭:
 
1. **控制面板 → 网络和共享中心 → 更改适配器设置**
2. 右键你的连接(以太网或 WLAN) → **属性**
3. 取消勾选「**Internet 协议版本 6 (TCP/IPv6)**」
4. 确定
#### 5.3 配置 Script 覆写
 
打开 Clash Verge → **订阅**页面 → 点击「**全局扩展脚本**」卡片。
 
按 `Ctrl + A` 全选 → `Delete` 删光 → 粘贴下面这一份:
 
```javascript
function main(config) {
  // 1. VPS 跳板(SOCKS5)
  config.proxies = config.proxies || [];
  config.proxies.unshift({
    name: "US_VPS_Jump",
    type: "socks5",
    server: "YOUR_VPS_IP",          // 替换为你的 VPS IP
    port: 1080,
    username: "YOUR_USER",
    password: "YOUR_PASSWORD",
    udp: true
  });
 
  // 2. 住宅代理(通过 VPS 前置)
  config.proxies.unshift({
    name: "Residential_ISP",
    type: "http",
    server: "RESIDENTIAL_IP",       // 替换为你的住宅代理 IP
    port: 443,
    username: "PROXY_USER",
    password: "PROXY_PASSWORD",
    "dialer-proxy": "US_VPS_Jump"
  });
 
  // 3. 代理组
  config["proxy-groups"] = config["proxy-groups"] || [];
  config["proxy-groups"].unshift({
    name: "社媒固定IP",
    type: "select",
    proxies: ["Residential_ISP"]
  });
 
  // 4. 规则
  const fixedIPRules = [
    "DOMAIN-SUFFIX,twitter.com,社媒固定IP",
    "DOMAIN-SUFFIX,x.com,社媒固定IP",
    "DOMAIN-KEYWORD,twitter,社媒固定IP",
    "DOMAIN-SUFFIX,twimg.com,社媒固定IP",
    "DOMAIN-SUFFIX,t.co,社媒固定IP",
    "DOMAIN-SUFFIX,instagram.com,社媒固定IP",
    "DOMAIN-SUFFIX,cdninstagram.com,社媒固定IP",
    "DOMAIN-SUFFIX,facebook.com,社媒固定IP",
    "DOMAIN-SUFFIX,fbcdn.net,社媒固定IP",
    "DOMAIN-SUFFIX,fb.com,社媒固定IP",
    "DOMAIN-SUFFIX,tiktok.com,社媒固定IP",
    "DOMAIN-SUFFIX,tiktokcdn.com,社媒固定IP",
    "DOMAIN-SUFFIX,tiktokv.com,社媒固定IP",
    "DOMAIN-SUFFIX,claude.ai,社媒固定IP",
    "DOMAIN-SUFFIX,claude.com,社媒固定IP",
    "DOMAIN-SUFFIX,anthropic.com,社媒固定IP",
    "DOMAIN-KEYWORD,anthropic,社媒固定IP",
    "DOMAIN-KEYWORD,claude,社媒固定IP",
    "DOMAIN-SUFFIX,openai.com,社媒固定IP",
    "DOMAIN-SUFFIX,chatgpt.com,社媒固定IP",
    "DOMAIN-SUFFIX,oaistatic.com,社媒固定IP",
    "DOMAIN-SUFFIX,oaiusercontent.com,社媒固定IP",
    "DOMAIN-KEYWORD,openai,社媒固定IP",
    "DOMAIN-KEYWORD,chatgpt,社媒固定IP",
    "DOMAIN-SUFFIX,gemini.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,bard.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,aistudio.google.com,社媒固定IP",
    "DOMAIN-SUFFIX,generativelanguage.googleapis.com,社媒固定IP",
    "DOMAIN-SUFFIX,challenges.cloudflare.com,社媒固定IP",
    "DOMAIN-SUFFIX,ipinfo.io,社媒固定IP",
    "DOMAIN-SUFFIX,ifconfig.me,社媒固定IP",
    "DOMAIN-SUFFIX,ipify.org,社媒固定IP"
  ];
  config.rules = [...fixedIPRules, ...(config.rules || [])];
 
  return config;
}
```
 
**保存(`Ctrl + S`)** → 回订阅页面 → 点击订阅卡片右下角的 **C 形刷新图标**。
 
---
 
### 第六步:验证成功
 
#### 方法 1:浏览器验证
 
新开无痕窗口(`Ctrl + Shift + N`),访问:
 
```
https://ipinfo.io/ip
```
 
应显示住宅代理的 IP。
 
#### 方法 2:Clash 连接页面
 
左侧「连接」页面,访问 ipinfo.io 后会出现两条连接,链路应显示:
 
- `ipinfo.io:443` → `社媒固定IP / Residential_ISP`
- `<VPS_IP>:443` → `US_VPS_Jump`
#### 方法 3:PowerShell 命令行验证
 
```powershell
curl.exe https://ipinfo.io/ip
```
 
应返回住宅代理 IP。
 
---
 
## Windows 特有问题
 
### Q1: TUN 模式开关灰色无法点击
 
**原因**:Service Mode 没装好。
 
**解决**:
 
1. 设置 → 服务模式 → 卸载服务 → 重新安装
2. 安装时 UAC 弹窗一定要点「是」
3. 仍不行:右键 Clash Verge → 以管理员身份运行
---
 
### Q2: 系统代理关了,但浏览器还是走代理
 
Windows 浏览器除了系统代理,Edge/Chrome 也读 IE 设置的代理。强制刷新:
 
```powershell
# 清除 IE/Edge 的代理设置
netsh winhttp reset proxy
```
 
或者去 **设置 → 网络和 Internet → 代理 → 关闭所有手动代理**。
 
---
 
### Q3: PowerShell 命令行工具(Python、git、npm)被强制走代理
 
**Windows 系统代理在注册表里**,Python 等工具会读取:
 
```powershell
# 临时清除当前 PowerShell 会话的代理变量
$env:HTTP_PROXY = $null
$env:HTTPS_PROXY = $null
$env:ALL_PROXY = $null
 
# 验证
Get-ChildItem env: | Where-Object { $_.Name -like "*PROXY*" }
```
 
如果想永久不让 Python 走系统代理,在脚本里加:
 
```python
import requests
s = requests.Session()
s.trust_env = False  # 忽略系统代理
```
 
或者**关闭 Clash Verge 的「系统代理」开关**(Tun 模式开着即可)。
 
---
 
### Q4: DNS 缓存导致访问异常
 
修改了 Clash 规则后,Windows DNS 缓存还是旧的(指向 fake-ip 198.18.0.x)。清理:
 
```powershell
# 以管理员身份运行 PowerShell
ipconfig /flushdns
 
# 重启 Clash 内核(Clash Verge → 设置 → 重启内核)
```
 
---
 
### Q5: 环境变量永久清理
 
如果之前在 Windows 系统环境变量里设过 `HTTPS_PROXY`,需要去:
 
1. **此电脑** 右键 → **属性** → **高级系统设置**
2. **环境变量**
3. 找到 `HTTPS_PROXY` / `HTTP_PROXY`,删除
4. 重启所有终端、IDE 让变量生效
---
 
### Q6: 防火墙阻止 Clash
 
Windows Defender 防火墙可能拦截 Clash 的 Tun 网络。第一次开 Tun 时,如果有弹窗:
 
- **允许** → 公用网络 + 专用网络都勾选
- **拒绝** → Clash 无法工作
如果不小心拒绝了,重置:
 
1. **控制面板 → Windows Defender 防火墙 → 允许应用**
2. 找到 Clash Verge,确保两列都打钩
3. 找不到的话点「**允许其他应用**」加进去
---
 
### Q7: 360/腾讯电脑管家拦截 Clash
 
国产安全软件经常误报 Clash 内核(mihomo.exe)是病毒。需要:
 
1. 把 Clash Verge 的安装目录加到信任列表
2. 或者临时关闭防护
否则 mihomo.exe 会被隔离,Clash 启动就崩溃。
 
---
 
## 验证命令速查
 
| 用途 | macOS 命令 | Windows 命令 |
|------|-----------|-------------|
| 查看出口 IP | `curl https://ipinfo.io/ip` | `curl.exe https://ipinfo.io/ip` |
| 查 DNS 解析 | `nslookup example.com` | `nslookup example.com` |
| 清 DNS 缓存 | `sudo dscacheutil -flushcache` | `ipconfig /flushdns` |
| 看代理变量 | `env \| grep -i proxy` | `Get-ChildItem env: \| Where-Object { $_.Name -like "*PROXY*" }` |
| 清代理变量(临时) | `unset HTTP_PROXY HTTPS_PROXY` | `$env:HTTP_PROXY=$null; $env:HTTPS_PROXY=$null` |
| 看网卡(找 utun/Tun) | `ifconfig \| grep -A 3 utun` | `ipconfig /all` |
| 测试 SSH | `ssh root@IP` | `ssh root@IP`(需 OpenSSH 客户端) |
 
---
 
## 常用 PowerShell 一键诊断脚本
 
把下面这段保存为 `check.ps1`,需要诊断时双击运行:
 
```powershell
Write-Host "===== Clash 状态诊断 =====" -ForegroundColor Cyan
 
Write-Host ""
Write-Host "[1/4] 当前出口 IP:" -ForegroundColor Yellow
curl.exe -s https://ipinfo.io/ip
Write-Host ""
 
Write-Host "[2/4] 系统代理变量:" -ForegroundColor Yellow
Get-ChildItem env: | Where-Object { $_.Name -like "*PROXY*" } | Format-Table -AutoSize
 
Write-Host "[3/4] DNS 解析 (eastmoney 应该是真实国内 IP):" -ForegroundColor Yellow
nslookup eastmoney.com 2>$null | Select-String "Address"
Write-Host ""
 
Write-Host "[4/4] DNS 解析 (twitter 应该是 198.18.x fake-ip):" -ForegroundColor Yellow
nslookup twitter.com 2>$null | Select-String "Address"
Write-Host ""
 
Write-Host "===== 诊断完成 =====" -ForegroundColor Green
pause
```
 
运行方法:
1. 右键 PowerShell 图标 → 以管理员身份运行
2. `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`(允许执行脚本)
3. 切到脚本目录,执行 `.\check.ps1`
---
 
## 路由器方案
 
如果你想让全家 Windows 设备都用固定 IP,可以参考主 README 的[路由器方案](../README.md#在路由器上也能这样配吗),原理一致。
 
---
 
## 推荐服务商
 
以下是我经过对比后选择自用的服务,通过我的链接注册可以获得优惠/返利,感谢支持 🙏:
 
| 服务 | 推荐 | 链接 | 备注 |
|------|------|------|------|
| 🛰️ 机场(翻墙) | WgetCloud 全球加速 | [注册](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf) | Trojan 协议,IEPL 专线 |
| 🖥️ VPS(跳板) | Racknerd | [注册](https://my.racknerd.com/aff.php?aff=19430) | 年付 $10-15 特价 |
| 🏠 美国住宅 IP | Cliproxy 静态长效 ISP | [注册](https://share.cliproxy.com/share/l1bvl4pxt) | $3.8 起/月 ⭐ |
 
> 通过推广链接注册不会给你带来任何额外费用,反而会让你享受到新用户优惠或返利。如不想走推广链接,可直接搜索访问服务商官网。
 
### 成本估算
 
| 项目 | 费用 | 频率 | 年化成本 |
|------|------|------|----------|
| [WgetCloud 机场](https://invite.wgetcloud.ltd/auth/register?code=4YxbYf) | ~$10-15 | 月 | ~$120-180 |
| [Racknerd VPS](https://my.racknerd.com/aff.php?aff=19430) | **$10-15** | **年** | **~$10-15** ⭐ |
| [Cliproxy 住宅代理](https://share.cliproxy.com/share/l1bvl4pxt) | $3.8+ | 月 | ~$45+ |
| **总计** | | | **~$175-240 / 年** |
 
---
 
## 反馈与贡献
 
文档有问题或想补充?欢迎在主仓库提 [Issue](https://github.com/caseyjie-create/social-fixed-ip-guide/issues)。
 
返回 [主 README](../README.md)
