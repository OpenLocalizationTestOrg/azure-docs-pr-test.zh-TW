---
title: "Azure 虛擬網路 （傳統） 的網路組態檔 aaaConfigure |Microsoft 文件"
description: "深入了解如何 toocreate 和匯出、 變更和匯入網路組態檔來修改虛擬網路 （傳統）。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>使用網路組態檔來設定虛擬網路 (傳統)
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello Resource Manager 部署模型。

您可以建立及使用 Azure 命令列介面 (CLI) 1.0 hello 或 Azure PowerShell 所使用的網路組態檔設定虛擬網路 （傳統）。 您無法建立或修改透過 hello Azure Resource Manager 部署模型使用網路組態檔的虛擬網路。 您無法使用 Azure 入口網站 toocreate hello 或修改使用網路組態檔的虛擬網路 （傳統），不過您可以使用 hello Azure 入口網站 toocreate 虛擬網路 （傳統），而不使用網路組態檔。

建立和使用網路組態檔設定虛擬網路 （傳統） 需要匯出、 變更和匯入 hello 檔案。

## <a name="export"></a>匯出網路組態檔

您可以使用 PowerShell 或 hello Azure CLI tooexport 網路組態檔。 PowerShell 匯出 XML 檔案，而 hello Azure CLI 匯出 json 檔案。

### <a name="powershell"></a>PowerShell
 
1. [安裝 Azure PowerShell 並登入 tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 變更 hello 目錄 （及確保它存在），並在 hello 的檔名遵循與所需，然後執行 hello 命令 tooexport hello 網路組態檔的命令：

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [安裝 hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 完成剩餘步驟，Azure CLI 1.0 的命令提示字元的 hello。
2. 輸入 hello 登入 tooAzure`azure login`命令。
3. 確認您是在 asm 模式中，輸入 hello`azure config mode asm`命令。
4. 變更 hello 目錄 （及確保它存在），並在 hello 的檔名遵循與所需，然後執行 hello 命令 tooexport hello 網路組態檔的命令：
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>建立或修改網路組態檔

網路組態檔是 XML 檔案 （當使用 PowerShell） 或 json 檔案 （當使用 Azure CLI hello）。 您可以編輯任何文字或 XML/json 編輯器中的 hello 檔案。 hello[網路組態檔結構描述設定](https://msdn.microsoft.com/library/azure/jj157100.aspx)文章包含的所有設定的詳細資料。 如 hello 設定其他說明，請參閱[檢視虛擬網路與設定](virtual-network-manage-network.md#view-vnet)。 hello 作 toohello 檔案：

- 必須符合與 hello 結構描述或匯入 hello 網路組態檔將會失敗。
- 會覆寫您訂用帳戶的任何現有網路設定，因此在進行修改時請特別小心。 例如，參考 hello 範例網路組態檔，請遵循。 說出 hello 原始檔案包含兩個**VirtualNetworkSite**執行個體，以及您已變更，hello 範例所示。 Hello 檔案時，Azure 會刪除 hello 虛擬網路的 hello **VirtualNetworkSite**您移除 hello 檔案中的執行個體。 這個簡化的案例假設沒有任何資源都在 hello 虛擬網路，因為如果有的話，無法刪除 hello 虛擬網路，以及 hello 匯入將會失敗。

> [!IMPORTANT]
> Azure 會考慮的項目具有子網路部署為 tooit**使用**。 使用中的子網路無法加以修改。 在修改之前網路組態檔中的子網路資訊，移動任何您已部署 toohello 子網路 tooa 不同的子網路的未修改的項目。 請參閱[移動 VM 或角色執行個體 tooa 不同的子網路](virtual-networks-move-vm-role-to-subnet.md)如需詳細資訊。

### <a name="example-xml-for-use-with-powershell"></a>與 PowerShell 搭配使用的範例 XML

hello 下列的範例網路組態檔建立虛擬網路，名為*myVirtualNetwork*與位址空間的*10.0.0.0/16*在 hello*美國東部*Azure區域。 hello 虛擬網路包含一個名為的子網路*mySubnet*位址前置詞的*10.0.0.0/24*。

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

如果您匯出的 hello 網路組態檔不包含任何內容，您可以複製 hello 先前範例中的 hello XML，並將它貼到新的檔案。

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>範例 JSON hello Azure CLI 1.0 搭配使用

hello 下列的範例網路組態檔建立虛擬網路，名為*myVirtualNetwork*與位址空間的*10.0.0.0/16*在 hello*美國東部*Azure區域。 hello 虛擬網路包含一個名為的子網路*mySubnet*位址前置詞的*10.0.0.0/24*。

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

如果您匯出的 hello 網路組態檔不包含任何內容，您可以複製 hello 先前範例中的 hello json，並將它貼到新的檔案。

## <a name="import"></a>匯入網路組態檔

您可以使用 PowerShell 或 hello Azure CLI tooimport 網路組態檔。 Hello Azure CLI 匯入 json 檔案時，PowerShell 會匯入 XML 檔案。 如果 hello 匯入失敗，請確認該 hello 檔案符合 hello[網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。 

### <a name="powershell"></a>PowerShell
 
1. [安裝 Azure PowerShell 並登入 tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)。
2. 變更 hello 目錄和檔案名稱中 hello 下列命令，如有必要，然後再執行 hello 命令 tooimport hello 網路組態檔：
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [安裝 hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 完成剩餘步驟，Azure CLI 1.0 的命令提示字元的 hello。
2. 輸入 hello 登入 tooAzure`azure login`命令。
3. 確認您是在 asm 模式中，輸入 hello`azure config mode asm`命令。
4. 變更 hello 目錄和檔案名稱中 hello 下列命令，如有必要，然後再執行 hello 命令 tooimport hello 網路組態檔：

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
