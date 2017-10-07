---
title: "Azure 虛擬網路對等互連-aaaCreate 不同的部署模型的不同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等互連虛擬網路之間建立透過存在於不同的 Azure 訂用帳戶中的不同的 Azure 部署模型。"
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>建立虛擬網路對等互連 - 不同部署模型和訂用帳戶

在此教學課程中，您學會 toocreate 對等互連是透過不同的部署模型建立的虛擬網路之間的虛擬網路。 hello 虛擬網路位於不同的訂用帳戶。 在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。 深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。 

hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。 了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：

|Azure 部署模型  | Azure 訂閱  |
|--------- |---------|
|[兩者皆使用 Resource Manager](virtual-network-create-peering.md) |相同|
|[兩者皆使用 Resource Manager](create-peering-different-subscriptions.md) |不同|
|[一個使用 Resource Manager、一個使用傳統部署模型](create-peering-different-deployment-models.md) |相同|

無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。 虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。 當建立對等互連存在不同的訂用帳戶，hello 兩者都必須是訂用帳戶中的虛擬網路之間的虛擬網路相關聯 toohello 相同 Azure Active Directory 租用戶。 如果您還沒有 Azure Active Directory 租用戶，可以快速地[建立一個租用戶](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。 如果您需要 tooconnect 虛擬網路同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區，或存在於訂用帳戶相關聯 toodifferent Azure Active Directory 租用戶，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。 

> [!WARNING]
> 在透過不同 Azure 部署模型建立且存在於不同訂用帳戶中的虛擬網路之間建立虛擬網路對等互連，目前是預覽版功能。 在此案例中建立的虛擬網路對等互連無權 hello 相同層級的可用性和可靠性，做為建立虛擬網路對等互連中案例一般可用性版本。 在此情況下建立的虛擬網路對等互連不受支援、可能功能受限，且可能並非在所有 Azure 區域中都可供使用。 Hello 上這項功能的可用性與狀態的最新通知，請檢查 hello [Azure 虛擬網路更新](https://azure.microsoft.com/updates/?product=virtual-network)頁面。

您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，或 Azure [PowerShell](#powershell) toocreate 虛擬網路對等互連。 直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。

## <a name="register"></a>Hello preview 的註冊

hello preview tooregister，完成 hello 遵照的步驟，針對包含虛擬網路的 hello 這兩個訂閱您想 toopeer。 hello tooregister 用於 hello 預覽的工具是 PowerShell。

1. 安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段，並登入使用 hello tooAzure`login-azurermaccount`命令。
3. 輸入下列命令的 hello 註冊 hello 預覽的訂用帳戶：

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    無法完成這篇文章的 hello 入口網站、 Azure CLI 或 PowerShell 章節中的 hello 步驟直到 hello **RegistrationState**輸出之後輸入下列命令的 hello 收到**註冊**這兩個訂用帳戶：

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>建立對等互連 - Azure 入口網站

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用相同的所有步驟的帳戶，請略過記錄超出 hello 入口網站的 hello 步驟和略過 hello 步驟指定另一位使用者的權限 toohello 虛擬網路的 hello。 在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。 tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。 請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。
 
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
8. 在 hello**選取**方塊中，選取使用者 b，或輸入使用者 b 的電子郵件地址 toosearch。 hello 使用者顯示的清單是來自 hello 與 hello 虛擬網路的同一個 Azure Active Directory 租用戶您正要設定 hello 對等。 當它出現在 hello 清單，請按一下使用者 b。
9. 按一下 [儲存] 。
10. 登出 hello 入口網站為使用者 a，則 UserB 身分登入。
11. 按一下**+ 新增**，型別*虛擬網路*在 hello**搜尋 hello Marketplace**方塊，然後按一下**虛擬網路**hello 搜尋結果中.
12. 在 hello**虛擬網路**刀鋒視窗中，選取**傳統**在 hello**選取部署模型**方塊，然後按一下 **建立**。
13.   會顯示 hello 建立虛擬網路 （傳統） 方塊中輸入下列值的 hello:

    - **名稱**：*myVnetB*
    - **位址空間**：*10.1.0.0/16*
    - **子網路名稱**：*預設值*
    - **子網路位址範圍**：*10.1.0.0/24*
    - **訂用帳戶**︰選取訂用帳戶 B。
    - **資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupB*
    - **位置**：*美國東部*

14. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetB*。 按一下**myVnetB** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnetB**虛擬網路。
15. 在 [hello **myVnetB**刀鋒視窗中，按一下**屬性**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。 複製 hello**資源識別碼**，這用於後續的步驟。 hello 資源識別碼是下列範例類似 toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. 針對 myVnetB 完成步驟 5-9，其中在步驟 8 輸入 **UserA**。
17. 登出為 UserB hello 入口網站，並以 UserA 登入。
18. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetA*。 按一下**myVnetA** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnet**虛擬網路。
19. 按一下 [myVnetA]。
20. 在 [hello **myVnetA**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。
21. 在 hello **myVnetA-對等互連**刀鋒視窗中出現，按一下**+ 新增**
22. 在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:
     - **名稱**：*myVnetAToMyVnetB*
     - **虛擬網路部署模型**︰選取 [傳統]。
     - **我知道我的資源識別碼**：核取此方塊。
     - **資源識別碼**： 輸入 myVnetB hello 資源識別碼，從步驟 15。
     - **允許虛擬網路存取**：確定已選取 [啟用]。
    本教學課程中不會使用其他設定。 讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。
23. 按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnetA-對等互連**刀鋒視窗一次。 幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。 **連接**會列在 hello**對等互連狀態**hello 的資料行**myVnetAToMyVnetB**對等互連您建立。 現在建立 hello 對等互連。 沒有需要 toopeer hello 虛擬網路 （傳統） toohello 虛擬網路 （資源管理員）。

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

24. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
25. **選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。

## <a name="cli"></a>建立對等互連 - Azure CLI

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。 取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。 

在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。 tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。 請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。

1. [安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)hello Azure CLI 1.0 toocreate hello 虛擬網路 （傳統）。
2. 開啟 CLI 工作階段，並以使用者 b 使用 hello 登入 tooAzure`azure login`命令。
3. 服務管理模式中執行 hello CLI，方式是輸入 hello`azure config mode asm`命令。
4. 輸入下列命令 toocreate hello 虛擬網路 （傳統） 的 hello:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. bash 殼層中使用 Azure CLI 2.0.4 hello 必須完成剩餘步驟 hello 或更新版本[安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)，或使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 按一下 hello**試試**hello 中的按鈕的指令碼後面，這會開啟您登入 Azure 帳戶 tooyour 雲端殼層。 如選項上執行被 Windows 用戶端上的 CLI 指令碼，請參閱 < [Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 
6. 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。 使用您的訂用帳戶 ID 來取代 `<SubscriptionB-Id>` 。 如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。 hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。複製 hello 修改指令碼，將它貼入 tooyour CLI 2.0 工作階段中，然後按`Enter`。 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    當您建立 hello 虛擬網路 （傳統） 在步驟 4 中時，Azure 會建立 hello 的 hello 虛擬網路*預設網路*資源群組。
7. 記錄超出 Azure 與記錄檔中的 UserB 為 UserA hello CLI 2.0。
8. 建立資源群組和虛擬網路 (Resource Manager)。 複製 hello 下列指令碼，將它貼入 tooyour CLI 工作階段中，然後按`Enter`。 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. 建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。 複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。 使用您的訂用帳戶 ID 來取代 `<SubscriptionB-id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。 hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。Azure 建立 hello 虛擬網路 （傳統） 您在步驟 4 建立的資源群組中名為*預設網路*。 在您 CLI 工作階段中，貼上 hello 修改指令碼，然後按下`Enter`。

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。 複製下列指令碼的 hello，並再將它貼入您 CLI 的工作階段中：

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

11. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
12. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。

## <a name="powershell"></a>建立對等互連 - PowerShell

本教學課程針對每個訂用帳戶使用不同的帳戶。 如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。 取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。 

在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。 tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。 請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。

1. 安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)和[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段。
3. 在 PowerShell 中，記錄 Dbz tooUserB 的訂用帳戶中輸入 hello`Add-AzureAccount`命令。
4. toocreate 具有 PowerShell （傳統） 的虛擬網路，您必須建立新的或修改現有的網路組態檔。 了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 hello 檔案應該包含 hello 下列**VirtualNetworkSite** hello 這個教學課程中使用的虛擬網路的項目：

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
    > 匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。 確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。 

5. 記錄 Dbz toouse 資源管理員命令 tooUserB 的訂用帳戶中，輸入 hello`login-azurermaccount`命令。
6. 指派使用者 a 的權限 toovirtual 網路 b 複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦上，並取代`<SubscriptionB-id>`訂閱 b 的 hello 識別碼如果您不知道 hello 訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。 hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。 Azure 建立 hello 虛擬網路 （傳統） 您在步驟 4 建立的資源群組中名為*預設網路*。 tooexecute hello 指令碼中，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. 登出 Azure 以做為 UserB 和記錄 UserA tooUserA 的訂用帳戶中，輸入 hello`login-azurermaccount`命令。 登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。 請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。
8. 複製下列指令碼，將它貼在 tooPowerShell，，然後按下的 hello 建立 hello 虛擬網路 （資源管理員） `Enter`:

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

9. 指派使用者 b 的權限 toomyVnetA。 複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦上，並取代`<SubscriptionA-Id>`識別碼為訂用帳戶 A.hello如果您不知道 hello 訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。 hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。 在 PowerShell 中，貼上 hello hello 指令碼已修改的版本，然後按下`Enter`tooexecute 它。

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. 複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦，並取代`<SubscriptionB-id>`識別碼 hello 為訂用帳戶 B.toopeer myVnetA toomyVNetB，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. 複製下列指令碼，將它貼到 PowerShell，並按下的 hello 檢視 myVnetA hello 對等互連狀態`Enter`。

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    hello 狀態是**Connected**。 它會隨之變更**Connected**一旦您設定從 myVnetB hello 對等互連 toomyVnetA。

    所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。 如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。 如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。 深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

12. **選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。
13. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。

## <a name="permissions"></a>權限

您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。 例如，如果您已對等互連名為 myVnetA 和 myVnetB 的兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:
    
|虛擬網路|部署模型|角色|權限|
|---|---|---|---|
|myVnetA|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Resource Manager|[網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||傳統|[傳統網路參與者](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。

## <a name="delete"></a>刪除資源
當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。 刪除資源群組時，也會刪除 hello 資源群組中的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroupA**。 在 hello 搜尋結果中，按一下  **myResourceGroupA**。
2. 在 hello **myResourceGroupA**刀鋒視窗中，按一下 hello**刪除**圖示。
3. tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroupA**，然後按一下**刪除**。
4. 在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetB*。 按一下**myVnetB** hello 搜尋結果中出現。 刀鋒視窗會顯示 hello **myVnetB**虛擬網路。
5. 在 hello **myVnetB**刀鋒視窗中，按一下 **刪除**。
6. tooconfirm hello 刪除、 按一下**是**在 hello**刪除虛擬網路**方塊。

### <a name="delete-cli"></a>Azure CLI

1. 登入使用 hello tooAzure CLI 2.0 toodelete hello 虛擬網路 （資源管理員） 以 hello 下列命令：

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. 登入使用 hello tooAzure Azure CLI 1.0 toodelete hello 虛擬網路 （傳統） 以 hello 下列命令：

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Hello PowerShell 命令提示字元中輸入下列命令 toodelete hello 虛擬網路 （資源管理員） 的 hello:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello 虛擬網路 （傳統） 使用 PowerShell，您必須修改現有的網路組態檔。 了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。 移除下列 hello 這個教學課程中使用的虛擬網路的 VirtualNetworkSite 元素 hello:

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
    > 匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。 請務必僅卸除 hello 的上一個虛擬網路，且您不變更或移除您的訂用帳戶中的任何其他現有的虛擬網路。 

## <a name="next-steps"></a>後續步驟

- 請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。
- 了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。
- 了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。
