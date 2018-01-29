---
title: "Azure 應用程式閘道的常見問題集 | Microsoft Docs"
description: "本頁提供 Azure 應用程式閘道相關常見問題的解答"
documentationcenter: na
services: application-gateway
author: davidmu1
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: davidmu
ms.openlocfilehash: f92af44df9863bbf48abb4afcf9b1505c843fadc
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>應用程式閘道的常見問題集

## <a name="general"></a>一般

**問：什麼是應用程式閘道？**

Azure 應用程式閘道是服務形式的應用程式傳遞控制器 (ADC)，可為您的應用程式提供各種第 7 層負載平衡功能。 它提供高度可用並可調整的服務，這完全由 Azure 管理。

**問：應用程式閘道支援哪些功能？**

應用程式閘道支援 SSL 卸載和端對端 SSL、Web 應用程式防火牆、以 cookie 為基礎的工作階段親和性、以 url 路徑為基礎的路由、多重站台裝載和其他功能。 如需完整的支援功能清單，請瀏覽[應用程式閘道簡介](application-gateway-introduction.md)

**問：應用程式閘道與 Azure Load Balancer 之間的差異為何？**

應用程式閘道是第 7 層負載平衡器，這表示它只會使用網路流量 (HTTP/HTTPS/WebSocket)。 它支援功能，例如 SSL 終止、以 cookie 為基礎的工作階段親和性，以及用於平衡流量負載的循環配置資源。 負載平衡器，平衡第 4 層 (TCP/UDP) 的流量負載。

**問：應用程式閘道支援哪些通訊協定？**

Azure 應用程式閘道支援 HTTP、HTTPS 和 WebSocket。

**問：目前支援哪些資源做為後端集區的一部分？**

後端集區可以包含 NIC、虛擬機器擴展集、公用 IP、內部 IP、完整的網域名稱 (FQDN)，以及如 Azure Web 應用程式的多租用戶後端。 應用程式閘道後端集區成員不會繫結至可用性設定組。 只要後端集區成員具有 IP 連線能力，就可以跨越叢集、資料中心或在 Azure 外部。

**問：哪些區域提供此服務？**

