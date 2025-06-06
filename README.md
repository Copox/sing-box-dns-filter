# 一个简单的 Sing-Box DNS 过滤器

## 简介

简陋的 Sing-Box DNS 过滤器实现，个人使用。

## 引用过滤器

### AdGuard DNS 过滤器

AdGuard DNS 过滤器包含多个过滤器，主要包括：

- **AdGuard 基础过滤器**

- **社交媒体过滤器**

- **防跟踪保护过滤器**

- **移动广告过滤器**

- **EasyList 和 EasyPrivacy**

该过滤器经过简化，确保与 DNS 级别的广告拦截兼容。AdGuard DNS 服务器使用此过滤器有效拦截广告和跟踪器。

[查看规则](https://github.com/AdguardTeam/AdGuardSDNSFilter)

### OISD 过滤器

OISD 阻止列表旨在防止设备连接到不必要或有害的域。其特点包括：

- **减少广告**

- **降低恶意软件风险**

- **提升隐私保护**

OISD 列表优先考虑功能性，适合在家庭、工作等场合使用，用户反馈普遍良好。

[查看规则](https://oisd.nl)

## 添加规则

[Fork](https://github.com/tmby/sing-box-dns-filter/fork) 后在 `run.py` 中自行增减，actions 会每天上传一次编译产物。

## 使用方法

以下是配置示例：

### 1.10.0-alpha.25+

```json
{
  "dns": {
    "servers": [
      {
        "tag": "dns_block",
        "address": "rcode://success"
      }
    ],
    "rules": [
      {
        "rule_set": "geosite-dnsblock",
        "server": "dns_block"
      }
    ]
  },
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "geosite-dnsblock",
        "format": "binary",
        "url": "https://github.com/tmby/sing-box-dns-filter/raw/refs/heads/main/geosite-dnsblock.srs",
        "download_detour": "proxy"
      }
    ]
  }
}
```

### 1.11.0-alpha.7+

```json
{
  "dns": {
    "rules": [
      {
        "rule_set": "geosite-dnsblock",
        "action": "reject"
      }
    ]
  },
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "geosite-dnsblock",
        "format": "binary",
        "url": "https://github.com/tmby/sing-box-dns-filter/raw/refs/heads/main/geosite-dnsblock.srs",
        "download_detour": "proxy"
      }
    ]
  }
}
```

通过上述配置，您可以在 Sing-Box 中实现基本的 DNS 过滤功能，提升网络安全与隐私保护。
