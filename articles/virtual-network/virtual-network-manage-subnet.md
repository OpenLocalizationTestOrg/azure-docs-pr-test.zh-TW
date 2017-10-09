---
title: "aaaAdd，變更或刪除的 Azure 虛擬網路子網路 |Microsoft 文件"
description: "了解如何 tooadd，變更或刪除 Azure 虛擬網路子網路。"
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
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>加入、變更或刪除虛擬網路子網路

了解如何 tooadd，變更或刪除虛擬網路子網路。 

如果您不熟悉虛擬網路，建議在加入、變更或刪除子網路之前，先閱讀 [Azure 虛擬網路概觀](virtual-networks-overview.md)和[建立、變更或刪除虛擬網路](virtual-network-manage-network.md)。 所有部署到虛擬網路的 Azure 資源都會部署到虛擬網路內的子網路。 通常，虛擬網路中會建立多個子網路，以便：
- **篩選子網路之間的流量**。 您可以套用網路安全性群組 toosubnets toofilter 傳入和傳出網路流量 （例如虛擬機器） 的 hello 虛擬網路中的所有資源。 toolearn 深入了解如何 toocreate 網路安全性群組，請參閱[建立網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)。
- **控制子網路之間的路由**。 Azure 會建立預設路由，以便在子網路之間自動路由傳送流量。 您可以建立使用者定義的路由，來覆寫 Azure 預設路由。 toolearn 進一步了解使用者定義的路由，請參閱[建立使用者定義的路由](virtual-network-create-udr-arm-ps.md)。 

本文說明 tooadd，變更與刪除使用 hello Azure Resource Manager 部署模型所建立的虛擬網路的子網路的方式。
 
## <a name="before"></a>開始之前

開始本文章中所述的 hello 工作之前，請完成下列必要條件 hello:

