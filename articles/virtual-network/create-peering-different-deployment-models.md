---
title: "aaaCreate Azure 虛擬網路對等式不同的部署模型的相同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等虛擬網路之間建立透過不同的 Azure 部署模型中存在 hello 相同 Azure 訂用帳戶。"
services: virtual-network
documentationcenter: 
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
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>建立虛擬網路對等互連 - 不同部署模型、相同訂用帳戶 

在此教學課程中，您學會 toocreate 對等互連是透過不同的部署模型建立的虛擬網路之間的虛擬網路。 這兩個虛擬網路中存在 hello 相同訂用帳戶。 在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。 深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。 

hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。 了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：

|Azure 部署模型  | Azure 訂閱  |
|--------- |---------|
|[兩者皆使用 Resource Manager](virtual-network-create-peering.md) |相同|
|[兩者皆使用 Resource Manager](create-peering-different-subscriptions.md) |不同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models-subscriptions.md) |不同|

無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。 虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。 如果您需要同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區 tooconnect 虛擬網路，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。 

您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，或 Azure [PowerShell](#powershell) toocreate 虛擬網路對等互連。 直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。

## <a name="cli"></a>建立對等互連 - 入口網站

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
4. 按一下 [+ 新增]。 在 hello**搜尋 hello Marketplace**方塊中，輸入*虛擬網路*。 按一下**虛擬網路**hello 搜尋結果中出現。 
5. 在 hello**虛擬網路**刀鋒視窗中，選取**傳統**在 hello**選取部署模型**方塊，然後再按一下**建立**。
6. 在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:
    - **名稱**： *myVnet2*
    - **位址空間**：*10.1.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.1.0.0/24*
    - **訂用帳戶**︰選取您的訂用帳戶
    - **資源群組**：選取 [使用現有] 並選取 *myResourceGroup*
    - **位置**：*美國東部*
7. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myResourceGroup*。 按一下**myResourceGroup** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myresourcegroup**資源群組。 hello 資源群組包含兩個 hello 前述步驟中建立虛擬網路。
8. 按一下 [myVNet1]。
9. 在 [hello **myVnet1**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。
10. 在 hello **myVnet1-對等互連**刀鋒視窗中出現，按一下**+ 新增**
11. 在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:
     - **名稱**：*myVnet1ToMyVnet2*
     - **虛擬網路部署模型**︰選取 [傳統]。 
     - **訂用帳戶**︰選取您的訂用帳戶
     - **虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。
     - **允許虛擬網路存取**：確定已選取 [啟用]。
    本教學課程中不會使用其他設定。 讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。
12. 按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnet1-對等互連**刀鋒視窗一次。 幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。 **連接**會列在 hello**對等互連狀態**hello 的資料行**myVnet1ToMyVnet2**對等互連您建立。

    現在建立 hello 對等互連。 所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。
13. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
14. **選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。

## <a name="cli"></a>建立對等互連 - Azure CLI

1. [安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)hello Azure CLI 1.0 toocreate hello 虛擬網路 （傳統）。
2. 開啟 命令工作階段並登入使用 hello tooAzure`azure login`命令。
3. 服務管理模式中執行 hello CLI，方式是輸入 hello`azure config mode asm`命令。
4. 輸入下列命令 toocreate hello 虛擬網路 （傳統） 的 hello:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. 建立資源群組和虛擬網路 (Resource Manager)。 您可以使用 hello CLI 1.0 或 2.0 ([安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json))。 在本教學課程，hello CLI 2.0 都是使用的 toocreate hello 虛擬網路 （資源管理員），因為 2.0 必須為使用的 toocreate hello 對等互連。 執行的 hello 下列撞 CLI 指令碼，從本機電腦與 hello CLI 2.0.4 安裝或更新版本。 如選項上執行被 Windows 用戶端上的 CLI 指令碼，請參閱 < [Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 您也可以執行使用 hello Azure 雲端殼層 hello 指令碼。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 按一下 hello**試試**按鈕，如下所示，記錄您的雲端殼層會叫用來登入 tooyour hello 指令碼中使用的 Azure 帳戶。 tooexecute hello 指令碼中，按一下 hello**複製**按鈕和 貼上，hello 內容到您的雲端殼層，然後按`Enter`。

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. 建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。 使用您的訂用帳戶 ID 來取代 `<subscription id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。 hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。Tooyour CLI 工作階段中，貼上 hello 修改指令碼，然後按下`Enter`。

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。 複製 hello 下列命令，將它貼入您的 CLI 工作階段中，然後按`Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。 

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。
8. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
9. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。

## <a name="powershell"></a>建立對等互連 - PowerShell

1. 安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)和[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段。
3. 在 PowerShell 中，登入 tooAzure 輸入 hello`Add-AzureAccount`命令。
4. toocreate 具有 PowerShell （傳統） 的虛擬網路，您必須建立新的或修改現有的網路組態檔。 了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 hello 檔案應該包含 hello 下列**VirtualNetworkSite** hello 這個教學課程中使用的虛擬網路的項目：

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > 匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。 確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。 
5. 登入 tooAzure toocreate hello 虛擬網路 （資源管理員） 中，輸入 hello`login-azurermaccount`命令。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
6. 建立資源群組和虛擬網路 (Resource Manager)。 複製 hello 指令碼，將它貼到 PowerShell，然後按`Enter`。

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. 建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。 使用您的訂用帳戶 ID 來取代 `<subscription id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。 hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。 tooexecute hello 指令碼中，複製 hello 修改指令碼從您的文字編輯器，然後以滑鼠右鍵按一下您的 PowerShell 工作階段，然後按`Enter`。

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。 複製 hello 下列命令，將它貼入您的 PowerShell 工作階段中，然後按`Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

9. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
10. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。
 
## <a name="permissions"></a>權限

您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。 例如，如果您已對等互連名為 myVnet1 和 myVnet2 的兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:
    
|虛擬網路|部署模型|角色|權限|
|---|---|---|---|
|myVnet1|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnet2|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。

## <a name="delete"></a>刪除資源
當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。 刪除資源群組時，也會刪除 hello 資源群組中的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。 在 hello 搜尋結果中，按一下  **myResourceGroup**。
2. 在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。
3. tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。

### <a name="delete-cli"></a>Azure CLI

1. 使用下列命令的 hello hello Azure CLI 2.0 toodelete hello 虛擬網路 （資源管理員）：

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. 使用下列命令的 hello hello Azure CLI 1.0 toodelete hello 虛擬網路 （傳統）：

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. 輸入下列命令 toodelete hello 虛擬網路 （資源管理員） 的 hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello 虛擬網路 （傳統） 使用 PowerShell，您必須修改現有的網路組態檔。 了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 移除下列 hello 這個教學課程中使用的虛擬網路的 VirtualNetworkSite 元素 hello:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > 匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。 請務必僅卸除 hello 的上一個虛擬網路，且您不變更或移除您的訂用帳戶中的任何其他現有的虛擬網路。 

## <a name="next-steps"></a>後續步驟

- 請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。
- 了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。
- 了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。
