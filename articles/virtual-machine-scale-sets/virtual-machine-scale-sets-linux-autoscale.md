---
title: "自動調整 Linux 虛擬機器擴展集 | Microsoft Docs"
description: "使用 Azure CLI 設定自動調整 Linux 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="d1240-103">在虛擬機器擴展集中自動調整 Linux 機器</span><span class="sxs-lookup"><span data-stu-id="d1240-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="d1240-104">虛擬機器擴展集可讓您將完全相同的虛擬機器以集合的方式進行部署和管理。</span><span class="sxs-lookup"><span data-stu-id="d1240-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="d1240-105">調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。</span><span class="sxs-lookup"><span data-stu-id="d1240-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="d1240-106">若要深入了解，請參閱 [虛擬機器擴展集概觀](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="d1240-107">本教學課程說明如何使用最新版本的 Ubuntu Linux 建立 Linux 虛擬機器的擴展集。</span><span class="sxs-lookup"><span data-stu-id="d1240-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="d1240-108">本教學課程也會說明如何針對集合中的機器進行自動調整。</span><span class="sxs-lookup"><span data-stu-id="d1240-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="d1240-109">您會透過建立 Azure Resource Manager 範本並使用 Azure CLI 部署它，來建立擴展集並設定調整。</span><span class="sxs-lookup"><span data-stu-id="d1240-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="d1240-110">如需範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="d1240-111">若要深入了解擴展集的自動調整，請參閱 [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md)(自動調整和虛擬機器擴展集)。</span><span class="sxs-lookup"><span data-stu-id="d1240-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="d1240-112">在本教學課程中，您可以部署下列資源和擴充：</span><span class="sxs-lookup"><span data-stu-id="d1240-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="d1240-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="d1240-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="d1240-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="d1240-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="d1240-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="d1240-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="d1240-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="d1240-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="d1240-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="d1240-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="d1240-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="d1240-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="d1240-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="d1240-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="d1240-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="d1240-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="d1240-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="d1240-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="d1240-122">如需 Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="d1240-123">開始本教學課程的步驟之前，請 [安裝 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="d1240-124">步驟 1：建立資源群組和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d1240-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="d1240-125">**登入 Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="d1240-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="d1240-126">在您的命令列介面 (Bash、終端機、命令提示字元) 中切換到 Resource Manager 模式，然後[使用您的公司或學校識別碼進行登入](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)。遵循提示以取得 Azure 帳戶的互動式登入體驗。</span><span class="sxs-lookup"><span data-stu-id="d1240-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="d1240-127">如果您有工作或學校識別碼，而且未啟用雙因素驗證，請使用 `azure login -u` 及識別碼來在沒有互動式工作階段的情況下進行登入。</span><span class="sxs-lookup"><span data-stu-id="d1240-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="d1240-128">如果您沒有工作或學校識別碼，您可以[從個人的 Microsoft 帳戶建立工作或學校識別碼](../active-directory/active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="d1240-129">**建立資源群組**</span><span class="sxs-lookup"><span data-stu-id="d1240-129">**Create a resource group**</span></span>  
<span data-ttu-id="d1240-130">所有資源都必須部署至資源群組。</span><span class="sxs-lookup"><span data-stu-id="d1240-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="d1240-131">在本教學課程中，我們將資源群組命名為 **vmsstest1**。</span><span class="sxs-lookup"><span data-stu-id="d1240-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="d1240-132">**將儲存體帳戶部署到新的資源群組中**</span><span class="sxs-lookup"><span data-stu-id="d1240-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="d1240-133">此儲存體帳戶用來存放範本。</span><span class="sxs-lookup"><span data-stu-id="d1240-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="d1240-134">建立名為 **vmsstestsa**的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1240-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="d1240-135">步驟 2：建立範本</span><span class="sxs-lookup"><span data-stu-id="d1240-135">Step 2: Create the template</span></span>
<span data-ttu-id="d1240-136">有了 Azure Resource Manager 範本之後，您就可以使用 JSON 來說明資源、相關設定和部署參數，一起部署和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="d1240-137">在您慣用的編輯器中，建立檔案 VMSSTemplate.json ，並新增初始的 JSON 結構以支援範本。</span><span class="sxs-lookup"><span data-stu-id="d1240-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

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

2. <span data-ttu-id="d1240-138">參數並非總是必要的項目，但它們能提供在部署範本時輸入值的方式。</span><span class="sxs-lookup"><span data-stu-id="d1240-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="d1240-139">在您新增至範本的參數父元素下，新增下列參數。</span><span class="sxs-lookup"><span data-stu-id="d1240-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="d1240-140">用來存取擴展集內機器之個別虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1240-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="d1240-141">用來存放範本之儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1240-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="d1240-142">最初在調整集內建立的虛擬機器執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="d1240-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="d1240-143">虛擬機器之系統管理帳戶的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d1240-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="d1240-144">建立以支援擴展集之資源的名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="d1240-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="d1240-145">變數可以在範本中用來指定會經常變更的值或需要透過參數值組合建立的值。</span><span class="sxs-lookup"><span data-stu-id="d1240-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="d1240-146">在您新增至範本的變數父元素下，新增下列變數。</span><span class="sxs-lookup"><span data-stu-id="d1240-146">Add these variables under the variables parent element that you added to the template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="d1240-147">網路介面所使用的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d1240-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="d1240-148">虛擬網路和子網路的 IP 位址名稱和前置詞。</span><span class="sxs-lookup"><span data-stu-id="d1240-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="d1240-149">虛擬網路、負載平衡器和網路介面的名稱和識別碼。</span><span class="sxs-lookup"><span data-stu-id="d1240-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="d1240-150">與調整集內的機器相關聯之帳戶的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d1240-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="d1240-151">安裝在虛擬機器上的診斷延伸模組的設定。</span><span class="sxs-lookup"><span data-stu-id="d1240-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="d1240-152">如需診斷延伸模組的詳細資訊，請參閱[使用 Azure Resource Manager 範本建立具有監控和診斷功能的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d1240-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="d1240-153">在您新增至範本的資源父元素下，新增下列儲存體帳戶資源：</span><span class="sxs-lookup"><span data-stu-id="d1240-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="d1240-154">此範本使用迴圈來建立儲存作業系統磁碟和診斷資料的五個建議的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1240-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="d1240-155">這組帳戶最多可在一個調整集內支援 100 個虛擬機器，這是目前的最大值。</span><span class="sxs-lookup"><span data-stu-id="d1240-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="d1240-156">每個儲存體帳戶的命名方式都相同，即變數中所定義的字母指示項，加上您在參數中為範本提供的後置詞。</span><span class="sxs-lookup"><span data-stu-id="d1240-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
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

5. <span data-ttu-id="d1240-157">新增虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-157">Add the virtual network resource.</span></span> <span data-ttu-id="d1240-158">如需詳細資訊，請參閱 [網路資源提供者](../virtual-network/resource-groups-networking.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="d1240-159">新增負載平衡器和網路介面所使用的公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

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

7. <span data-ttu-id="d1240-160">新增調整集所使用的負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="d1240-161">如需詳細資料，請參閱 [Azure 資源管理員的負載平衡器支援](../load-balancer/load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d1240-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="d1240-162">新增個別的虛擬機器所使用的網路介面資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="d1240-163">由於擴展集內的機器無法直接透過公用 IP 位址來存取，因此必須在相同的虛擬網路中建立個別的虛擬機器，以從遠端存取該機器。</span><span class="sxs-lookup"><span data-stu-id="d1240-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

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

9. <span data-ttu-id="d1240-164">在與擴展集相同的網路中新增個別的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d1240-164">Add the separate virtual machine in the same network as the scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="d1240-165">新增虛擬機器擴展集資源，並指定在擴展集內所有虛擬機器上安裝的診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="d1240-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="d1240-166">此資源有許多設定都與虛擬機器資源相類似。</span><span class="sxs-lookup"><span data-stu-id="d1240-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="d1240-167">主要差異是指定擴展集中虛擬機器數量的容量元素，以及指定如何對虛擬機器進行更新的 upgradePolicy。</span><span class="sxs-lookup"><span data-stu-id="d1240-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="d1240-168">在依照 dependsOn 元素的指示建立所有的儲存體帳戶之前，不會建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="d1240-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="d1240-169">新增 autoscaleSettings 資源，以定義如何根據調整集內各機器的處理器使用情形進行調整集的調整。</span><span class="sxs-lookup"><span data-stu-id="d1240-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="d1240-170">在本教學課程中，以下的值相當重要：</span><span class="sxs-lookup"><span data-stu-id="d1240-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="d1240-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="d1240-171">**metricName**</span></span>  
    <span data-ttu-id="d1240-172">此值與我們在 wadperfcounter 變數中定義的效能計數器相同。</span><span class="sxs-lookup"><span data-stu-id="d1240-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="d1240-173">使用該變數，診斷擴充功能會收集 **Processor\PercentProcessorTime** 計數器。</span><span class="sxs-lookup"><span data-stu-id="d1240-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="d1240-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="d1240-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="d1240-175">此值是虛擬機器擴展集的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="d1240-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="d1240-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="d1240-176">**timeGrain**</span></span>  
    <span data-ttu-id="d1240-177">此值是所收集之計量的精細度。</span><span class="sxs-lookup"><span data-stu-id="d1240-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="d1240-178">此範本中，此值設為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d1240-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="d1240-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="d1240-179">**statistic**</span></span>  
    <span data-ttu-id="d1240-180">此值會決定如何結合計量以因應自動調整動作的需要。</span><span class="sxs-lookup"><span data-stu-id="d1240-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="d1240-181">可能的值為：Average、Min、Max。</span><span class="sxs-lookup"><span data-stu-id="d1240-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="d1240-182">在這個範本中，將會收集虛擬機器的平均總 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="d1240-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="d1240-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="d1240-183">**timeWindow**</span></span>  
    <span data-ttu-id="d1240-184">此值是收集執行個體資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="d1240-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="d1240-185">其值必須介於 5 分鐘到 12 小時之間。</span><span class="sxs-lookup"><span data-stu-id="d1240-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="d1240-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="d1240-186">**timeAggregation**</span></span>  
    <span data-ttu-id="d1240-187">此值會決定收集的資料應如何隨著時間結合。</span><span class="sxs-lookup"><span data-stu-id="d1240-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="d1240-188">預設值為 Average。</span><span class="sxs-lookup"><span data-stu-id="d1240-188">The default value is Average.</span></span> <span data-ttu-id="d1240-189">可能的值為：Average、Minimum、Maximum、Last、Total、Count。</span><span class="sxs-lookup"><span data-stu-id="d1240-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="d1240-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="d1240-190">**operator**</span></span>  
    <span data-ttu-id="d1240-191">此值是用來比較計量資料和臨界值的運算子。</span><span class="sxs-lookup"><span data-stu-id="d1240-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="d1240-192">可能的值為：Equals、NotEquals、GreaterThan、GreaterThanOrEqual、LessThan、LessThanOrEqual。</span><span class="sxs-lookup"><span data-stu-id="d1240-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="d1240-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="d1240-193">**threshold**</span></span>  
    <span data-ttu-id="d1240-194">此值是觸發調整動作的值。</span><span class="sxs-lookup"><span data-stu-id="d1240-194">This value triggers the scale action.</span></span> <span data-ttu-id="d1240-195">在此範本中，會在調整集內的機器之間的平均 CPU 使用率超過 50% 時，將機器新增至調整集。</span><span class="sxs-lookup"><span data-stu-id="d1240-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="d1240-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="d1240-196">**direction**</span></span>  
    <span data-ttu-id="d1240-197">此值會決定達到臨界值時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="d1240-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="d1240-198">可能的值為 Increase 或 Decrease。</span><span class="sxs-lookup"><span data-stu-id="d1240-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="d1240-199">在此範本中，如果臨界值在定義的時間範圍內超過 50%，則會增加調整集內的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="d1240-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="d1240-200">**type**</span><span class="sxs-lookup"><span data-stu-id="d1240-200">**type**</span></span>  
    <span data-ttu-id="d1240-201">此值是所應採取的動作類型，必須設為 ChangeCount。</span><span class="sxs-lookup"><span data-stu-id="d1240-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="d1240-202">**value**</span><span class="sxs-lookup"><span data-stu-id="d1240-202">**value**</span></span>  
    <span data-ttu-id="d1240-203">此值是從擴展集內新增或移除的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="d1240-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="d1240-204">此值必須是 1 或更大。</span><span class="sxs-lookup"><span data-stu-id="d1240-204">This value must be 1 or greater.</span></span> <span data-ttu-id="d1240-205">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="d1240-205">The default value is 1.</span></span> <span data-ttu-id="d1240-206">在此範本中，會在達到臨界值時，將調整集內的機器數目加 1。</span><span class="sxs-lookup"><span data-stu-id="d1240-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="d1240-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="d1240-207">**cooldown**</span></span>  
    <span data-ttu-id="d1240-208">此值是在上一個調整動作之後、下一個動作執行之前的等待時間量。</span><span class="sxs-lookup"><span data-stu-id="d1240-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="d1240-209">此值必須介於一分鐘到一週之間。</span><span class="sxs-lookup"><span data-stu-id="d1240-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="d1240-210">儲存範本檔案。</span><span class="sxs-lookup"><span data-stu-id="d1240-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="d1240-211">步驟 3：將範本上傳至儲存體</span><span class="sxs-lookup"><span data-stu-id="d1240-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="d1240-212">只要您知道您在步驟 1 中建立之儲存體帳戶的名稱和主要金鑰，即可上傳範本。</span><span class="sxs-lookup"><span data-stu-id="d1240-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="d1240-213">在您的命令列介面 (Bash、終端機、命令提示字元) 中，執行下列命令來設定存取儲存體帳戶所需的環境變數：</span><span class="sxs-lookup"><span data-stu-id="d1240-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="d1240-214">您可以在 Azure 入口網站中檢視儲存體帳戶資源，並按一下金鑰圖示，以取得此金鑰。</span><span class="sxs-lookup"><span data-stu-id="d1240-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="d1240-215">使用 Windows 命令提示字元時，請輸入 **set** 而不是 export。</span><span class="sxs-lookup"><span data-stu-id="d1240-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="d1240-216">建立儲存範本的容器。</span><span class="sxs-lookup"><span data-stu-id="d1240-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="d1240-217">將範本檔案上傳至新的容器。</span><span class="sxs-lookup"><span data-stu-id="d1240-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="d1240-218">步驟 4：部署範本</span><span class="sxs-lookup"><span data-stu-id="d1240-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="d1240-219">建立範本後，您就可以開始部署資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="d1240-220">使用下列命令啟動程序：</span><span class="sxs-lookup"><span data-stu-id="d1240-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="d1240-221">當您按 Enter 鍵時，系統會提示您提供您所指派的變數值。</span><span class="sxs-lookup"><span data-stu-id="d1240-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="d1240-222">請提供下列值：</span><span class="sxs-lookup"><span data-stu-id="d1240-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="d1240-223">所有資源要順利部署完成，大約需要 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d1240-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="d1240-224">您也可以使用入口網站的功能來部署資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="d1240-225">請使用此連結：https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="d1240-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="d1240-226">步驟 5：監視資源</span><span class="sxs-lookup"><span data-stu-id="d1240-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="d1240-227">您可以使用下列方法，取得關於虛擬機器調整集的某些資訊：</span><span class="sxs-lookup"><span data-stu-id="d1240-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="d1240-228">Azure 入口網站 - 目前，使用入口網站可以取得限定數量的資訊。</span><span class="sxs-lookup"><span data-stu-id="d1240-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="d1240-229">[Azure 資源總管](https://resources.azure.com/) - 此工具是瀏覽擴展集目前狀態的最佳選項。</span><span class="sxs-lookup"><span data-stu-id="d1240-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="d1240-230">按照此路徑，您應該會看到您所建立之調整集的執行個體檢視：</span><span class="sxs-lookup"><span data-stu-id="d1240-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="d1240-231">Azure CLI - 使用下列命令可取得某些資訊：</span><span class="sxs-lookup"><span data-stu-id="d1240-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="d1240-232">比照任何其他機器連接到 Jumpbox 虛擬機器，您即可從遠端存取調整集內的虛擬機器，以監視個別程序。</span><span class="sxs-lookup"><span data-stu-id="d1240-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="d1240-233">在 [虛擬機器調整集](https://msdn.microsoft.com/library/mt589023.aspx)中可以找到用來取得調整集相關資訊的完整 REST API。</span><span class="sxs-lookup"><span data-stu-id="d1240-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="d1240-234">步驟 6：移除資源</span><span class="sxs-lookup"><span data-stu-id="d1240-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="d1240-235">您將為 Azure 中所使用的資源支付費用，因此，刪除不再需要的資源永遠是最好的做法。</span><span class="sxs-lookup"><span data-stu-id="d1240-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="d1240-236">您不需要從資源群組個別刪除每個資源。</span><span class="sxs-lookup"><span data-stu-id="d1240-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="d1240-237">您可以刪除資源群組，其所有資源都將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="d1240-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="d1240-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1240-238">Next steps</span></span>
* <span data-ttu-id="d1240-239">在 [Azure 監視器跨平台 CLI 快速入門範例](../monitoring-and-diagnostics/insights-cli-samples.md)中找到 Azure 監視器監視功能的範例</span><span class="sxs-lookup"><span data-stu-id="d1240-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="d1240-240">若要深入了解通知功能，請參閱[使用自動調整動作在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="d1240-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="d1240-241">深入了解如何[使用稽核記錄，在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="d1240-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="d1240-242">請參閱 [Ubuntu 16.04 的自動調整示範應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale)範本，其中設定 Python/Bottle 應用程式執行虛擬機器擴展集的自動調整功能。</span><span class="sxs-lookup"><span data-stu-id="d1240-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