- 如果您是新 tooworking 搭配虛擬網路時，我們建議您檢閱中的 hello 練習[建立第一個 Azure 虛擬網路](virtual-network-get-started-vnet-subnet.md)。 這個練習有助您更加熟悉虛擬網路。
- 有關限制的虛擬網路，檢閱 toolearn [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)。
- 登入 Azure 入口網站 toohello、 hello Azure 命令列工具 (Azure CLI) 或 Azure PowerShell，使用您的 Azure 帳戶。 如果您沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果您計劃的 toouse PowerShell 命令的這篇文章中所述的 toocomplete hello 工作，您必須先[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell cmdlet 安裝最新版本。 tooget 說明 hello 範例中的 PowerShell 命令的輸入`get-help <command> -full`。
- 如果您計劃的 toouse Azure CLI 命令的這篇文章中所述的 toocomplete hello 工作，您必須：
    - [安裝和設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello Azure CLI 安裝最新版本。
    - 使用 Azure 雲端殼層 hello。 而不是安裝 hello CLI 和其相依性，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層 (**> _**) 在 hello hello Azure 入口網站頂端的圖示。 

  使用 Azure CLI 命令的 tooget 說明輸入`az <command> --help`。

## <a name="create-subnet"></a>加入子網路

tooadd 子網路：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，按一下 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想要的子網路 tooadd hello 虛擬網路。
4. 在 hello 虛擬網路刀鋒視窗中，按一下 **子網路**。
5. 按一下 [+子網路]。
6. 在 hello**加入子網路**刀鋒視窗中，輸入 hello 下列參數的值：
    - **名稱**: hello 名稱必須是唯一 hello 虛擬網路內。
    - **位址範圍**: hello 範圍內必須是唯一 hello hello 虛擬網路的位址空間。 hello 範圍不能與 hello 虛擬網路內的其他子網路位址範圍重疊。 必須使用無類別網域間路由選擇 (CIDR) 標記法指定 hello 位址空間。 例如，在位址空間為 10.0.0.0/16 的虛擬網路中，您可以定義 10.0.0.0/24 的子網路位址空間。 hello 最小的範圍，您可以指定為/29，可提供八個 IP 位址 hello 子網路。 Azure 會保留先 hello 和上次中為了符合通訊協定的每個子網路位址。 Azure 還會保留三個位址供 Azure 服務使用。 如此一來，定義具有/29 子網路位址範圍導致 hello 子網路中的三個可使用 IP 位址。 如果您計劃 tooconnect tooa 虛擬網路 VPN 閘道，您必須建立閘道子網路。 深入了解[閘道子網路位址範圍的具體考量](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)。 您可以在之後加入 hello 子網路，在特定情況下，變更 hello 位址範圍。 如何 toochange 子網路位址範圍，請參閱的 toolearn[變更子網路設定](#change-subnet)本文中。
    - **網路安全性群組**: （選擇性） 您可以將現有的網路安全性群組與 hello 子網路 toocontrol 篩選 hello 子網路的傳入和傳出網路流量。 hello 網路安全性群組必須存在於 hello 相同訂用帳戶和與 hello 虛擬網路的位置。 也必須建立使用 hello Resource Manager 部署模型。 toolearn 深入了解如何 toocreate 網路安全性群組，請參閱[網路安全性群組](virtual-networks-create-nsg-arm-pportal.md)。
    - **路由表**: （選擇性） 您可以將現有的路由表與 hello 子網路 toocontrol 網路流量路由 tooother 網路。 hello 路由表必須存在於 hello 相同訂用帳戶和與 hello 虛擬網路的位置。 也必須建立使用 hello Resource Manager 部署模型。 toolearn 深入了解如何 toocreate 路由表，請參閱[使用者定義的路由](virtual-network-create-udr-arm-ps.md)。
    - **使用者**： 您可以使用內建的角色或您自己的自訂角色來控制存取 toohello 子網路。 toolearn 進一步了解指派角色和使用者 tooaccess hello 的子網路，請參閱[使用角色指派 toomanage 存取 tooyour Azure 資源](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access)。
7. tooadd hello 子網路 toohello 虛擬網路，您選取，請按一下**確定**。

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>變更子網路設定

您可以管理的子網路的資源，以變更網路安全性群組、 路由表，以及使用者存取 tooa 子網路。 有關這些設定，toolearn 中[新增子網路](#create-subnet)，請參閱步驟 6。 如果您想 toochange hello 位址空間的子網路，您必須先刪除 hello 子網路中的任何資源。 hello 步驟採取 toodelete 資源的 hello 資源有所不同。 toolearn toodelete 資源子網路，每個資源的讀取的 hello 文件中，輸入您想 toodelete。 toochange hello 子網路的位址範圍：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，按一下 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想要的 toochange 子網路位址範圍的 hello 虛擬網路。
4. 按一下您想要的 toochange hello 位址範圍的 hello 子網路。
5. Hello 子網路 刀鋒視窗，在 hello**位址範圍**方塊中，輸入 hello 新的位址範圍。 hello 範圍內必須是唯一 hello hello 虛擬網路的位址空間。 hello 範圍不能與 hello 虛擬網路內的其他子網路位址範圍重疊。 必須使用 CIDR 表示法指定 hello 位址空間。 例如，在位址空間為 10.0.0.0/16 的虛擬網路中，您可以定義 10.0.0.0/24 的子網路位址空間。 hello 最小的範圍，您可以指定為/29，可提供八個 IP 位址 hello 子網路。 Azure 會保留先 hello 和上次中為了符合通訊協定的每個子網路位址。 Azure 還會保留三個位址供 Azure 服務使用。 因此，使用 /29 位址範圍的子網路最終可用的 IP 位址只有三個。 如果您計劃 tooconnect tooa 虛擬網路 VPN 閘道，您必須建立閘道子網路。 深入了解[閘道子網路位址範圍的具體考量](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub)。 您可以在之後建立 hello 子網路時，在特定情況下，變更 hello 位址範圍。 如何 toochange 子網路位址範圍，請參閱的 toolearn[變更子網路設定](#change-subnet)本文中。
6. 按一下 [儲存] 。

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>刪除子網路

只有當 hello 子網路中沒有資源，您可以刪除子網路。 如果有 hello 子網路中的資源，您必須刪除位於 hello 的子網路，才能刪除 hello 子網路的 hello 資源。 hello 步驟採取 toodelete 資源的 hello 資源有所不同。 toolearn toodelete 資源子網路，每個資源的讀取的 hello 文件中，輸入您想 toodelete。 toodelete 子網路：

1. 登入 toohello[入口網站](https://portal.azure.com)指派 hello 網路參與者角色 （至少） 訂用帳戶的權限的帳戶。 進一步了解指派角色和權限 tooaccounts toolearn 看到[Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 [hello] 入口網站搜尋方塊中，輸入**虛擬網路**。 在 hello 搜尋結果中，按一下 **虛擬網路**。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想 toodelete 從子網路的 hello 虛擬網路。
4. 在 hello 虛擬網路刀鋒視窗中，在**設定**，按一下 **子網路**。
5. 在 hello 子刀鋒視窗中，以滑鼠右鍵按一下 hello 子網路出現的 hello 清單的子網路中想 toodelete 中，按一下**刪除**，然後按一下**是**toodelete hello 子網路。

**命令**

|工具|命令|
|---|---|
|Azure CLI|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>接續步驟

toocreate 虛擬機器的子網路，請參閱[建立虛擬網路，並將 Vm 部署 hello 子網路中](virtual-network-get-started-vnet-subnet.md#create-vms)。
