---
layout: category-index
title: How service.gov.uk domain names are managed
category: domain-names
type: category-index
audience:
  primary: service-managers, web-ops, tech-archs
  secondary:
status: draft
phases:
  - discovery
  - alpha
  - beta
  - live
breadcrumbs:
  -
    title: Home
    url: /service-manual
  -
    title: Where services live on the web
    url: /service-manual/domain-names
---

## service.gov.uk 的域名是如何管理的

一旦[一項服務的域名定案之後](/service-manual/domain-names/setting-up.html)，GDS Infrastructure Team 會在
service.gov.uk 之下配給一個域名、並將這個之網域的管理權限授權給這項服務的經營團隊。這經營團隊要提供自己
準備的域名伺服器的資訊、而 GDS 會將 {service-name}.service.gov.uk 的管理權援權給這些域名伺服器。
這時，這服務的經營團隊將能夠進一步管理 (這個網域下) 諸如哪個域名指向哪個伺服器之類的詳細設定。

## 這跟 direct.gov.uk 域名的管理方式有何不同？

directogov.uk 這網域是由 DirectGov Service Desk 直接管理 (而交由 GDS 承接)。
所有網域都由 DirectGov 掌管，而且每個子網域不會有自己的 DNS 伺服器。

也就是說，各項服務得要將自己的域名和網頁伺服器的 IP 位址等細節交給 DirectGov、讓 DirectGov 去新增所需
的 A records 和 CNAME records。DirectGov Service Desk 也負責了所有 DNS 設定的變動。

而 service.gov.uk 網域的新模式要求你得自行找 DNS 伺服器來回應對 {something}.{servicename}.service.gov.uk
的查詢請求。你不一定得要自己再另外架設主機來提供 DNS 伺服器，還有別的方法：

1. 有些 GCloud 上的服務供應商會提供 DNS 代管服務、讓你可以透過他們的 web 介面來管理你託管給他們的 DNS records。
2. 許多主機代管供應商也會提供 DNS services 給客戶使用。
3. 再找不到其他方法、或是對於規模較大的服務，你也可以要求供應商以任何他們覺得合理的方式來提供 DNS services
   (包括前兩種方法)

## 我們為何這麼做？

It is likely that as you build and iterate your service you will need to make a number of changes to its
configuration. You might introduce load balancers or content delivery networks, you may move hosting
providers, or your provider might need to change the IP addresses that your servers are assigned. In any
of those cases it is important that your team is able to quickly respond to the situation and make any
relevant changes with as few intermediaries as possible. By delegating control GDS ensures that control
is in the hands of the service team and not blocked by a central authority.

在你建立和反覆改進你的服務時，很可能會需要經常變動域名設定。例如：你可能會要在服務架構中引進 load balancers
或 CDN、你可能會改換代管服務供應商、或你的供應商可能需要改變你伺服器 IP 位置。在這些狀況下你的團隊要能快速地
調整 DNS 設定以回應這些變動、經手的中間人越少越好。透過授權，GDS 確保域名的管理權是掌握在服務的經營團隊自己手裡、
不是受一個集權的中央所阻擋。
