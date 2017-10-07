---
title: "具有多個 Nic 的 Azure Resource Manager 範本的 VM aaaCreate |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立具有多個 NIC 的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>使用範本建立具有多個 NIC 的 VM
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-ps.md)。
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。

## <a name="prerequisites"></a>必要條件
您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。 toocreate 這些資源，完成下列步驟 hello:

1. 瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。
2. 在 hello 範本頁面中，右邊 toohello**父資源群組**，按一下 **部署 tooAzure**。
3. 如有需要變更為 hello 參數值，然後遵循 hello hello Azure 預覽入口網站 toodeploy hello 資源群組中的步驟。

> [!IMPORTANT]
> 請確定您的儲存體帳戶名稱是唯一的。 在 Auzre 中不能有重複的儲存體帳戶名稱。
> 

## <a name="understand-hello-deployment-template"></a>了解 hello 部署範本
部署與此文件提供的 hello 範本之前，請確定您了解其用途。 下列步驟的 hello 提供 hello 範本很好的概觀：

1. 瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。
2. 按一下**azuredeploy.json** tooopen hello 範本檔案。
3. 請注意 hello *osType*下面所列的參數。 這個參數是使用的 tooselect 哪些 hello 的資料庫伺服器，以及多個作業系統的 VM 映像 toouse 相關設定。

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. 向下捲動 toohello 清單的變數，並檢查 hello hello 定義**dbVMSetting**下面所列的變數。 它會接收一個 hello 陣列中包含的元素 hello **dbVMSettings**變數。 如果您熟悉軟體開發術語，您可以檢視 hello **dbVMSettings**變數作為雜湊表或字典。

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. 假設您決定在 hello 後端中執行 SQL toodeploy Windows Vm。 然後 hello 值**osType**會*Windows*，和 hello **dbVMSetting**變數會包含下面列出代表 hello hello 中的第一個值之 hello 元素**dbVMSettings**變數。

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. 請注意 hello **vmSize**包含 hello 值*Standard_DS3*。 只有特定 VM 大小允許 hello 使用多個 Nic。 您可以確認哪些 VM 大小來支援多個 Nic 讀取 hello [Windows VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[Linux VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)文件。

7. 向下捲動太**資源**和注意事項 hello 第一個元素。 它描述儲存體帳戶。 這個儲存體帳戶將會使用每個資料庫的 VM 所使用的 toomaintain hello 資料磁碟。 在此案例中，每部資料庫 VM 都有儲存在一般儲存體的作業系統磁碟，以及儲存在 SSD (進階) 儲存體的兩個資料磁碟。

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. 捲動 toohello 下一個資源，如下所示。 此資源代表的 hello NIC 用於每個 VM 的資料庫中的資料庫存取權。 請注意 hello 使用 hello**複製**這項資源中的函式。 hello 範本可讓您 toodeploy 許多 Vm 所要根據 hello **dbCount**參數。 因此，您需要 toocreate hello 相同數量的 Nic，來存取資料庫，其中每個 VM。

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. 捲動 toohello 下一個資源，如下所示。 此資源代表的 hello NIC 用於 VM 的每個資料庫中的管理。 同樣地，每個資料庫 VM 都需要一個這種 NIC。 請注意 hello **networkSecurityGroup**項目，連結允許存取 tooRDP/SSH toothis NIC 只 NSG。

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. 捲動 toohello 下一個資源，如下所示。 此資源代表共用資料庫的所有 Vm 的可用性集 toobe。 這樣一來，您保證，永遠都會有一個 VM 中設定在維護期間執行的 hello。

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. 捲動 toohello 下一個資源。 此資源代表 hello 資料庫的 Vm，如中所示 hello 先下面所列的幾行。 請注意 hello 使用 hello**複製**函式一次，確保會建立多個 Vm 根據 hello **dbCount**參數。 同時也請注意 hello **dependsOn**集合。 它會列出所需 toobe hello 部署 VM，以及 hello 可用性設定組，與 hello 儲存體帳戶之前建立的兩個 Nic。

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Hello VM 資源 toohello 中向下捲動**networkProfile**項目，如下所示。 請注意，每部 VM 都有兩個參照的 NIC。 當您建立多個 Nic vm 時，您必須設定 hello**主要**hello Nic 之一的屬性太*true*，和太 hello rest*false*。

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>使用部署 hello ARM 範本按一下 toodeploy

> [!IMPORTANT]
> 請確定您遵循 hello[先決條件](#Pre-requisites)之前 hello 指示下面的步驟。
> 

hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。 toodeploy 此範本使用按一下 toodeploy，遵循[此連結](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)，右邊 toohello**後端資源群組 （請參閱文件）**按一下**部署 tooAzure**，取代hello 必要時，預設參數值，並遵循 hello 入口網站中的 hello 指示。

hello 圖會顯示 hello 內容 hello 新資源群組的部署之後。

![後端資源群組](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>使用 PowerShell 來部署 hello 範本
您使用 PowerShell 下載 toodeploy hello 範本安裝和設定 PowerShell hello 中的 hello 步驟[安裝和設定 PowerShell](/powershell/azure/overview)發行項，然後完成 hello 下列步驟：

執行 hello  **`New-AzureRmResourceGroup`** 資源群組使用的 cmdlet toocreate hello 範本。

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

預期的輸出：

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>使用 Azure CLI hello 部署 hello 範本
使用 Azure CLI hello toodeploy hello 範本，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello  **`azure config mode`** 命令 tooswitch tooResource 管理員模式，如下所示。

    ```azurecli
    azure config mode arm
    ```

    hello 預期輸出如下所示：

        info:    New mode is arm

3. 開啟 hello[參數檔](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json)、 選取它的內容，和它 tooa 將檔案儲存在您的電腦。 對於此範例中，我們儲存 hello 參數檔案太*parameters.json*。
4. 執行 hello  **`azure group deployment create`**  hello 範本和參數使用新的 VNet 檔案您下載並修改上述指令程式 toodeploy hello。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    預期的輸出：
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

