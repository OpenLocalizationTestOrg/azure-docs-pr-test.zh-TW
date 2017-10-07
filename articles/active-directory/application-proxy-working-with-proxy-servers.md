---
title: "aaaWork 與現有的內部 proxy 伺服器與 Azure AD |Microsoft 文件"
description: "涵蓋如何 toowork 與現有的內部 proxy 伺服器。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>使用現有的內部部署 Proxy 伺服器

這篇文章說明如何 tooconfigure Azure Active Directory (Azure AD) 應用程式 Proxy 連接器 toowork 與連出 proxy 伺服器。 它適用於具有現有 Proxy 之網路環境的客戶。

我們先來看看這些主要部署案例︰
* 設定連接器 toobypass 您在內部部署輸出 proxy。
* 設定連接器 toouse 連出 proxy tooaccess Azure AD Application Proxy。

如需連接器運作方式的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。

## <a name="configure-hello-outbound-proxy"></a>設定 hello 連出 proxy

如果您的環境中有輸出 proxy，請使用適當的權限 tooconfigure hello 連出 proxy 使用的帳戶。 因為 hello 安裝程式會執行 hello 負責 hello 安裝 hello 使用者內容中，您可以使用 Microsoft Edge 或其他網際網路瀏覽器檢查 hello 組態。

在 Microsoft Edge tooconfigure hello proxy 設定：

