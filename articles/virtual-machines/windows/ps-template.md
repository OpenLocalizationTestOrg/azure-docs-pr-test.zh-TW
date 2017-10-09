---
title: "Windows Azure 中的範本 VM aaaCreate |Microsoft 文件"
description: "使用資源管理員範本，然後 PowerShell tooeasily 建立新的 Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>利用 Resource Manager 範本建立 Windows 虛擬機器

本文章將示範如何 toodeploy Azure Resource Manager 範本使用 PowerShell。 您所建立的 hello 範本部署單一虛擬機器執行 Windows Server 中具有單一子網路的新虛擬網路。

Hello 虛擬機器資源的詳細說明，請參閱[Azure Resource Manager 範本中的虛擬機器](template-description.md)。 如需在範本中的所有 hello 資源的詳細資訊，請參閱[Azure Resource Manager 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。

它花費大約五分鐘 toodo hello 本文章中的步驟。

## <a name="install-azure-powershell"></a>安裝 Azure PowerShell

請參閱[如何 tooinstall 和設定 Azure PowerShell](../../powershell-install-configure.md)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。

## <a name="create-a-resource-group"></a>建立資源群組

所有資源都必須部署在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。

1. 取得可以建立資源的可用位置清單。
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. 在您選取的 hello 位置建立 hello 資源群組。 此範例顯示 hello 建立名為資源群組的**myResourceGroup**在 hello**美國西部**位置：

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>建立 hello 檔案

在此步驟中，您會建立部署 hello 資源範本檔，以及提供參數值 toohello 範本參數檔案。 您也可以建立使用的 tooperform Azure Resource Manager 作業的授權檔案。

1. 建立名為*CreateVMTemplate.json*並將此 JSON 程式碼 tooit:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. 建立名為*Parameters.json*並將此 JSON 程式碼 tooit:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. 建立新的儲存體帳戶和容器：

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. 上傳 hello 檔案 toohello 儲存體帳戶：

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    變更 hello-hello 檔案儲存的檔案路徑 toohello 位置。

## <a name="create-hello-resources"></a>建立 hello 資源

部署使用 hello 參數 hello 範本：

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> 您也可以從本機檔案部署範本和參數。 詳細資訊，請參閱 toolearn[與 Azure 儲存體使用 Azure PowerShell](../../storage/common/storage-powershell-guide-full.md)。

## <a name="next-steps"></a>後續步驟

- 如果沒有與 hello 部署問題，您可能會看看[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](../../resource-manager-common-deployment-errors.md)。
- 深入了解如何 toocreate 及管理中的虛擬機器[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

