---
title: "aaaConfigure Azure 網路介面的 IP 位址 |Microsoft 文件"
description: "了解如何 tooadd、 變更及移除網路介面的私人和公用 IP 位址。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>新增、變更或移除 Azure 網路介面的 IP 位址

了解如何 tooadd、 變更及移除網路介面的公用和私用 IP 位址。 私用 IP 位址指派 tooa 網路介面啟用虛擬機器 toocommunicate 與 Azure 虛擬網路和連線的網路中的其他資源。 私人 IP 位址也可讓連出通訊 toohello 網際網路使用無法預期的 IP 位址。 A[公用 IP 位址](virtual-network-public-ip-address.md)指派 tooa 網路介面可讓從 hello 網際網路輸入的通訊 tooa 虛擬機器。 hello 位址也可讓從 hello 虛擬機器 toohello 網際網路使用可預測的 IP 位址的連出通訊。 如需詳細資訊，請參閱[了解 Azure 中的輸出連線](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 

如果您需要 toocreate，變更或刪除網路介面，讀取 hello[管理網路介面](virtual-network-network-interface.md)發行項。 如果您需要 tooadd 網路介面 tooor 移除網路介面，從虛擬機器，請閱讀 hello[新增或移除網路介面](virtual-network-network-interface-vm.md)發行項。 


## <a name="before-you-begin"></a>開始之前

這份文件的任何部分中的步驟完成 hello 之前完成任何下列工作：

- 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)文章 toolearn 有關公用與私人 IP 位址的限制。
- 登入 toohello Azure[入口網站](https://portal.azure.com)，Azure 命令列介面 (CLI) 或 Azure PowerShell 的 Azure 帳戶。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果使用 PowerShell 命令在本文中 toocomplete 工作[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell 指令程式，安裝最新版本。 tooget 說明的 PowerShell 命令，與範例中，輸入`get-help <command> -full`。
- 如果使用 Azure 命令列介面 (CLI) 命令 toocomplete 工作，在本文中[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)。

## <a name="add-ip-addresses"></a>新增 IP 位址

您可以將它新增為許多[私人](#private)和[公用](#public) [IPv4](#ipv4)為必要 tooa 網路介面，hello 的限制範圍內的位址列在 hello [Azure 的限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)發行項。 （雖然您可以使用 hello 入口 tooadd 私用的 IPv6 位址 tooa 網路介面，當您建立 hello 網路介面），您無法使用 hello 入口 tooadd IPv6 位址 tooan 現有網路介面。 您可以使用 PowerShell 或 hello CLI tooadd 私用的 IPv6 位址 tooone[次要 IP 設定](#secondary)（只要有任何現有的次要 ipconfiguration） 現有的網路介面不是連結 tooa 虛擬機器。 您無法使用任何工具 tooadd 公用的 IPv6 位址 tooa 網路介面。 如需使用 IPv6 位址的詳細資訊，請參閱 [IPv6](#ipv6)。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要針對 tooadd IPv4 位址的 hello 網路介面。
4. 按一下**IP 組態**在 hello**設定**hello 您選取的網路介面的 hello 刀鋒視窗的區段。
5. 按一下**+ 加**hello 刀鋒視窗中開啟的 IP 組態。
6. 指定 hello 下列項目，然後按一下**確定**tooclose hello**新增 IP 組態**刀鋒視窗中：

    |設定|必要？|詳細資料|
    |---|---|---|
    |名稱|是|必須是唯一的 hello 網路介面|
    |類型|是|因為您要新增的 IP 組態 tooan 現有網路介面，而且每個網路介面必須有[主要](#primary)IP 設定，唯一的選擇是**次要**。|
    |私人 IP 位址指派方法|是|[**動態**](#dynamic)位址可能變更，如果已經在 hello 停止 （取消配置） 的狀態之後，重新啟動 hello 虛擬機器。 Hello hello 子網路 hello 網路介面的位址空間的可用位址連接到 azure 的指派。 [**靜態**](#static)位址不釋放，直到刪除為止 hello 網路介面。 指定 hello 子網路位址空間範圍內，目前不使用另一個 IP 組態的 IP 位址。|
    |公用 IP 位址|否|**已停用：**沒有公用 IP 位址資源是目前相關聯的 toohello IP 組態。 **已啟用：**選取現有的 IPv4 公用 IP 位址，或建立一個新的。 toolearn toocreate 公用 IP 位址，如何讀取 hello[公用 IP 位址](virtual-network-public-ip-address.md#create-a-public-ip-address)發行項。|
7. 完成在 hello hello 指示，手動將次要私用 IP 位址 toohello 虛擬機器作業系統[指派多個 IP 位址的電腦作業系統 toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config)發行項。 請參閱[私人](#private)手動新增 IP 位址 tooa 虛擬機器作業系統之前的特殊考量的 IP 位址。 請勿將任何公用 IP 位址 toohello 虛擬機器的作業系統。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>變更 IP 位址設定

您可能需要 toochange hello 分派方法的 IPv4 位址，變更 hello 靜態 IPv4 位址，或變更 hello 公用 IP 位址指派 tooa 網路介面。 如果您要變更虛擬機器中的次要網路介面相關聯的次要 ipconfiguration 的 hello 私人 IPv4 位址 (深入了解[主要和次要網路介面](virtual-network-network-interface-vm.md#about))，虛擬位置 hello機器進入 hello 完成下列步驟的 hello 之前停止 （取消配置） 的狀態： 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要 tooview 或變更 IP 位址設定的 hello 的網路介面。
4. 按一下**IP 組態**在 hello**設定**hello 您選取的網路介面的 hello 刀鋒視窗的區段。
5. 按一下您想從 hello 刀鋒視窗中開啟的 IP 組態中的 hello 清單 toomodify hello IP 設定。
6. 變更 hello，所需的設定，使用在步驟 6 中的 hello hello 設定的 hello 資訊[新增的 IP 組態](#create-ip-config)本文一節。 按一下**儲存**tooclose hello IP 組態，您已變更的 hello 刀鋒視窗。

>[!NOTE]
>如果 hello 主要網路介面具有多個 IP 組態，而且您變更的主要 IP 設定 hello hello 私人 IP 位址，您必須以手動方式重新指派 hello 主要和次要 IP 位址 toohello 網路介面在 Windows (notfor Linux 必要）。 toomanually 指派 IP 位址 tooa 網路介面在作業系統中，讀取 hello[指派多個 IP 位址 toovirtual 機器](virtual-network-multiple-ip-addresses-portal.md#os-config)發行項。 請參閱[私人](#private)手動新增 IP 位址 tooa 虛擬機器作業系統之前的特殊考量的 IP 位址。 請勿將任何公用 IP 位址 toohello 虛擬機器的作業系統。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>移除 IP 位址

您可以移除[私人](#private)和[公用](#public)IP 位址從網路介面，但網路介面必須永遠有至少一個私人 IPv4 位址指派 tooit。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 讀取 hello [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)文章 toolearn 更多關於指派 tooaccounts 角色和權限。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*網路介面*。 當**網路介面**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**網路介面**刀鋒視窗中，按一下您想要從 tooremove IP 位址的 hello 網路介面。
4. 按一下**IP 組態**在 hello**設定**hello 您選取的網路介面的 hello 刀鋒視窗的區段。
5. 以滑鼠右鍵按一下[次要](#secondary)IP 設定 (您無法刪除 hello[主要](#primary)組態) 您想 toodelete，請按一下**刪除**，然後按一下  **[是]** tooconfirm hello 刪除。 如果 hello 組態具有公用 IP 位址資源相關聯 tooit、 hello 資源分開 hello IP 設定，但 hello 資源不會刪除。
6. 關閉 hello **IP 組態**刀鋒視窗。

**命令**

|工具|命令|
|---|---|
|CLI|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>IP 組態

[私用](#private)以及 （選擇性）[公用](#public)tooone 指派 IP 位址或多個 IP 組態指派 tooa 網路介面。 IP 組態有兩種：

### <a name="primary"></a>主要

每個網路介面都需指派一個主要 IP 組態。 主要 IP 組態：

- 具有[私人](#private) [IPv4](#ipv4) tooit 指派位址。 您無法將指定私用[IPv6](#ipv6)位址 tooa 主要 IP 設定。
- 也可能[公用](#public)IPv4 位址指派 tooit。 您無法指派公用 IPv6 位址 tooa 主要或次要 IP 設定。 不過您可以指派公用的 IPv6 位址 tooan Azure 負載平衡器，這可以負載平衡流量 tooa 虛擬機器的私用的 IPv6 位址。 如需詳細資訊，請參閱 [IPv6 的詳細資訊和限制](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations)。

### <a name="secondary"></a>次要

此外 tooa 主要 IP 設定網路介面可能有零個或多個次要 IP 組態指派 tooit。 次要 IP 組態：

- 必須有私用的 IPv4 或 IPv6 位址指派 tooit。 如果 hello 位址是 IPv6，hello 網路介面只可以有一個次要 IP 設定。 如果 hello 位址是 IPv4，hello 網路介面可能會有指派 tooit 的多個次要 IP 組態。 toolearn 有關 tooa 網路介面，可以指派多少的私人和公用 IPv4 位址的詳細資訊，請參閱 「 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)發行項。  
- 可能也有公用的 IPv4 位址指派 tooit，如果 hello 私人 IP 位址是 IPv4。 如果 hello 私人 IP 位址是 IPv6，您無法指派的公用 IPv4 或 IPv6 位址 toohello IP 組態。 指派多個 IP 位址 tooa 網路介面是在案例中很有幫助例如：
    - 在單一伺服器上，以不同 IP 位址和 SSL 憑證裝載多個網站或服務。
    - 做為網路虛擬設備 (例如防火牆或負載平衡器) 的虛擬機器。
    - hello 能力 tooadd 任何 hello 私人 IPv4 位址的任何 hello 網路介面 tooan Azure 負載平衡器後端集區。 在過去的 hello，只有 hello 主要 IPv4 位址 hello 主要網路介面無法新增 tooa 後端集區。 toolearn 深入了解如何 tooload 平衡多個 IPv4 組態，請參閱 hello[負載平衡多個 IP 組態](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。 
    - hello 能力 tooload 平衡一個 IPv6 位址指派的 tooa 網路介面。 toolearn 深入了解如何 tooload 平衡 tooa 私用的 IPv6 位址，請參閱 hello[負載的平衡的 IPv6 位址](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。


## <a name="address-types"></a>位址類型

您可以指派下列類型的 IP 位址 tooan hello [IP 組態](#ip-configurations):

### <a name="private"></a>私人

私用[IPv4](#ipv4)位址啟用虛擬機器 toocommunicate 與虛擬網路或其他連線的網路中的其他資源。 無法通訊，輸入虛擬機器也不可以 hello 虛擬機器通訊輸出具有私用[IPv6](#ipv6)位址，有一個例外狀況。 虛擬機器可以與 hello Azure 負載平衡器使用 IPv6 位址進行通訊。 如需詳細資訊，請參閱 [IPv6 的詳細資訊和限制](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations)。 

根據預設，hello Azure DHCP 伺服器指派 hello 私人 IPv4 位址[主要 IP 設定](#primary)hello 網路介面 toohello 網路介面的 hello 虛擬機器作業系統內。 除非必要，您應該永遠不會手動設定 hello hello 虛擬機器的作業系統內的網路介面的 IP 位址。 

> [!WARNING]
> 如果 hello 做 hello 主要 IP 位址的虛擬機器作業系統內的網路介面，hello 分派 toohello 主要 IP 設定 hello 主要網路介面的私人 IPv4 位址和以往不同設定的 IPv4 位址連接 tooa在 Azure 中的虛擬機器，您會失去連線能力 toohello 虛擬機器。

有必要 toomanually 設定 hello hello 虛擬機器的作業系統內的網路介面的 IP 位址所在的方案。 例如，您必須手動設定 Windows 作業系統的 hello 主要和次要 IP 位址加入多個 IP 位址 tooan Azure 虛擬機器時。 針對 Linux 虛擬機器，您可能只需要 toomanually 組 hello 次要的 IP 位址。 請參閱[新增 IP 位址 tooa VM 作業系統](virtual-network-multiple-ip-addresses-portal.md#os-config)如需詳細資訊。 當您手動設定 hello hello 作業系統內的 IP 位址時，建議您一律指派 hello 位址 toohello IP 網路介面設定使用 hello 靜態 （而非動態） 的分派方法。 指派 hello 位址使用 hello 靜態方法，可確保 hello 位址不會在 Azure 中變更。 如果您需要指派 tooan IP 組態的 toochange hello 位址，建議您：

1. tooensure hello 虛擬機器正在接收來自 hello Azure DHCP 伺服器的位址，變更 hello 作業系統和重新啟動 hello 虛擬機器中的 hello IP 位址後 tooDHCP hello 指派。
2. 停止 （取消配置） hello 虛擬機器。
3. 變更在 Azure 中的 hello IP 組態的 hello IP 位址。
4. 啟動 hello 虛擬機器。
5. [手動設定](virtual-network-multiple-ip-addresses-portal.md#os-config)hello 次要 IP hello 作業系統 （以及在 Windows hello 主要 IP 位址） 內的位址 toomatch 您在 Azure 中的設定。
 
依照 hello 先前的步驟，hello 私用 IP 位址指派 toohello 網路介面在 Azure 中，並在虛擬機器的作業系統，維持 hello 相同。 其中您手動設定 IP 位址內的作業系統，您訂用帳戶內的虛擬機器，請考慮加入 Azure tookeep 追蹤[標記](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)toohello 虛擬機器。 例如，您可以使用「IP 位址指派：靜態」。 如此一來，您可以輕鬆地找到 hello 虛擬機器您已經手動設定 hello IP 位址 hello 作業系統內您訂用帳戶內。

此外 tooenabling 虛擬機器 toocommunicate 與其他資源內 hello 相同，或已連線虛擬網路的私人 IP 位址也可讓虛擬機器 toocommunicate 輸出 toohello 網際網路。 輸出連接都是由 Azure tooan 無法預期的公用 IP 位址轉譯的來源網路位址。 深入了解 Azure 輸出的網際網路連線，讀取 hello toolearn [Azure 輸出的網際網路連線](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。 您無法將輸入的 tooa 虛擬機器的私人 IP 位址從 hello 網際網路進行通訊。

### <a name="public"></a>公開

公用 IP 位址啟用 hello 網際網路中的輸入的連線 tooa 虛擬機器。 傳出連接 toohello 網際網路使用可預期的 IP 位址。 如需詳細資訊，請參閱[了解 Azure 中的輸出連線](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 您可能會指派一個公用 IP 位址 tooan IP 設定，但不需要。 如果您不指派公用 IP 位址 tooa 虛擬機器，它仍然可以進行通訊輸出 toohello 網際網路使用其私人 IP 位址。 更多關於公用 IP 位址，讀取 hello toolearn[公用 IP 位址](virtual-network-public-ip-address.md)發行項。

有限制 toohello 數目私人和公用 IP 位址，您可以指派 tooa 網路介面。 如需詳細資訊，請閱讀 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)發行項。

> [!NOTE]
> Azure 會將轉譯的虛擬機器的私人 IP 位址 tooa 公用 IP 位址。 如此一來，hello 作業系統不會察覺指派 tooit 任何公用 IP 位址，所以不需要 tooever 手動指派 hello 作業系統內的公用 IP 位址。

## <a name="assignment-methods"></a>指派方法

使用下列方法指派的 hello 指派公用與私人 IP 位址：

### <a name="dynamic"></a>動態

系統預設會指派動態的私人 IPv4 和 IPv6 (選擇性) 位址。 動態位址可能變更，如果 hello 虛擬機器會放入 hello 停止 （取消配置） 的狀態，然後再啟動。 如果您不想 IPv4 位址 toochange hello hello 虛擬機器的存留期間，指派 hello 位址使用 hello 靜態方法。 您只能指派私用的 IPv6 位址使用 hello 動態指派的方法。 您無法指派公用 IPv6 位址 tooan IP 設定使用哪一種方法。

### <a name="static"></a>靜態

刪除虛擬機器之前，使用 hello 靜態方法指派的位址不會變更。 Hello 子網路 hello 網路介面是在中，手動指派靜態私人 IPv4 位址 tooan IP 組態從 hello 位址空間。 （選擇性），您可以指派一個公用或私用靜態 IPv4 位址 tooan IP 設定。 您無法指定一個靜態公用或私用 IPv6 位址 tooan IP 設定。 toolearn 深入了解 Azure 如何指派靜態公用 IPv4 位址，請參閱 hello[公用 IP 位址](virtual-network-public-ip-address.md)發行項。

## <a name="ip-address-versions"></a>IP 位址版本

您可以指定 hello 指派位址時，下列版本：

### <a name="ipv4"></a>IPv4

每個網路介面都必須有一個[主要](#primary) IP 組態具有指派的[私人](#private) [IPv4](#ipv4) 位址。 您可以新增一或多個[次要](#secondary) IP 組態，其各擁有一個 IPv4 私人及 (選擇性) 一個 IPv4 [公用](#public) IP 位址。

### <a name="ipv6"></a>IPv6

您可以指定零個或一個私用[IPv6](#ipv6)位址 tooone 次要 IP 設定的網路介面。 hello 網路介面不能有任何現有的次要 IP 設定。 您無法將 IP 組態使用 hello 入口網站的 IPv6 位址。 使用 PowerShell 或 CLI tooadd IP 組態的 hello 與私用 IPv6 位址 tooan 現有網路介面。 hello 網路介面不能附加的 tooan 現有 VM。

> [!NOTE]
> 雖然您可以建立網路介面的 IPv6 位址使用 hello 入口網站，您無法加入現有網路介面 tooa 全新或現有的虛擬機器，使用 hello 入口網站。 使用 PowerShell 或 hello Azure CLI 2.0 toocreate 網路介面搭配私用的 IPv6 位址，然後在建立虛擬機器時附加 hello 網路介面。 您無法附加指派 tooit tooan 現有虛擬機器的私用的 IPv6 位址的網路介面。 您無法加入私人 IPv6 位址 tooan IP 設定為使用任何工具 （入口網站、 CLI 或 PowerShell） 任何網路介面附加 tooa 虛擬機器。

您無法指派公用 IPv6 位址 tooa 主要或次要 IP 設定。

## <a name="next-steps"></a>後續步驟
toocreate 虛擬機器使用不同的 IP 組態，讀取 hello 下列文章：

|Task|工具|
|---|---|
|建立具有多個 NIC 的 VM|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|建立具有多個 IPv4 位址的單一 NIC VM|[CLI](virtual-network-multiple-ip-addresses-cli.md)、[PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|建立具有私人 IPv6 位址的單一 NIC VM (在 Azure Load Balancer 後端)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Azure Resource Manager 範本](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
