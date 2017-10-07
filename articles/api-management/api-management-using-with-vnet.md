---
title: "虛擬網路的 aaaHow toouse Azure API 管理"
description: "了解如何 toosetup 連接 tooa 虛擬網路在 Azure API 管理及存取 web 服務透過它。"
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>如何搭配虛擬網路的 toouse Azure API 管理
Azure 虛擬網路 (Vnet) 可讓您 tooplace 任何非網際網路 routeable 網路而您控制在您的 Azure 資源存取權。 這些網路接著可以使用各種不同的 VPN 技術 tooyour 連線在內部部署網路。 有關 Azure 虛擬網路的詳細資訊與 hello 資訊開始的 toolearn: [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。

您可以 hello 虛擬網路 (VNET)，內部部署 azure API 管理，讓它能夠存取 hello 網路中的後端服務。 hello 開發人員入口網站和 API 閘道，可以設定的 toobe 從 hello 網際網路或只在 hello 虛擬網路內存取。

> [!NOTE]
> Azure API 管理支援傳統和 Azure Resource Manager Vnet。
>
>

## <a name="enable-vpn"> </a>啟用 VNET 連線
> [!NOTE]
> VNET 連線位於 hello **Premium**和**開發人員**層。 hello 層之間 tooswitch hello Azure 入口網站中開啟您的 API 管理服務，然後再開啟 hello**小數位數和定價** 索引標籤。在 hello**定價層**區段中，選取 hello Premium 或開發人員階層，然後按一下 儲存。
>

tooenable VNET 連線能力，在 hello Azure 入口網站中開啟您的 API 管理服務，並開啟 hello**虛擬網路**頁面。

![API 管理的虛擬網路功能表][api-management-using-vnet-menu]

選取所需的 hello 存取類型：

* **外部**: hello API 管理閘道和開發人員入口網站進行存取 hello 外部負載平衡器透過公用網際網路。 hello 閘道可以存取 hello 虛擬網路內的資源。

![公用對等互連][api-management-vnet-public]

* **內部**: hello API 管理閘道和開發人員入口網站會透過內部負載平衡器的 hello 虛擬網路只能從存取。 hello 閘道可以存取 hello 虛擬網路內的資源。

![私人對等互連][api-management-vnet-private]

您現在會看見佈建 API 管理服務所在的所有區域的清單。 為每個區域選取 VNET 和子網路。 hello 清單會填入傳統和資源管理員會安裝在您要設定的 hello 地區您 Azure 訂用帳戶中可用的虛擬網路。

> [!NOTE]
> **服務端點**hello 上面圖表中包含閘道/Proxy、 發行者入口網站、 開發人員入口網站、 GIT、 和 hello 直接管理端點。
> **管理端點**hello 上面圖表中是透過 Azure 入口網站和 Powershell hello 服務 toomanage 組態上所裝載的 hello 端點。
> 另請注意，，，即使 hello 圖表顯示其各種端點的 API 管理服務的 IP 位址**只**回應其設定的主機名稱。

> [!IMPORTANT]
> 在部署 Azure API 管理執行個體 tooa 資源管理員的 VNET，hello 服務必須是不包含 Azure API 管理執行個體以外的任何其他資源的專用子網路。 如果嘗試 toodeploy Azure API 管理執行個體 tooa 資源管理員 VNET 子網路，其中包含其他資源，hello 部署將會失敗。
>
>

![選取 VPN][api-management-setup-vpn-select]

按一下**儲存**頂端 hello 囉 」 畫面。

> [!NOTE]
> hello hello API 管理執行個體的 VIP 位址將會變更每個 VNET 已啟用或停用的時間。  
> API 管理從移動時，也會變更 hello VIP 位址**外部**太**內部**或反之亦然
>


> [!IMPORTANT]
> 如果您移除 VNET 中的 API 管理，或變更其中一個部署中的 hello，hello 先前使用過的 VNET，可以保持鎖定 too4 時數。 在這段期間將不會是可能 toodelete hello VNET 或部署新的資源 tooit。

## <a name="enable-vnet-powershell"> </a>使用 PowerShell cmdlet 來啟用 VNET 連線
您也可以啟用使用 hello PowerShell cmdlet 的 VNET 連線

* **建立 API 管理服務內 VNET**： 使用 hello cmdlet[新增 AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate VNET 內的 Azure API 管理服務。

* **部署在 VNET 內現有的 API 管理服務**： 使用 hello cmdlet[更新 AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove 虛擬網路內現有的 Azure API 管理服務。

## <a name="connect-vnet"></a>Tooa web 服務裝載於虛擬網路連接
API 管理服務連線的 toohello VNET 後，存取在其中的後端服務並無不同存取公用服務。 只要輸入 hello 本機 IP 位址或 hello 主機名稱 （如果 DNS 伺服器設定為 hello VNET） 您的 web 服務中 hello **Web 服務 URL**欄位建立新的應用程式開發介面時，或編輯現有的 fgpp。

![透過 VPN 加入 API][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"> </a>常見的網路組態問題
以下是將 API 管理服務部署到虛擬網路時可能發生的常見錯誤設定問題清單。

* **自訂的 DNS 伺服器安裝**: hello 的 API 管理服務取決於數個 Azure 服務。 API 管理裝載在自訂的 DNS 伺服器的 VNET，當需要這些 Azure 服務 tooresolve hello 主機名稱。 請遵循 [這份](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 有關自訂 DNS 設定的指引。 請參閱表的 hello 連接埠及其他參考的網路需求。

> [!IMPORTANT]
> 我們建議您，如果您使用自訂 DNS 伺服器 hello VNET，您將設定的**之前**部署到其中的 API 管理服務。 否則您需要太 hello API 管理服務每次變更 hello DNS 伺服器 (s) 執行更新 hello[套用網路組態設定作業](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **API 管理所需的連接埠**： 輸入與輸出流量至 API 管理以部署的 hello 子網路可以使用控制[網路安全性群組][Network Security Group]。 如果這些連接埠中有任何一個無法使用，「API 管理」可能就無法正常運作而可能變成無法存取。 搭配 VNET 使用 API 管理時，封鎖這其中一或多個連接埠是另一個常見的錯誤組態問題。

API 管理服務執行個體裝載在 VNET 中，會使用 hello hello 下表中的連接埠。

| 來源 / 目的地連接埠 | 方向 | 傳輸通訊協定 | 目的 | 來源 / 目的地 | 存取類型 |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |輸入 |TCP |用戶端通訊 tooAPI 管理 |INTERNET / VIRTUAL_NETWORK |外部 |
| * / 3443 |輸入 |TCP |Azure 入口網站和 PowerShell 的管理端點 |INTERNET / VIRTUAL_NETWORK |外部和內部 |
| * / 80, 443 |輸出 |TCP |與「Azure 儲存體」和「Azure 服務匯流排」的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| * / 1433 |輸出 |TCP |與 Azure SQL 的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| * / 11000 - 11999 |輸出 |TCP |與 Azure SQL V12 的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| * / 14000 - 14999 |輸出 |TCP |與 Azure SQL V12 的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| * / 5671 |輸出 |AMQP |記錄 tooEvent 中樞原則和監視的代理程式的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| 6381 - 6383 / 6381 - 6383 |輸入和輸出 |UDP |與「Redis 快取」的相依性 |VIRTUAL_NETWORK / VIRTUAL_NETWORK |外部和內部 |-
| * / 445 |輸出 |TCP |與「適用於 GIT 的 Azure 檔案共用」的相依性 |VIRTUAL_NETWORK / INTERNET |外部和內部 |
| * / * | 輸入 |TCP |Azure 基礎結構負載平衡器 | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |外部和內部 |

* **SSL 功能**： 鏈結建立和驗證 hello API 管理服務需要輸出網路連線 tooocsp.msocsp.com、 mscrl.microsoft.com 以及 crl.microsoft.com tooenable SSL 憑證。如果您上傳 tooAPI 管理任何憑證包含 hello 完整鏈結 toohello CA 根，則不需要，此相依性。

* **DNS 存取**：需要有連接埠 53 的輸出存取，才能與 DNS 伺服器通訊。 如果自訂的 DNS 伺服器上有 hello 另一端的 VPN 閘道，hello DNS 伺服器必須是裝載 API 管理的 hello 子網路觸達。

* **度量和健全狀況監視**： 輸出網路連線 tooAzure 監視端點，但在 hello 下列網域解析： global.metrics.nsatc.net、 shoebox2.metrics.nsatc.net、 prod3.metrics.nsatc.net。

* **快速路由安裝**： 常見的客戶設定是 toodefine 強制傳出網際網路流量 tooinstead 資料流程在內部自己預設路由 (0.0.0.0/0)。 此流量必定中斷連線，使用 Azure API 管理，因為 hello 傳出流量會被封鎖在內部，或 NAT 的 tooan 無法辨識無法再使用不同的 Azure 端點的位址集。 hello 解決方案是 toodefine 一個 （或更多） 使用者定義的路由 ([UDRs][UDRs]) 包含 hello Azure API 管理的 hello 子網路上。 UDR 定義特定子網路的路由，則會採用而不是 hello 預設路由。
  可能的話，我們建議下列組態 toouse hello:
 * hello ExpressRoute 組態通告 0.0.0.0/0，並依預設強制通道連接所有輸出流量的內部。
 * 包含 hello Azure API 管理的 hello UDR 套用 toohello 子網路都會定義 0.0.0.0/0 與網際網路的下一個躍點類型。
 hello 聯合的影響這些步驟是，hello 子網路層級 UDR 優先於 hello ExpressRoute 強制通道，以確保從 hello Azure API 管理的對外網際網路存取。

>[!WARNING]  
>Azure API 管理不支援使用 ExpressRoute 組態，**不正確地跨通告 hello 公用互連路徑 toohello 私用對等互連路徑路由**。 已設定公用對等互連的 ExpressRoute 組態，會收到來自 Microsoft 的一大組 Microsoft Azure IP 位址範圍的路由通告。 如果這些位址範圍不正確地跨通告 hello 私用對等互連路徑上，hello 最終結果是從 hello Azure API 管理執行個體的子網路的所有輸出網路封包會不正確地使用強制通道 tooa 客戶的內部部署網路基礎結構。 這個網路流量會中斷 Azure API 管理。 hello 方案 toothis 問題是 toostop 跨廣告 hello 公用互連路徑 toohello 私用對等互連路徑路由。


## <a name="troubleshooting"></a>疑難排解
變更 tooyour 網路時，請參閱太[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus)，toovalidate 如果 hello API 管理服務未中斷的 hello 存取 tooany 重要的資源，其定義取決於它。 應該每隔 15 分鐘更新 hello 連線狀態。

## <a name="limitations"> </a>限制
* 包含「API 管理」執行個體的子網路無法包含任何其他 Azure 資源類型。
* hello 子網路和 hello API 管理服務必須在 hello 相同訂用帳戶。
* 包含「API 管理」執行個體的子網路無法跨訂用帳戶移動。
* 當使用內部虛擬網路，就可以從內部 IP 位址僅 hello 範圍中所述[RFC 1918](https://tools.ietf.org/html/rfc1918)，無法提供的公用 IP 位址。
* 多區域 API 管理部署中，與內部虛擬網路設定，使用者必須負責管理他們自己的負載平衡它們擁有 hello DNS。


## <a name="related-content"> </a>相關內容
* [連接虛擬網路 toobackend 使用 Vpn 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [從不同的部署模型連接虛擬網路](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Toouse hello API Inspector tootrace 如何呼叫在 Azure API 管理](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
