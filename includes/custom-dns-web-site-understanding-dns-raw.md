hello 網域名稱系統 (DNS) 是使用的 toolocate 資源上 hello 網際網路。 例如，當您在瀏覽器中輸入 web 應用程式位址，或按一下網頁上的連結，它會使用 DNS tootranslate hello 網域為 IP 位址。 hello IP 位址就像街道地址，但不是人力非常方便。 比方說，是更容易 tooremember 的 DNS 名稱，例如**contoso.com**比是 tooremember 例如 192.168.1.88 或 2001:0:4137:1f67:24a2:3888:9cce:fea3 的 IP 位址。

hello DNS 系統根據*記錄*。 記錄會將特定的 *名稱*(如 **contoso.com**)，與 IP 位址或其他 DNS 名稱相關聯。 當應用程式，例如網頁瀏覽器，在 DNS 中的名稱查閱它找到 hello 記錄，並使用任何它所指 tooas hello 位址。 如果 hello 值點 toois IP 位址，hello 瀏覽器將會使用該值。 如果它所指 tooanother DNS 名稱，然後 hello 應用程式具有 toodo 解析度一次。 所有名稱解析最終會導出一個 IP 位址。

當您建立 web 應用程式，App Service 中時，DNS 名稱會自動指派 toohello web 應用程式。 這個名稱會採用 hello 形式 **&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。 另外還有一個虛擬 IP 位址可供使用時建立 DNS 記錄，因此您可以建立記錄該點 toohello **。 名稱是.azurewebsites.net**，或您可以指向 toohello IP 位址。

> [!NOTE]
> hello IP 位址的 web 應用程式將會變更，如果您刪除並重新建立您的 web 應用程式，或也變更 hello 應用程式服務計劃模式**免費**它已經過設定之後**基本**，**共用**，或**標準**。
> 
> 

有多種記錄類型，每種記錄都有其本身的功能與限制，但對於 Web 應用程式只需要關注兩種記錄，即 A 和 CNAME。

### <a name="address-record-a-record"></a>位址記錄 (A 記錄)
A 記錄將定義域對應，例如**contoso.com**或**www.contoso.com**，*或萬用字元網域*例如 **\*。 contoso.com**，tooan IP 位址。 在 web 應用程式，App Service 中的 hello 情況下，hello hello 服務或您購買您的 web 應用程式的特定 IP 位址的虛擬 IP。

hello 的 A 記錄透過 CNAME 記錄的主要好處包括：

* 您可以對應根網域，例如**contoso.com** tooan IP 位址; 許多的註冊機構只允許此使用 A 記錄
* 您可以擁有一個使用萬用字元的項目，例如 **\*.contoso.com**，即可處理多個子網域的要求，例如 **mail.contoso.com**、**blogs.contoso.com** 或 **www.contso.com**。

> [!NOTE]
> 由於 A 記錄對應 tooa 靜態 IP 位址，無法自動解決您的 web 應用程式變更 toohello IP 位址。 當您設定自訂網域名稱設定 web 應用程式; 提供用於記錄的 IP 位址不過，這個值可能會變更如果您刪除和重新建立您的 web 應用程式，或變更應用程式服務計劃模式 tooback hello 太**免費**。
> 
> 

### <a name="alias-record-cname-record"></a>別名記錄 (CNAME 記錄)
CNAME 記錄對應*特定*DNS 名稱，例如**mail.contoso.com**或**www.contoso.com**，tooanother （標準） 的網域名稱。 在 App Service Web 應用程式的 hello 情況下，hello 正式網域名稱為 hello  **&lt;yourwebappname >。 名稱是.azurewebsites.net**您 web 應用程式的網域名稱。 Hello CNAME 建立之後，建立一個別名 hello  **&lt;yourwebappname >。 名稱是.azurewebsites.net**網域名稱。 hello 的 CNAME 項目將 toohello IP 位址，解析您 **&lt;yourwebappname >。 名稱是.azurewebsites.net**網域名稱，因此 hello hello web 應用程式的 IP 位址變更時，如果您不需要 tootake 任何動作。

> [!NOTE]
> 一些網域註冊機構只允許您 toomap 子網域時使用的 CNAME 記錄，例如**www.contoso.com**，和不根名稱，例如**contoso.com**。如需有關 CNAME 記錄的詳細資訊，請參閱您的註冊機構所提供的 hello 文件<a href="http://en.wikipedia.org/wiki/CNAME_record">hello 維基百科項目上的 CNAME 記錄</a>，或使用 hello <a href="http://tools.ietf.org/html/rfc1035">IETF 網域名稱-實作和規格</a>文件。
> 
> 

### <a name="web-app-dns-specifics"></a>Web 應用程式 DNS 詳細規格
Web 應用程式上使用 A 記錄需要您 toofirst 建立 hello 下列 TXT 記錄的其中一個：

* **Hello 根網域**-DNS TXT 記錄 **@** 太 **&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。
* **為特定的子網域**-DNS 名稱**&lt;子網域 >**太**&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。 例如，**部落格**若 hello 記錄為**blogs.contoso.com**。
* **如 hello 萬用字元 sub dodmains** -DNS TXT 記錄的 * * * 太 **&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。

此 TXT 記錄是使用的 tooverify 您擁有您正嘗試 toouse hello 網域。 此外，這是指 toohello 虛擬 IP 位址的 web 應用程式的 toocreating A 記錄。

您可以找到 hello IP 位址和**。 名稱是.azurewebsites.net**執行您 web 應用程式的名稱 hello 下列步驟：

1. 在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello **Web 應用程式**刀鋒視窗中，按一下 hello 的 web 應用程式的名稱，然後選取**自訂網域**從 hello hello 頁面的底部。
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. 在 hello**自訂網域**刀鋒視窗中，您會看到 hello 虛擬 IP 位址。 儲存此資訊，這在建立 DNS 記錄時會用得到
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > 您無法使用自訂網域名稱與**免費**web 應用程式，必須升級，然後 hello App Service 方案太**共用**，**基本**，**標準**，或**Premium**層。 如需有關 hello 應用程式服務計劃的定價層，包括如何 toochange hello 您 web 應用程式的定價層，請參閱[tooscale web 應用程式的方式](../articles/app-service-web/web-sites-scale.md)。
   > 
   > 

