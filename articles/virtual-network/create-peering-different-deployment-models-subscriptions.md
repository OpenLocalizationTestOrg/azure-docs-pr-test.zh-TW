---
title: "建立 Azure 虛擬網路對等互連 - 不同部署模型 - 不同訂用帳戶 |Microsoft Docs"
description: "了解如何在透過不同 Azure 部署模型建立且存在於不同 Azure 訂用帳戶中的虛擬網路之間，建立虛擬網路對等互連。"
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
ms.date: 09/15/2017
ms.author: jdial;anavin
ms.openlocfilehash: 441bb0a269de400c82abc083118f5e0642523640
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>建立虛擬網路對等互連 - 不同部署模型和訂用帳戶

在本教學課程中，您會了解如何在透過不同部署模型建立的虛擬網路之間，建立虛擬網路對等互連。 這些虛擬網路存在於不同的訂用帳戶中。 對等互連兩個虛擬網路，可讓不同虛擬網路中的資源彼此通訊，且通訊時會有相同的頻寬和延遲，彷彿這些資源是位於相同的虛擬網路中。 深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。

建立虛擬網路對等互連的步驟會因一些因素而有所不同，這取決於虛擬網路是位於相同還是不同的訂用帳戶中，以及是透過哪一個 [Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立虛擬網路。 請按一下下表中的案例，以了解如何在其他案例中建立虛擬網路對等互連：

|Azure 部署模型  | Azure 訂閱  |
|--------- |---------|
|[兩者皆使用 Resource Manager](virtual-network-create-peering.md) |相同|
|[兩者皆使用 Resource Manager](create-peering-different-subscriptions.md) |不同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models.md) |相同|