1. 跳過**設定** > **檢視進階設定** > **開啟的 Proxy 設定** > **手動 Proxy 安裝**.
2. 設定**使用 proxy 伺服器**太**上**，選取 hello **（內部網路） 的本機位址不要使用 hello proxy 伺服器**核取方塊，然後按一下 變更 hello 位址和連接埠 tooreflect您的本機 proxy 伺服器。
3. 填入 hello 必要的 proxy 設定。

   ![Proxy 設定的對話方塊](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>略過輸出 Proxy

連接器有會發出輸出要求的基礎作業系統元件。 這些元件會自動嘗試 toolocate hello 網路上的 proxy 伺服器。 如果啟用 hello 環境中，他們會使用 Web Proxy 自動探索 (WPAD)。

hello OS 元件嘗試一波波的 wpad.domainsuffix 的 DNS 查閱 toolocate proxy 伺服器。 如果此解析在 DNS 中，HTTP 要求接著會 toohello IP wpad.dat 的位址。 此要求會變成您的環境中的 hello proxy 組態指令碼。 hello 連接器會使用這個指令碼 tooselect 連出 proxy 伺服器。 不過，連接器流量可能仍然不經過，由於在 hello proxy 所需的其他組態設定。

您可以設定它使用您在內部部署 proxy tooensure 直接連線 toohello Azure hello 連接器 toobypass 服務。 我們建議您使用這種方法 （如果它允許您的網路原則），因為這表示您有一個較少的組態 toomaintain。

hello 連接器 toodisable 連出 proxy 使用方式編輯 hello C:\Program Files\Microsoft AAD 應用程式 Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，並新增 hello *system.net*此程式碼範例所示的區段:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure hello 連接器更新程式服務也會略過 hello proxy，使類似變更 toohello ApplicationProxyConnectorUpdaterService.exe.config 檔案位於 C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器更新程式。

是 hello 原始檔，確定 toomake 副本，以防您需要 toorevert toohello 預設.config 檔案。

## <a name="use-hello-outbound-proxy-server"></a>使用 hello 連出 proxy 伺服器

某些環境中需要所有的輸出流量 toogo 透過輸出 proxy，而沒有例外狀況。 如此一來，略過 hello proxy 不是選項。

您可以設定透過 hello 輸出 proxy，hello 連接器流量 toogo hello 下列圖表所示：

 ![設定連接器流量 toogo 透過連出 proxy tooAzure AD 應用程式 Proxy](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

因此只有輸出流量的沒有任何需要 tooconfigure 輸入通過防火牆的存取。

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>步驟 1： 設定 hello 連接器和相關服務 toogo 透過 hello 連出 proxy

Hello 連接器就如同舊版中，如果 WPAD hello 環境中啟用並適當地設定，會自動探索 hello 連出 proxy 伺服器，並嘗試 toouse 它。 不過，您可以明確地設定 hello 連接器 toogo 透過輸出的 proxy。

toodo 因此編輯 hello C:\Program Files\Microsoft AAD 應用程式 Proxy Connector\ApplicationProxyConnectorService.exe.config 檔案，然後新增 hello *system.net* > 一節，此程式碼範例所示。 變更*proxyserver:8080* tooreflect 您本機 proxy 伺服器名稱或 IP 位址與 hello 連接埠會接聽。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

接下來，進行類似的變更 toohello 檔案位於 C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器 Updater\ApplicationProxyConnectorUpdaterService.exe.config 設定 hello 連接器更新程式服務 toouse hello proxy。

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>步驟 2： 設定從 hello 連接器和相關的服務 tooflow 透過 hello proxy tooallow 流量

在 hello 連出 proxy 有四個層面 tooconsider:
* Proxy 輸出規則
* Proxy 驗證
* Proxy 連接埠
* SSL 審查

#### <a name="proxy-outbound-rules"></a>Proxy 輸出規則
允許存取 toohello 下列連接器服務存取的端點：

* *.msappproxy.net
* *.servicebus.windows.net

初始的註冊，允許存取 toohello 下列端點：

* login.windows.net
* login.microsoftonline.com

如果您不允許連線的 FQDN，而且需要 toospecify IP 範圍相反地，使用這些選項：

* 允許 hello 連接器對外存取 tooall 目的地。
* 允許 hello 連接器對外存取太[Azure 資料中心 IP 範圍](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)。 使用 hello Azure 資料中心 IP 範圍清單的 hello 挑戰是每週更新。 您需要 tooput 位置 tooensure 據以更新您的存取規則中的處理序。

#### <a name="proxy-authentication"></a>Proxy 驗證

目前不支援 Proxy 驗證。 我們目前建議 tooallow hello 連接器匿名存取 toohello 網際網路目的地。

#### <a name="proxy-ports"></a>Proxy 連接埠

hello 連接器可藉由使用 hello CONNECT 方法的輸出的 ssl 連線。 這個方法基本上穿過 hello 連出 proxy 設定。 設定 hello proxy 伺服器 tooallow 通道 tooports 443 和 80。

>[!NOTE]
>當服務匯流排在 HTTPS 上執行時，它會使用連接埠 443。 不過，根據預設，服務匯流排嘗試直接 TCP 連線，而且會回復 tooHTTPS 只有直接連線失敗時。

hello 流量也會傳送 hello 連出 proxy 伺服器透過服務匯流排，請確認該 hello 連接器無法直接連線 toohello tooensure Azure 服務的連接埠 9350、 9352 和 5671。

#### <a name="ssl-inspection"></a>SSL 審查
請勿用於 SSL 檢查 hello 連接器流量，因為這會導致 hello 連接器流量的問題。

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>針對連接器 Proxy 問題和服務連線問題進行疑難排解
現在您應該會看到所有流量流經 hello proxy。 如果您有問題，應該有助於 hello 下列疑難排解資訊。

hello 最佳方式 tooidentify 和連接器連線問題疑難排解的問題是的 tootake 啟動 hello 連接器服務時擷取 hello 連接器服務的網路。 這可能是令人怯步的工作，因此讓我們看看關於擷取及篩選網路追蹤的快速提示。

您可以使用 hello 監視您所選擇的工具。 針對 hello 本文的目的，我們會使用 Microsoft 網路監視器 3.4。 您可以[從 Microsoft 下載](https://www.microsoft.com/download/details.aspx?id=4865)。

hello 範例和我們在 hello 下列各節中使用的篩選特定 tooNetwork 監視器，但 hello 原則可以套用的 tooany 分析工具。

### <a name="take-a-capture-by-using-network-monitor"></a>使用網路監視器進行擷取

toostart 擷取：

1. 開啟網路監視器，並按一下 [新增擷取]。
2. 按一下 hello**啟動** 按鈕。

   ![網路監視器視窗](./media/application-proxy-working-with-proxy-servers/network-capture.png)

完成擷取之後，請按一下 hello**停止**按鈕 tooend 它。

### <a name="take-a-capture-of-connector-traffic"></a>擷取連接器流量

初始疑難排解時，執行下列步驟的 hello:

1. 從 services.msc，停止 hello Azure AD 應用程式 Proxy 連接器服務。
2. 啟動 hello 網路擷取。
3. 啟動 hello Azure AD 應用程式 Proxy 連接器服務。
4. 停止 hello 網路擷取。

   ![services.msc 中的 Azure AD 應用程式 Proxy 連接器服務](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>查看 hello 要求從 hello 連接器 toohello proxy 伺服器

現在您有網路擷取，您已準備好 toofilter 它。 hello 金鑰 toolooking hello 追蹤在了解如何 toofilter hello 擷取。

一個篩選條件如下所示 （其中 8080 是 hello proxy 服務連接埠）：

**(http.Request or http.Response) and tcp.port==8080**

如果您輸入此篩選條件在 hello**顯示篩選**視窗，然後選取**套用**，它會篩選根據 hello 篩選 hello 擷取流量。

hello 上述篩選條件會顯示只 hello HTTP 要求和回應從 hello proxy 連接埠。 連接器啟動，其中 hello 連接器是設定的 toouse proxy 伺服器，會顯示 hello 篩選結果類似這樣：

 ![篩選之 HTTP 要求和回應的範例清單](./media/application-proxy-working-with-proxy-servers/http-requests.png)

您想要現在特別尋求的 hello 連線要求，顯示與 hello proxy 伺服器的通訊。 成功時，您會收到 HTTP OK (200) 回應。

如果您看到其他回應碼，例如 407 或 502，hello proxy 需要驗證，或因其他原因而禁止 hello 流量。 此時您會與您的 Proxy 伺服器支援團隊合作。

### <a name="identify-failed-tcp-connection-attempts"></a>識別失敗的 TCP 連線嘗試

hello 其他常見的案例，您可能會想要時 hello 連接器嘗試 tooconnect 直接，但它失敗。

另一個網路監視器篩選，可協助您 tooeasily 識別這個問題是：

**property.TCPSynRetransmit**

SYN 封包是 hello 第一個封包傳送 tooestablish TCP 連線。 如果這個封包不會傳回回應，hello SYN 重試失敗。 您可以使用任何重新傳輸的 Syn 之前篩選 toosee hello。 然後，您可以檢查這些 Syn 是否對應 tooany 連接器相關的資料流。

hello 下例示範失敗的連線嘗試 tooService 匯流排連接埠則為 9352:

 ![失敗連線嘗試的範例回應](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

如果您看到類似前面回應 hello，hello 連接器正嘗試 toocommunicate 直接與 hello Azure 服務匯流排服務。 如果您預期 hello 連接器 toomake 直接連接 toohello Azure 服務，此回應是清楚知道您是否有網路或防火牆問題。

>[!NOTE]
>如果您是設定的 toouse proxy 伺服器，可能表示這個回應，Service Bus 嘗試直接 TCP 連線之後，才能透過 HTTPS 切換 tooattempting 連接。
>

網路追蹤分析並非適合每個人。 但它可以是與您的網路狀況有關的寶貴工具 tooget 快速資訊。

如果您繼續 toostruggle 與連接器連線問題，請使用我們支援小組建立票證。 hello 小組可協助您進行進一步的疑難排解。

如需有關解決應用程式 Proxy 連接器錯誤的相關資訊，請參閱[疑難排解應用程式 Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)。

## <a name="next-steps"></a>後續步驟

[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)<br>
[Toosilently hello Azure AD 應用程式 Proxy 連接器的安裝方式](active-directory-application-proxy-silent-installation.md)
