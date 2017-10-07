---
title: "Azure 虛擬網路 （傳統） 含有多個子網路 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 在 Azure 中的多個子網路的虛擬網路 （傳統）。"
services: virtual-network
documentationcenter: 
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
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>建立有多個子網路的虛擬網路 (傳統)

> [!IMPORTANT]
> Azure 有二種建立和處理資源的[不同部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)：Resource Manager 和傳統模型。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議您建立最新的虛擬網路透過 hello[資源管理員](virtual-networks-create-vnet-arm-pportal.md)部署模型。

在本教學課程，了解如何 toocreate 基本的 Azure 虛擬網路 （傳統） 具有不同公用和私用子網路。 您可以在子網路中建立 Azure 資源，像是虛擬網路、雲端服務。 建立虛擬網路 （傳統） 中的資源可以通訊，以及與其他網路連線的 tooa 虛擬網路中的資源。

深入了解所有[虛擬網路](virtual-network-manage-network.md)和[子網路](virtual-network-manage-subnet.md)設定。

> [!WARNING]
> 當[訂用帳戶停用](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit)時，Azure 會立即刪除虛擬網路 (傳統)。 不論資源是否存在 hello 虛擬網路中也會刪除虛擬網路 （傳統）。 如果您稍後再重新啟用 hello 訂用帳戶，就必須重新建立 hello 虛擬網路中存在的資源。

您可以建立虛擬網路 （傳統） 使用 hello [Azure 入口網站](#portal)，hello [Azure 命令列介面 (CLI) 1.0](#azure-cli)，或[PowerShell](#powershell)。

## <a name="portal"></a>入口網站

1. 在網際網路瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com)。 使用您的 [Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)登入。 如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。
2. 按一下**+ 新增**hello 入口網站中。
3. 輸入*虛擬網路*在 hello**搜尋 hello Marketplace**方塊上方的 hello hello**新增**刀鋒視窗中出現。  按一下**虛擬網路**hello 搜尋結果中出現。
4. 選取**傳統**在 hello**選取部署模型**方塊中 hello**虛擬網路**刀鋒視窗中出現，然後按一下**建立**。 
5. 輸入 hello 遵循 hello 值**建立虛擬網路 （傳統）**刀鋒視窗，然後按一下**建立**:

    |設定|值|
    |---|---|
    |名稱|myVnet|
    |位址空間|10.0.0.0/16|
    |子網路名稱|公開|
    |子網路位址範圍|10.0.0.0/24|
    |資源群組|讓 [新建] 保持選取狀態，然後輸入 **myResourceGroup**。|
    |訂用帳戶和位置|選取您的訂用帳戶和位置。

    如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)(也稱為 tooas*區域*)。
4. 在 hello 入口網站中，您可以建立只有一個子網路時建立虛擬網路。 在本教學課程中，您會建立第二個子網路之後建立 hello 虛擬網路。 您稍後可能會建立可存取網際網路資源 hello**公用**子網路。 您也可以建立不是可從在 hello hello 網際網路存取的資源**私人**子網路。 toocreate hello 第二個子網路中，輸入**myVnet**在 hello**搜尋資源**hello hello 頁頂端的方塊。 按一下**myVnet** hello 搜尋結果中出現。
5. 按一下**子網路**(在 hello**設定**> 一節) 上 hello**建立虛擬網路 （傳統）**刀鋒視窗中出現。
6. 按一下**+ 加**上 hello **myVnet-子網路**刀鋒視窗中出現。
7. 輸入**私人**如**名稱**上 hello**加入子網路**刀鋒視窗。 在 [位址範圍] 輸入 **10.0.1.0/24**。  按一下 [確定] 。
8. 在 hello **myVnet-子網路**刀鋒視窗中，您可以看到 hello**公用**和**私人**您所建立的子網路。
9. **選擇性**： 當您完成本教學課程時，您可能想 toodelete hello 資源，您所建立，讓您不必承受使用費用：
    - 按一下**概觀**上 hello **myVnet**刀鋒視窗。
    - 按一下 hello**刪除**圖示 hello **myVnet**刀鋒視窗。
    - tooconfirm hello 刪除、 按一下**是**在 hello**刪除虛擬網路**方塊。

## <a name="azure-cli"></a>Azure CLI

1. 您可以[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)，或使用 hello CLI hello Azure 雲端殼層內。 hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。 它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。 CLI 命令的 tooget 說明輸入`azure <command> --help`。 
2. CLI 工作階段中，登入 tooAzure hello 命令所示。 如果您按一下**試試**hello 方塊下方，在雲端殼層會開啟。 您可以登入 tooyour Azure 訂用帳戶，而不需輸入 hello 下列命令：

    ```azurecli-interactive
    azure login
    ```

3. tooensure hello CLI 可在服務管理模式中，輸入下列命令的 hello:

    ```azurecli-interactive
    azure config mode asm
    ```

4. 建立具有私人子網路的虛擬網路：

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. 建立 hello 虛擬網路內的公用子網路：

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. 檢閱 hello 虛擬網路和子網路：

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **選擇性**： 您可以建立當您完成本教學課程，讓您不必承受使用費 toodelete hello 資源：

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> 雖然您無法指定資源群組 toocreate （傳統） 的虛擬網路中使用 hello CLI，Azure 會建立名為的資源群組的 hello 虛擬網路*預設網路*。

## <a name="powershell"></a>PowerShell

1. 安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)模組。 如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 啟動 PowerShell 工作階段。
3. 在 PowerShell 中，登入 tooAzure 輸入 hello`Add-AzureAccount`命令。
4. 變更 hello 以下路徑和檔案名稱，視需要再匯出您現有的網路組態檔：

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate 具有公用和私用子網路的虛擬網路使用任何文字編輯器 tooadd hello **VirtualNetworkSite**後面 toohello 網路組態檔項目。

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    完整檢閱 hello[網路組態檔結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。

6. 匯入 hello 網路組態檔：

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > 匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。 確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。 

7. 檢閱 hello 虛擬網路和子網路：

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **選擇性**： 您可能會想 toodelete hello 資源時所建立完成此教學課程中，如此您就不會產生使用費用。 toodelete hello 虛擬網路，完成步驟 4-6 同樣地，此時間移除 hello **VirtualNetworkSite**步驟 5 中所加入的項目。
 
> [!NOTE]
> 雖然您無法在 PowerShell 中使用指定的資源群組 toocreate （傳統） 的虛擬網路，Azure 會建立名為的資源群組的 hello 虛擬網路*預設網路*。

---

## <a name="next-steps"></a>後續步驟

- toolearn 有關所有虛擬網路和子網路設定，請參閱[管理虛擬網路](virtual-network-manage-network.md)和[管理虛擬網路子網路](virtual-network-manage-subnet.md)。 您必須使用實際執行環境 toomeet 不同需求中的虛擬網路和子網路的各種選項。
- 輸入和輸出 toofilter 子網路的流量，建立和套用[網路安全性群組](virtual-networks-nsg.md)toosubnets。
- 建立[Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器，然後將它連線 tooan 現有的虛擬網路。
- tooconnect 兩個虛擬網路在 hello 相同的 Azure 位置中建立[虛擬網路對等互連](create-peering-different-deployment-models.md)hello 虛擬網路之間。 您可以對等虛擬網路 （資源管理員） tooa 虛擬網路 （傳統），但您無法建立對等互連介於兩個虛擬網路 （傳統）。
- 使用 hello 虛擬網路 tooan 在內部部署網路連線[VPN 閘道](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)循環。
