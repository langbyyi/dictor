# 实战精选 · 即开即用

从全库挑出 **38 个真正能打的**,按场景分 4 类,总计 ~17 万行。
打开任何工具(hydra/ffuf/sqlmap/burp)直接喂文件即可。

## 目录速查

### 01-密码TOP/(6 个) ~10k 行
场景:SSH/RDP/MySQL/Web 登录爆破。

| 文件 | 行数 | 用途 |
|---|---|---|
| TOP1000-中文弱口令.txt | 1k | **国内首选** |
| TOP1000-Web后台管理员.txt | 1k | Web 后台专用 |
| TOP2000-WiFi默认.txt | 2k | WiFi 爆破 |
| TOP6000-中文加强版.txt | 6k | 1000 跑完再升级 |
| Windows-NTLM哈希爆破.txt | 565 | NTLM hash 离线爆破 |
| 设备默认口令.txt | 280 | 路由器/摄像头/IoT |

**推荐顺序**:TOP1000中文 → TOP6000中文加强 → NTLM/设备默认

### 02-目录爆破/(16 个) ~113k 行
场景:dirsearch/ffuf/dirb/gobuster。

| 文件 | 行数 | 用途 |
|---|---|---|
| 敏感文件.txt | 4.7k | **优先跑** |
| API接口路径.txt | 1.7k | API 发现 |
| Robots禁用-TOP1000.txt | 1k | robots 提取 |
| 后台路径-1.2万.txt | 12k | 找后台 |
| 备份文件.txt | 7.4k | .zip/.bak/.tar.gz |
| raft-large目录(5.6万).txt | 56k | **兜底大字典** |
| SpringBoot端点.txt | 389 | /actuator/* |
| Oracle路径.txt | 1k | 中间件代表 |
| WordPress路径.txt | 7.7k | 常见产品 |
| phpMyAdmin路径.txt | 2.7k | 常见产品 |
| Editor路径.txt | 4.5k | 编辑器 |
| PHP路径.txt | 3.1k | 技术栈 |
| JSP路径.txt | 4.2k | 技术栈 |
| ASP路径.txt | 2.6k | 技术栈 |
| ASPX路径.txt | 1k | 技术栈 |
| 扩展名-raft.txt | 2.4k | 后缀枚举 |

**推荐**:敏感文件 → 后台路径 → 备份文件 → raft-large 兜底

### 03-用户名爆破/(6 个) ~30k 行
场景:hydra -L / burp intruder。

| 文件 | 行数 | 用途 |
|---|---|---|
| 通用-2000.txt | 2k | **通用首选** |
| 中文姓名-1300.txt | 1.3k | 中文全拼/简写 |
| 中文姓名组合-2000.txt | 2k | 姓+名 组合 |
| Linux用户-2800.txt | 2.8k | /etc/passwd 风格 |
| 手机号字典-3600.txt | 3.6k | 国内手机号 |
| usernames-1.9万.txt | 18k | 兜底大字典 |

**推荐**:通用-2000 → 中文姓名 → Linux/手机号 → usernames 兜底

### 04-WebPayload/(10 个) ~16k 行
场景:sqlmap / burp intruder / XSStrike / ffuf fuzz。

| 文件 | 行数 | 用途 |
|---|---|---|
| SQL注入-Generic.txt | 266 | 通用 SQLi |
| XSS-JHaddix.txt | 107 | 经典 JHaddix 集 |
| XSS-easy-1850.txt | 1.8k | 大全 XSS |
| 上传-all_fuzz.txt | 2.7k | 文件上传 fuzz(全栈) |
| LFI-JHaddix.txt | 865 | 文件包含 |
| RCE-WAF绕过.txt | 148 | RCE WAF bypass |
| SSRF.txt | 528 | SSRF payload |
| UserAgent绕过.txt | 2.4k | UA 鉴权绕过 |
| Authorization绕过.txt | 1.8k | Auth header 绕过 |
| 参数枚举-5600.txt | 5.6k | 隐藏参数发现 |

## 用法示例

```bash
# SSH 爆破
hydra -L _实战精选/03-用户名爆破/通用-2000.txt \
      -P _实战精选/01-密码TOP/TOP1000-中文弱口令.txt \
      ssh://1.2.3.4

# 目录扫描
ffuf -u https://target/FUZZ \
     -w _实战精选/02-目录爆破/敏感文件.txt

# SQLi 注入
sqlmap -u "https://target/?id=1" --batch \
       --payload-file _实战精选/04-WebPayload/SQL注入-Generic.txt

# Burp Intruder 直接加载 02/03/04 任意字典
```

## 不在这里的怎么办?

完整扩展库在父目录:
- `passwords/` — 服务口令、扩展密码字典(100w+ 行)
- `directories/` — 各产品/技术栈/CMS 漏洞路径全集
- `web-specific/` — 完整 Payload 库 + 模糊测试集

需要更深覆盖时去那里取。

最后更新:2026-06-18(38 个精选)
