---
title: "aaaCreate Azure 虛擬網路的資源管理員的對等互連不同的訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等互連虛擬網路之間透過 Resource Manager 建立存在於不同的 Azure 訂用帳戶中。"
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>建立虛擬網路對等互連 - Resource Manager，不同訂用帳戶 

在此教學課程中，您學會 toocreate 虛擬網路透過 Resource Manager 建立的虛擬網路之間的對等互連。 hello 虛擬網路位於不同的訂用帳戶。 在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。 深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。 

hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。 了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：

|Azure 部署模型  | Azure 訂閱  |
|--------- |---------|
|[兩者皆使用 Resource Manager](virtual-network-create-peering.md) |相同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models.md) |相同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models-subscriptions.md) |不同|

無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。 虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。 當建立對等互連存在不同的訂用帳戶，hello 兩者都必須是訂用帳戶中的虛擬網路之間的虛擬網路相關聯 toohello 相同 Azure Active Directory 租用戶。 如果您還沒有 Azure Active Directory 租用戶，可以快速地[建立一個租用戶](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。 如果您需要 tooconnect 虛擬網路同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區，或存在於訂用帳戶相關聯 toodifferent Azure Active Directory 租用戶，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。 

您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，或 Azure [PowerShell](#powershell) toocreate 虛擬網路對等互連。 直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。

## <a name="portal"></a>建立對等互連 - Azure 入口網站

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用相同的所有步驟的帳戶，請略過記錄超出 hello 入口網站的 hello 步驟和略過 hello 步驟指定另一位使用者的權限 toohello 虛擬網路的 hello。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)UserA 為。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
2. 依序按一下 [新增]、[網路] 及 [虛擬網路]。
3. 在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:
    - **名稱**：*myVnetA*
    - **位址空間**：*10.0.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.0.0.0/24*
    - **訂用帳戶**︰選取訂用帳戶 A。
    - **資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupA*
    - **位置**：*美國東部*
4. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetA*。 按一下**myVnetA** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnetA**虛擬網路。
5. 在 [hello **myVnetA**刀鋒視窗中，按一下**存取控制 (IAM)**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。
6. 在 hello **myVnetA-存取控制 (IAM)**刀鋒視窗中，按一下**+ 加**。
7. 在 hello**新增權限**刀鋒視窗中，選取**網路參與者**在 hello**角色**方塊。
8. 在 hello**選取**方塊中，選取使用者 b，或輸入使用者 b 的電子郵件地址 toosearch。 hello 使用者顯示的清單是來自 hello 與 hello 虛擬網路的同一個 Azure Active Directory 租用戶您正要設定 hello 對等。
9. 按一下 [儲存] 。
10. 在 hello **myVnetA-存取控制 (IAM)**刀鋒視窗中，按一下 **屬性**從 hello 垂直 hello 左邊的 hello 刀鋒視窗上的選項清單。 複製 hello**資源識別碼**，這用於後續的步驟。 hello 資源識別碼是下列範例類似 toohello: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA。
11. 登出 hello 入口網站為使用者 a，則 UserB 身分登入。
12. 完成步驟 2-3，輸入或選取 hello 遵循步驟 3 中的值：

    - **名稱**：*myVnetB*
    - **位址空間**：*10.1.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.1.0.0/24*
    - **訂用帳戶**︰選取訂用帳戶 B。
    - **資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupB*
    - **位置**：*美國東部*

13. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetB*。 按一下**myVnetB** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnetB**虛擬網路。
14. 在 [hello **myVnetB**刀鋒視窗中，按一下**屬性**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。 複製 hello**資源識別碼**，這用於後續的步驟。 hello 資源識別碼是下列範例類似 toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB。
15. 按一下**存取控制 (IAM)**在 hello **myVnetB**刀鋒視窗，然後完成步驟 5-10 的 myVnetB，輸入**UserA**在步驟 8。
16. 登出為 UserB hello 入口網站，並以 UserA 登入。
17. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetA*。 按一下**myVnetA** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnet**虛擬網路。
18. 按一下 [myVnetA]。
19. 在 [hello **myVnetA**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。
20. 在 hello **myVnetA-對等互連**刀鋒視窗中出現，按一下**+ 新增**
21. 在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:
     - **名稱**：*myVnetAToMyVnetB*
     - **虛擬網路部署模型**：選取 [Resource Manager]。
     - **我知道我的資源識別碼**：核取此方塊。
     - **資源識別碼**： 步驟 14 中輸入 hello 資源識別碼。
     - **允許虛擬網路存取**：確定已選取 [啟用]。
    本教學課程中不會使用其他設定。 讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。
22. 按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnetA-對等互連**刀鋒視窗一次。 幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。 **起始**會列在 hello**對等互連狀態**hello 的資料行**myVnetAToMyVnetB**對等互連您建立。 您已所以 myVnetA toomyVnetB，但現在 myVnetB toomyVnetA 必須對等。 對等互連 hello 必須建立兩個方向 hello 虛擬網路 toocommunicate tooenable 資源彼此。
23. 登出 hello 入口網站為使用者 a 和使用者 b 的身分登入。
24. 針對 myVnetB 完成步驟 17 到 21。 在 21 步驟中，命名為對等互連 hello *myVnetBToMyVnetA*，選取*myVnetA*如**虛擬網路**，，輸入 hello 識別碼與步驟 10 中 hello **的資源識別碼**方塊。
25. 幾秒鐘後按一下**[確定]** toocreate hello 對等 myVnetB，hello **myVnetBToMyVnetA**對等互連您剛建立列為**已連接**hello中**對等互連狀態**資料行。
26. 登出為 UserB hello 入口網站，並以 UserA 登入。
27. 再次完成步驟 17 到 19。 hello**對等互連狀態**hello **myVnetAToVNetB**對等互連現在也是**Connected**。 之後您會看到 hello 對等互連已成功建立**Connected**在 hello**對等互連狀態**中 hello 對等互連這兩個虛擬網路的資料行。 所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。
28. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
29. **選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。

## <a name="cli"></a>建立對等互連 - Azure CLI

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。 取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。

下列指令碼的 hello:

- 需要 hello Azure CLI 版本 2.0.4 或更新版本。 toofind hello 版本，執行`az --version`。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。
- 適用於 Bash 殼層。 在 Windows 用戶端上執行 Azure CLI 指令碼選項，請參閱[Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 

而不是安裝 hello CLI 和其相依性，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 按一下 hello**試試**hello 指令碼，如下所示會叫用一個雲端 shell 工具，您可以登入 tooyour Azure 帳戶中的按鈕。 

1. 開啟 CLI 工作階段，並以 UserA 使用 hello 登入 tooAzure`azure login`命令。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
2. 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello，取代`<SubscriptionA-Id>`以 hello SubscriptionA 的識別碼，然後複製 hello 修改指令碼，將它貼入您 CLI 工作階段，然後按中`Enter`。 如果您不知道您的訂用帳戶 Id，請輸入 hello 'az 帳戶顯示' 命令。 hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     使用者 b 的 hello 的權限指派並不是需求。 對等互連可建立即使使用者個別引發其各自的虛擬網路的對等要求，只要 hello 要求相符項目。 網路參與者 hello 本機虛擬網路中新增 myVNetB 高權限的使用者，讓它更輕鬆地 toodo hello 設定。
3. 登出 Azure，以使用 hello UserA`az logout`命令，然後登入為 UserB tooAzure。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
4. 建立 myVnetB。 在您的電腦上的步驟 2 tooa 文字編輯器中複製 hello 指令碼內容。 取代`<SubscriptionA-Id>`以 hello SubscriptionB 的識別碼。 變更 10.0.0.0/16 too10.1.0.0/16、 變更為 tooB，以及所有 Bs tooA。 複製 hello 修改指令碼，請將它貼入中 tooyour CLI 工作階段，然後按`Enter`。 
5. 登出 UserB 身分登入 Azure，並登入為 UserA tooAzure。
6. 建立虛擬網路從 myVnetA toomyVnetB 對等互連。 複製下列指令碼內容 tooa 文字編輯器在您的電腦上的 hello。 取代`<SubscriptionB-Id>`以 hello SubscriptionB 的識別碼。 tooexecute hello 指令碼中，複製 hello 修改指令碼、 將它貼到您的 CLI 工作階段，然後按 Enter。
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. 檢視 myVnetA hello 對等互連狀態。

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    hello 狀態是**起始**。 它會隨之變更**Connected** myVnetB 從建立 hello 對等互連 toomyVnetA 之後。

8. 登出使用者 a 從 Azure，並登入為 UserB tooAzure。
9. 建立從 myVnetB toomyVnetA 的 hello 對等互連。 在您的電腦上的步驟 6 tooa 文字編輯器中複製 hello 指令碼內容。 取代`<SubscriptionB-Id>`SubscriptionA，全部都做為 tooB 和所有 Bs tooA 變更 hello 識別碼。 複製 hello 做好 hello 變更後，修改指令碼，將它貼到您的 CLI 工作階段，然後按`Enter`。
10. 檢視 myVnetB hello 對等互連狀態。 在您的電腦上的步驟 7 tooa 文字編輯器中複製 hello 指令碼內容。 變更 tooB hello 資源群組和虛擬網路名稱，將 hello 指令碼複製、 tooyour CLI 工作階段中，貼上 hello 修改指令碼，然後按`Enter`。 hello 對等互連狀態是**Connected**。 hello myVnetA 變更的對等互連狀態太**Connected**建立 hello 對等互連從 myVnetB toomyVnetA 之後。 您可以 UserA 回重新登入 tooAzure 和完成的步驟 7 的 myVnetA tooverify hello 對等互連狀態。 

    > [!NOTE]
    > hello 對等互連，不會建立 hello 對等互連狀態直到**Connected**兩個虛擬網路。

11. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
12. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。

所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。
 
## <a name="powershell"></a>建立對等互連 - PowerShell

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。 取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。

1. 安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段。
3. 在 PowerShell 中，以登入 tooAzure UserA 輸入 hello`login-azurermaccount`命令。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
4. 建立資源群組和虛擬網路 a 複製 hello 下列指令碼 tooa 文字編輯器在您的電腦上。 取代`<SubscriptionA-Id>`以 hello SubscriptionA 的識別碼。 如果您不知道您的訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。 hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。 tooexecute hello 指令碼中，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    使用者 b 的 hello 的權限指派並不是需求。 對等互連可建立即使使用者個別引發其各自的虛擬網路的對等要求，只要 hello 要求相符項目。 新增授權的使用者的 hello hello 區域虛擬網路中的使用者的其他虛擬網路讓您更輕鬆地 toodo hello 設定。
5. 將 UserA 登出 Azure，然後以 UserB 身分登入。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
6. 在您的電腦上的步驟 4 tooa 文字編輯器中複製 hello 指令碼內容。 取代`<SubscriptionA-Id>`針對訂用帳戶 B.變更 10.0.0.0/16 too10.1.0.0/16 hello 識別碼。 所有以 tooB 和所有 Bs tooA 變更。 tooexecute hello 指令碼中，複製 hello 修改指令碼，powershell 中，貼上，然後按`Enter`。
7. 將 UserB 登出 Azure，然後以 UserA 身分登入。
8. 建立從 myVnetA toomyVnetB 的 hello 對等互連。 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。 取代`<SubscriptionB-Id>`識別碼 hello 為訂用帳戶 B.tooexecute hello 指令碼，複製 hello 修改指令碼，在 tooPowerShell，貼上，然後按`Enter`。
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. 檢視 myVnetA hello 對等互連狀態。

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    hello 狀態是**起始**。 它會隨之變更**Connected**一旦您設定從 myVnetB hello 對等互連 toomyVnetA。

10. 將 UserA 登出 Azure，然後以 UserB 身分登入。
11. 建立從 myVnetB toomyVnetA 的 hello 對等互連。 在您的電腦上的步驟 8 tooa 文字編輯器中複製 hello 指令碼內容。 取代`<SubscriptionB-Id>`hello 識別碼的所有訂用帳戶的和變更的 tooB 和所有 B tooA。 tooexecute hello 指令碼中，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。
12. 檢視 myVnetB hello 對等互連狀態。 在您的電腦上的步驟 9 tooa 文字編輯器中複製 hello 指令碼內容。 變更 tooB hello 資源群組和虛擬網路名稱。 tooexecute hello 指令碼，hello 修改指令碼貼到 PowerShell，並按一下`Enter`。 hello 狀態是**Connected**。 hello 的對等互連狀態**myVnetA**會隨之變更**Connected**建立 hello 對等互連從之後**myVnetB**太**myVnetA**。 您可以記錄 UserA tooAzure 和完成 步驟 9 中的回一次的 myVnetA tooverify hello 對等互連狀態。 

    > [!NOTE]
    > hello 對等互連，不會建立 hello 對等互連狀態直到**Connected**兩個虛擬網路。

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

13. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
14. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。

## <a name="permissions"></a>權限

您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。 例如，如果您兩個虛擬網路，名為對等互連**myVnetA**和**myVnetB**，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:
    
|虛擬網路|角色|權限|
|---|---|---|
|myVnetA|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。

## <a name="delete"></a>刪除資源
當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。 刪除資源群組時，也會刪除 hello 資源群組中的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 以登入 toohello Azure 入口網站使用者 a。
2. 在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroupA**。 在 hello 搜尋結果中，按一下  **myResourceGroupA**。
3. 在 hello **myResourceGroupA**刀鋒視窗中，按一下 hello**刪除**圖示。
4. tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroupA**，然後按一下**刪除**。
5. 登出 hello 入口網站為使用者 a 和使用者 b 的身分登入。
6. 針對 myResourceGroupB，完成步驟 2 到 4。

### <a name="delete-cli"></a>Azure CLI

1. 登入為 UserA tooAzure，然後執行下列命令的 hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. 以 UserA 身分登出 Azure，然後以 UserB 身分登入。
3. 執行下列命令的 hello:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. 登入為 UserA tooAzure，然後執行下列命令的 hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. 以 UserA 身分登出 Azure，然後以 UserB 身分登入。
3. 執行下列命令的 hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>後續步驟

- 請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。
- 了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。
- 了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。
