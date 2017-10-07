---
title: "Azure 應用程式閘道常見問題 aaaFrequently |Microsoft 文件"
description: "此頁面提供的解答 toofrequently 常見問題解答 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>應用程式閘道的常見問題集

## <a name="general"></a>一般

**問：什麼是應用程式閘道？**

Azure 應用程式閘道是服務形式的應用程式傳遞控制器 (ADC)，可為您的應用程式提供各種第 7 層負載平衡功能。 它提供高度可用並可調整的服務，這完全由 Azure 管理。

**問：應用程式閘道支援哪些功能？**

應用程式閘道支援 SSL 卸載和結束 tooend SSL、 Web 應用程式防火牆、 cookie 架構工作階段親和性、 url 路徑架構路由、 多站台裝載和其他人。 如需支援功能的完整清單，請瀏覽[簡介 tooApplication 閘道](application-gateway-introduction.md)

**問：Hello 應用程式閘道與 Azure 負載平衡器之間的差異為何？**

應用程式閘道是第 7 層負載平衡器，這表示它只會使用網路流量 (HTTP/HTTPS/WebSocket)。 它支援功能，例如 SSL 終止、以 cookie 為基礎的工作階段親和性，以及用於平衡流量負載的循環配置資源。 負載平衡器，平衡第 4 層 (TCP/UDP) 的流量負載。

**問：應用程式閘道支援哪些通訊協定？**

Azure 應用程式閘道支援 HTTP、HTTPS 和 WebSocket。

**問：目前支援哪些資源做為後端集區的一部分？**

後端集區可以包含 NIC、虛擬機器擴展集、公用 IP、內部 IP、完整的網域名稱 (FQDN)，以及如 Azure Web 應用程式的多租用戶後端。 應用程式閘道後端集區成員不會繫結 tooan 可用性設定組。 只要後端集區成員具有 IP 連線能力，就可以跨越叢集、資料中心或在 Azure 外部。

**問：哪些區域位於 hello 服務？**

