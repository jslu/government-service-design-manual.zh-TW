---
layout: category-index
title: HTTPS
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

## HTTPS

許多服務會需要從使用者那裡取得個人資料。確保惡意的第三方無法在這些資料正經由網路傳送的過程中加以攔劫，是非常重要的。

因此，所有經由 service.gov.uk 網域來存取的服務 (包含各種 API) *必須* 只能透過安全的連線。這對於 web-based 的服務而言，
就是只能使用 HTTPS 連線 (這些安全連線是建立在一種縮寫為 TLS 或 SSL 的協定之上，所以我們也常常用這兩個縮寫去稱呼之)。
所有服務在任何情況下都不能接受 HTTP 連線。

### Strict Transport Security

Strict Transport Security 或 [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) 是一個 HTTPS
協定的延伸協定，用來讓瀏覽器知道 他們應該要多做些程序去驗證連線的安全性：他們必須假設在一定時間內 所有跟伺服器的運線
都得是經由 HTTPS、不能有安全連線與不安全連線混用的頁面內容 (就是頁面中有些內容是用 HTTPS 送出來的、有些是用 HTTP 送出來的)
這對連線安全的可信度提供了額外的保障。

一旦一個服務的管理者確認了他們的 HTTPS 設置可以順利運作，他們 *應該* 在 production 網域 (如 www., admin. 和 assets.) 上
以設置一個如下的 HTTP response header 來啟用 HSTS。

    Strict-Transport-Security: max-age=1209600, includeSubDomains;

代表一個 14 天內只用 HTTPS 連線的承諾。一旦服務管理者確信 HSTS 設定正確，你 *應該* 將這承諾延長至月或年：

    Strict-Transport-Security: max-age=31536000, includeSubDomains;

### SSL 憑證的驗證

為了在 HTTPS 上提供你的服務，你得從受過公證的供應商購買一個或多個憑證。SSL 供應商大不相同，但不管你選哪一家，
你都得向供應商證明你的網域擁有權。

常用的驗證方式 (依偏好順序) 是：

1. 在你的網站上建立一個檔案、裡面有供應商所給的特別碼
2. 以供應商所給的碼 建立一個特別的 DNS record
3. 寄一封 email 給 service.gov.uk 這網域的擁有者

最不建議的寄 email 給網域擁有者的方式，必須得要 GDS Infrastructure Team 有看到認證信並回覆。如果真有需要這麼做，
那麼就先以你自己的信箱寄個 email 到你要用來做驗證的信箱去、提醒說你的服務需要做個 SSL 驗證。

你的要求要送到 hostmaster@digital.cabinet-office.gov.uk，且要提到說有個 SSL 認證信會寄給他們。如果你順便把要保護的網域
和 SSL 憑證供應商的名字都一起順便在信中告知，那會更有幫助。

Infrastructure team 無法確認寄到 @service.gov.uk 信箱的需求的真偽。
