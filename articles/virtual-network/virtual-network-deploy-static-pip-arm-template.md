---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure Resource Manager 範本 |Microsoft 文件"
description: "了解如何 toocreate VM 的靜態公用 IP 位址使用 Azure Resource Manager 範本。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本建立具有靜態公用 IP 位址的 VM

> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [範本](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (傳統)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>範本檔案中的公用 IP 資源
您可以檢視和下載 hello[範例範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json)。

hello 下一節顯示 hello hello 公用 IP 資源，根據上述的 hello 案例定義：

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

請注意 hello **publicIPAllocationMethod**屬性，設定得*靜態*。 這個屬性可以是 Dynamic (預設值) 或 Static。 設定 toostatic 可確保永遠不會變更 hello 指派公用 IP 位址。

hello 下一節顯示 hello 與之間的關聯 hello 公用 IP 位址的網路介面：

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

請注意 hello **publicIPAddress**屬性指向 toohello**識別碼**的資源，名為**variables('webVMSetting').pipName**。 這是 hello hello 如上所示公用 IP 資源的名稱。

最後，上述的 hello 網路介面會列在 hello **networkProfile** hello VM 正在建立的屬性。

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>使用部署 hello 範本按一下 toodeploy

hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。 toodeploy 此範本使用按一下 toodeploy，按一下 **部署 tooAzure** hello hello Readme.md 檔案中[VM 使用靜態的 PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP)範本。 如果有需要，取代 hello 預設參數值並輸入 hello 空白參數的值。  請遵循 hello hello 入口 toocreate 具有靜態公用 IP 位址的虛擬機器中的指示。

## <a name="deploy-hello-template-by-using-powershell"></a>使用 PowerShell 來部署 hello 範本

您使用 PowerShell 下載 toodeploy hello 範本，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure PowerShell，完成 hello 步驟 hello[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. 在 PowerShell 主控台中，執行 hello `New-AzureRmResourceGroup` cmdlet toocreate 新的資源群組，如有必要。 如果您已經建立的資源群組，請移 toostep 3。

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    預期的輸出：
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. 在 PowerShell 主控台中，執行 hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello 範本。

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    預期的輸出：
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>使用 Azure CLI hello 部署 hello 範本
使用 Azure CLI，完成下列步驟的 hello hello toodeploy hello 範本：

1. 如果您從未使用過 Azure CLI，請遵循在 hello hello 步驟[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)文章 tooinstall 並加以設定。
2. 執行 hello`azure config mode`命令 tooswitch tooResource 管理員模式，如下所示。

    ```azurecli
    azure config mode arm
    ```

    hello 預期 hello 上述命令中的輸出：

        info:    New mode is arm

3. 開啟 hello[參數檔](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json)、 選取其內容，和它 tooa 將檔案儲存在您的電腦。 例如，hello 參數會儲存名為 tooa 檔案*parameters.json*。 變更 hello 參數值，如有需要，hello 檔案內，但最少，建議您變更 hello hello adminPassword 參數 tooa 唯一的複雜密碼的值。
4. 執行 hello `azure group deployment create` cmd toodeploy hello hello 範本和參數使用新的 VNet 檔案下載，並修改上方。 在下方的 hello 命令，取代<path>hello 路徑 hello 檔案儲存至。 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    預期的輸出 (列出使用的參數值)︰

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

