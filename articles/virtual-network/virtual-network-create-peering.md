---
title: "Azure 虛擬網路對等互連-aaaCreate 資源管理員的相同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等虛擬網路之間透過 Resource Manager 建立存在於 hello 相同 Azure 訂用帳戶。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>建立虛擬網路對等互連 - Resource Manager，相同訂用帳戶

在此教學課程中，您學會 toocreate 虛擬網路透過 Resource Manager 建立的虛擬網路之間的對等互連。 這兩個虛擬網路中存在 hello 相同訂用帳戶。 在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。 深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。 

hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。 了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：

|Azure 部署模型  | Azure 訂閱  |
|--------- |---------|
|[兩者皆使用 Resource Manager](create-peering-different-subscriptions.md) |不同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models.md) |相同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models-subscriptions.md) |不同|

無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。 虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。 如果您需要同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區 tooconnect 虛擬網路，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。 

您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，Azure [PowerShell](#powershell)，或[Azure Resource Manager 範本](#template) toocreate 虛擬網路對等互連。 直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。

## <a name="portal"></a>建立對等互連 - Azure 入口網站

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
2. 依序按一下 [新增]、[網路] 及 [虛擬網路]。
3. 在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:
    - **名稱**：*myVnet1*
    - **位址空間**：*10.0.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.0.0.0/24*
    - **訂用帳戶**︰選取您的訂用帳戶
    - **資源群組**：選取 [新建] 並輸入 *myResourceGroup*
    - **位置**：*美國東部*
4. 完成步驟 2-3 再次指定 hello 遵循步驟 3 中的值：
    - **名稱**： *myVnet2*
    - **位址空間**：*10.1.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.1.0.0/24*
    - **訂用帳戶**︰選取您的訂用帳戶
    - **資源群組**：選取 [使用現有] 並選取 *myResourceGroup*
    - **位置**：*美國東部*
5. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myResourceGroup*。 按一下**myResourceGroup** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myresourcegroup**資源群組。 hello 資源群組包含兩個 hello 前述步驟中建立虛擬網路。
6. 按一下 [myVNet1]。
7. 在 [hello **myVnet1**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。
8. 在 hello **myVnet1-對等互連**刀鋒視窗中出現，按一下**+ 新增**
9. 在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:
     - **名稱**：*myVnet1ToMyVnet2*
     - **虛擬網路部署模型**：選取 [Resource Manager]。 
     - **訂用帳戶**︰選取您的訂用帳戶
     - **虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。
     - **允許虛擬網路存取**：確定已選取 [啟用]。
    本教學課程中不會使用其他設定。 讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。
10. 按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnet1-對等互連**刀鋒視窗一次。 幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。 **起始**會列在 hello**對等互連狀態**hello 的資料行**myVnet1ToMyVnet2**對等互連您建立。 您已所以 Vnet1 tooVnet2，但現在 myVnet2 toomyVnet1 必須對等。 對等互連 hello 必須建立兩個方向 hello 虛擬網路 toocommunicate tooenable 資源彼此。
11. 針對 myVnet2 再次完成步驟 5-10。  名稱 hello 對等互連*myVnet2ToMyVnet1*。
12. 幾秒鐘後按一下**[確定]** toocreate hello 對等 MyVnet2，hello **myVnet2ToMyVnet1**對等互連您剛建立列為**已連接**hello中**對等互連狀態**資料行。
13. 針對 MyVnet1 再次完成步驟 5-7。 hello**對等互連狀態**hello **myVnet1ToVNet2**對等互連現在也是**Connected**。 之後您會看到 hello 對等互連已成功建立**Connected**在 hello**對等互連狀態**中 hello 對等互連這兩個虛擬網路的資料行。
14. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
15. **選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。

所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

## <a name="cli"></a>建立對等互連 - Azure CLI

下列指令碼的 hello:

- 需要 hello Azure CLI 版本 2.0.4 或更新版本。 toofind hello 版本，執行 hello`az --version`命令。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。
- 適用於 Bash 殼層。 在 Windows 用戶端上執行 Azure CLI 指令碼選項，請參閱[Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 

而不是安裝 hello CLI 和其相依性，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 按一下 hello**試試**按鈕，如下所示，記錄您的雲端殼層會叫用來登入 tooyour hello 指令碼中使用的 Azure 帳戶。 tooexecute hello 指令碼中，按一下 hello**複製**按鈕，然後將 hello 內容貼到您的雲端 Shell。

1. 建立一個資源群組和兩個虛擬網路。

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. 建立對等互連 hello 兩個虛擬網路之間的虛擬網路。
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Hello 指令碼執行之後，請檢閱每個虛擬網路的對等互連 hello。 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Hello 之前再次執行命令，取代*myVnet1*與*myVnet2*。 hello 輸出兩個命令顯示**Connected**在 hello **PeeringState**資料行。

     所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

4. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
5. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。


## <a name="powershell"></a>建立對等互連 - PowerShell

1. 安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. toostart PowerShell 工作階段，跳過**啟動**，輸入**powershell**，然後按一下 **PowerShell**。
3. 在 PowerShell 中，登入 tooAzure 輸入 hello`login-azurermaccount`命令。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
4. 建立一個資源群組和兩個虛擬網路。 tooexecute hello 指令碼中，複製 hello 下列指令碼，將它貼到 PowerShell，然後按`Enter`囉 」 畫面上出現 hello 最後一行之後：

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. 建立對等互連 hello 兩個虛擬網路之間的虛擬網路。 複製 hello 下列指令碼，在 tooPowerShell，貼上，然後按`Enter`囉 」 畫面上出現 hello 最後一行之後：
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello 子網路的 hello 虛擬網路，複本 hello 下列命令，在 tooPowerShell，貼上，然後按`Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hello 之前再次執行命令，取代*myVnet1*與*myVnet2*。 hello 輸出兩個命令顯示**Connected**在 hello **PeeringState**資料行。
7. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
8. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。

所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

## <a name="template"></a>建立對等互連 - Resource Manager 範本

1. 參考[建立虛擬網路對等互連](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager 範本。 指示會提供搭配 hello 範本部署 hello 範本使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI。 登入您選擇使用的帳戶具有 toodeploy hello 範本 toowhichever 工具 hello toocreate 必要的權限的虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
2. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
3. **選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete)> 一節的本文中，使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI。

## <a name="permissions"></a>權限

您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。 例如，如果您已對等互連名為 VNet1 和 VNet2 這兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:
    
|虛擬網路|角色|權限|
|---|---|---|
|VNet1|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。

## <a name="delete"></a>刪除資源
當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。 刪除資源群組時，也會刪除 hello 資源群組中的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。 在 hello 搜尋結果中，按一下  **myResourceGroup**。
2. 在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。
3. tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。

### <a name="delete-cli"></a>Azure CLI

輸入下列命令的 hello:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

輸入下列命令的 hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>後續步驟

- 請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。
- 了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。
- 了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。
