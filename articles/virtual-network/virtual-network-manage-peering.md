---
title: "aaaCreate，變更或刪除 Azure 虛擬網路對等互連 |Microsoft 文件"
description: "了解如何 toocreate，變更或刪除虛擬網路對等互連。"
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>建立、變更或刪除虛擬網路對等互連

了解如何 toocreate，變更或刪除虛擬網路對等互連。 虛擬網路對等互連可讓您 tooconnect 兩個虛擬網路中的 hello 透過相同的 Azure 位置 hello Azure 骨幹網路。 所以，一旦 hello 兩個虛擬網路會仍會視為不同的資源管理。 其中一個虛擬網路中的資源與通訊 hello 相同延遲和頻寬好像 hello 資源在 hello 相同虛擬網路。 如果您不熟悉虛擬網路對等互連，我們建議您閱讀 hello[虛擬網路對等互連概觀](virtual-network-peering-overview.md)並完成 hello[建立虛擬網路對等互連教學課程](virtual-network-create-peering.md)，才能完成本文章中的 hello 工作。

## <a name="before-you-begin"></a>開始之前

完成下列工作之前完成任何一節中的步驟 hello:

- 檢閱 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits)文章 toolearn 有關限制的對等互連。
- 記錄 toohello Azure 入口網站、 Azure 命令列介面 (CLI) 或 Azure PowerShell 中使用的 Azure 帳戶。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果使用 PowerShell 命令在本文中 toocomplete 工作[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure PowerShell cmdlet 安裝最新版本。 tooget 說明的 PowerShell 命令，與範例中，輸入`get-help <command> -full`。
- 如果使用 Azure 命令列介面 (CLI) 命令 toocomplete 工作，在本文中[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 hello 雲端殼層有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)。 

## <a name="create-a-peering"></a>建立對等互連

>[!NOTE]
>有幾項需求，條件約束，並考量 toosuccessfully 可讓您建立的虛擬網路對等互連。 之前建立的對等互連，請確定您已研讀 hello[需求和限制條件](#requirements-and-constraints)和[必要的權限](#permissions)。
>

1. 登入 toohello[入口網站](https://portal.azure.com)帳戶指派必要 hello[角色或權限](#permissions)。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*虛擬網路*。 當**虛擬網路**會出現在 hello 搜尋結果中，按一下它。 請勿選取**虛擬網路 （傳統）**如果則會出現在 hello 清單中，當您無法建立虛擬網路透過 hello 傳統部署模型部署從對等互連。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您要的對等互連 toocreate hello 虛擬網路。
4. 在顯示 hello 您選取的虛擬網路的 hello 窗格中按一下**對等互連**在 hello**設定**> 一節。
5. 按一下 [+ 新增]。 
6. <a name="add-peering"></a>在 hello**加入對等互連**刀鋒視窗中，輸入或選取值 hello 下列設定：
    - **名稱：** hello hello 對等互連名稱必須是唯一 hello 虛擬網路內。
    - **虛擬網路部署模型：** toopeer 與已部署到選取的部署模型 hello 虛擬網路，您想要。
    - **我知道我的資源 ID:**如果您有想 toopeer 與讀取權限 toohello 虛擬網路，將此核取方塊未選取。 如果您沒有讀取權限 toohello 虛擬網路或想 toopeer 與訂用帳戶，請核取此方塊。 輸入您想要在 hello 與 toopeer hello 虛擬網路的 hello 完整資源識別碼**資源識別碼**您核取方塊 hello 時出現的方塊。 您輸入的識別碼必須存在於虛擬網路的 hello 資源 hello 相同 Azure[位置](https://azure.microsoft.com/regions)為此虛擬網路。 hello 完整資源識別碼看起來類似太/訂用帳戶/<Id>/resourceGroups/ < 資源-群組-名稱 > /providers/Microsoft.Network/virtualNetworks/ < 虛擬-網路-名稱 >。 您可以檢視虛擬網路的 hello 屬性，來取得虛擬網路 hello 資源識別碼。 如何 tooview hello 屬性，針對虛擬網路，請參閱的 toolearn[管理虛擬網路](virtual-network-manage-network.md#view-vnet)。
    - **訂用帳戶：**選取 hello[訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)想與 toopeer hello 虛擬網路。 視帳戶有權讀取的訂用帳戶而定，系統會列出一或多個訂用帳戶。 當您核取 hello**資源識別碼**核取方塊，這項設定無法使用。 若要讓不同訂用帳戶中的兩個虛擬網路對等互連，則這兩個虛擬網路都必須是透過 Resource Manager 所建立的才行。 透過不同的部署模型建立的訂用帳戶之間的 hello 能力 toopeer 處於預覽版本。 註冊之前建立的對等互連透過存在於不同的訂用帳戶中的不同的部署模型所部署的虛擬網路之間的 hello 預覽。 深入了解如何 tooregister hello preview 和[對等透過不同的訂用帳戶中不同的部署模型所建立的虛擬網路](create-peering-different-deployment-models-subscriptions.md)。
    - **虛擬網路：**選取 hello 想 toopeer 與虛擬網路。 您可以選取其中一個 Azure 部署模型，透過建立虛擬網路但 hello 虛擬網路必須位於相同位置 hello 虛擬網路正在起始 hello 從對等互連的 hello。 您必須具有讀取存取 toohello 虛擬網路，toobe 在 hello 清單中看到。 如果列出虛擬網路，但灰色，它可能是因為 hello hello 虛擬網路的位址空間與 hello 這個虛擬網路的位址空間重疊。 如果虛擬網路的位址空間重疊，您就無法讓這些位址空間對等互連。 當您核取 hello**資源識別碼**核取方塊，這項設定無法使用。
    - **允許的虛擬網路存取：**選取**啟用**（預設值） 如果您想 tooenable hello 兩個虛擬網路之間的通訊。 啟用虛擬網路之間的通訊可讓連接資源彼此與 tooeither 虛擬網路 toocommunicate hello 相同的頻寬和延遲好像連接的 toohello 相同虛擬網路。 Hello 兩個虛擬網路中的資源之間的所有通訊都都會透過 hello Azure 私人網路。 hello **VirtualNetwork**網路安全性群組的預設標記包含 hello 虛擬網路，所以虛擬網路。 深入了解 toolearn 網路安全性的群組的預設標記、 讀取 hello[網路安全性群組概觀](virtual-networks-nsg.md#default-tags)發行項。  選取**已停用**如果您不想流量 tooflow toohello 所以虛擬網路。 您可能會選取**已停用**如果您已經所以虛擬網路與另一個虛擬網路，但偶爾會需要 toodisable hello 兩個虛擬網路之間的流量。 您可能會發現啟用/停用功能比起先刪除再重新建立對等互連更為方便。 停用此設定時，流量不會之間 hello 所以虛擬網路。
    - **允許轉送的流量：**核取此方塊 tooallow 轉送流量 toohello 所以虛擬網路 （不屬於原始 hello 所以虛擬網路中的流量） tooflow toothis 虛擬網路。 當您部署了您正在使用中的對等互連，並建立使用者定義的路由 tooforward 流量透過 hello 網路的虛擬應用裝置 hello 虛擬網路中的網路虛擬設備，常會使用流量轉送。 如果您離開此方塊未核取 （預設值），從 hello 所以虛擬網路轉送流量無法順利 toothis 虛擬網路。 啟用這項功能可讓透過對等互連 hello hello 轉送流量，它不會建立使用者定義的任何路由或網路虛擬裝置。 使用者定義的路由和網路虛擬設備是另外建立的。 了解[使用者定義的路由](virtual-networks-udr-overview.md)。
    - **允許閘道傳輸：**核取此方塊，如果您有一個虛擬網路閘道連接的 toothis 虛擬網路，而且想 tooallow 流量從 hello 所以透過 hello 閘道的虛擬網路 tooflow。 例如，此虛擬網路可能附加的 tooan 透過虛擬網路閘道的內部部署網路。 檢查此方塊可讓來自 hello 流量，所以透過 hello 閘道附加的 toothis 虛擬網路的虛擬網路 tooflow。 如果您核取此方塊，hello 所以虛擬網路不能有設定閘道。 hello 所以虛擬網路必須有 hello**使用遠端閘道**設定 hello 對等互連從 hello 其他虛擬網路 toothis 虛擬網路時選取核取方塊。 如果您離開此方塊未核取 （預設值），從 hello 所以虛擬網路的流量仍然流動 toothis 虛擬網路，但無法通過虛擬網路閘道連接的 toothis 虛擬網路。 深入了解[虛擬網路閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti)。 
    
    如果您要讓虛擬網路 (Resource Manager) 與虛擬網路 (傳統) 對等互連，您將無法啟用此選項。 雖然 hello 流量流 hello 兩個虛擬網路之間，透過網路閘道連接的 toohello 虛擬網路 （資源管理員） 也無法順利 hello 虛擬網路 （傳統） 流量。
    - **使用遠端閘道：**檢查從透過虛擬網路閘道連接的 toohello 虛擬網路您對等互連與此虛擬網路 tooflow 此方塊 tooallow 流量。 比方說，您對等互連與 hello 虛擬網路已連接的 VPN 閘道，可讓通訊 tooan 在內部部署網路。  核取此方塊可讓此虛擬網路 tooflow，透過 hello VPN 閘道附加的 toohello 所以虛擬網路的流量。 如果您核取此方塊，hello 所以虛擬網路必須有虛擬網路閘道連接 tooit 而且必須具有 hello**允許閘道傳輸**checkbox 已核取。 如果您離開此方塊未核取 （預設值），從 hello 所以虛擬網路仍流量 toothis 虛擬網路，但不會流經虛擬網路閘道連接的 toothis 虛擬網路。 
    
    如果您要讓虛擬網路 (Resource Manager) 與虛擬網路 (傳統) 對等互連，您將無法啟用此選項。 雖然 hello 流量流 hello 兩個虛擬網路之間，hello 虛擬網路 （資源管理員） 無法流量透過網路閘道連接的 toohello 虛擬網路 （傳統）。
7. 按一下 hello**確定**按鈕 tooadd hello 子 toohello 虛擬網路您選取。

### <a name="commands"></a>命令

|工具|命令|
|---|---|
|CLI|[az network vnet peering create](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>案例

透過建立 hello 相同，虛擬網路之間建立的虛擬網路對等互連，或存在於不同的部署模型 hello 相同，或不同的訂用帳戶。 完成其中一個 hello 下列案例的逐步教學課程：
 
|Azure 部署模型  | 訂用帳戶  |
|---------|---------|
|兩者皆使用 Resource Manager |[相同](virtual-network-create-peering.md)|
| |[不同](create-peering-different-subscriptions.md)|
|一個使用 Resource Manager、一個使用傳統部署模型     |[相同](create-peering-different-deployment-models.md)|
| |[不同](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>檢視或變更對等互連設定

1. 登入 toohello[入口網站](https://portal.azure.com)帳戶指派必要 hello[角色或權限](#permissions)。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*虛擬網路*。 當**虛擬網路**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您要的對等互連 toocreate hello 虛擬網路。
4. 在顯示 hello 您選取的虛擬網路的 hello 窗格中按一下**對等互連**在 hello**設定**> 一節。
5. 按一下 對等互連 hello tooview 或變更設定。
6. 變更 hello 適當設定。 瞭解每個設定中的 hello 選項[步驟 6](#add-peering) hello 建立本文的對等區段。 

    >[!NOTE]
    >有幾項需求，條件約束，並考量 toosuccessfully 可讓您建立的虛擬網路對等互連。 之前建立的對等互連，請確定您已研讀 hello[需求和限制條件](#requirements-and-constraints)和[必要的權限](#permissions)。
    >

7. 按一下 [儲存] 。

**命令**

|工具|命令|
|---|---|
|CLI|[az 網路 vnet 對等互連清單](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list)toolist 對等互連之虛擬網路， [az 網路 vnet 對等互連顯示](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show)tooshow 設定特定對等互連，和[az 網路 vnet 對等互連更新](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update)toochange 對等設定。|
|PowerShell|[Get AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve 檢視對等設定和[組 AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange 設定。|

## <a name="delete-a-peering"></a>刪除對等互連
刪除的對等互連時，從虛擬網路的流量不會再流向 toohello 所以虛擬網路。 當部署透過資源管理員的虛擬網路對等時，每個虛擬網路有對等互連 toohello 其他虛擬網路。 刪除 hello 對等互連，一個虛擬網路從停用 hello hello 虛擬網路之間的通訊，雖然它不會刪除 hello 對等互連 hello 從其他虛擬網路。 hello 對等的狀態，對等互連，hello 存在 hello 中其他虛擬網路是**Disconnected**。 您無法重新建立 hello 對等互連，直到您重新建立 hello 的第一個虛擬網路中的 hello 對等互連和 hello 對等互連狀態的虛擬網路變更太*Connected*。 

如果您想要的虛擬網路 toocommunicate 某些情況下，但是不一定，而不是刪除的對等互連，您可以設定 hello**允許的虛擬網路存取**太設定**已停用**改為。 toolearn 作法，請閱讀步驟 6 的 hello[建立的對等互連](#create-peering)本文一節。 您可能會發現停用和啟用網路存取比起先刪除再重新建立對等互連更為簡單。

1. 登入 toohello[入口網站](https://portal.azure.com)帳戶指派必要 hello[角色或權限](#permissions)。
2. 在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*虛擬網路*。 當**虛擬網路**會出現在 hello 搜尋結果中，按一下它。
3. 在 hello**虛擬網路**刀鋒視窗中，按一下您想從對等互連 toodelete hello 虛擬網路。
4. 在 hello 刀鋒視窗中出現的 hello 您選取的虛擬網路，按一下 **對等互連**下**設定**。
5. Hello 在清單中會出現在 hello 對等互連刀鋒視窗中，以滑鼠右鍵按一下 hello 對等互連您想 toodelete 的對等互連，按一下 **刪除**，然後**是**toodelete hello hello 的第一個虛擬網路從對等互連。
6. 完整的 hello 上一個步驟 toodelete hello 從對等互連 hello hello 對等互連中的其他虛擬網路。

**命令**

|工具|命令|
|---|---|
|CLI|[az network vnet peering delete](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>需求和限制 

- 您對等的 hello 虛擬網路必須具有非重疊的 IP 位址空間。
- 一旦虛擬網路與另一個虛擬網路對等互連，您便無法在虛擬網路中新增或刪除位址空間。 tooadd 或移除位址空間，對等互連，刪除 hello 新增或移除 hello 位址空間，然後重新建立 hello 對等互連。 tooadd 位址空間，或移除虛擬網路位址空間讀取 hello[建立、 變更或刪除虛擬網路](virtual-network-manage-network.md#add-address-spaces)發行項。 
- 您可以對等透過資源管理員] 或 [虛擬網路與虛擬網路透過 hello 傳統部署模型部署部署透過資源管理員所部署的兩個虛擬網路。 您無法對等透過 hello 傳統部署模型所建立的兩個虛擬網路。 如果您不熟悉 Azure 的部署模型，請參閱 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。 您可以使用[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)tooconnect 兩個透過 hello 傳統部署模型所建立的虛擬網路。
- 當透過 Resource Manager 建立的兩個虛擬網路對等互連，對等互連必須設定每個虛擬網路中對等互連 hello。 當您從 hello 的第一個虛擬網路建立 hello 對等互連 toohello 第二個虛擬網路時，hello 對等的狀態是*起始*。  當您建立 hello 從 hello 第二個虛擬網路 toohello 第一個虛擬網路進行對等互連時，其對等的狀態是*Connected*。 如果您檢視 hello hello 的第一個虛擬網路對等狀態時，您會看到其狀態變更從*起始*太*Connected*。 hello 對等互連，不會成功建立 hello 對等互連這兩個虛擬網路對等互連狀態直到*Connected*。 
- 當對等互連建立透過資源管理員透過 hello 傳統部署模型所建立的虛擬網路與虛擬網路，您只設定對等互連 hello 部署透過資源管理員的虛擬網路。 您無法設定虛擬網路 （傳統），或透過 hello 傳統部署模型所部署的兩個虛擬網路之間，對等互連。 當您建立從 hello 虛擬網路 （資源管理員） toohello 虛擬網路 （傳統） 的 hello 對等互連時，hello 對等的狀態是*更新*，然後很快就會隨之變更*已連接*。   
- 兩個虛擬網路之間建立了對等互連。 對等互連不具轉移性。 如果您在下列項目之間建立對等互連：
    - VirtualNetwork1 & VirtualNetwork2
    - VirtualNetwork2 & VirtualNetwork3

  則 VirtualNetwork1 與 VirtualNetwork3 之間並無法透過 VirtualNetwork2 而建立對等互連。 如果您想 toocreate 虛擬網路之間 VirtualNetwork1 VirtualNetwork3 對等互連，您尚未 toocreate VirtualNetwork1 之間 VirtualNetwork3 對等互連。
- 您無法使用預設的 Azure 名稱解析在對等互連的虛擬網路中解析名稱。 tooresolve 名稱中的其他虛擬網路，您必須使用自訂的 DNS 伺服器。 toolearn tooset DNS 伺服器，如何讀取 hello[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)發行項。
- 在對等互連 hello 這兩個虛擬網路中的資源可與對方進行通訊與 hello 相同頻寬和延遲就如同在 hello 相同虛擬網路。 不過，每個虛擬機器大小各有其網路頻寬上限。 深入了解不同的虛擬機器大小，讀取 hello 的最大網路頻寬 toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器大小的發行項。
- 您可以對等體的虛擬網路部署透過資源管理員會在 hello 相同，或不同的訂用帳戶。
- 您可以對等透過會在 hello 相同，不同的部署模型所部署的虛擬網路或不同的訂用帳戶 （預覽）。 
- hello 訂閱這兩個虛擬網路中必須是相關聯的 toohello 同一個 Azure Active Directory 租用戶。 如果您還沒有 AD 租用戶，您可以快速地[建立一個](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。 您可以使用[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)tooconnect 兩個不同的訂用帳戶中存在的虛擬網路相關聯 toodifferent Active Directory 租用戶。
- 虛擬網路可以是所以 tooanother 虛擬網路，而且也會連接的 tooanother 虛擬網路與 Azure 虛擬網路閘道。 當透過對等互連和閘道連線的虛擬網路時，則會在透過 hello 對等設定，而不是 hello 閘道流動 hello 虛擬網路之間的流量。
- 我們會針對使用虛擬網路對等互連的輸入和輸出流量收取少許費用。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/virtual-network)。


## <a name="permissions"></a>權限

您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。 例如，如果您已對等互連名為 myVnetA 和 myVnetB 的兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:
    
|虛擬網路|部署模型|角色|權限|
|---|---|---|---|
|myVnetA|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。

## <a name="next-steps"></a>接續步驟

深入了解如何 toocreate[中樞和支點網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
