hello 網域名稱系統 (DNS) 是使用的 toolocate 項目上 hello 網際網路。 例如，當您在瀏覽器中輸入的位址，或按一下網頁上的連結，它會使用 DNS tootranslate hello 網域為 IP 位址。 hello IP 位址就像街道地址，但不是人力非常方便。 比方說，是更容易 tooremember 的 DNS 名稱，例如**contoso.com**比是 tooremember 例如 192.168.1.88 或 2001:0:4137:1f67:24a2:3888:9cce:fea3 的 IP 位址。

hello DNS 系統根據*記錄*。 記錄會將特定的 *名稱*(如 **contoso.com**)，與 IP 位址或其他 DNS 名稱相關聯。 當應用程式，例如網頁瀏覽器，在 DNS 中的名稱查閱它找到 hello 記錄，並使用任何它所指 tooas hello 位址。 如果 hello 值點 toois IP 位址，hello 瀏覽器將會使用該值。 如果它所指 tooanother DNS 名稱，然後 hello 應用程式具有 toodo 解析度一次。 所有名稱解析最終會導出一個 IP 位址。

當您建立 Azure 網站時，DNS 名稱會自動指派 toohello 站台。 這個名稱會採用 hello 形式 **&lt;yoursitename&gt;。 名稱是.azurewebsites.net**。 當您為 Azure Traffic Manager 端點加入您的網站時，您的網站，就可透過 hello 存取 **&lt;yourtrafficmanagerprofile&gt;。 trafficmanager.net**網域。

> [!NOTE]
> 當您的網站設定為流量管理員端點時，您會使用 hello **。 trafficmanager.net**位址建立 DNS 記錄時。
> 
> 您只能搭配使用 CNAME 記錄與流量管理員
> 
> 

另外還有多種類型的記錄，每個都有自己的函式和限制，但設定的網站 tooas Traffic Manager 端點，如我們只負責一個;*CNAME*記錄。

### <a name="cname-or-alias-record"></a>CNAME 或別名記錄
CNAME 記錄對應*特定*DNS 名稱，例如**mail.contoso.com**或**www.contoso.com**，tooanother （標準） 的網域名稱。 在 Azure 網站使用 Traffic Manager 的 hello 情況下，hello 正式網域名稱為 hello  **&lt;myapp >。 trafficmanager.net** Traffic Manager 設定檔網域名稱。 Hello CNAME 建立之後，建立一個別名 hello  **&lt;myapp >。 trafficmanager.net**網域名稱。 hello 的 CNAME 項目將 toohello IP 位址，解析您 **&lt;myapp >。 trafficmanager.net**網域名稱，因此 hello 網站 hello IP 位址變更時，如果您不需要 tootake 任何動作。

一旦流量到達在 Traffic Manager，然後路由傳送嗨流量 tooyour 網站使用 hello 負載平衡的方法設定為。 這是完全透明 toovisitors tooyour 網站。 它們只會看到瀏覽器中的 hello 自訂網域名稱。

> [!NOTE]
> 一些網域註冊機構只允許您 toomap 子網域時使用的 CNAME 記錄，例如**www.contoso.com**，和不根名稱，例如**contoso.com**。如需有關 CNAME 記錄的詳細資訊，請參閱您的註冊機構所提供的 hello 文件<a href="http://en.wikipedia.org/wiki/CNAME_record">hello 維基百科項目上的 CNAME 記錄</a>，或使用 hello <a href="http://tools.ietf.org/html/rfc1035">IETF 網域名稱-實作和規格</a>文件。
> 
> 

