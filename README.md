<div align="center">

# 🛡️ Slapp VPN — Routing

**Готовые конфигурации маршрутизации для [Happ](https://happ.su)**

> Точечная маршрутизация без лишнего: только нужные сервисы через прокси, всё остальное напрямую

**Target:** 🇷🇺 Россия

</div>

---

## 📦 Доступные конфиги

### 🔹 Одиночные профили

| # | Название | Описание | Ссылка | 
|---|----------|----------|----------|
| 1 | **Full Pack** | Все нужное | [JSON](https://raw.githubusercontent.com/pxdxx/Routing/refs/heads/main/Happ-Routing/Full%20Pack/Full.json?token=GHSAT0AAAAAAD2K4GPGK67D6HHGP6WORX6U2PJEA7Q) |

### 🔹 Одиночные профили

| # | Название | Описание | Ссылка | 
|---|----------|----------|----------|
| 1 | **Только Telegram** | Только Telegram через прокси |
| 2 | **Только YouTube** | Только YouTube через прокси |
| 3 | **Только WhatsApp** | Только WhatsApp через прокси |
| 4 | **Только TikTok** | Только TikTok через прокси |

### 🔸 Комбинированные профили

| # | Название | Сервисы |
|---|----------|---------|
| 5 | **TG + WA + TT + YT** | Telegram + WhatsApp + TikTok + YouTube |
| 6 | **TG + TT + YT** | Telegram + TikTok + YouTube |
| 7 | **TG + YT** | Telegram + YouTube |
| 8 | **TG + WA** | Telegram + WhatsApp |
| 9 | **WA + YT** | WhatsApp + YouTube |
| 10 | **TT + YT** | TikTok + YouTube |
| 11 | **TG + WA + TT** | Telegram + WhatsApp + TikTok |

---

## 🗺️ Принцип маршрутизации

Все конфиги используют порядок правил `block → proxy → direct`.

### 🟢 DIRECT (напрямую)

Следующее всегда идёт напрямую, без прокси:

- 🇷🇺 Российские домены (`geosite:category-ru`, `geosite:whitelist`)
- 🔒 Приватные сети (`geosite:private`, `geoip:private`)
- 🖥️ Microsoft, Apple — корректная работа устройств
- 🎮 Игровые платформы: Steam, Epic Games, Riot, Escape from Tarkov
- 📺 Twitch, Pinterest, Faceit

### 🔵 PROXY (через VPN)

Зависит от профиля — только выбранные сервисы:

| Сервис | Домены | IP-диапазоны |
|--------|--------|--------------|
| **Telegram** | `geosite:telegram` | `geoip:telegram` |
| **YouTube** | `geosite:youtube`, `googlevideo.com`, `ytimg.com`, `youtu.be` | `geoip:google` |
| **WhatsApp** | `geosite:whatsapp`, `whatsapp.com`, `whatsapp.net`, `wa.me` | `geoip:facebook` |
| **TikTok** | `geosite:tiktok`, `tiktok.com`, `tiktokcdn.com`, `byteoversea.com` | — |

### 🔴 BLOCK (блокировка)

- 🚫 Телеметрия Windows (`geosite:win-spy`)
- 🚫 Торренты (`geosite:torrent`)
- 🚫 Реклама (`geosite:category-ads`)

---

## 🌐 DNS

| Назначение | Сервер | Адрес |
|------------|--------|-------|
| 🏠 Domestic (для прямого трафика) | Google Public DNS | `77.88.8.8` (DoH) |
| 🌍 Remote (для проксируемого трафика) | Google Public DNS | `8.8.8.8` (DoH) |

---

## ⚙️ Параметры конфигурации

Все конфиги имеют следующие базовые настройки:

```
GlobalProxy:     false        — только выбранные сервисы через прокси
RouteOrder:      block-proxy-direct
DomainStrategy:  IPIfNonMatch — резолвинг IP если домен не совпал с правилами
FakeDNS:         false
UseChunkFiles:   true
```

GeoIP и Geosite базы:
```
GeoIP:    https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@.../geoip.dat
Geosite:  https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@.../geosite.dat
```

---

## 📋 Конфиги

<details>
<summary><b>1. Только Telegram</b></summary>

```json
{
  "Name": "RoscomVPN — Только Telegram",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": ["geosite:telegram"],
  "ProxyIp": ["geoip:telegram"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>2. Только YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — Только YouTube",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:youtube", "domain:googlevideo.com",
    "domain:ytimg.com", "domain:ggpht.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>3. Только WhatsApp</b></summary>

```json
{
  "Name": "RoscomVPN — Только WhatsApp",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:whatsapp", "domain:whatsapp.com",
    "domain:whatsapp.net", "domain:wa.me"
  ],
  "ProxyIp": ["geoip:facebook"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>4. Только TikTok</b></summary>

```json
{
  "Name": "RoscomVPN — Только TikTok",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:tiktok", "domain:tiktok.com", "domain:tiktokcdn.com",
    "domain:tiktokv.com", "domain:muscdn.com", "domain:byteoversea.com"
  ],
  "ProxyIp": [],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>5. Telegram + WhatsApp + TikTok + YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — TG + WA + TT + YT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:telegram",
    "geosite:whatsapp", "domain:whatsapp.com", "domain:whatsapp.net", "domain:wa.me",
    "geosite:tiktok", "domain:tiktok.com", "domain:tiktokcdn.com",
    "domain:tiktokv.com", "domain:muscdn.com", "domain:byteoversea.com",
    "geosite:youtube", "domain:googlevideo.com", "domain:ytimg.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:telegram", "geoip:facebook", "geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>6. Telegram + TikTok + YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — TG + TT + YT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:telegram",
    "geosite:tiktok", "domain:tiktok.com", "domain:tiktokcdn.com",
    "domain:tiktokv.com", "domain:muscdn.com", "domain:byteoversea.com",
    "geosite:youtube", "domain:googlevideo.com", "domain:ytimg.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:telegram", "geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>7. Telegram + YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — TG + YT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:telegram",
    "geosite:youtube", "domain:googlevideo.com", "domain:ytimg.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:telegram", "geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>8. Telegram + WhatsApp</b></summary>

```json
{
  "Name": "RoscomVPN — TG + WA",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:telegram",
    "geosite:whatsapp", "domain:whatsapp.com", "domain:whatsapp.net", "domain:wa.me"
  ],
  "ProxyIp": ["geoip:telegram", "geoip:facebook"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>9. WhatsApp + YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — WA + YT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:whatsapp", "domain:whatsapp.com", "domain:whatsapp.net", "domain:wa.me",
    "geosite:youtube", "domain:googlevideo.com", "domain:ytimg.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:facebook", "geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>10. TikTok + YouTube</b></summary>

```json
{
  "Name": "RoscomVPN — TT + YT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:tiktok", "domain:tiktok.com", "domain:tiktokcdn.com",
    "domain:tiktokv.com", "domain:muscdn.com", "domain:byteoversea.com",
    "geosite:youtube", "domain:googlevideo.com", "domain:ytimg.com", "domain:youtu.be"
  ],
  "ProxyIp": ["geoip:google"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

<details>
<summary><b>11. Telegram + WhatsApp + TikTok</b></summary>

```json
{
  "Name": "RoscomVPN — TG + WA + TT",
  "GlobalProxy": "false",
  "UseChunkFiles": "true",
  "RemoteDNSType": "DoH",
  "RemoteDNSDomain": "https://8.8.8.8/dns-query",
  "RemoteDNSIP": "8.8.8.8",
  "DomesticDNSType": "DoH",
  "DomesticDNSDomain": "https://77.88.8.8/dns-query",
  "DomesticDNSIP": "77.88.8.8",
  "Geoipurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip@202604220533/release/geoip.dat",
  "Geositeurl": "https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite@202604152235/release/geosite.dat",
  "LastUpdated": "1776836041",
  "DnsHosts": {
    "lkfl2.nalog.ru": "213.24.64.175",
    "lknpd.nalog.ru": "213.24.64.181"
  },
  "RouteOrder": "block-proxy-direct",
  "DirectSites": [
    "geosite:private", "geosite:category-ru", "geosite:whitelist",
    "geosite:microsoft", "geosite:apple", "geosite:epicgames",
    "geosite:riot", "geosite:escapefromtarkov", "geosite:steam",
    "geosite:twitch", "geosite:pinterest", "geosite:faceit"
  ],
  "DirectIp": ["geoip:private", "geoip:direct"],
  "ProxySites": [
    "geosite:telegram",
    "geosite:whatsapp", "domain:whatsapp.com", "domain:whatsapp.net", "domain:wa.me",
    "geosite:tiktok", "domain:tiktok.com", "domain:tiktokcdn.com",
    "domain:tiktokv.com", "domain:muscdn.com", "domain:byteoversea.com"
  ],
  "ProxyIp": ["geoip:telegram", "geoip:facebook"],
  "BlockSites": ["geosite:win-spy", "geosite:torrent", "geosite:category-ads"],
  "BlockIp": [],
  "DomainStrategy": "IPIfNonMatch",
  "FakeDNS": "false"
}
```

</details>

---

## 📱 Совместимые приложения

| Приложение | Платформа | Поддержка |
|------------|-----------|-----------|
| [Happ](https://happ.su) | iOS / Android | ✅ |
| [INCY](https://incy.cc) | iOS / Android | ✅ |

---

<div align="center">

> Ставь ⭐ и не пропускай обновления

###### Сделано с ❤️ к свободному интернету

</div>
