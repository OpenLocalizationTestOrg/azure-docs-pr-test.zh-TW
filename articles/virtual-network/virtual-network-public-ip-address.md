---
title: "aaaCreate，變更或刪除 Azure 的公用 IP 位址 |Microsoft 文件"
description: "了解如何 toocreate，變更或刪除公用 IP 位址。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>建立、變更或刪除公用 IP 位址

深入了解公用 IP 位址以及 toocreate，如何變更及刪除其中一個。 公用 IP 位址是可加以設定的資源。 指派的公用 IP 位址 tooother Azure 資源，可讓：
- 傳入網際網路連線 tooresources，例如 Azure 虛擬機器 (VM)、 Azure 虛擬機器擴展集、 Azure VPN 閘道，應用程式閘道以及網際網路對向 Azure 負載平衡器。 Azure 資源無法接收輸入的通訊 hello 網際網路不含指派的公用 IP 位址。 本質上就可透過公用 IP 位址存取某些 Azure 資源時，其他資源必須指派 toothem toobe hello 網際網路從可以存取的公用 IP 位址。
- 輸出連線 toohello 網際網路使用可預測的 IP 位址。 例如，虛擬機器可以通訊輸出 toohello 網際網路沒有公用的 IP 位址指派 tooit，但其位址是由 Azure tooan 無法預期的公用位址轉譯的網路位址。 指派公用 IP 位址 tooa 資源可讓您 tooknow hello 輸出連線所使用的 IP 位址。 雖然可預測，hello 位址可能變更，根據選擇的 hello 分派方法。 如需詳細資訊，請參閱＜[建立公用 IP 位址](#create-a-public-ip-address)＞。 深入了解 Azure 資源，讀取 hello 傳出連線 toolearn[了解輸出連線](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。

## <a name="before-you-begin"></a>開始之前

這份文件的任何部分中的步驟完成 hello 之前完成任何下列工作：

- 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)文章 toolearn 關於公用 IP 位址的限制。
- 登入 toohello Azure[入口網站](https://portal.azure.com)，Azure 命令列介面 (CLI) 或 Azure PowerShell 的 Azure 帳戶。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果使用 PowerShell 命令在本文中 toocomplete 工作[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell 指令程式，安裝最新版本。 tooget 說明的 PowerShell 命令，與範例中，輸入`get-help <command> -full`。
- 如果使用 Azure 命令列介面 (CLI) 命令 toocomplete 工作，在本文中[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)。

公用 IP 位址需要少許費用。 tooview hello 定價，讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 

## <a name="create-a-public-ip-address"></a>建立公用 IP 位址

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*公用 ip 位址*。 當**公用 IP 位址**會出現在 hello 搜尋結果中，按一下它。
3. 按一下**+ 加**在 hello**公用 IP 位址**刀鋒視窗中出現。
4. 輸入或選取 hello 遵循 hello 中的設定的值，**建立公用 IP 位址**刀鋒視窗中出現，然後按一下**建立**:

    |設定|必要？|詳細資料|
    |---|---|---|
    |名稱|是|hello 名稱必須是唯一您選取的 hello 資源群組中。|
    |IP 版本|是| 選取 IPv4 或 IPv6。 公用 IPv4 位址可以指派 tooseveral Azure 資源，而 IPv6 公用 IP 位址可以只指派 tooan 網際網路對向負載平衡器。 hello 負載平衡器可以載入平衡 IPv6 流量 tooAzure 虛擬機器。 深入了解[負載平衡 IPv6 流量 toovirtual 機器](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。
    |IP 位址指派|是|**動態：**動態位址會指派只 hello 公用 IP 位址相關聯後 tooa NIC 附加 tooa VM，hello VM 啟動 hello 第一次。 動態位址可以變更 hello VM hello NIC 是否附加的 toois 停止 （取消配置）。 hello 位址會維持 hello 相同如果 hello VM 會重新啟動或停止 （但不是會取消配置）。 **靜態：**建立 hello 公用 IP 位址時，會指派靜態位址。 靜態位址進行不變更甚至如果 hello VM 放在 hello 停止 （取消配置） 狀態。 刪除 hello NIC 時，只會釋放 hello 位址。 建立 hello NIC 後，您可以變更 hello 分派方法。 如果您選取 IPv6 hello **IP 版本**，hello 只能指派方法**動態**。|
    |閒置逾時 (分鐘)|否|不需依賴用戶端 toosend 保持運作訊息的 TCP 或 HTTP 連線開啟的 tookeep 分鐘數。 如果您選取 IPv6 作為 **IP 版本**，則無法變更此值。 |
    |DNS 名稱標籤|否|內必須是唯一 hello （跨越所有訂用帳戶及所有客戶） 建立 hello 名稱中的 Azure 位置。 hello Azure 公用 DNS 服務會自動註冊 hello 名稱和 IP 位址，讓您能連接 tooa 資源 hello 名稱。 Azure 會將附加*location.cloudapp.azure.com* toohello 名稱您完全提供 toocreate hello （其中位置是您選取的 hello 位置） 限定 DNS 名稱。 如果您選擇 toocreate 這兩個位址版本，hello 相同的 DNS 名稱會指派 tooboth hello IPv4 和 IPv6 位址。 hello Azure DNS 服務包含 IPV4 和 IPv6 AAAA 名稱記錄，然後 hello DNS 名稱查閱兩筆記錄會回應。 hello 用戶端選擇使用哪一個位址 （IPv4 或 IPv6） toocommunicate。|
    |建立 IPv6 (或 IPv4) 位址|否| 顯示 IPv6 或 IPv4 取決於您選取的 **IP 版本**。 例如，如果您選取 **IPv4** 作為 **IP 版本**，則此處會顯示 **IPv6**。
    |名稱 (如果您核取 hello 唯一可見**建立 IPv6 （或 IPv4） 位址**核取方塊)|是，如果您選取 hello**建立 IPv6** （或 IPv4） 核取方塊。|hello 名稱必須與您第一次輸入 hello hello 名稱不同**名稱**這份清單中。 如果 IPv4 和 IPv6 位址，您可以選擇 toocreate，hello 入口網站會建立兩個個別公用 IP 位址資源，與指派 tooit 每個 IP 位址版本的其中一個。|
    |IP 位址指派 (只有當您核取 hello 看得到**建立 IPv6 （或 IPv4） 位址**核取方塊)|是，如果您選取 hello**建立 IPv6** （或 IPv4） 核取方塊。|如果 hello 核取方塊顯示**建立 IPv4 位址**，您可以選擇指派方法。 如果 hello 核取方塊顯示**建立 IPv6 位址**，您無法選取指派方法，因為它必須**動態**。|
    |訂用帳戶|是|必須存在於 hello 相同[訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)hello 資源為您想要 tooassociate hello 公用 IP 位址。|
    |資源群組|是|可以存在於相同或不同，hello[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)hello 資源為您想要 tooassociate hello 公用 IP 位址。|
    |位置|是|必須存在於 hello 相同[位置](https://azure.microsoft.com/regions)，為您想要 tooassociate hello 公用 IP 位址的 hello 資源，也稱為 tooas 區域。|

**命令**

雖然 hello 入口網站提供 hello 選項 toocreate 兩個公用 IP 位址資源 （一個 IPv4 和一個 IPv6），hello 遵循 CLI 和 PowerShell 命令建立一個資源位址的 IP 版本或 hello 其他。 如果您想要的兩個公用 IP 位址資源，其中每個 IP 版本，您必須執行 hello 命令兩次，指定不同的名稱和 hello 公用 IP 位址資源的版本。 

|工具|命令|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>檢視、變更公用 IP 位址的設定，或刪除公用 IP 位址

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*公用 ip 位址*。 當**公用 IP 位址**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**公用 IP 位址**刀鋒視窗中，按一下 hello hello 公用 IP 位址名稱想 tooview、 變更設定，或刪除。
4. 在 hello 刀鋒視窗中顯示 hello 的公用 IP 位址，而完成的其中一個 hello 下列選項取決於您 tooview，刪除或變更 hello 公用 IP 位址。
    - **檢視**: hello**概觀**hello 刀鋒視窗的區段會顯示 hello 公用 IP 位址設定，例如 hello 網路介面它有相關聯的太 （如果 hello 位址相關聯的 tooa 網路介面）。 hello 入口網站不會顯示 hello 版本 hello 位址 （IPv4 或 IPv6）。 tooview hello 版本資訊，使用 hello PowerShell 或 CLI 命令 tooview hello 公用 IP 位址。 如果 hello 的 IP 位址版本是 IPv6，hello 指派位址不會顯示 hello 入口網站、 PowerShell 或 hello CLI。 
    - **刪除**: toodelete hello 公用 IP 位址，按一下 [**刪除**在 hello**概觀**hello] 刀鋒視窗的區段。 如果 hello 位址是目前相關聯的 tooan IP 設定，無法刪除。 如果目前與組態相關聯 hello 位址，請按一下**中斷**toodissociate hello 位址從 hello IP 組態。
    - **變更**：按一下 [組態]。 變更使用中的 hello 步驟 4 hello 資訊設定[建立公用 IP 位址](#create-a-public-ip-address)本文一節。 toochange hello 分派從 toodynamic 靜態 IPv4 位址，您必須先中斷關聯至相關聯的 hello IP 組態的 hello 公用 IPv4 位址。 您可以變更 hello 分派方法 toodynamic 並按一下**關聯**tooassociate hello IP 位址 toohello 相同 IP 設定、 不同的組態，或您可以將它保留取消關聯。 公用 IP 位址，在 hello toodissociate**概觀**區段中，按一下**中斷**。

>[!WARNING]
>在您從靜態 toodynamic hello 分派方法時，您會遺失 hello toohello 公用 IP 位址指派的 IP 位址。 雖然 hello Azure 公用 DNS 伺服器維護靜態或動態位址與任何 DNS 名稱標籤 （如果有定義一個） 之間的對應，hello VM 啟動之後在 hello 正在停止 （取消配置） 狀態時，就可能會變更為動態 IP 位址。 tooprevent hello 位址變更，指派靜態 IP 位址。

**命令**

|工具|命令|
|---|---|
|CLI|[az 網路的公用 ip 清單](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list)toolist 公用 IP 位址， [az 網路公用-ip-顯示](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show)tooshow 設定;[az 網路公用 ip 更新](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update)tooupdate;[az 網路公用 ip 刪除](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)toodelete|
|PowerShell|[Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve 公用 IP 位址物件，並檢視其設定[組 AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate 設定;[移除 AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>後續步驟
建立 hello 下列 Azure 資源時指派的公用 IP 位址：

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 虛擬機器
- [網際網路面向的 Azure Load Balancer](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure 應用程式閘道](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [使用 Azure VPN 閘道的站對站連線](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure 虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
