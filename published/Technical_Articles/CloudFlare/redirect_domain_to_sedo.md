---
id: cf42f
title: 如何把 CloudFlare 的域名跳转到 Sedo 的域名售卖地址（或者任意地址）？
permalink: /how-to-redirect-CloudFlare-domain-name-to-sedo-domain-name-sales-address
date: 2025-05-16 11:00:24
thumbnail: example_1.jpg
tags: [Domain, CloudFlare]
---

做为域名投资者，希望自己的域名能被潜在的买家关注到。买家可能通过在浏览器中直接输入域名的方式来测试域名。这时，跳转到 Sedo 或其它域名网站的售卖链接是很好的。

### 第一步，创建三条 DNS A 记录

Click `CloudFlare -> Your Domain -> DNS -> Records -> Add record`.

1. Record 1
    - Record type: A
    - Name: @
    - IPv4 address: 192.0.2.1

2. Record 2
    - Record type: A
    - Name: www
    - IPv4 address: 192.0.2.1

3. Record 3
   - Record type: A
   - Name: *
   - IPv4 address: 192.0.2.1

### 第二步，创建一条 `Page Rule`

- 点击 `Rules -> Page Rules -> Create Page Rule`.
- `URL`填写`*yourdomain.com*`. (替换掉`yourdomain.com`为实际域名)。
- `Pick a Setting (required)`填写`Forwarding URL`, `Select status code (required)`填写`301`.
- `Enter destination URL (required)`填写`https://sedo.com/search/details/?domain=yourdomain.com`
- 点击 `Save and Deploy Page Rule`.
- 在弹出的`This rule may not apply to your traffic`页面，选中`Ignore and deploy rule anyway`，然后点击`Deploy Rule`.

### 第三步，测试效果

在浏览器中输入:

- https://yourdomain.com
- https://www.yourdomain.com
- https://abc.yourdomain.com
- https://yourdomain.com/abcd
- http://yourdomain.com
- http://www.yourdomain.com
- http://abcd.yourdomain.com
- http://yourdomain.com/

如果全部都能跳转正确，说明配置成功。
