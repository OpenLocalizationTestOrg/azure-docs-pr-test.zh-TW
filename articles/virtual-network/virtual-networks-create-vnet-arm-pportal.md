---
title: "aaaCreate 多個子網路的 Azure 虛擬網路 |Microsoft 文件"
description: "深入了解如何 toocreate 具有多個子網路，在 Azure 中的虛擬網路。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>建立有多個子網路的虛擬網路

在本教學課程，了解如何 toocreate 基本 Azure 虛擬網路具有不同公用和私用子網路。 您可以在子網路中建立各種 Azure 資源 (如虛擬機器、App Service 環境、虛擬機器擴展集、Azure HDInsight 及雲端服務)。 虛擬網路中的資源可以進行通訊與彼此、 與其他網路連線的 tooa 虛擬網路中的資源。

hello 以下各節包含的步驟，toocreate 虛擬網路使用 hello [Azure 入口網站](#portal)，hello Azure 命令列介面 ([Azure CLI](#azure-cli))， [Azure PowerShell](#powershell)，和[Azure Resource Manager 範本](#resource-manager-template)。 hello 結果為的 hello 相同，而不論您使用 toocreate hello 虛擬網路的工具。 按一下任何一個工具連結 toogo toothat hello 教學課程。 深入了解所有[虛擬網路](virtual-network-manage-network.md)和[子網路](virtual-network-manage-subnet.md)設定。

本文提供步驟 toocreate hello Resource Manager 部署模型，也就是 hello 部署模型，我們建議您建立新的虛擬網路時，使用透過虛擬網路。 如果您需要 toocreate 虛擬網路 （傳統），請參閱[建立虛擬網路 （傳統）](create-virtual-network-classic.md)。 如果您不熟悉 Azure 部署模型，請參閱[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。

## <a name="portal"></a>Azure 入口網站

1. 在網際網路瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com)。 使用您的 [Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)登入。 如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。
2. 在 hello 入口網站中，按一下  **+ 新增** > **網路** > **虛擬網路**。
3. 在 hello**建立虛擬網路**刀鋒視窗中，輸入下列值的 hello，然後按一下**建立**:

    |設定|值|
    |---|---|
    |名稱|myVnet|
    |位址空間|10.0.0.0/16|
    |子網路名稱|公開|
    |子網路位址範圍|10.0.0.0/24|
    |資源群組|讓 [新建] 保持選取狀態，然後輸入 **myResourceGroup**。|
    |訂用帳戶和位置|選取您的訂用帳戶和位置。

    如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)(也稱為 tooas*區域*)。
4. 在 hello 入口網站中，您可以建立只有一個子網路時建立虛擬網路。 在本教學課程中，您會建立第二個子網路之後建立 hello 虛擬網路。 您稍後可能會建立可存取網際網路資源 hello**公用**子網路。 您也可以建立不是可從在 hello hello 網際網路存取的資源**私人**子網路。 toocreate hello 第二個中的子網路，hello**搜尋資源**hello hello 頁頂端的方塊中，輸入**myVnet**。 在 hello 搜尋結果中，按一下  **myVnet**。 如果您有多個虛擬網路與 hello 您訂用帳戶中的相同名稱，請檢查 hello 列在每個虛擬網路的資源群組。 請確定您按一下 hello **myVnet**搜尋具有 hello 資源群組的結果**myResourceGroup**。
5. 在 hello **myVnet**刀鋒視窗底下**設定**，按一下**子網路**。
6. 在 hello **myVnet-子網路**刀鋒視窗中，按一下  **+ 子網路**。
7. 在 hello**加入子網路**刀鋒視窗中，針對**名稱**，輸入**私用**。 對 [位址範圍] 輸入 **10.0.1.0/24**。  按一下 [確定] 。
8. 在 hello **myVnet-子網路**刀鋒視窗中，檢閱 hello 子網路。 您可以看到 hello**公用**和**私人**您所建立的子網路。
9. **選擇性：** toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-portal)本文中。

## <a name="azure-cli"></a>Azure CLI

Azure CLI 命令都 hello 相同，無論您從 Windows、 Linux 或 macOS 執行 hello 命令。 不過，不同作業系統殼層的指令碼編寫會有差異。 Bash 殼層中，執行 hello 步驟中的 hello 指令碼。 

