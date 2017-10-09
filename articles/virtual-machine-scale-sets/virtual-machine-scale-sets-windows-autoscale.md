---
title: "Windows 虛擬機器擴展集 aaaAutoscale |Microsoft 文件"
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
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="a6e1e-103">在虛擬機器擴展集中自動調整機器</span><span class="sxs-lookup"><span data-stu-id="a6e1e-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="a6e1e-104">虛擬機器擴展集讓您輕鬆為您 toodeploy 和管理一組相同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="a6e1e-105">調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="a6e1e-106">如需調整集的詳細資訊，請參閱 [虛擬機器調整集](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="a6e1e-107">本教學課程會示範如何設定 toocreate Windows 虛擬機器，並自動在 hello 的小數位數 hello 機器規模集。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="a6e1e-108">您建立設定和設定調整建立 Azure 資源管理員範本，並將它使用 Azure PowerShell 部署的 hello 小數位數。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="a6e1e-109">如需範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a6e1e-110">請參閱詳細的擴展集自動調整 toolearn[自動縮放和虛擬機器規模設定](virtual-machine-scale-sets-autoscale-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="a6e1e-111">在本文中，您將部署 hello 下列資源和擴充功能：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="a6e1e-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="a6e1e-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="a6e1e-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="a6e1e-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="a6e1e-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="a6e1e-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="a6e1e-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="a6e1e-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="a6e1e-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="a6e1e-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="a6e1e-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a6e1e-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="a6e1e-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="a6e1e-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="a6e1e-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="a6e1e-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="a6e1e-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="a6e1e-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="a6e1e-121">如需 Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="a6e1e-122">步驟 1：安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6e1e-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="a6e1e-123">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooAzure 資訊。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="a6e1e-124">步驟 2：建立資源群組和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a6e1e-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="a6e1e-125">**建立資源群組**– 所有資源必須都是已部署的 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="a6e1e-126">使用[新增 AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate 資源群組命名為**vmsstestrg1**。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="a6e1e-127">**建立儲存體帳戶**– 這個儲存體帳戶是儲存 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="a6e1e-128">使用[新增 AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate 儲存體帳戶名稱為**vmsstestsa**。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="a6e1e-129">步驟 3： 建立 hello 範本</span><span class="sxs-lookup"><span data-stu-id="a6e1e-129">Step 3: Create hello template</span></span>
<span data-ttu-id="a6e1e-130">Azure 資源管理員範本可讓您 toodeploy，並使用 hello 資源和相關聯的部署參數的 JSON 描述一起管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="a6e1e-131">在您最愛的編輯器，建立 hello 檔案 C:\VMSSTemplate.json 並加入 hello 初始 JSON 結構 toosupport hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="a6e1e-132">參數並非必要，但它們的方式 tooinput 值時提供部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="a6e1e-133">加入這些參數，就像加入 toohello 範本 hello 參數父元素底下。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="a6e1e-134">Hello 不同的虛擬機器使用的 tooaccess hello 機器 hello 規模集中的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="a6e1e-135">hello hello hello 範本儲存所在的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="a6e1e-136">虛擬機器 tooinitially 的 hello 數目建立 hello 規模集中。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="a6e1e-137">hello 名稱與 hello hello 虛擬機器上的系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="a6e1e-138">設定會建立 toosupport hello 標尺的 hello 資源的名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="a6e1e-139">變數可以用於會經常變更的範本 toospecify 值，或從參數值組合建立需要 toobe 的值。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="a6e1e-140">新增這些變數，就像加入 toohello 範本 hello 變數的父元素底下。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
   
    * <span data-ttu-id="a6e1e-141">Hello 網路介面所使用的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="a6e1e-142">hello IP 位址名稱和 hello 虛擬網路和子網路前置詞。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="a6e1e-143">hello 名稱和識別碼 hello 虛擬網路的負載平衡器，與網路介面。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="a6e1e-144">Hello 帳戶 hello 規模集中的 hello 機器相關聯的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="a6e1e-145">Hello hello 虛擬機器已安裝的診斷延伸模組的設定。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="a6e1e-146">如需 hello 診斷延伸模組的詳細資訊，請參閱[使用監視和診斷使用 Azure Resource Manager 範本建立 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="a6e1e-147">將您加入 toohello 範本 hello 資源父元素底下的 hello 儲存體帳戶資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="a6e1e-148">此範本會使用建議的五個儲存體帳戶迴圈 toocreate hello hello 作業系統磁碟和診斷資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="a6e1e-149">這組帳戶可以支援註冊 too100 虛擬機器規模集中的也就是 hello 目前最大值。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="a6e1e-150">每個儲存體帳戶是名為 hello 範本 hello 參數中提供的 hello 前置詞與 hello 變數中所定義的字母指示項。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

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

5. <span data-ttu-id="a6e1e-151">新增 hello 虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-151">Add hello virtual network resource.</span></span> <span data-ttu-id="a6e1e-152">如需詳細資訊，請參閱 [網路資源提供者](../virtual-network/resource-groups-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="a6e1e-153">加入所使用的 hello 的 hello 公用 IP 位址資源負載平衡器和網路介面。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="a6e1e-154">新增 hello 負載平衡器資源，以供 hello 規模集。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="a6e1e-155">如需詳細資料，請參閱 [Azure 資源管理員的負載平衡器支援](../load-balancer/load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="a6e1e-156">新增 hello 網路介面資源，以供 hello 不同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="a6e1e-157">規模集中的電腦無法存取透過公用 IP 位址，因為不同的虛擬機器中建立 hello 相同虛擬網路 tooremotely 存取 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="a6e1e-158">新增的 hello hello 小數位數設定為相同網路中的 hello 不同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="a6e1e-159">新增 hello 虛擬機器規模集的資源，並指定 hello 規模集中的所有虛擬機器已安裝的 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="a6e1e-160">其中許多 hello 這個資源的設定都與 hello 虛擬機器資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="a6e1e-161">hello 主要差異是 hello 規模集中，指定虛擬機器的 hello 數目的 hello 容量項目以及 upgradePolicy，指定如何進行更新 toovirtual 機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="a6e1e-162">hello 規模集不會建立直到所有 hello 儲存體帳戶都建立與 hello dependsOn 元素所指定。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="a6e1e-163">新增定義如何 hello 規模集調整根據 hello hello hello 規模集中的電腦上的處理器使用量的 hello autoscaleSettings 資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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

    <span data-ttu-id="a6e1e-164">在本教學課程中，以下的值相當重要：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="a6e1e-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-165">**metricName**</span></span>  
    <span data-ttu-id="a6e1e-166">此值為 hello 相同 hello 我們 hello wadperfcounter 變數中所定義的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="a6e1e-167">使用該變數，hello 診斷擴充功能會收集 hello **processor （_total)\%處理器時間**計數器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="a6e1e-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="a6e1e-169">此值為 hello 虛擬機器規模集的 hello 資源識別項。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="a6e1e-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-170">**timeGrain**</span></span>  
    <span data-ttu-id="a6e1e-171">此值為 hello 的 hello 計量所收集的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="a6e1e-172">在此範本，它會設定 tooone 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="a6e1e-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-173">**statistic**</span></span>  
    <span data-ttu-id="a6e1e-174">這個值會決定如何 hello 度量資訊會結合的 tooaccommodate hello 自動調整規模動作。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="a6e1e-175">hello 可能的值為： 平均值、 最小值、 最大值。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="a6e1e-176">在此範本中，會收集 hello 平均 CPU 使用量總計的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="a6e1e-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-177">**timeWindow**</span></span>  
    <span data-ttu-id="a6e1e-178">此值為 hello 收集執行個體資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="a6e1e-179">其值必須介於 5 分鐘到 12 小時之間。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="a6e1e-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-180">**timeAggregation**</span></span>  
    <span data-ttu-id="a6e1e-181">其值會決定如何隨著時間結合收集的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="a6e1e-182">hello 預設值是 Average。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-182">hello default value is Average.</span></span> <span data-ttu-id="a6e1e-183">hello 可能的值為： 平均、 最小值、 最大值、 最後一個、 總和、 計數。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="a6e1e-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-184">**operator**</span></span>  
    <span data-ttu-id="a6e1e-185">這個值是使用的 toocompare hello 度量資料與 hello 臨界值的 hello 運算子。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="a6e1e-186">hello 可能的值為： NotEquals、 GreaterThan、 GreaterThanOrEqual、 LessThan、 LessThanOrEqual 等於。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="a6e1e-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-187">**threshold**</span></span>  
    <span data-ttu-id="a6e1e-188">此值為 hello 觸發 hello 調整規模動作。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="a6e1e-189">在此範本中，機器會新增 toohello 小數位數時，設定 hello 集合中的機器之間 hello 平均 CPU 使用量超過 50%。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="a6e1e-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-190">**direction**</span></span>  
    <span data-ttu-id="a6e1e-191">這個值會決定 hello 為止 hello 臨界值時所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="a6e1e-192">hello 可能的值為增加或減少。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="a6e1e-193">此範本中 hello hello 規模集中的虛擬機器數目會增加如果 hello 臨界值超過所定義的 hello 時間視窗中的 50%。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="a6e1e-194">**type**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-194">**type**</span></span>  
    <span data-ttu-id="a6e1e-195">此值為 hello 應該會發生，且必須設定 tooChangeCount 的動作類型。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="a6e1e-196">**value**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-196">**value**</span></span>  
    <span data-ttu-id="a6e1e-197">此值為 hello 的新增或移除 hello 規模集中的虛擬機器的數目。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="a6e1e-198">此值必須是 1 或更大。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-198">This value must be 1 or greater.</span></span> <span data-ttu-id="a6e1e-199">hello 預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-199">hello default value is 1.</span></span> <span data-ttu-id="a6e1e-200">此範本中 hello 機器 hello 規模組數目會增加 1 符合 hello 臨界值時。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="a6e1e-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="a6e1e-201">**cooldown**</span></span>  
    <span data-ttu-id="a6e1e-202">Hello 下一個動作發生之前，這個值會是 hello 數量時間 toowait 自 hello 的最後一個調整動作。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="a6e1e-203">此值必須介於一分鐘到一週之間。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="a6e1e-204">儲存 hello 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="a6e1e-205">步驟 4： 上傳 hello 範本 toostorage</span><span class="sxs-lookup"><span data-stu-id="a6e1e-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="a6e1e-206">可以上傳 hello 範本，只要您知道 hello 名稱以及您在步驟 1 中建立的 hello 儲存體帳戶的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="a6e1e-207">在 hello Microsoft Azure PowerShell 視窗中，設定指定 hello hello 您在步驟 1 中建立的儲存體帳戶名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="a6e1e-208">設定指定 hello hello 儲存體帳戶的主索引鍵的變數。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="a6e1e-209">您可以按一下 hello 索引鍵圖示，hello Azure 入口網站中檢視 hello 儲存體帳戶資源時，以取得此金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="a6e1e-210">建立 hello 儲存體帳戶的內容物件所使用的 toovalidate 作業與 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="a6e1e-211">建立 hello 容器儲存 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="a6e1e-212">上傳 hello 範本檔案 toohello 新容器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="a6e1e-213">步驟 5： 部署的 hello 範本</span><span class="sxs-lookup"><span data-stu-id="a6e1e-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="a6e1e-214">現在，您建立 hello 範本時，就可以開始部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="a6e1e-215">使用此命令 toostart hello 程序：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="a6e1e-216">當您按下輸入，會提示的 tooprovide hello 變數指派給您的值。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="a6e1e-217">請提供下列值：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="a6e1e-218">它的所有 hello 資源 toosuccessfully 都部署時間大約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="a6e1e-219">您也可以使用 hello 入口網站的能力 toodeploy hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="a6e1e-220">請使用此連結：「https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>」</span><span class="sxs-lookup"><span data-stu-id="a6e1e-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="a6e1e-221">步驟 6：監視資源</span><span class="sxs-lookup"><span data-stu-id="a6e1e-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="a6e1e-222">您可以使用下列方法，取得關於虛擬機器調整集的某些資訊：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="a6e1e-223">hello Azure 入口網站-目前就可以使用 hello 入口網站的資訊數量有限。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="a6e1e-224">hello [Azure 資源總管](https://resources.azure.com/)-此工具為 hello 最適合瀏覽 hello 擴展集的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="a6e1e-225">按照此路徑，您應該會看到您建立 hello hello 標尺的執行個體檢視集：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="a6e1e-226">subscriptions > {您的訂用帳戶} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a6e1e-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="a6e1e-227">Azure PowerShell-使用此命令 tooget 一些資訊：</span><span class="sxs-lookup"><span data-stu-id="a6e1e-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="a6e1e-228">或</span><span class="sxs-lookup"><span data-stu-id="a6e1e-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="a6e1e-229">就像任何其他電腦，然後您可以從遠端存取 hello hello 小數位數組 toomonitor 個別處理程序中的虛擬機器，如同連接 toohello 不同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a6e1e-230">在 [虛擬機器調整集](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="a6e1e-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="a6e1e-231">步驟 7： 移除 hello 資源</span><span class="sxs-lookup"><span data-stu-id="a6e1e-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="a6e1e-232">因為您負責 Azure 中使用的資源，但它永遠是很好的作法 toodelete 資源不再需要的。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="a6e1e-233">您不需要 toodelete 分開資源群組的每個資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="a6e1e-234">您可以刪除 hello 資源群組，而且會自動刪除其所有資源。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="a6e1e-235">如果您想 tookeep 資源群組，您可以刪除 hello 只設定的小數位數。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="a6e1e-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6e1e-236">Next steps</span></span>
* <span data-ttu-id="a6e1e-237">管理您剛 hello 規模集使用中的 hello 資訊建立[管理虛擬機器規模集中的虛擬機器](virtual-machine-scale-sets-windows-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="a6e1e-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="a6e1e-238">透過檢閱 [使用虛擬機器擴展集垂直自動調整](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="a6e1e-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="a6e1e-239">在 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)中找到 Azure 監視器監視功能的範例</span><span class="sxs-lookup"><span data-stu-id="a6e1e-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="a6e1e-240">了解通知功能[用於 Azure 監視的自動調整規模動作 toosend 電子郵件和 webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a6e1e-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="a6e1e-241">了解如何太[使用稽核記錄 toosend 電子郵件和 webhook 警示通知，在 Azure 監視器](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="a6e1e-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