應用程式閘道適用於全域 Azure 的所有區域。 它也適用於 [Azure China](https://www.azure.cn/) 和 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)

**問：這是我的訂用帳戶專用的部署，還是所有客戶共用？**

應用程式閘道是您虛擬網路中專用的部署。

**問：是否支援 HTTP->HTTPS 重新導向？**

支援重新導向。 若要深入了解，請瀏覽[應用程式閘道重新導向概觀](application-gateway-redirect-overview.md)。

**問：接聽程式的處理順序為何？**

接聽程式會依其顯示順序處理。 因此，如果基本接聽程式符合傳入的要求，就會先處理它。  多站台接聽程式應在基本接聽程式之前設定，以確保流量會路由傳送到正確的後端。

**問：哪裡可找到應用程式閘道的 IP 和 DNS？**

使用公用 IP 位址做為端點時，可以在入口網站中應用程式閘道站的公用 IP 位址資源 或 [概觀] 頁面上找到這項資訊。 如需內部 IP 位址，可以在 [概觀] 頁面上找到這項資訊。

**問：IP 或 DNS 是否會在應用程式閘道的存留期內變更？**

如果客戶停止後啟動閘道，VIP 可能會變更。 與應用程式閘道相關聯的 DNS 不會在閘道的存留期內變更。 基於這個理由，建議使用 CNAME 別名並將它指向應用程式閘道的 DNS 位址。

**問：應用程式閘道是否支援靜態 IP？**

否，應用程式閘道不支援靜態公用 IP 位址，但是支援靜態內部 IP。

**問：應用程式閘道是否在閘道上支援多個公用 IP？**

應用程式閘道只支援一個公用 IP 位址。

**問：應用程式閘道是否支援 x-forwarded-for 標頭？**

是，應用程式閘道會將 x-forwarded-for、x-forwarded-proto 和 x-forwarded-port 標頭插入已轉寄至後端的要求。 x-forwarded-for 標頭的格式是以逗號分隔的 IP:Port 清單。 x-forwarded-proto 的有效值為 http 或 https。 X-forwarded-port 指定要求送達應用程式閘道的連接埠。

**問：部署應用程式閘道需要多久的時間？進行更新時，我的應用程式閘道是否仍有作用？**

新的應用程式閘道部署可能需要長達 20 分鐘來佈建。 執行個體大小/計數的變更不會產生干擾，而閘道會在這段期間保持作用中。

## <a name="configuration"></a>組態

**問：應用程式閘道一律部署在虛擬網路中？**

是，應用程式閘道一律部署在虛擬網路子網路中。 這個子網路只包含應用程式閘道。

**問：應用程式閘道是否可與其虛擬網路外部的執行個體通訊？**

應用程式閘道只要具有 IP 連線能力，即可與其虛擬網路外部的執行個體通訊。 如果您打算使用內部 IP 做為後端集區成員，則需要 [VNET 對等互連](../virtual-network/virtual-network-peering-overview.md)或 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。

**問：是否可以在應用程式閘道子網路中部署其他任何項目？**

否，但是您可以在子網路中部署其他應用程式閘道。

**問：應用程式閘道子網路是否支援網路安全性群組？**

應用程式閘道子網路支援網路安全性群組，但有下列限制：

* 必須放入連接埠 65503-65534 上傳入流量的例外狀況，後端健康情況才能正常運作。

* 不會封鎖輸出網際網路連線。

* 必須允許來自 AzureLoadBalancer 標籤的流量。

**問：應用程式閘道的限制為何？是否可以增加這些限制？**

請瀏覽[應用程式閘道限制](../azure-subscription-service-limits.md#application-gateway-limits)以檢視相關限制。

**問：是否可以同時對外部和內部流量使用應用程式閘道？**

是，應用程式閘道支援每個應用程式閘道擁有具有一個內部 IP 和一個外部 IP。

**問：是否支援 VNet 對等互連？**

是，支援 VNet 對等互連，這對於平衡其他虛擬網路中的流量負載很有幫助。

**問：我可與經由 ExpressRoute 或 VPN 通道連線的內部部署伺服器通訊嗎？**

是，只有流量允許即可。

**問：是否可有一個為不同連接埠上的許多應用程式提供服務的後端集區？**

支援微服務架構。 您必須進行多項 http 設定，以在不同的連接埠上探查。

**問：自訂探查是否支援回應資料使用萬用字元/regex？**

自訂探查不支援回應資料使用萬用字元或 regex。 

**問：規則的處理方式為何？**

規則會依其設定順序處理。 建議在基本規則前設定多站台規則，以減少流量路由傳送到不適當後端的機會，因為在評估多站台規則之前，基本規則會根據連接埠比對流量。

**問：規則的處理方式為何？**

規則會依其建立順序處理。 建議在基本規則前面設定多網站規則。 藉由先設定多網站接聽程式，此設定可以減少流量路由傳送到不適當後端的機會。 因為在評估多網站規則之前，基本規則會先根據連接埠比對流量，所以會發生此路由問題。

**問：自訂探查的 [主機] 欄位表示什麼？**

主機欄位指定探查要送達的名稱。 只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。 此值與 VM 主機名稱不同，其格式為 \<protocol\>://\<host\>:\<port\>\<path\>。

**問：我可以將一些來源 IP 的應用程式閘道存取列入允許清單嗎？**

使用應用程式閘道子網路上的 NSG 可以完成此案例。 應依照所列的優先順序在子網路施加下列限制：

* 允許來源 IP/IP 範圍的傳入流量。

* 允許從所有來源至連接埠 65503-65534 的傳入要求以便進行[後端健康情況通訊](application-gateway-diagnostics.md)。

* 允許 [NSG](../virtual-network/virtual-networks-nsg.md) 上傳入的 Azure 負載平衡器探查 (AzureLoadBalancer 標籤) 和輸入虛擬網路流量 (VirtualNetwork 標籤)。

* 使用「全部拒絕」規則封鎖所有其他傳入流量。

* 允許所有目的地對網際網路的輸出流量。

## <a name="performance"></a>效能

**問：應用程式閘道如何支援高可用性和延展性？**

如果您已部署 2 個以上的執行個體，應用程式閘道即可支援高可用性案例。 Azure 會將這些執行個體分散於更新和容錯網域，確保所有執行個體不會同時失敗。 應用程式閘道支援延展性的方式為藉由新增相同閘道的多個執行個體來分攤負載。

**問：如何利用應用程式閘道跨越資料中心封存 DR 案例？**

客戶可以使用流量管理員，將流量分散於不同資料中心內的多個應用程式閘道。

**問：是否支援自動調整大小？**

否，但應用程式閘道有輸送量計量，可用於在達到閾值時發出警示。 手動新增執行個體或變更大小，不會重新啟動閘道，也不會影響現有的流量。

**問：手動相應增加/相應減少會造成停機嗎？**

不會停機，執行個體已分散於升級網域和容錯網域。

**問：是否可在中斷的情況下，將執行個體大小從中型變成大型？**

是，Azure 會將執行個體分散於更新和容錯網域，確保所有執行個體不會同時失敗。 應用程式閘道支援調整的方式為藉由新增相同閘道的多個執行個體來分攤負載。

## <a name="ssl-configuration"></a>SSL 組態

**問：應用程式閘道支援哪些憑證？**

支援自我簽署憑證、CA 憑證和萬用字元憑證。 不支援 EV 憑證。

**問：應用程式閘道目前支援哪些加密套件？**

以下是應用程式閘道目前支援的加密套件。 請參閱：[在應用程式閘道上設定 SSL 原則版本和加密套件](application-gateway-configure-ssl-policy-powershell.md)，以了解如何自訂 SSL 選項。

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**問：應用程式閘道是否也支援後端流量的重新加密？**

是，應用程式閘道支援 SSL 卸載，以及可重新加密後端流量的端對端 SSL。

**問：是否可設定 SSL 原則來控制 SSL 通訊協定版本嗎？**

是，您可以將應用程式閘道設定為拒絕 TLS1.0、TLS1.1 和 TLS1.2。 SSL 2.0 和 3.0 都已預設停用並，無法加以設定。

**問：可以設定加密套件和原則的順序嗎？**

是，支援[加密套件的設定](application-gateway-ssl-policy-overview.md)。 定義自訂原則時，必須啟用至少一個下列的加密套件。 應用程式閘道使用 SHA256 進行後端管理。

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**問：支援多少個 SSL 憑證？**

最多支援 20 個 SSL 憑證。

**問：針對後端重新加密支援多少個驗證憑證？**

最多支援 10 個驗證憑證 (預設值為 5)。

**問：應用程式閘道是否原本就與 Azure Key Vault 整合？**

不，它並未與 Azure Key Vault 整合。

## <a name="web-application-firewall-waf-configuration"></a>Web 應用程式防火牆 (WAF) 組態

**問：WAF SKU 是否提供適用於標準 SKU 的所有功能？**

是，WAF 支援標準 SKU 中的所有功能。

**問：應用程式閘道支援的 CRS 版本為何？**

應用程式閘道支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)。

**問：如何監視 WAF？**

WAF 是透過診斷記錄功能來監視，如需診斷記錄的詳細資訊，請參閱[應用程式閘道的診斷記錄和計量](application-gateway-diagnostics.md)

**問：偵測模式是否會封鎖流量？**

否，偵測模式只會記錄觸發 WAF 規則的流量。

**問：如何自訂 WAF 規則？**

是，WAF 規則是可自訂的，如需如何自訂它們的詳細資訊，請瀏覽[自訂 WAF 規則群組與規則](application-gateway-customize-waf-rules-portal.md)

**問：目前可使用哪些規則？**

WAF 目前支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)，其針對 Open Web Application Security Project (OWASP) 所識別的大多數前 10 大弱點 (請參閱 [OWASP 的前 10 大弱點 (英文)](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)) 提供基準安全性