1. [安裝和設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 hello 雲端殼層有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層 (**> _**) 在 hello hello 最上方的按鈕[入口網站](https://portal.azure.com)或直接按一下 hello*試試*hello 遵循的步驟中的按鈕。 
2. 如果在本機執行 hello CLI，請登入以 hello tooAzure`az login`命令。 如果使用 hello 雲端殼層，您已登入。
3. 檢閱 hello 下列指令碼和其註解。 在瀏覽器中將 hello 指令碼複製並貼到您的 CLI 工作階段：

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Hello 指令碼完成時執行，請檢閱 hello hello 虛擬網路的子網路。 複製下列命令，hello 並貼到您的 CLI 工作階段中：

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。

## <a name="powershell"></a>PowerShell

1. 安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 在 PowerShell 工作階段中，登入與 tooAzure 您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)使用 hello`login-azurermaccount`命令。

3. 檢閱 hello 下列指令碼和其註解。 在瀏覽器中將 hello 指令碼複製並貼到您的 PowerShell 工作階段：

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview hello hello 虛擬網路子網路複製 hello 下列命令，並貼到您的 PowerShell 工作階段中：

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。

## <a name="resource-manager-template"></a>Resource Manager 範本

您可以使用 Azure Resource Manager 範本來部署虛擬網路。 toolearn 進一步了解範本，請參閱[什麼是資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment)。 tooaccess hello 範本和 toolearn 有關它的參數，請參閱 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本。 您可以部署 hello 範本使用 hello[入口網站](#template-portal)， [Azure CLI](#template-cli)，或[PowerShell](#template-powershell)。

**選擇性：** toodelete hello 您在本教學課程中建立的資源，步驟的任何小節中的完整 hello[刪除資源](#delete)本文中。

### <a name="template-portal"></a>Azure 入口網站

1. 在瀏覽器中，開啟 hello[範本頁面](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets)。
2. 按一下 hello**部署 tooAzure**  按鈕。 如果您未登入 tooAzure，在出現的 hello Azure 入口網站的登入畫面上登入。
3. 使用登入 toohello 入口網站您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。 如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。
4. 輸入 hello 遵循 hello 參數的值：

    |參數|值|
    |---|---|
    |訂用帳戶|選取您的訂用帳戶|
    |資源群組|myResourceGroup|
    |位置|選取位置|
    |Vnet 名稱|myVnet|
    |Vnet 位址首碼|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|公開|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|私人|

5. 同意 toohello 條款和條件，然後再按 **購買**toodeploy hello 虛擬網路。

### <a name="template-cli"></a>Azure CLI

1. [安裝和設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 確定您擁有 hello hello Azure CLI 安裝最新版本。 CLI 命令的 tooget 說明輸入`az <command> --help`。 而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 hello 雲端殼層有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)，或直接按一下 hello**試試**hello 遵循的步驟中的按鈕。 
2. 如果在本機執行 hello CLI，請登入以 hello tooAzure`az login`命令。 如果使用 hello 雲端殼層，您已登入。
3. toocreate hello 虛擬網路的資源群組中，複製 hello 下列命令，並將它貼到您的 CLI 工作階段：

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. 您可以使用下列參數選項的 hello 的其中一個部署 hello 範本：
    - **預設參數值**。 輸入下列命令的 hello:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **自訂參數值**。 下載並修改 hello 範本，再部署 hello 範本。 您也可以部署 hello 範本在 hello 命令列使用參數，或部署 hello 範本與個別參數檔案。 toodownload hello 範本和參數檔案，按一下 hello**瀏覽 GitHub 上**按鈕 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本頁面。 在 GitHub 中，按一下 hello **azuredeploy.parameters.json**或**azuredeploy.json**檔案。 然後，按一下 hello **Raw**按鈕 toodisplay hello 檔案。 在瀏覽器中，複製 hello hello 檔案內容。 儲存您的電腦上的 hello 內容 tooa 檔案。 您可以修改 hello 範本中的 hello 參數值，或使用不同的參數檔案部署 hello 範本。  

    toolearn 深入了解如何使用這些方法，toodeploy 範本鍵入`az group deployment create --help`。

### <a name="template-powershell"></a>PowerShell

1. 安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 在 PowerShell 工作階段中使用 toosign 您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)，輸入`login-azurermaccount`。
3. toocreate 資源群組 hello 虛擬網路，請輸入下列命令的 hello:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. 您可以使用下列參數選項的 hello 的其中一個部署 hello 範本：
    - **預設參數值**。 輸入下列命令的 hello:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **自訂參數值**。 下載並修改 hello 範本，再部署。 您也可以部署 hello 範本在 hello 命令列使用參數，或部署 hello 範本與個別參數檔案。 toodownload hello 範本和參數檔案，按一下 hello**瀏覽 GitHub 上**按鈕 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本頁面。 在 GitHub 中，按一下 hello **azuredeploy.parameters.json**或**azuredeploy.json**檔案。 然後，按一下 hello **Raw**按鈕 toodisplay hello 檔案。 在瀏覽器中，複製 hello hello 檔案內容。 儲存您的電腦上的 hello 內容 tooa 檔案。 您可以修改 hello 範本中的 hello 參數值，或使用不同的參數檔案部署 hello 範本。  

    toolearn 深入了解如何使用這些方法，toodeploy 範本鍵入`Get-Help New-AzureRmResourceGroupDeployment`。 

## <a name="delete"></a>刪除資源

當您完成本教學課程中時，您可能想 toodelete hello 資源，您所建立，如此您就不會產生使用費用。 刪除資源群組時，也會刪除 hello 資源群組中的所有資源。

### <a name="delete-portal"></a>Azure 入口網站

1. 在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。 在 hello 搜尋結果中，按一下  **myResourceGroup**。
2. 在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。
3. tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。

### <a name="delete-cli"></a>Azure CLI

CLI 工作階段中，輸入下列命令的 hello:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

在 PowerShell 工作階段中，輸入下列命令的 hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>後續步驟

- toolearn 有關所有虛擬網路和子網路設定，請參閱[管理虛擬網路](virtual-network-manage-network.md#view-vnet)和[管理虛擬網路子網路](virtual-network-manage-subnet.md#create-subnet)。 您必須使用實際執行環境 toomeet 不同需求中的虛擬網路和子網路的各種選項。
- 輸入和輸出 toofilter 子網路的流量，建立和套用[網路安全性群組](virtual-networks-nsg.md)toosubnets。
- 建立[Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器，然後將它連線 tooan 現有的虛擬網路。
- tooconnect 兩個虛擬網路在 hello 相同的 Azure 位置中建立[虛擬網路對等互連](virtual-network-peering-overview.md)hello 虛擬網路之間。
- 使用 hello 虛擬網路 tooan 在內部部署網路連線[VPN 閘道](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)循環。
