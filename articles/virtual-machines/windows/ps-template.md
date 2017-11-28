---
title: "從 Azure 中的範本建立 Windows VM | Microsoft Docs"
description: "使用 Resource Manager 範本和 PowerShell 輕鬆地建立新的 Windows VM。"
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="281df-103">利用 Resource Manager 範本建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="281df-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="281df-104">本文說明如何使用 PowerShell 來部署 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="281df-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="281df-105">您建立的範本會在具有單一子網路的新虛擬網路中，部署執行 Windows Server 的單一虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="281df-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="281df-106">如需虛擬機器資源的詳細說明，請參閱 [Azure Resource Manager 範本中的虛擬機器 (英文)](template-description.md)。</span><span class="sxs-lookup"><span data-stu-id="281df-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="281df-107">如需有關範本中所有資源的詳細資訊，請參閱 [Azure Resource Manager 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="281df-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="281df-108">執行本文中的步驟約需 5 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="281df-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="281df-109">安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="281df-109">Install Azure PowerShell</span></span>

<span data-ttu-id="281df-110">如需如何安裝最新版 Azure PowerShell、選取訂用帳戶，以及登入帳戶的相關資訊，請參閱[如何安裝和設定 Azure PowerShell](../../powershell-install-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="281df-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="281df-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="281df-111">Create a resource group</span></span>

<span data-ttu-id="281df-112">所有資源都必須部署在[資源群組](../../azure-resource-manager/resource-group-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="281df-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="281df-113">取得可以建立資源的可用位置清單。</span><span class="sxs-lookup"><span data-stu-id="281df-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="281df-114">在您選取的位置中建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="281df-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="281df-115">此範例示範如何在 [West US] \(美國西部\) 位置中建立名為 **myResourceGroup** 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="281df-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="281df-116">建立檔案</span><span class="sxs-lookup"><span data-stu-id="281df-116">Create the files</span></span>

<span data-ttu-id="281df-117">在此步驟中，您會建立部署資源的範本檔案，以及為範本提供參數值的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="281df-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="281df-118">您也會建立用來執行 Azure Resource Manager 作業的授權檔案。</span><span class="sxs-lookup"><span data-stu-id="281df-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="281df-119">建立名為 *CreateVMTemplate.json* 的檔案並加入此 JSON 程式碼：</span><span class="sxs-lookup"><span data-stu-id="281df-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="281df-120">建立名為 *Parameters.json* 的檔案並加入此 JSON 程式碼：</span><span class="sxs-lookup"><span data-stu-id="281df-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="281df-121">建立新的儲存體帳戶和容器：</span><span class="sxs-lookup"><span data-stu-id="281df-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="281df-122">將檔案上傳至儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="281df-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="281df-123">將 -File 路徑變更為您儲存檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="281df-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="281df-124">建立資源</span><span class="sxs-lookup"><span data-stu-id="281df-124">Create the resources</span></span>

<span data-ttu-id="281df-125">使用參數部署範本：</span><span class="sxs-lookup"><span data-stu-id="281df-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="281df-126">您也可以從本機檔案部署範本和參數。</span><span class="sxs-lookup"><span data-stu-id="281df-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="281df-127">若要深入了解，請參閱[搭配使用 Azure PowerShell 與 Azure 儲存體](../../storage/common/storage-powershell-guide-full.md)。</span><span class="sxs-lookup"><span data-stu-id="281df-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="281df-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="281df-128">Next Steps</span></span>

- <span data-ttu-id="281df-129">如果部署發生問題，您可以查看[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](../../resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="281df-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="281df-130">請參閱[使用 Azure PowerShell 模組建立和管理 Windows VM](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，以了解如何建立和管理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="281df-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

