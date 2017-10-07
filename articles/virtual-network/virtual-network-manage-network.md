---
title: "aaaCreate，變更或刪除 Azure 虛擬網路 |Microsoft 文件"
description: "了解如何 toocreate，變更或刪除虛擬網路在 Azure 中。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>建立、變更或刪除虛擬網路

了解如何 toocreate 和刪除虛擬網路] 和 [變更設定，例如 DNS 伺服器和 IP 位址空間，現有的虛擬網路。

虛擬網路是網路的您自己 hello 雲端中的表示法。 虛擬網路是 hello 的隔離是 hello 的專用的 tooyour Azure 訂用帳戶的 Azure 雲端的邏輯。 對於您建立的每個虛擬網路，您可以：
- 選擇的位址空間 tooassign。 位址空間包含使用無類別網域間路由 (CIDR) 表示法所定義的一或多個位址範圍，例如 10.0.0.0/16。
- 請選擇 toouse hello Azure 提供的 DNS 伺服器，或使用您自己的 DNS 伺服器。 連接的 toohello 虛擬網路的所有資源都皆 hello 虛擬網路中的此 DNS 伺服器 tooresolve 名稱。
- 區段 hello 虛擬網路子網路，到每個都有它自己的位址範圍，hello hello 虛擬網路位址空間中。 如何 toocreate、 變更和刪除子網路，請參閱的 toolearn[新增、 變更或刪除子網路](virtual-network-manage-subnet.md)。

本文將說明 toocreate，變更，並刪除虛擬網路使用 hello Azure Resource Manager 部署模型。

## <a name="before"></a>開始之前

開始本文章中所述的 hello 工作之前，請完成下列必要條件 hello:

- 如果您是新 tooworking 搭配虛擬網路時，我們建議您檢閱中的 hello 練習[建立第一個 Azure 虛擬網路](virtual-network-get-started-vnet-subnet.md)。 這個練習有助您更加熟悉虛擬網路。
- 有關限制的虛擬網路，檢閱 toolearn [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)。
- 登入 Azure 入口網站 toohello、 hello Azure 命令列工具 (Azure CLI) 或 Azure PowerShell，使用您的 Azure 帳戶。 如果您沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果您計劃的 toouse PowerShell 命令的這篇文章中所述的 toocomplete hello 工作，您必須先[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell cmdlet 安裝最新版本。 tooget 說明 hello 範例中的 PowerShell 命令的輸入`get-help <command> -full`。
- 如果您計劃的 toouse Azure CLI 命令的這篇文章中所述的 toocomplete hello 工作，您必須先[安裝及設定 Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello Azure CLI 安裝最新版本。 使用 Azure CLI 命令的 tooget 說明輸入`az <command> --help`。


## <a name="create-vnet"></a>建立虛擬網路

toocreate 虛擬網路：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 按一下 [新增]  >  [網路]  >  [虛擬網路]。
3. 在 hello**虛擬網路**刀鋒視窗中的，在 hello**選取部署模型**方塊中，保留**資源管理員**選取，然後再按一下**建立**.
4. 在 hello**建立虛擬網路**刀鋒視窗中，輸入或選取值為 hello 下列設定，然後按一下**建立**:
    - **名稱**: hello 名稱必須是唯一的 hello[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)您選取 toocreate hello 虛擬網路中的。 建立 hello 虛擬網路之後，您無法變更 hello 名稱。 您可以隨著時間建立多個虛擬網路。 如需命名建議，請參閱[命名慣例](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions)。 下列命名慣例可協助使用者更容易 toomanage 多個虛擬網路。
    - **位址空間**： 以 CIDR 標記法指定 hello 位址空間。 您定義的 hello 位址空間可以是公用或私用 (RFC 1918)。 您定義 hello 位址空間為公用或私用，hello 位址空間只能從 hello 的虛擬網路內，從互連的虛擬網路，以及任何您已連接 toohello 虛擬網路的內部部署網路連線。 您無法新增下列位址空間的 hello:
        - 224.0.0.0/4 (多點傳送)
        - 255.255.255.255/32 (廣播)
        - 127.0.0.0/8 (回送)
        - 169.254.0.0/16 (連結-本機)
        - 168.63.129.16/32 (內部 DNS)

      雖然您可以定義只能有一個位址空間，當您建立 hello 虛擬網路時，您可以在 hello 虛擬網路建立之後加入其他位址空間。 toolearn 如何 tooadd 位址空間 tooan 現有的虛擬網路，請參閱[新增或移除地址空間](#add-address-spaces)本文中。

      >[!WARNING]
      >如果虛擬網路與另一個虛擬網路或內部網路的重疊的位址空間，無法連線 hello 兩個網路。 您定義的位址空間之前，請考慮是否可能會想 tooconnect hello 虛擬網路 tooother 虛擬網路或內部部署網路中 hello 未來。
      >
      >

    - **子網路名稱**: hello 子網路名稱必須是唯一 hello 虛擬網路內。 Hello 子網路建立之後，您無法變更 hello 子網路名稱。 hello 入口網站會要求您定義一個子網路時建立虛擬網路，即使虛擬網路不是必要的 toohave 任何子網路。 在 hello 入口網站中，您可以定義一個子網路時建立虛擬網路。 更新版本中，建立 hello 虛擬網路之後，您可以加入更多的子網路 toohello 虛擬網路。 tooadd 子 tooa 虛擬網路，請參閱[建立子網路](virtual-network-manage-subnet.md#create-subnet)中[建立、 變更或刪除子網路](virtual-network-manage-subnet.md)。 您可以使用 Azure CLI 或 PowerShell，建立具有多個子網路的虛擬網路。

      >[!TIP]
      >某些情況下，系統管理員 」 建立不同的子網路 hello 子網路間路由 toofilter 或控制流量。 定義子網路之前，請考慮如何想 toofilter 和您的子網路之間路由傳送流量。 toolearn 進一步了解篩選子網路之間流量，請參閱[網路安全性群組](virtual-networks-nsg.md)。 Azure 會自動路由傳送子網路之間的流量，但您可以覆寫 Azure 預設路由。 toolearn 如何 toooverride Azure 預設子網路流量路由，請參閱[使用者定義的路由](virtual-networks-udr-overview.md)。
      >

    - **子網路位址範圍**: hello 範圍都必須是您所輸入的 hello 虛擬網路的 hello 位址空間內。 hello 最小的範圍，您可以指定為/29，可提供八個 IP 位址 hello 子網路。 Azure 會保留先 hello 和上次中為了符合通訊協定的每個子網路位址。 Azure 還會保留三個位址供 Azure 服務使用。 因此，使用 /29 子網路位址範圍的虛擬網路只有三個可用的 IP 位址。 如果您計劃 tooconnect tooa 虛擬網路 VPN 閘道，您必須建立閘道子網路。 深入了解[閘道子網路位址範圍的具體考量](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)。 您可以在之後建立 hello 子網路時，在特定情況下，變更 hello 位址範圍。 如何 toochange 子網路位址範圍，請參閱的 toolearn[變更子網路設定](#change-subnet)中[新增、 變更或刪除子網路](virtual-network-manage-subnet.md)。
    - **訂用帳戶**︰選取[訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)。 您無法使用 hello 多個 Azure 訂用帳戶中的相同虛擬網路。 不過，您可以連接其他訂用帳戶中的一個訂用帳戶 toovirtual 網路中的虛擬網路。 tooconnect 不同的訂用帳戶中的虛擬網路使用 Azure VPN 閘道或虛擬網路對等互連。 任何您 toohello 虛擬網路連線的 Azure 資源必須在 hello hello 虛擬網路相同訂用帳戶。
    - **資源群組**：選取現有[資源群組](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups)或建立新的資源群組。 您 toohello 虛擬網路連線的 Azure 資源可以在 hello 與 hello 虛擬網路或不同的資源群組中的相同資源群組。
    - **位置**︰選取 Azure [位置](https://azure.microsoft.com/regions/) (也稱為區域)。 虛擬網路只能位於一個 Azure 位置。 不過，您可以使用的 VPN 閘道連接一個位置 tooa 虛擬網路中其他位置中的虛擬網路。 任何您 toohello 虛擬網路連線的 Azure 資源必須在 hello 與 hello 虛擬網路相同的位置。

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>檢視虛擬網路與設定

tooview 虛擬網路和設定：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，按一下 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想要針對 tooview 設定 hello 虛擬網路。
4. hello 下列設定詳列 hello 您選取的虛擬網路的 hello 刀鋒視窗上：
    - **概觀**： 提供 hello 虛擬網路，包括位址空間和 DNS 伺服器的相關資訊。 hello 下列螢幕擷取畫面顯示 hello 概觀設定虛擬網路，名為**MyVNet**:

        ![網路介面概觀](./media/virtual-network-manage-network/vnet-overview.png)

      在 hello**概觀**刀鋒視窗中，您可以移動的虛擬網路 tooa 不同訂用帳戶或資源群組。 如何 toomove 虛擬網路，請參閱的 toolearn[移動資源 tooa 不同資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 hello 文章列出先決條件及如何使用 toomove 資源 hello Azure 入口網站、 PowerShell 和 Azure CLI。 連接的 toohello 虛擬網路的所有資源必須都移動與 hello 虛擬網路。
    - **位址空間**: hello 分派 toohello 虛擬網路的位址空間會列出。 toolearn tooadd 移除地址空間中，如何完成 hello 中的步驟[新增或移除地址空間](#address-spaces)本文中。
    - **連接的裝置**： 連接的 toohello 虛擬網路的任何資源都會列出。 在上述螢幕擷取畫面的 hello，三個網路介面和一個負載平衡器是連接的 toohello 虛擬網路。 會列出任何新的資源，您所建立，且 toohello 虛擬網路連線。 如果您刪除已連接的 toohello 虛擬網路的資源，不會再出現在 [hello] 清單中。
    - **子網路**: hello 虛擬網路內存在的子網路的清單會顯示。 如何 tooadd 並移除子網路，請參閱的 toolearn[建立子網路](virtual-network-manage-subnet.md#create-subnet)和[刪除該子網路](virtual-network-manage-subnet.md#delete-subnet)中[新增、 變更或刪除子網路](virtual-network-manage-subnet.md)。
    - **DNS 伺服器**： 您可以指定是否 hello Azure 內部的 DNS 伺服器或自訂的 DNS 伺服器名稱解析為提供連接的 toohello 虛擬網路的裝置。 當您使用 hello Azure 入口網站建立虛擬網路時，Azure 的 DNS 伺服器用於名稱解析內虛擬網路，根據預設。 中的 toomodify hello DNS 伺服器，請完成 hello 步驟[新增、 變更或移除 DNS 伺服器](#dns-servers)本文中。
    - **對等互連**： 如果 hello 訂用帳戶中有現有的對等互連，此處所列。 您可以檢視現有對等互連的設定，也可以建立、變更或刪除對等互連。 toolearn 深入了解對等互連，請參閱[虛擬網路對等互連](virtual-network-peering-overview.md)。
    - **屬性**: hello 虛擬網路，其中包括 hello 虛擬網路的資源識別碼和 hello Azure 訂用帳戶處於大約的顯示設定。
    - **圖表**: hello 圖表提供連接的 toohello 虛擬網路的所有裝置的視覺表示法。 hello 圖表都有一些重要 hello 裝置資訊。 toomanage hello 圖表中的這個檢視中的裝置按一下 hello 裝置。
    - **一般的 Azure 設定**: toolearn 深入了解一般 Azure 的設定，請參閱下列資訊的 hello:
        *   [活動記錄檔](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [存取控制 (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [標記](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [鎖定](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [自動化指令碼](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>新增或移除位址空間

您可以新增和移除虛擬網路的位址空間。 位址空間，必須指定以 CIDR 標記法，而且不能重疊 hello 內其他位址空間與相同虛擬網路。 您定義的 hello 位址空間可以是公用或私用 (RFC 1918)。 您定義 hello 位址空間為公用或私用，hello 位址空間只能從 hello 的虛擬網路內，從互連的虛擬網路，以及任何您已連接 toohello 虛擬網路的內部部署網路連線。 您無法新增下列位址空間的 hello:

- 224.0.0.0/4 (多點傳送)
- 255.255.255.255/32 (廣播)
- 127.0.0.0/8 (回送)
- 169.254.0.0/16 (連結-本機)
- 168.63.129.16/32 (內部 DNS)

tooadd 或移除的位址空間：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，選取 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想 tooadd 或移除地址空間 hello 虛擬網路。
4. 在 hello 虛擬網路刀鋒視窗中，在**設定**，按一下 **位址空間**。
5. Hello 位址空間的 hello 刀鋒視窗，完成其中一種 hello 下列選項：
    - **加入位址空間**： 輸入 hello 新的位址空間。 hello 位址空間不得與現有定義 hello 虛擬網路位址空間重疊。
    - **移除地址空間**︰以滑鼠右鍵按一下位址空間，然後按一下移除。 如果子網路存在 hello 位址空間中，您無法移除 hello 位址空間。 tooremove 位址空間，您必須先刪除任何子網路 （和任何連接的 toohello 子網路的資源） 存在於 hello 位址空間中。
6. 按一下 [儲存] 。

**命令**

|工具|命令|
|---|---|
|Azure CLI|僅限 Resource Manager|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>新增、變更或移除 DNS 伺服器

所有連接的 toohello 虛擬網路的 Vm 註冊 hello 您指定 hello 虛擬網路的 DNS 伺服器。 他們也使用指定的 hello 進行名稱解析的 DNS 伺服器。 VM 中的每個網路介面 (NIC) 都可以有自己的 DNS 伺服器設定。 如果 NIC 有它自己的 DNS 伺服器設定，它們會覆寫 hello hello 虛擬網路的 DNS 伺服器設定。 toolearn 深入了解 NIC 的 DNS 設定，請參閱[網路介面的工作和設定](virtual-network-network-interface.md#change-dns-servers)。 toolearn 有關 Vm 和 Azure 雲端服務中的角色執行個體的名稱解析的詳細資訊請參閱[Vm 和角色執行個體的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)。 tooadd，變更或移除 DNS 伺服器：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，選取 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想 toochange DNS 設定 hello 虛擬網路。
4. 在 hello 虛擬網路刀鋒視窗中，在**設定**，按一下  **DNS 伺服器**。
5. 選取其中一個 hello 下列列出 DNS 伺服器的 hello 刀鋒視窗上的選項：
    - **預設值 （Azure 提供）**： 所有的資源名稱和私人 IP 位址皆會自動註冊的 toohello Azure DNS 伺服器。 您可以解決任何連接的 toohello 資源之間的名稱相同的虛擬網路。 您無法使用此選項 tooresolve 名稱多個虛擬網路。 tooresolve 多個虛擬網路的名稱，您必須使用自訂的 DNS 伺服器。
    - **自訂**： 您可以加入一個或多部伺服器，註冊 toohello Azure 虛擬網路的限制。 toolearn 進一步了解 DNS 伺服器限制，請參閱[Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic)。 您有下列選項的 hello:
        - **新增地址**： 新增 hello 伺服器 tooyour 虛擬網路 DNS 伺服器清單。 此選項也會註冊使用 Azure 的 hello DNS 伺服器。 如果您已經已向 Azure 登錄 DNS 伺服器，您可以在 hello 清單中選取該 DNS 伺服器。
        - **移除地址**： 按一下您想 tooremove 下, 一個 toohello 伺服器**X**。刪除 hello 伺服器 hello 伺服器只能從清單中移除此虛擬網路。 hello DNS 伺服器仍留在 Azure 中的其他的虛擬網路 toouse 已註冊的。
        - **重新排序 DNS 伺服器位址**： 很重要，您會列出您的 DNS 伺服器在 hello tooverify 正確的順序為您的環境。 DNS 伺服器清單用於 hello 順序來指定。 它們不會當作循環配置資源設定運作。 如果可以達到 hello 第一部 DNS 伺服器 hello 清單中的，hello 用戶端會使用該 DNS 伺服器，而不管是否 hello DNS 伺服器是否正常運作。 移除所列的所有 hello DNS 伺服器，然後再重新加入您想要的 hello 排序。
        - **變更位址**： 反白顯示 hello hello 清單中的 DNS 伺服器，然後輸入 hello 新名稱。
6. 按一下 [儲存] 。
7. 重新啟動 hello Vm 的連線的 toohello 虛擬網路，因此它們會指派 hello 新的 DNS 伺服器設定。 在重新啟動之前，Vm 將繼續 toouse 其目前的 DNS 設定。

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>刪除虛擬網路

只有在沒有資源連線的 tooit，您可以刪除虛擬網路。 如果有 hello 虛擬網路內的資源已連線的 tooany 子網路，您必須先刪除連線的 tooall hello 虛擬網路內的子網路的 hello 資源。 hello 步驟採取 toodelete 資源的 hello 資源有所不同。 已連線的 toosubnets toodelete 資源的讀取方式 toolearn hello 文件要 toodelete 為每個資源類型。 toodelete 虛擬網路：

1. 登入 toohello[入口網站](https://portal.azure.com)帳戶也就是指派 （至少） 角色的權限 hello 網路參與者訂用帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，按一下 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，選取 hello 想 toodelete 的虛擬網路。
4. Hello 虛擬網路] 刀鋒視窗中，沒有任何裝置 tooconfirm 連接 toohello 虛擬網路，底下**設定**，按一下 [**連接的裝置**。 如果沒有連接的裝置，您必須刪除它們，才能刪除 hello 虛擬網路。 如果沒有已連線的裝置，請按一下 [概觀]。
5. 在 hello hello 刀鋒視窗頂端，按一下 hello**刪除**圖示。
6. tooconfirm hello 刪除 hello 虛擬網路中，按一下**是**。


**命令**

|工具|命令|
|---|---|
|Azure CLI|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>接續步驟

- toocreate VM，然後將它連接 tooa 虛擬網路，請參閱[建立虛擬網路和 Vm 連線](virtual-network-get-started-vnet-subnet.md#create-vms)。
- 請參閱 toofilter 虛擬網路內的子網路之間的網路流量[建立網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)。
- toopeer 虛擬網路 tooanother 虛擬網路，請參閱[建立虛擬網路對等互連](virtual-network-create-peering.md#portal)。
- toolearn 有關選項的連接虛擬網路 tooan 在內部部署網路，請參閱[有關 VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams)。