* SQL 插入式攻擊保護

* 跨網站指令碼保護

* 常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊

* 防範 HTTP 通訊協定違規

* 防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭

* 防範 Bot、編目程式和掃描器

 * 偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)

**問：WAF 是否也支援 DDoS 預防？**

否，WAF 不提供 DDoS 預防。

## <a name="diagnostics-and-logging"></a>診斷和記錄

**問：應用程式閘道可使用哪些記錄檔類型？**

應用程式閘道可使用三種記錄檔。 如需有關這些記錄和其他診斷功能的詳細資訊，請瀏覽[應用程式閘道的後端健康情況、診斷記錄和計量](application-gateway-diagnostics.md)。

- **ApplicationGatewayAccessLog** - 此存取記錄包含提交至應用程式閘道前端的每個要求。 此資料包含呼叫者的 IP、所要求的 URL、回應延遲、傳回碼、輸入和輸出位元組。每隔 300 秒會收集一次存取記錄檔。 此記錄檔包含每個應用程式閘道執行個體的一筆記錄。
- **ApplicationGatewayPerformanceLog** - 此效能記錄會擷取每個執行個體的效能資訊，包括提供的要求總數、輸送量 (以位元組為單位)、提供的總要求數、失敗的要求計數、狀況良好和狀況不良的後端執行個體計數。
- **ApplicationGatewayFirewallLog** - 此防火牆記錄包含透過應用程式閘道的偵測或防護模式 (依 Web 應用程式防火牆的設定) 所記錄的要求。

**問：如何知道我的後端集區成員狀態良好？**

您可以藉由造訪[應用程式閘道診斷](application-gateway-diagnostics.md)，使用 PowerShell Cmdlet `Get-AzureRmApplicationGatewayBackendHealth` 或透過入口網站驗證健康狀態

**問：診斷記錄檔的保留原則為何？**

診斷記錄檔會送至客戶儲存體帳戶，而客戶可以根據其喜好來設定保留原則。 診斷記錄檔也可以傳送至事件中樞或 Log Analytics。 如需詳細資訊，請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)。

**問：如何取得應用程式閘道的稽核記錄檔？**

稽核記錄檔可用於應用程式閘道。 在入口網站中，按一下應用程式閘道功能表刀鋒視窗中的 [活動記錄檔] 以存取稽核記錄檔。 

**問：是否可以設定應用程式閘道的警示？**

是，應用程式閘道可以支援警示，並可將警示設定為關閉計量。  應用程式閘道目前有「輸送量」計量，這可設定用於警示。 若要深入了解警示，請瀏覽[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

**問：後端健康情況傳回不明狀態，什麼導致這個狀態？**

最常見的原因是後端的存取遭到 NSG 或自訂 DNS 所封鎖。 若要深入了解，請瀏覽[應用程式閘道的後端健康狀態、診斷記錄及計量](application-gateway-diagnostics.md)。

## <a name="next-steps"></a>後續步驟

若要深入了解應用程式閘道，請瀏覽[應用程式閘道簡介](application-gateway-introduction.md)。
