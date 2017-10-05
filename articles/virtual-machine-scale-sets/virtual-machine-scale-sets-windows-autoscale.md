---
title: "自動調整 Windows 虛擬機器擴展集 | Microsoft Docs"
description: "使用 Azure PowerShell 設定自動調整 Windows 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 91f731bec46c005221f4e66e95822994070d4c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="09bd9-103">在虛擬機器擴展集中自動調整機器</span><span class="sxs-lookup"><span data-stu-id="09bd9-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="09bd9-104">虛擬機器擴展集可讓您將完全相同的虛擬機器以集合的方式進行部署和管理。</span><span class="sxs-lookup"><span data-stu-id="09bd9-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="09bd9-105">調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。</span><span class="sxs-lookup"><span data-stu-id="09bd9-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="09bd9-106">如需調整集的詳細資訊，請參閱 [虛擬機器調整集](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="09bd9-107">本教學課程說明如何建立 Windows 虛擬機器的擴展集，並對擴展集中的機器進行自動調整。</span><span class="sxs-lookup"><span data-stu-id="09bd9-107">This tutorial shows you how to create a scale set of Windows virtual machines and automatically scale the machines in the set.</span></span> <span data-ttu-id="09bd9-108">您會透過建立 Azure Resource Manager 範本並使用 Azure PowerShell 部署它，來建立擴展集並設定調整。</span><span class="sxs-lookup"><span data-stu-id="09bd9-108">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="09bd9-109">如需範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="09bd9-110">若要深入了解擴展集的自動調整，請參閱 [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md)(自動調整和虛擬機器擴展集)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-110">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="09bd9-111">在本文中，您可以部署下列資源和擴充：</span><span class="sxs-lookup"><span data-stu-id="09bd9-111">In this article, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="09bd9-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="09bd9-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="09bd9-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="09bd9-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="09bd9-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="09bd9-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="09bd9-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="09bd9-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="09bd9-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="09bd9-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="09bd9-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="09bd9-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="09bd9-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="09bd9-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="09bd9-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="09bd9-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="09bd9-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="09bd9-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="09bd9-121">如需 Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="09bd9-122">步驟 1：安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09bd9-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="09bd9-123">如需如何安裝最新版 Azure PowerShell、選取訂用帳戶，以及登入 Azure 的相關資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="09bd9-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to Azure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="09bd9-124">步驟 2：建立資源群組和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="09bd9-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="09bd9-125">**建立資源群組** - 所有資源都必須部署至資源群組。</span><span class="sxs-lookup"><span data-stu-id="09bd9-125">**Create a resource group** – All resources must be deployed to a resource group.</span></span> <span data-ttu-id="09bd9-126">使用 [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) 以建立名為 **vmsstestrg1**的資源群組。</span><span class="sxs-lookup"><span data-stu-id="09bd9-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) to create a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="09bd9-127">**建立儲存體帳戶** - 此儲存體帳戶是範本的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="09bd9-127">**Create a storage account** – This storage account is where the template is stored.</span></span> <span data-ttu-id="09bd9-128">使用 [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) 建立名為 **vmsstestsa**的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="09bd9-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) to create a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-the-template"></a><span data-ttu-id="09bd9-129">步驟 3：建立範本</span><span class="sxs-lookup"><span data-stu-id="09bd9-129">Step 3: Create the template</span></span>
<span data-ttu-id="09bd9-130">有了 Azure Resource Manager 範本之後，您就可以使用 JSON 來說明資源、相關設定和部署參數，一起部署和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-130">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="09bd9-131">在您慣用的編輯器中，建立檔案 C:\VMSSTemplate.json ，並新增初始的 JSON 結構以支援範本。</span><span class="sxs-lookup"><span data-stu-id="09bd9-131">In your favorite editor, create the file C:\VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="09bd9-132">參數並非總是必要的項目，但它們能提供在部署範本時輸入值的方式。</span><span class="sxs-lookup"><span data-stu-id="09bd9-132">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="09bd9-133">在您新增至範本的參數父元素下，新增下列參數。</span><span class="sxs-lookup"><span data-stu-id="09bd9-133">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="09bd9-134">用來存取擴展集內機器之個別虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd9-134">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
    * <span data-ttu-id="09bd9-135">用來存放範本的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd9-135">The name of the storage account where the template is stored.</span></span>
    * <span data-ttu-id="09bd9-136">最初在擴展集內建立的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="09bd9-136">The number of virtual machines to initially create in the scale set.</span></span>
    * <span data-ttu-id="09bd9-137">虛擬機器之系統管理帳戶的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="09bd9-137">The name and password of the administrator account on the virtual machines.</span></span>
    * <span data-ttu-id="09bd9-138">建立以支援擴展集之資源的名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="09bd9-138">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="09bd9-139">變數可以在範本中用來指定會經常變更的值或需要透過參數值組合建立的值。</span><span class="sxs-lookup"><span data-stu-id="09bd9-139">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="09bd9-140">在您新增至範本的變數父元素下，新增下列變數。</span><span class="sxs-lookup"><span data-stu-id="09bd9-140">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="09bd9-141">網路介面所使用的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd9-141">DNS names that are used by the network interfaces.</span></span>

        * <span data-ttu-id="09bd9-142">虛擬網路和子網路的 IP 位址名稱和前置詞。</span><span class="sxs-lookup"><span data-stu-id="09bd9-142">The IP address names and prefixes for the virtual network and subnets.</span></span>
        * <span data-ttu-id="09bd9-143">虛擬網路、負載平衡器和網路介面的名稱和識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bd9-143">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="09bd9-144">與調整集內的機器相關聯之帳戶的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd9-144">Storage account names for the accounts associated with the machines in the scale set.</span></span>
        * <span data-ttu-id="09bd9-145">安裝在虛擬機器上的診斷延伸模組的設定。</span><span class="sxs-lookup"><span data-stu-id="09bd9-145">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="09bd9-146">如需診斷延伸模組的詳細資訊，請參閱[使用 Azure Resource Manager 範本建立具有監控和診斷功能的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-146">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="09bd9-147">在您新增至範本的資源父元素下，新增下列儲存體帳戶資源：</span><span class="sxs-lookup"><span data-stu-id="09bd9-147">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="09bd9-148">此範本使用迴圈來建立儲存作業系統磁碟和診斷資料的五個建議的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="09bd9-148">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="09bd9-149">這組帳戶最多可在一個調整集內支援 100 個虛擬機器，這是目前的最大值。</span><span class="sxs-lookup"><span data-stu-id="09bd9-149">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="09bd9-150">每個儲存體帳戶的命名方式都相同，即變數中所定義的字母指示項，加上您在參數中為範本提供的前置詞。</span><span class="sxs-lookup"><span data-stu-id="09bd9-150">Each storage account is named with a letter designator that was defined in the variables combined with the prefix that you provide in the parameters for the template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="09bd9-151">新增虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-151">Add the virtual network resource.</span></span> <span data-ttu-id="09bd9-152">如需詳細資訊，請參閱 [網路資源提供者](../virtual-network/resource-groups-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="09bd9-153">新增負載平衡器和網路介面所使用的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-153">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="09bd9-154">新增調整集所使用的負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-154">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="09bd9-155">如需詳細資料，請參閱 [Azure 資源管理員的負載平衡器支援](../load-balancer/load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd9-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="09bd9-156">新增個別的虛擬機器所使用的網路介面資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-156">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="09bd9-157">由於擴展集內的機器無法直接透過公用 IP 位址來存取，因此必須在相同的虛擬網路中建立個別的虛擬機器，以從遠端存取該機器。</span><span class="sxs-lookup"><span data-stu-id="09bd9-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="09bd9-158">在與擴展集相同的網路中新增個別的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="09bd9-158">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="09bd9-159">新增虛擬機器擴展集資源，並指定在擴展集內所有虛擬機器上安裝的診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="09bd9-159">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="09bd9-160">此資源有許多設定都與虛擬機器資源相類似。</span><span class="sxs-lookup"><span data-stu-id="09bd9-160">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="09bd9-161">主要差異是指定擴展集中虛擬機器數量的容量元素，以及指定如何對虛擬機器進行更新的 upgradePolicy。</span><span class="sxs-lookup"><span data-stu-id="09bd9-161">The main differences are the capacity element that specifies the number of virtual machines in the scale set, and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="09bd9-162">在依照 dependsOn 元素的指示建立所有的儲存體帳戶之前，不會建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="09bd9-162">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="09bd9-163">新增 autoscaleSettings 資源，以定義擴展集如何根據擴展集中機器的處理器使用情形進行調整。</span><span class="sxs-lookup"><span data-stu-id="09bd9-163">Add the autoscaleSettings resource that defines how the scale set adjusts based on the processor usage on the machines in the scale set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="09bd9-164">在本教學課程中，以下的值相當重要：</span><span class="sxs-lookup"><span data-stu-id="09bd9-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="09bd9-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="09bd9-165">**metricName**</span></span>  
    <span data-ttu-id="09bd9-166">此值與我們在 wadperfcounter 變數中定義的效能計數器相同。</span><span class="sxs-lookup"><span data-stu-id="09bd9-166">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="09bd9-167">使用該變數時，診斷擴充將會收集 **Processor(_Total)\% Processor Time** 計數器。</span><span class="sxs-lookup"><span data-stu-id="09bd9-167">Using that variable, the Diagnostics extension collects the  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="09bd9-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="09bd9-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="09bd9-169">此值是虛擬機器擴展集的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="09bd9-169">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="09bd9-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="09bd9-170">**timeGrain**</span></span>  
    <span data-ttu-id="09bd9-171">此值是所收集之計量的精細度。</span><span class="sxs-lookup"><span data-stu-id="09bd9-171">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="09bd9-172">此範本中，此值設為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="09bd9-172">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="09bd9-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="09bd9-173">**statistic**</span></span>  
    <span data-ttu-id="09bd9-174">此值會決定如何結合計量以因應自動調整動作的需要。</span><span class="sxs-lookup"><span data-stu-id="09bd9-174">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="09bd9-175">可能的值為：Average、Min、Max。</span><span class="sxs-lookup"><span data-stu-id="09bd9-175">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="09bd9-176">在這個範本中，將會收集虛擬機器的平均總 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="09bd9-176">In this template, the average total CPU usage of the virtual machines is collected.</span></span>
    
    * <span data-ttu-id="09bd9-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="09bd9-177">**timeWindow**</span></span>  
    <span data-ttu-id="09bd9-178">此值是收集執行個體資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="09bd9-178">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="09bd9-179">其值必須介於 5 分鐘到 12 小時之間。</span><span class="sxs-lookup"><span data-stu-id="09bd9-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="09bd9-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="09bd9-180">**timeAggregation**</span></span>  
    <span data-ttu-id="09bd9-181">此值會決定收集的資料應如何隨著時間結合。</span><span class="sxs-lookup"><span data-stu-id="09bd9-181">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="09bd9-182">預設值為 Average。</span><span class="sxs-lookup"><span data-stu-id="09bd9-182">The default value is Average.</span></span> <span data-ttu-id="09bd9-183">可能的值為：Average、Minimum、Maximum、Last、Total、Count。</span><span class="sxs-lookup"><span data-stu-id="09bd9-183">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="09bd9-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="09bd9-184">**operator**</span></span>  
    <span data-ttu-id="09bd9-185">此值是用來比較計量資料和臨界值的運算子。</span><span class="sxs-lookup"><span data-stu-id="09bd9-185">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="09bd9-186">可能的值為：Equals、NotEquals、GreaterThan、GreaterThanOrEqual、LessThan、LessThanOrEqual。</span><span class="sxs-lookup"><span data-stu-id="09bd9-186">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="09bd9-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="09bd9-187">**threshold**</span></span>  
    <span data-ttu-id="09bd9-188">此值是觸發調整動作的值。</span><span class="sxs-lookup"><span data-stu-id="09bd9-188">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="09bd9-189">在此範本中，會在調整集內的機器之間的平均 CPU 使用率超過 50% 時，將機器新增至調整集。</span><span class="sxs-lookup"><span data-stu-id="09bd9-189">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="09bd9-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="09bd9-190">**direction**</span></span>  
    <span data-ttu-id="09bd9-191">此值會決定達到臨界值時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="09bd9-191">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="09bd9-192">可能的值為 Increase 或 Decrease。</span><span class="sxs-lookup"><span data-stu-id="09bd9-192">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="09bd9-193">在此範本中，如果臨界值在定義的時間範圍內超過 50%，則會增加調整集內的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="09bd9-193">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>
    
    * <span data-ttu-id="09bd9-194">**type**</span><span class="sxs-lookup"><span data-stu-id="09bd9-194">**type**</span></span>  
    <span data-ttu-id="09bd9-195">此值是所應採取的動作類型，必須設為 ChangeCount。</span><span class="sxs-lookup"><span data-stu-id="09bd9-195">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="09bd9-196">**value**</span><span class="sxs-lookup"><span data-stu-id="09bd9-196">**value**</span></span>  
    <span data-ttu-id="09bd9-197">此值是從擴展集內新增或移除的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="09bd9-197">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="09bd9-198">此值必須是 1 或更大。</span><span class="sxs-lookup"><span data-stu-id="09bd9-198">This value must be 1 or greater.</span></span> <span data-ttu-id="09bd9-199">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="09bd9-199">The default value is 1.</span></span> <span data-ttu-id="09bd9-200">在此範本中，會在達到臨界值時，將調整集內的機器數目加 1。</span><span class="sxs-lookup"><span data-stu-id="09bd9-200">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>
    
    * <span data-ttu-id="09bd9-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="09bd9-201">**cooldown**</span></span>  
    <span data-ttu-id="09bd9-202">此值是在上一個調整動作之後、下一個動作執行之前的等待時間量。</span><span class="sxs-lookup"><span data-stu-id="09bd9-202">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="09bd9-203">此值必須介於一分鐘到一週之間。</span><span class="sxs-lookup"><span data-stu-id="09bd9-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="09bd9-204">儲存範本檔案。</span><span class="sxs-lookup"><span data-stu-id="09bd9-204">Save the template file.</span></span>    

## <a name="step-4-upload-the-template-to-storage"></a><span data-ttu-id="09bd9-205">步驟 4：將範本上傳至儲存體</span><span class="sxs-lookup"><span data-stu-id="09bd9-205">Step 4: Upload the template to storage</span></span>
<span data-ttu-id="09bd9-206">只要您知道您在步驟 1 中建立之儲存體帳戶的名稱和主要金鑰，即可上傳範本。</span><span class="sxs-lookup"><span data-stu-id="09bd9-206">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="09bd9-207">在 Microsoft Azure PowerShell 視窗中，設定一個變數來指定您在步驟 1 中建立的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd9-207">In the Microsoft Azure PowerShell window, set a variable that specifies the name of the storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="09bd9-208">設定一個變數，指定儲存體帳戶的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="09bd9-208">Set a variable that specifies the primary key of the storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="09bd9-209">您可以在 Azure 入口網站中檢視儲存體帳戶資源，並按一下金鑰圖示，以取得此金鑰。</span><span class="sxs-lookup"><span data-stu-id="09bd9-209">You can get this key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span>
3. <span data-ttu-id="09bd9-210">建立用來驗證儲存體帳戶之作業的儲存體帳戶內容物件。</span><span class="sxs-lookup"><span data-stu-id="09bd9-210">Create the storage account context object that is used to validate operations with the storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="09bd9-211">建立儲存範本的容器。</span><span class="sxs-lookup"><span data-stu-id="09bd9-211">Create the container for storing the template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="09bd9-212">將範本檔案上傳至新的容器。</span><span class="sxs-lookup"><span data-stu-id="09bd9-212">Upload the template file to the new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-the-template"></a><span data-ttu-id="09bd9-213">步驟 5：部署範本</span><span class="sxs-lookup"><span data-stu-id="09bd9-213">Step 5: Deploy the template</span></span>
<span data-ttu-id="09bd9-214">建立範本後，您就可以開始部署資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-214">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="09bd9-215">使用下列命令啟動程序：</span><span class="sxs-lookup"><span data-stu-id="09bd9-215">Use this command to start the process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="09bd9-216">當您按 Enter 鍵時，系統會提示您提供您所指派的變數值。</span><span class="sxs-lookup"><span data-stu-id="09bd9-216">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="09bd9-217">請提供下列值：</span><span class="sxs-lookup"><span data-stu-id="09bd9-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="09bd9-218">所有資源要順利部署完成，大約需要 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="09bd9-218">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="09bd9-219">您也可以使用入口網站的功能來部署資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-219">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="09bd9-220">請使用此連結：「https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>」</span><span class="sxs-lookup"><span data-stu-id="09bd9-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="09bd9-221">步驟 6：監視資源</span><span class="sxs-lookup"><span data-stu-id="09bd9-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="09bd9-222">您可以使用下列方法，取得關於虛擬機器調整集的某些資訊：</span><span class="sxs-lookup"><span data-stu-id="09bd9-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="09bd9-223">Azure 入口網站 - 目前，使用入口網站可以取得限定數量的資訊。</span><span class="sxs-lookup"><span data-stu-id="09bd9-223">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>
* <span data-ttu-id="09bd9-224">[Azure 資源總管](https://resources.azure.com/) - 此工具是瀏覽擴展集目前狀態的最佳選項。</span><span class="sxs-lookup"><span data-stu-id="09bd9-224">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="09bd9-225">按照此路徑，您應該會看到您所建立之調整集的執行個體檢視：</span><span class="sxs-lookup"><span data-stu-id="09bd9-225">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    <span data-ttu-id="09bd9-226">subscriptions > {您的訂用帳戶} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="09bd9-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="09bd9-227">Azure PowerShell - 使用下列命令可取得某些資訊：</span><span class="sxs-lookup"><span data-stu-id="09bd9-227">Azure PowerShell - Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="09bd9-228">或</span><span class="sxs-lookup"><span data-stu-id="09bd9-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="09bd9-229">比照連接到任何其他機器的方式來連接到個別的虛擬機器，即可從遠端存取擴展集中的虛擬機器以監視個別的程序。</span><span class="sxs-lookup"><span data-stu-id="09bd9-229">Connect to the separate virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="09bd9-230">在 [虛擬機器調整集](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="09bd9-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-the-resources"></a><span data-ttu-id="09bd9-231">步驟 7：移除資源</span><span class="sxs-lookup"><span data-stu-id="09bd9-231">Step 7: Remove the resources</span></span>
<span data-ttu-id="09bd9-232">您將為 Azure 中所使用的資源支付費用，因此，刪除不再需要的資源永遠是最好的做法。</span><span class="sxs-lookup"><span data-stu-id="09bd9-232">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="09bd9-233">您不需要從資源群組個別刪除每個資源。</span><span class="sxs-lookup"><span data-stu-id="09bd9-233">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="09bd9-234">您可以刪除資源群組，其所有資源都將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="09bd9-234">You can delete the resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="09bd9-235">如果您想要保留資源群組，您可以只刪除調整集。</span><span class="sxs-lookup"><span data-stu-id="09bd9-235">If you want to keep your resource group, you can delete the scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="09bd9-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09bd9-236">Next steps</span></span>
* <span data-ttu-id="09bd9-237">使用 [管理虛擬機器擴展集中的虛擬機器](virtual-machine-scale-sets-windows-manage.md)中的資訊，管理您剛建立的擴展集。</span><span class="sxs-lookup"><span data-stu-id="09bd9-237">Manage the scale set that you just created using the information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="09bd9-238">透過檢閱 [使用虛擬機器擴展集垂直自動調整](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="09bd9-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="09bd9-239">在 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)中找到 Azure 監視器監視功能的範例</span><span class="sxs-lookup"><span data-stu-id="09bd9-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="09bd9-240">若要深入了解通知功能，請參閱[使用自動調整動作在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="09bd9-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="09bd9-241">深入了解如何[使用稽核記錄，在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="09bd9-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

