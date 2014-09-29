---
layout: detailed-guidance
title: Operating a service.gov.uk subdomain
subtitle: Consistency across central government digital services
category: operations
type: guide
audience:
  primary: tech-archs
  secondary: service-managers, web-ops
status: draft
breadcrumbs:
  -
    title: Home
    url: /service-manual
  -
    title: Operations
    url: /service-manual/operations
---

政府提供一些不同的數位服務給公民。雖然在使用歷程中的開始和結束會是在 GOV.UK 上，這服務本身通常會架設在其他地方，也因此會需要不同的網域名稱。本頁說明 `service.gov.uk` 之子網域在架設數位服務方面的用途。

> 注意：這份文件是寫來做為一份 '標準'，因此如 *必須*、*應該*、*可以* 和 *不得* 等用詞的意義是依照 [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) 的定義。

## 單一進入點

英國政府所提供的每個數位服務在網路上 *必須* 只有一個廣為人知的位置，當使用者想要使用該服務時可以去那裡找到。那廣為人知的位置會是在 GOV.UK 上相關的開始頁面 -- 例如， DVLA 的 tax disc 服務就是在 [https://www.gov.uk/tax-disc](https://www.gov.uk/tax-disc)。

服務的管理者 *不得* 將那個 GOV.UK 上開始頁面之外的其他網址 當成 該服務的開始點 來對外宣傳。這會被印在宣傳單張上、用在 email 簽名檔和電視廣告上。

一個服務的開始頁網址，會由 GDS 經過 與服務管理者討論 和 對使用者行為、搜尋引擎推薦等相關資料的分析之後 再行配置。

## 設立一個網域

一個服務的往覆溝通的部份 -- 也就是那些當使用者與該服務互動時所動態產生出來的頁面 -- 通常不會是架設在 `www.gov.uk` 這網域下。這意味著每個服務往覆溝通的部份需要它自己的網域名稱。

> 注意：這原則不適用於 GDS 與其他政府部門所合作開發和維護的那組 GOV.UK 上名為 'smart answers' 的互動工具。

對於在 2013 年四月一日之後上線的所有新的數位政府服務，GDS 會設立一個形式為 `servicename.service.gov.uk` 的域名 (其中 "servicename" 是一個相關部門/單位與 Government Digital Service 取得共識而定的一個對此服務的英文簡述)。這會為所有數位服務的中央政府域名帶來一致性，並去除了對部門子網域的依賴 (這樣的依賴會受到政府組織架構改變的影響) 和對現已退役之 DirectGov 和 BusinessLink 等線上品牌的依賴。

取得一個 `service.gov.uk` 子域名的程序 可由兩種不同的情境開始：一個是當服務管理者向 Government Digital Service 的產品經理索取一個 GOV.UK 上的開始頁面時 (對於在 2013 年三月十三日時正在進行的服務而言)、另一個是當服務管理者經由填寫 GOV.UK 服務台的政府聯繫表單去要求建立一個子域名時 (這是對 2013 年三月十三日之後開始開發的服務)。 `service.gov.uk` 的子域名 *應該* 要描述該服務 (例如 `lastingpowerofattorney.service.gov.uk`) 且不應該包含該服務所屬的部門或單位的名稱 (例如 `ministryofmagicwandregistration.service.gov.uk`)。

The service-owning dept/agency will be given delegated authority to manage the domain and its subdomains, although in some cases this work will be carried out by third party suppliers.
服務的所屬部門/單位將會被授予權限去管理該網域或其子網域，雖然有些情況下這些會交由第三方供應商來執行。

## 子網域

關於一個服務管理者在拿到 `servicename.service.gov.uk` 的管控權之後該建立什麼子網域，這一節列出一些指引。

**看得到的子網域的最大數量**

與使用者直接面對的線上即時服務 *應該* 最多以三個使用者看得到的 `servicename.service.gov.uk` 子網域來運作：

* `www.servicename.service.gov.uk` 是給構成你服務的那些直接面對公眾的即時動態產生的網頁。
* `assets.servicename.service.gov.uk` 是用來放例如靜態圖檔、共享的 JavaScript 等服務在進行中會用到的資源檔案 (注意：關於這服務的文字性內容，例如資格的引導或申請人的細則，則 *應該* 放在 GOV.UK 上)
* `admin.servicename.service.gov.uk` 是放一些功能，讓非技術人員可以執行服務 (例如：聯絡中心的員工可以用這個子域名去存取和處理一些需要人工判斷的工作項目)

你 *不應該* 為 application programming interfaces (APIs) 建立個別的網域，除非真的有很好的理由要有一個完全分開的網域。 (真的這麼適合理由很少很少)

如果你想在除了上列的三種使用者看得到的子網域之外建立新的，服務管理者應該 (透過你的 transformation team contact) 通知 Government Digital Service 的技術架構師。除了主流的互動服務，我們也正在為一些比較非常態的系統設計建立模式，而且我們也隨時可以針對例外或特殊案例進行討論。

**使用者名稱和密碼**

如果服務還在 private alpha 或 private beta 的階段，那它應該要以只有開發團隊和測試人員知道的帳號和密碼保護起來。如果一項服務、或該服務的部份 進入了 public alpha 或 beta 階段，那麼它應該在每個頁面上和每個 API 回應中以文字標籤明確標示 (也就是說，不要用裡面寫著 alpha 或 beta 文字的圖片)。

**多重環境**

對任何服務而言，為開發、測試、上線的版本準備多種的 '環境' 是很好的實務。[開發和測試環境](/service-manual/making-software/sandbox-and-staging-servers.html)讓團隊可以在一個服務上線前評估正確性和品質。一般而言，用來存取開發和測試版之服務的子域名 架構方式和上線版之服務的子域名一樣。

因此，你 *可以* 為了測試和開發的用途在 `servicename.service.gov.uk` 下[建立其他子域名](/service-manual/domain-names/service-subdomain-names.html)，例如 `www-preview.` 和 `www-dev.`，或 `www.preview.` 和 `www.dev.`。如果有很強有力的理由要用一個非 `.gov.uk` 的網域來做測試及/或開發用子網域，那也可以接受。

不管用什麼網域名稱，測試和開發網域上的 web-based 服務 (包含 APIs) 應該要以 private alpha 和 beta 階段一樣的使用者名稱和密碼來保護。

## Transport Layer Security

許多服務會需要向使用者索取得個人資料。確保惡意的第三方無法在這些資料正經由網路傳送的過程中加以攔劫，是非常重要的。

因此，所有經由 service.gov.uk 網域來存取的服務 (包含各種 API) *必須* 只能透過安全的連線。這對於 web-based 的服務而言，
就是只能使用 HTTPS 連線 (這些安全連線是建立在一種縮寫為 TLS 或 SSL 的協定之上，所以我們也常常用這兩個縮寫去稱呼之)。
所有服務在任何情況下都不能接受 HTTP 連線。

一旦一個服務的管理者確認了他們的 HTTPS 設置可以順利運作，他們 *應該* 在 production 網域 (如 www., admin. 和 assets.) 上
以設置一個如下的 HTTP response header 來啟用 HSTS。

    Strict-Transport-Security: max-age=1209600, includeSubDomains;

代表一個 14 天內只用 HTTPS 連線的承諾。一旦服務管理者確信 HSTS 設定正確，你 *應該* 將這承諾延長至月或年：

    Strict-Transport-Security: max-age=31536000, includeSubDomains;

## Cookies

用在 `www.servicename.service.gov.uk` 和 `admin.servicename.service.gov.uk` 的 cookies *必須* 要把適用範圍限制於只在原來的網域。Cookie *不得* 將適用範圍擴大到 `servicename.service.gov.uk` 的網域。

Cookies *不應該* 用於 `assets.servicename.service.gov.uk` (因為這樣會[造成瀏覽器的額外負擔、造成回應使用者的時間變慢](https://developer.yahoo.com/performance/rules.html#cookie_free)卻又沒為服務管理者提供什麼好處。)

Cookies 送出時 *必須* 要設有 `Secure` 屬性，而且在時機適當的時候也要設有 `HttpOnly` 屬性。這些屬性設定[對瀏覽器處理 cookies 的方式提供了更多的安全保障](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_and_HttpOnly)。

## robots.txt and root level redirections

GOV.UK is the place for users to find all government services, so it’s important to ensure that users always start on the relevant GOV.UK page, rather than a different or duplicate start page on `www.servicename.service.gov.uk`.

As a result, services need to ask search engines not to index pages on their domains, so that the relevant GOV.UK page and the service domain don’t compete with each other in search engine results. This can be achieved by redirecting users to the relevant GOV.UK start page if they go directly to the service’s domain name, and by asking search engines not to index pages on the service’s domain name. Therefore, every service hosted on a service.gov.uk domain MUST:

* have a `robots.txt` file on the `www`, `admin` and `assets` subdomains asking search engines not to index any part of the site. Example content for `robots.txt` is given below, and more details can be found on [The Web Robots Pages](http://www.robotstxt.org/faq/prevent.html):

      User-agent: *
      Disallow: /

* have an HTTP 301 redirection from the top-level index page of the `www` and `assets` subdomains to the relevant start page on GOV.UK. (Note: this means that the service start page on GOV.UK SHOULD NOT link to the root of the `www` domain.)

## Origin servers for CDN-based provider of DDOS protection

If you have contracted with [CDN](https://en.wikipedia.org/wiki/Content_delivery_network)-based [DDOS](https://en.wikipedia.org/wiki/DDOS#Distributed_attack)-protection suppliers then you should register these additional subdomains for use by your suppliers:

*[DDOS]: Distributed Denial of Service
*[CDN]: Content Delivery Network

- `www-production.servicename.service.gov.uk`
- `admin-production.servicename.service.gov.uk`
- `assets-production.servicename.service.gov.uk`

Your suppliers will use these subdomains to address your `www`, `admin` and `assets` services.

Detailed configuration advice for origin servers is outside of the scope of this document, but it's important to ensure that these 'origin domains' only listen for traffic from trusted sources like:

- the DDOS protection provider’s servers
- the locations where the service itself is being developed and/or managed

At present we advise against allowing DDOS protection suppliers to terminate SSL connections for transactional services carrying personal information, but this behaviour isn't prohibited at present. Although SSL termination on the third party network would allow the supplier(s) to carry out additional analysis and potentially extra mitigations against certain types of attack, it would also give the supplier access to all the personal information being submitted to your service. 

There are obvious downsides to allowing this level of access, especially if the supplier’s network and processes have not been accredited to the same level as the rest of the service. It’s a risk-based decision, but if in doubt we suggest a presumption against SSL termination on third party networks.

Many suppliers offer IP forwarding DDOS protection, which does not have the same security issues as SSL termination, and is recommended in preference to SSL termination.  If your service requires transaction monitoring (which is not at all the same thing as DDOS protection) you should contact your CESG account manager for advice.  This is interim guidance and will be updated -- check back in early May 2013 for an update.

## Emails sent to service users

Emails to users of your service SHOULD be sent from a human-monitored email address that originates from the domain `servicename.service.gov.uk` (and not the dept/agency or any other domain name).

You SHOULD enable [SPF](https://en.wikipedia.org/wiki/Sender_Policy_Framework) on the sending domain. You MAY also want to use [DKIM](http://www.dkim.org/) on the sending domain; it can provide additional guarantees about message delivery and help recipients to more easily distinguish genuine mail from forgery.

## Lifecycle of service subdomains

If your service should need to wind down for any reason, you MUST ensure continued useful service and information for users by:

* continuing to use SSL
* serving a redirect from your service to the GOV.UK start page

For services that have been live for less than 6 months, you MUST continue to do the above for the remainder of a year total. For services that have been live longer than that you MUST continue to do the above for a further 12 months or until the expiry of the current SSL certificate, whichever comes first.

The GOV.UK start page will be amended to explain that the service is no longer running, and cease to provide a start button pointing at the defunct service.

*[SPF]: Sender Policy Framework
*[DKIM]: DomainKeys Identified Mail
*[APIs]: application programming interfaces
*[API]: application programming interface