應用程式閘道適用於全域 Azure 的所有區域。 它也適用於 [Azure China](https://www.azure.cn/) 和 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)

**問：這是我的訂用帳戶專用的部署，還是所有客戶共用？**

應用程式閘道是您虛擬網路中專用的部署。

**問：是否支援 HTTP->HTTPS 重新導向？**

支援重新導向。 請瀏覽[應用程式閘道重新導向概觀](application-gateway-redirect-overview.md)toolearn 更多。

**問：接聽程式的處理順序為何？**

接聽程式的處理順序 hello 它們會顯示。 因此，如果基本接聽程式符合傳入的要求，就會先處理它。  基本的接聽程式 tooensure 流量路由的 toohello 正確後端之前，應該設定多站台接聽程式。

**問：哪裡可找到應用程式閘道的 IP 和 DNS？**

時使用的公用 IP 位址做為端點，這項資訊可以 hello 入口網站中的 hello 應用程式閘道 hello 公用 IP 位址資源或 hello 概觀 頁面上找到。 內部 IP 位址，這可以找到 hello 概觀 頁面上。

**問：沒有 hello IP 或 DNS 變更 hello 存留期的 hello 應用程式閘道嗎？**

如果 hello 閘道就會停止並啟動 hello 客戶，可以變更 hello VIP。 hello 與應用程式閘道相關聯的 DNS 不會變更在 hello 生命週期的 hello 閘道。 基於這個理由，是建議 toouse CNAME 別名，而且它指向 hello 應用程式閘道 toohello DNS 位址。

**問：應用程式閘道是否支援靜態 IP？**

否，應用程式閘道不支援靜態公用 IP 位址，但是支援靜態內部 IP。

**問：應用程式閘道支援在多個公用 Ip 上 hello 閘道嗎？**

應用程式閘道只支援一個公用 IP 位址。

**問：應用程式閘道是否支援 x-forwarded-for 標頭？**

是，應用程式閘道插入 x 轉送如，x-轉送-通訊協定，且 x 轉送埠 hello 要求標頭轉送 toohello 後端。 x 轉送的標頭的 hello 格式是 IP:Port 的逗號分隔清單。 hello x 轉送 proto 有效值為 http 或 https。 X 轉送埠指定 hello 達 hello 應用程式閘道的 hello 要求連接埠。

**問：多久花費 toodeploy 應用程式閘道？進行更新時，我的應用程式閘道是否仍有作用？**

新的應用程式閘道部署可能會佔用 too20 分鐘 tooprovision。 變更 tooinstance 大小/計數不會干擾性，而且 hello 閘道會在這段期間保持使用中。

## <a name="configuration"></a>組態

**問：應用程式閘道一律部署在虛擬網路中？**

是，應用程式閘道一律部署在虛擬網路子網路中。 這個子網路只包含應用程式閘道。

**問：應用程式閘道可以討論其虛擬網路外的 tooinstances 嗎？**

應用程式閘道可以與 tooinstances hello 處於只要 IP 連線的虛擬網路外部通訊。 如果您計劃 toouse 內部 Ip 後端集區的成員，則需要[對等互連的 VNET](../virtual-network/virtual-network-peering-overview.md)或[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。

**問：我可以部署 hello 應用程式閘道子網路中的其他任何項目嗎？**

否，但您可以部署 hello 子網路中的其他應用程式閘道。

**問：為支援 hello 應用程式閘道子網路上的網路安全性群組？**

Hello 應用程式閘道子網路都支援網路安全性群組以 hello 下列限制：

* 例外狀況必須放在連入流量的連接埠 65503 65534 的後端健全狀況 toowork 正確。

* 不會封鎖輸出網際網路連線。

* 必須允許從 hello AzureLoadBalancer 標記的流量。

**問：Hello 限制應用程式閘道有哪些？是否可以增加這些限制？**

請瀏覽[應用程式閘道限制](../azure-subscription-service-limits.md#application-gateway-limits)tooview hello 限制。

**問：是否可以同時對外部和內部流量使用應用程式閘道？**

是，應用程式閘道支援每個應用程式閘道擁有具有一個內部 IP 和一個外部 IP。

**問：是否支援 VNet 對等互連？**

是，支援 VNet 對等互連，這對於平衡其他虛擬網路中的流量負載很有幫助。

**問：當他們透過 ExpressRoute 或 VPN 通道連接時可以說話 tooon 內部部署伺服器嗎？**

是，只有流量允許即可。

**問：是否可有一個為不同連接埠上的許多應用程式提供服務的後端集區？**

支援微服務架構。 您必須在不同的連接埠上的多個 http 設定 tooprobe。

**問：自訂探查是否支援回應資料使用萬用字元/regex？**

自訂探查不支援回應資料使用萬用字元或 regex。 

**問：規則的處理方式為何？**

規則的處理順序 hello 設定。 建議先流量的基本規則 tooreduce hello 機率為 hello 的基本規則將會比對所評估的連接埠先前 toohello 多站台規則為基礎的流量路由傳送 toohello 不適當的後端設定的多站台規則。

**問：規則的處理方式為何？**

規則的處理順序 hello 建立。 建議在基本規則前面設定多網站規則。 藉由第一次設定多站台接聽程式，此組態可以減少流量是路由的 toohello 不適當的後端的 hello 機會。 此路由問題可能是因為 hello 的基本規則將會比對所評估的連接埠先前 toohello 多站台規則為基礎的流量。

**問：自訂探查 hello [主機] 欄位代表什麼？**

主機 欄位指定用於 hello 名稱 toosend hello 探查。 只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。 此值與 VM 主機名稱不同，其格式為 \<protocol\>://\<host\>:\<port\>\<path\>。

**問：我可以白名單應用程式閘道存取 tooa 少來源 Ip？**

使用應用程式閘道子網路上的 NSG 可以完成此案例。 依優先順序列出 hello hello 子網路上應 hello 下列限制：

* 允許來源 IP/IP 範圍的傳入流量。

* 允許來自所有來源 tooports 65503 65534 的連入要求[後端健全狀況通訊](application-gateway-diagnostics.md)。

* 允許連入的 Azure 負載平衡器探查 （AzureLoadBalancer 標籤），輸入虛擬網路流量 （VirtualNetwork 標籤） 上 hello [NSG](../virtual-network/virtual-networks-nsg.md)。

* 使用「全部拒絕」規則封鎖所有其他傳入流量。

* 允許輸出流量 toohello 所有目的地的網際網路。

## <a name="performance"></a>效能

**問：應用程式閘道如何支援高可用性和延展性？**

如果您已部署 2 個以上的執行個體，應用程式閘道即可支援高可用性案例。 Azure 會將這些執行個體分散到所有執行個體不會在 hello 失敗的更新和錯誤網域 tooensure 相同的時間。 應用程式閘道支援延展性 hello 多個執行個體加入相同的閘道 tooshare hello 負載。

**問：如何利用應用程式閘道跨越資料中心封存 DR 案例？**

客戶可以使用 Traffic Manager toodistribute 流量，跨不同資料中心內的多個應用程式閘道。

**問：是否支援自動調整大小？**

否，但應用程式閘道有可能是使用的 tooalert 輸送量度量達到臨界值時。 手動新增執行個體，或變更大小不會重新啟動 hello 閘道，並不會影響現有的流量。

**問：手動相應增加/相應減少會造成停機嗎？**

不會停機，執行個體已分散於升級網域和容錯網域。

**問：可以變更執行個體大小而不中斷的中型 toolarge 從嗎？**

是，Azure 將執行個體分散到所有執行個體不會在 hello 失敗的更新和錯誤網域 tooensure 相同的時間。 藉由新增多個執行個體調整應用程式閘道支援 hello 相同閘道 tooshare hello 負載。

## <a name="ssl-configuration"></a>SSL 組態

**問：應用程式閘道支援哪些憑證？**

支援自我簽署憑證、CA 憑證和萬用字元憑證。 不支援 EV 憑證。

**問：Hello 目前的加密套件支援的應用程式閘道有哪些？**

hello 下面是 hello 應用程式閘道支援目前的加密套件。 請造訪：[設定 SSL 的原則版本和應用程式閘道上的加密套件](application-gateway-configure-ssl-policy-powershell.md)toolearn 如何 toocustomize SSL 選項。

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

**問：應用程式閘道也支援流量 toohello 後端重新加密？**

[是]，應用程式閘道支援 SSL 卸載，並結束 tooend SSL，重新加密 hello 流量 toohello 後端。

**問：可以設定 SSL 原則 toocontrol SSL 通訊協定版本嗎？**

是，您可以設定應用程式閘道 toodeny TLS1.0、 TLS1.1 和 TLS1.2。 SSL 2.0 和 3.0 都已預設停用並，無法加以設定。

**問：可以設定加密套件和原則的順序嗎？**

是，支援[加密套件的設定](application-gateway-ssl-policy-overview.md)。 定義自訂的原則，必須啟用至少一個 hello 遵循加密套件。 應用程式閘道會使用 SHA256 toofor 後端管理。

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**問：支援多少個 SSL 憑證？**

向上 too20 SSL 憑證支援。

**問：針對後端重新加密支援多少個驗證憑證？**

向上 too10 驗證憑證支援的預設值是 5。

**問：應用程式閘道是否原本就與 Azure Key Vault 整合？**

不，它並未與 Azure Key Vault 整合。

## <a name="web-application-firewall-waf-configuration"></a>Web 應用程式防火牆 (WAF) 組態

**問：Hello WAF SKU 是否提供以 hello 標準 SKU 所有 hello 功能？**

是，WAF 支援所有的 hello 功能 hello 標準 SKU 中。

**問：什麼是應用程式閘道支援的 hello CRS 版本？**

應用程式閘道支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 和 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)。

**問：如何監視 WAF？**

WAF 是透過診斷記錄功能來監視，如需診斷記錄的詳細資訊，請參閱[應用程式閘道的診斷記錄和計量](application-gateway-diagnostics.md)

**問：偵測模式是否會封鎖流量？**

否，偵測模式只會記錄觸發 WAF 規則的流量。

**問：如何自訂 WAF 規則？**

是，WAF 規則都可自訂的如需有關如何 toocustomize 它們瀏覽[自訂 WAF 規則群組與規則](application-gateway-customize-waf-rules-portal.md)

**問：目前可使用哪些規則？**

WAF 目前支援 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229)和[3.0](application-gateway-crs-rulegroups-rules.md#owasp30)，提供對大部分的 hello 的基準安全性 hello 開啟 Web 應用程式安全性專案 (OWASP)，請參閱所識別的前 10 個弱點[OWASP 前 10 個弱點](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

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

- **ApplicationGatewayAccessLog** -hello 存取記錄檔包含每個要求送出 toohello 應用程式閘道前端。 hello 資料包括 hello 呼叫者的 IP，URL 要求，回應延遲，和縮小傳回碼，位元組。每隔 300 秒會收集一次存取記錄檔。 此記錄檔包含每個應用程式閘道執行個體的一筆記錄。
- **ApplicationGatewayPerformanceLog** -hello 效能記錄檔擷取針對每個執行個體包括總計要求提供服務，以位元組為單位的輸送量效能資訊、 總計要求提供服務的失敗的要求計數，狀況良好和狀況不良後端執行個體計數。
- **ApplicationGatewayFirewallLog** -hello 防火牆記錄檔包含透過偵測或防止應用程式閘道以 web 應用程式的防火牆設定的模式所記錄的要求。

**問：如何知道我的後端集區成員狀態良好？**

您可以使用 hello PowerShell cmdlet`Get-AzureRmApplicationGatewayBackendHealth`或透過 hello 入口網站的健全狀況驗證造訪[應用程式閘道診斷](application-gateway-diagnostics.md)

**問：Hello hello 診斷記錄檔上的保留原則是什麼？**

診斷記錄流程 toohello 客戶儲存體帳戶和客戶可以設定 hello 保留原則，根據其喜好設定。 診斷記錄檔也可以傳送 tooan 事件中心] 或 [記錄分析。 如需詳細資訊，請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)。

**問：如何取得應用程式閘道的稽核記錄檔？**

稽核記錄檔可用於應用程式閘道。 在 hello 入口網站中，按一下 **活動記錄檔**在 hello 功能表刀鋒視窗中的應用程式閘道 tooaccess hello 稽核記錄檔。 

**問：是否可以設定應用程式閘道的警示？**

是，應用程式閘道可以支援警示，並可將警示設定為關閉計量。  應用程式閘道目前沒有 「"輸送量，輸送量的可設定的 tooalert 公制。 toolearn 進一步了解警示，請瀏覽[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

**問：後端健康情況傳回不明狀態，什麼導致這個狀態？**

hello 最常見的原因是 NSG 或自訂 DNS 正在封鎖存取 toohello 後端。 請瀏覽[後端健全狀況、 診斷記錄和度量的應用程式閘道](application-gateway-diagnostics.md)toolearn 更多。

## <a name="next-steps"></a>後續步驟

有關應用程式閘道的詳細資訊請造訪的 toolearn[簡介 tooApplication 閘道](application-gateway-introduction.md)。