虛擬網路對等互連無法在透過傳統部署模型建立的兩個虛擬網路之間建立。 目前，只有預覽中的功能能夠對等互連透過不同訂用帳戶中不同部署模型建立的虛擬網路。 若要完成本教學課程，您必須先[註冊](#register)以使用該功能。 本教學課程會使用存在同一個區域中的虛擬網路。 將不同區域中的虛擬網路視為對等的功能也是處於預覽狀態。 若要使用這項功能，您也必須先[註冊](#register)。 這兩個功能各自獨立。 若要完成本教學課程，您必須只註冊能夠將透過不同訂用帳戶中不同部署模型建立的虛擬網路對等互連的功能。 

在存在於不同訂用帳戶中的虛擬網路之間建立虛擬網路對等互連時，兩個訂用帳戶必須都與相同的 Azure Active Directory 租用戶關聯。 如果您還沒有 Azure Active Directory 租用戶，可以快速地[建立一個租用戶](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。 

無論虛擬網路是透過與相同或不同 Azure Active Directory 租用戶相關聯的部署模型、不同部署模型、不同區域或訂用帳戶所建立，能使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)來連線至這些虛擬網路的功能已在預覽版本中，且不需要註冊。

您可以使用 [Azure 入口網站](#portal)、Azure [命令列介面](#cli) (CLI) 或 Azure [PowerShell](#powershell) 來建立虛擬網路對等互連。 按一下任何先前的工具連結，直接前往使用您所選工具建立虛擬網路對等互連的步驟。

## <a name="portal"></a>建立對等互連 - Azure 入口網站

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出入口網站的步驟，以及略過指派另一位使用者權限給虛擬網路的步驟。 在完成下列任何步驟之前，您必須先註冊預覽版。 若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。 如果您沒有在預覽中註冊這兩個訂用帳戶，則剩下的步驟皆會失敗。
 
1. 以 UserA 身分登入 [Azure 入口網站](https://portal.azure.com)。 您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。 如需詳細資訊，請參閱本文的[權限](#permissions)一節。
2. 依序按一下 [新增]、[網路] 及 [虛擬網路]。
3. 在 [建立虛擬網路] 刀鋒視窗上，輸入或選取下列設定的值，然後按一下 [建立]：
    - **名稱**：*myVnetA*
    - **位址空間**：*10.0.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.0.0.0/24*
    - **訂用帳戶**︰選取訂用帳戶 A。
    - **資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupA*
    - **位置**：*美國東部*
4. 在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetA*。 當 myVnetA 出現在搜尋結果中時，按一下 [myVnetA]。 隨即會顯示 [myVnetA] 虛擬網路刀鋒視窗。
5. 在顯示的 [myVnetA] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [存取控制 (IAM)]。
6. 在顯示的 [myVnetA - 存取控制 (IAM)] 刀鋒視窗中，按一下 [+ 新增]。
7. 在顯示的 [新增權限] 刀鋒視窗中，選取 [角色] 方塊中的 [網路參與者]。
8. 在 [選取] 方塊中，選取 [UserB]，或輸入 UserB 的電子郵件地址來搜尋它。 顯示的使用者清單來自與您設定對等互連之虛擬網路相同的 Azure Active Directory 租用戶。 當 UserB 出現在清單中時，按一下 [UserB]。
9. 按一下 [儲存] 。
10. 以 UserA 身分登出入口網站，然後以 UserB 身分登入。
11. 按一下 [+ 新增]，在 [搜尋 Marketplace] 方塊中輸入*虛擬網路*，然後按一下搜尋結果中的 [虛擬網路]。
12. 在出現的 [虛擬網路] 刀鋒視窗中，於 [選取部署模型] 方塊中選取 [傳統]，然後按一下 [建立]。
13.   在顯示的 [建立虛擬網路 (傳統)] 方塊中，輸入下列值：

    - **名稱**：*myVnetB*
    - **位址空間**：*10.1.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.1.0.0/24*
    - **訂用帳戶**︰選取訂用帳戶 B。
    - **資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupB*
    - **位置**：*美國東部*

14. 在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetB*。 當 myVnetB 出現在搜尋結果中時，按一下 [myVnetB]。 隨即會顯示 [myVnetB] 虛擬網路刀鋒視窗。
15. 在顯示的 [myVnetB] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [屬性]。 複製 [資源識別碼]，在稍後的步驟中將會用到此識別碼。 資源識別碼與以下範例類似：/subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. 針對 myVnetB 完成步驟 5-9，其中在步驟 8 輸入 **UserA**。
17. 以 UserB 身分登出入口網站，然後以 UserA 身分登入。
18. 在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetA*。 當 myVnetA 出現在搜尋結果中時，按一下 [myVnetA]。 隨即會顯示 [myVnet] 虛擬網路刀鋒視窗。
19. 按一下 [myVnetA]。
20. 在顯示的 [myVnetA] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [對等]。
21. 在顯示的 [myVnetA - 對等互連] 刀鋒視窗中，按一下 [+ 新增]
22. 在顯示的 [新增對等互連] 刀鋒視窗中，輸入或選取下列選項，然後按一下 [確定]：
     - **名稱**：*myVnetAToMyVnetB*
     - **虛擬網路部署模型**︰選取 [傳統]。
     - **我知道我的資源識別碼**：核取此方塊。
     - **資源識別碼**： 輸入來自步驟 15 的 myVnetB 資源識別碼。
     - **允許虛擬網路存取**：確定已選取 [啟用]。
    本教學課程中不會使用其他設定。 若要了解所有對等互連設定，請閱讀[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。
23. 在上一個步驟中按一下 [確定] 之後，[新增對等互連] 刀鋒視窗隨就會關閉，而您則會再次看到 [myVnetA - 對等] 刀鋒視窗。 幾秒之後，您建立的對等互連會出現在刀鋒視窗中。 您所建立之 **myVnetAToMyVnetB** 對等互連的 [對等互連狀態] 資料行中會列出 [已連接]。 現在已建立對等互連。 沒有必要將虛擬網路 (傳統) 對等互連到虛擬網路 (Resource Manager)。

    您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。 如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。 如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。 了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

24. **選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。
25. **選擇性︰**若要刪除您在本教學課程中建立的資源，請完成本文之[刪除資源](#delete-portal)一節中的步驟。

## <a name="cli"></a>建立對等互連 - Azure CLI

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出 Azure 的步驟，以及移除建立使用者角色指派項目的指令碼行。 請使用您要用於 UserA 和 UserB 的使用者名稱來取代下列指令碼中的 UserA@azure.com 和 UserB@azure.com。 

在完成下列任何步驟之前，您必須先註冊預覽版。 若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。 如果您沒有在預覽中註冊這兩個訂用帳戶，則剩下的步驟皆會失敗。

1. [安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 1.0 以建立虛擬網路 (傳統)。
2. 開啟 CLI 工作階段，然後使用 `azure login` 命令來以 UserB 身分登入 Azure。
3. 輸入 `azure config mode asm` 命令來以「服務管理」模式執行 CLI。
4. 輸入下列命令來建立虛擬網路 (傳統)：
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. 完成剩餘步驟的方式是必須使用 Bash 殼層並搭配[安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 2.0.4 或更新版本，或是使用 Azure Cloud Shell。 Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。 它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。 按一下以下指令碼中的 [試試看] 按鈕，這會開啟可讓您登入 Azure 帳戶的 Cloud Shell。 如需在 Windows 用戶端上執行 Bash CLI 指令碼的選項，請參閱[在 Windows 中執行 Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 
6. 將下列指令碼複製到您電腦上的文字編輯器中。 使用您的訂用帳戶 ID 來取代 `<SubscriptionB-Id>` 。 如果您不知道您的訂用帳戶 ID，請輸入 `az account show` 命令。 輸出中的 **id** 值就是您的訂用帳戶 ID。請複製修改過的指令碼並貼到您的 CLI 2.0 工作階段中，然後按 `Enter`。 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    當您在步驟 4 中建立虛擬網路 (傳統) 時，Azure 是在 *Default-Networking* 資源群組中建立該虛擬網路。
7. 將 UserB 登出 Azure，然後在 CLI 2.0 中以 UserA 身分登入。
8. 建立資源群組和虛擬網路 (Resource Manager)。 請複製下列指令碼並貼到您的 CLI 工作階段中，然後按 `Enter`。 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get the id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions to myVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. 在透過不同部署模型建立的兩個虛擬網路之間，建立虛擬網路對等互連。 將下列指令碼複製到您電腦上的文字編輯器中。 使用您的訂用帳戶 ID 來取代 `<SubscriptionB-id>` 。如果您不知道您的訂用帳戶 ID，請輸入 `az account show` 命令。 輸出中的 **id** 值就是您的訂用帳戶 ID。Azure 已將您在步驟 4 中建立的虛擬網路 (傳統) 建立在名為 *Default-Networking* 的資源群組中。 請將修改過的指令碼貼到您的 CLI 工作階段中，然後按 `Enter`。

    ```azurecli-interactive
    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. 在指令碼執行之後，檢閱虛擬網路 (Resource Manager) 的對等互連。 請複製下列指令碼，然後將它貼到您的 CLI 工作階段中：

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    輸出會在 **PeeringState** 資料行中顯示 **Connected**。

    您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。 如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。 如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。 了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

11. **選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。
12. **選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-cli)中的步驟。

## <a name="powershell"></a>建立對等互連 - PowerShell

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出 Azure 的步驟，以及移除建立使用者角色指派項目的指令碼行。 請使用您要用於 UserA 和 UserB 的使用者名稱來取代下列指令碼中的 UserA@azure.com 和 UserB@azure.com。 

在完成下列任何步驟之前，您必須先註冊預覽版。 若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。 如果您沒有在預覽中註冊這兩個訂用帳戶，則剩下的步驟皆會失敗。

1. 安裝最新版的 PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) 和 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。 如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段。
3. 在 PowerShell 中，輸入 `Add-AzureAccount` 命令來以 UserB 身分登入 UserB 的訂用帳戶。
4. 若要使用 PowerShell 來建立虛擬網路 (傳統)，您必須建立一個新的或修改現有的網路組態檔。 了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 就本教學課程中使用的虛擬網路而言，此檔案應該包含下列 **VirtualNetworkSite** 元素：

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > 匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。 請確定您只新增先前的虛擬網路，並且未變更或移除您訂用帳戶中任何現有的虛擬網路。 

5. 輸入 `login-azurermaccount` 命令來以 UserB 身分登入 UserB 的訂用帳戶，以使用 Resource Manager 命令。
6. 將 UserA 權限指派給虛擬網路 B。將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 B 的 ID 來取代 `<SubscriptionB-id>`。如果您不知道訂用帳戶 ID，請輸入 `Get-AzureRmSubscription` 命令來檢視它。 傳回之輸出中的 **Id** 值就是您的訂用帳戶 ID。 Azure 已將您在步驟 4 中建立的虛擬網路 (傳統) 建立在名為 *Default-Networking* 的資源群組中。 若要執行指令碼，請複製修改過的指令碼並貼到 PowerShell 中，然後按 `Enter`。
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. 以 UserB 身分登出 Azure，然後輸入 `login-azurermaccount` 命令來以 UserA 身分登入 UserA 的訂用帳戶。 您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。 如需詳細資訊，請參閱本文的[權限](#permissions)一節。
8. 複製下列指令碼並貼到 PowerShell 中，然後按 `Enter`，以建立虛擬網路 (Resource Manager)：

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. 將 UserB 權限指派給 myVnetA。 將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 A 的 ID 來取代 `<SubscriptionA-Id>`。如果您不知道訂用帳戶 ID，請輸入 `Get-AzureRmSubscription` 命令來檢視它。 傳回之輸出中的 **Id** 值就是您的訂用帳戶 ID。 將修改過的指令碼版本貼到 PowerShell 中，然後按 `Enter` 來執行它。

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. 將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 B 的 ID 來取代 `<SubscriptionB-id>`。若要將 myVnetA 對等互連到 myVNetB，請複製修改過的指令碼並貼到 PowerShell 中，然後按 `Enter`。

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. 複製下列指令碼並貼到 PowerShell 中，然後按 `Enter`，以檢視 myVnetA 的對等互連狀態。

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    狀態為 **Connected**。 在您設定從 myVnetB 到 myVnetA 的對等互連之後，它就會變更為 **Connected**。

    您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。 如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。 如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。 了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

12. **選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。
13. **選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-powershell)中的步驟。

## <a name="permissions"></a>權限

您用於建立虛擬網路對等互連的帳戶必須具有必要的角色或權限。 例如，如果您是將名為 myVnetA 和 myVnetB 的兩個虛擬網路對等互連，您的帳戶就必須獲指派各個虛擬網路的下列最基本角色或權限：
    
|虛擬網路|部署模型|角色|權限|
|---|---|---|---|
|myVnetA|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)以及如何對[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)指派特定權限 (僅限 Resource Manager)。

## <a name="delete"></a>刪除資源
當您完成本教學課程時，您可能會想刪除您在教學課程中建立的資源，以免產生使用費。 刪除資源群組同時會刪除其內含的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 在入口網站搜尋方塊中，輸入 **myResourceGroupA**。 在搜尋結果中，按一下 [myResourceGroupA]。
2. 在 [myResourceGroupA] 刀鋒視窗中，按一下 [刪除] 圖示。
3. 若要確認刪除，請在 [輸入資源群組名稱] 方塊中輸入 **myResourceGroupA**，然後按一下 [刪除]。
4. 在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetB*。 當 myVnetB 出現在搜尋結果中時，按一下 [myVnetB]。 隨即會顯示 [myVnetB] 虛擬網路刀鋒視窗。
5. 在 [myVnetB] 刀鋒視窗中，按一下 [刪除]。
6. 若要確認刪除，請在 [刪除虛擬網路] 方塊中，按一下 [是]。

### <a name="delete-cli"></a>Azure CLI

1. 使用 CLI 2.0 來登入 Azure，以使用下列命令來刪除虛擬網路 (Resource Manager)：

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. 使用 Azure CLI 1.0 來登入 Azure，以使用下列命令來刪除虛擬網路 (傳統)：

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. 在 PowerShell 命令提示字元中，輸入下列命令來刪除虛擬網路 (Resource Manager)：

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. 若要使用 PowerShell 來刪除虛擬網路 (傳統)，您必須修改現有的網路組態檔。 了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 針對本教學課程中使用的虛擬網路，請移除下列 VirtualNetworkSite 元素：

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > 匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。 請確定您只移除先前的虛擬網路，並且未變更或移除您訂用帳戶中任何其他現有的虛擬網路。 

## <a name="register"></a>註冊預覽版

目前，只有預覽中的功能能夠對等互連透過不同訂用帳戶中不同 Azure 部署模型建立的虛擬網路。 預覽功能可能沒有與一般版本中的功能相同層級的可用性和可靠性。 如需預覽功能可用性和狀態的最新通知，請查看 [Azure 虛擬網路更新](https://azure.microsoft.com/updates/?product=virtual-network)頁面。 

您必須先註冊跨訂用帳戶和跨部署模型功能，才能使用。 使用 Azure PowerShell 或 Azure CLI，在要對等連線的虛擬網路所屬訂用帳戶中完成以下步驟：

### <a name="powershell"></a>PowerShell

1. 安裝最新版的 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。 如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段，然後使用 `Login-AzureRmAccount` 命令來登入 Azure。
3. 輸入下列命令，對於在您想要對等互連之每個虛擬網路適用的訂用帳戶註冊預覽：

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
4. 藉由輸入下列命令，確認您已註冊預覽版︰

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

    請等到您為兩個訂用帳戶輸入上述命令後所收到的 **RegistrationState** 輸出都變成 **Registered** 之後，才完成本文中入口網站、Azure CLI、PowerShell 或 Resource Manager 範本等節中的步驟。

> [!NOTE]
> 本教學課程會使用存在同一個區域中的虛擬網路。 將不同區域中的虛擬網路視為對等的功能也是處於預覽狀態。 若要註冊跨區域或全域對等互連，請使用 `-FeatureName AllowGlobalVnetPeering` (而不是 `-FeatureName AllowClassicCrossSubscriptionPeering`) 再次完成步驟 1-4。 這兩個功能彼此各自獨立。 您不需要兩個都註冊，除非您想要同時使用這兩個功能。 僅有限的區域 (初期為美國中西部、加拿大中部和美國西部 2) 可使用此功能。

### <a name="azure-cli"></a>Azure CLI

1. [安裝和設定 Azure CLI](/cli/azure/install-azure-cli?toc=%2Fazure%2Fvirtual-network%2Ftoc.json)。
2. 輸入 `az --version` 命令來確定您使用 2.0.18 版或更高版本的 Azure CLI。 如果不是，請安裝最新版本。
3. 使用 `az login` 命令登入 Azure。
4. 輸入下列命令來註冊預覽版︰

   ```azurecli-interactive
   az feature register --name AllowGlobalVnetPeering --namespace Microsoft.Network
   az provider register --name Microsoft.Network
   ```

5. 藉由輸入下列命令，確認您已註冊預覽版︰

    ```azurecli-interactive
    az feature show --name AllowGlobalVnetPeering --namespace Microsoft.Network
    ```

    請等到您為兩個訂用帳戶輸入上述命令後所收到的 **RegistrationState** 輸出都變成 **Registered** 之後，才完成本文中入口網站、Azure CLI、PowerShell 或 Resource Manager 範本等節中的步驟。

> [!NOTE]
> 本教學課程會使用存在同一個區域中的虛擬網路。 將不同區域中的虛擬網路視為對等的功能也是處於預覽狀態。 若要註冊跨區域或全域對等互連，請使用 `--name AllowGlobalVnetPeering` (而不是`--name AllowClassicCrossSubscriptionPeering`) 再次完成步驟 1-5。 這兩個功能彼此各自獨立。 您不需要兩個都註冊，除非您想要同時使用這兩個功能。 僅有限的區域 (初期為美國中西部、加拿大中部和美國西部 2) 可使用此功能。

## <a name="next-steps"></a>後續步驟

- 請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。
- 了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。
- 了解如何透過虛擬網路對等互連來[建立中樞和輪輻網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)。
