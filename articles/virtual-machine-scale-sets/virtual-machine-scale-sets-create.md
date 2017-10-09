---
title: "aaaCreate Azure 虛擬機器規模集 |Microsoft 文件"
description: "使用 Azure CLI、PowerShell、範本或 Visual Studio 建立和部署 Linux 或 Windows Azure 虛擬機器擴展集。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="f0017-103">建立和部署虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="f0017-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="f0017-104">虛擬機器擴展集讓您輕鬆為您 toodeploy 和管理一組相同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f0017-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="f0017-105">調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。</span><span class="sxs-lookup"><span data-stu-id="f0017-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="f0017-106">如需調整集的詳細資訊，請參閱[虛擬機器擴展集](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="f0017-107">此教學課程會示範如何 toocreate 虛擬機器規模集**沒有**使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f0017-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="f0017-108">如需如何 toouse hello Azure 入口網站資訊，請參閱[如何 toocreate 虛擬機器規模集以 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="f0017-109">如需 Azure Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="f0017-110">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f0017-110">Sign in tooAzure</span></span>

<span data-ttu-id="f0017-111">如果您使用 Azure CLI 2.0 或 Azure PowerShell toocreate 縮放設定，您首先需要 toosign tooyour 訂用帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="f0017-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="f0017-112">如需有關如何 tooinstall，設定，然後登入 tooAzure 使用 Azure CLI 或 PowerShell，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)或[開始使用 Azure PowerShell cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f0017-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f0017-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f0017-113">Create a resource group</span></span>

<span data-ttu-id="f0017-114">您必須先 toocreate hello 虛擬機器規模集資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="f0017-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="f0017-115">從 Azure CLI 建立</span><span class="sxs-lookup"><span data-stu-id="f0017-115">Create from Azure CLI</span></span>

<span data-ttu-id="f0017-116">使用 Azure CLI 建立虛擬機器擴展集最輕鬆。</span><span class="sxs-lookup"><span data-stu-id="f0017-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="f0017-117">如果您省略預設值，系統會為您提供預設值。</span><span class="sxs-lookup"><span data-stu-id="f0017-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="f0017-118">例如，如果您未指定任何虛擬網路資訊，則會為您建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f0017-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="f0017-119">如果您省略 hello 下列組件時，它們會為您建立：</span><span class="sxs-lookup"><span data-stu-id="f0017-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="f0017-120">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="f0017-120">A load balancer</span></span>
- <span data-ttu-id="f0017-121">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f0017-121">A virtual network</span></span>
- <span data-ttu-id="f0017-122">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f0017-122">A public IP address</span></span>

<span data-ttu-id="f0017-123">如果選擇 hello 想 toouse hello 虛擬機器規模集上的虛擬機器映像，則會有幾個選項：</span><span class="sxs-lookup"><span data-stu-id="f0017-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="f0017-124">URN</span><span class="sxs-lookup"><span data-stu-id="f0017-124">URN</span></span>  
<span data-ttu-id="f0017-125">資源 hello 識別項：</span><span class="sxs-lookup"><span data-stu-id="f0017-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="f0017-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="f0017-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="f0017-127">URN 別名</span><span class="sxs-lookup"><span data-stu-id="f0017-127">URN alias</span></span>  
<span data-ttu-id="f0017-128">URN 的好記名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0017-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="f0017-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="f0017-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="f0017-130">自訂資源識別碼</span><span class="sxs-lookup"><span data-stu-id="f0017-130">Custom resource id</span></span>  
<span data-ttu-id="f0017-131">hello 路徑 tooan Azure 資源：</span><span class="sxs-lookup"><span data-stu-id="f0017-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="f0017-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="f0017-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="f0017-133">Web 資源</span><span class="sxs-lookup"><span data-stu-id="f0017-133">Web resource</span></span>  
<span data-ttu-id="f0017-134">hello 路徑 tooan HTTP URI:</span><span class="sxs-lookup"><span data-stu-id="f0017-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="f0017-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="f0017-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="f0017-136">您可以使用 `az vm image list`取得可用的映像清單。</span><span class="sxs-lookup"><span data-stu-id="f0017-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="f0017-137">toocreate 的虛擬機器擴展集，您必須指定 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f0017-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="f0017-138">資源群組</span><span class="sxs-lookup"><span data-stu-id="f0017-138">Resource group</span></span> 
- <span data-ttu-id="f0017-139">名稱</span><span class="sxs-lookup"><span data-stu-id="f0017-139">Name</span></span>
- <span data-ttu-id="f0017-140">作業系統映像</span><span class="sxs-lookup"><span data-stu-id="f0017-140">Operating system image</span></span>
- <span data-ttu-id="f0017-141">驗證資訊</span><span class="sxs-lookup"><span data-stu-id="f0017-141">Authentication information</span></span> 
 
<span data-ttu-id="f0017-142">hello 下列範例會建立基本的虛擬機器規模集 （此步驟可能需要幾分鐘的時間）。</span><span class="sxs-lookup"><span data-stu-id="f0017-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="f0017-143">Hello 命令執行完成之後，您現在會有您的虛擬機器擴展集 建立。</span><span class="sxs-lookup"><span data-stu-id="f0017-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="f0017-144">因此，您可以連接 tooit，您可能需要 hello 虛擬機器 tooget hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0017-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="f0017-145">您可以使用下列命令的 hello 取得許多不同 hello 虛擬機器 （包括 hello IP 位址） 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f0017-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="f0017-146">從 PowerShell 建立</span><span class="sxs-lookup"><span data-stu-id="f0017-146">Create from PowerShell</span></span>

<span data-ttu-id="f0017-147">PowerShell 是更複雜的 toouse 比 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f0017-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="f0017-148">Azure CLI 會提供網路相關資源 (例如，負載平衡器、IP 位址和虛擬網路) 的預設值，PowerShell 不會提供。</span><span class="sxs-lookup"><span data-stu-id="f0017-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="f0017-149">使用 PowerShell 參考映像也有點複雜。</span><span class="sxs-lookup"><span data-stu-id="f0017-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="f0017-150">您可以取得映像以 hello 下列 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f0017-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="f0017-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="f0017-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="f0017-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="f0017-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="f0017-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="f0017-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="f0017-154">hello cmdlet 工作可以使用管線傳送的順序。</span><span class="sxs-lookup"><span data-stu-id="f0017-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="f0017-155">以下是範例的所有 tooget hello 的映都像**美國西部 2**與 hello 名稱 「 發行者 」 的區域**microsoft**中。</span><span class="sxs-lookup"><span data-stu-id="f0017-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="f0017-156">用於建立虛擬機器規模集的 hello 工作流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="f0017-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="f0017-157">建立保留 hello 規模集的相關資訊的組態物件。</span><span class="sxs-lookup"><span data-stu-id="f0017-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="f0017-158">參考 hello 基本 OS 映像。</span><span class="sxs-lookup"><span data-stu-id="f0017-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="f0017-159">Hello 作業系統設定： 驗證、 VM 名稱前置詞，以及使用者/密碼。</span><span class="sxs-lookup"><span data-stu-id="f0017-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="f0017-160">設定網路功能。</span><span class="sxs-lookup"><span data-stu-id="f0017-160">Configure networking.</span></span>
5. <span data-ttu-id="f0017-161">建立 hello 規模集。</span><span class="sxs-lookup"><span data-stu-id="f0017-161">Create hello scale set.</span></span>

<span data-ttu-id="f0017-162">這個範例為已安裝 Windows Server 2016 的電腦建立基本雙執行個體擴展集。</span><span class="sxs-lookup"><span data-stu-id="f0017-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="f0017-163">使用自訂虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="f0017-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="f0017-164">如果您要建立在擴展集從您自己的自訂映像，而不是從 hello 圖庫中，參考的虛擬機器映像 hello_組 AzureRmVmssStorageProfile_命令看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f0017-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="f0017-165">從範本建立</span><span class="sxs-lookup"><span data-stu-id="f0017-165">Create from a template</span></span>

<span data-ttu-id="f0017-166">您可以使用 Azure Resource Manager 範本部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="f0017-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="f0017-167">您可以建立您自己的範本，或使用的 hello[範本儲存機制](https://azure.microsoft.com/resources/templates/?term=vmss)。</span><span class="sxs-lookup"><span data-stu-id="f0017-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="f0017-168">您可以部署這些範本直接 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0017-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="f0017-169">toocreate 您自己的範本，建立 JSON 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="f0017-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="f0017-170">如需有關的一般資訊 toocreate 和自訂範本，請參閱[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f0017-171">您可以[在 GitHub 上](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set)取得範本範例。</span><span class="sxs-lookup"><span data-stu-id="f0017-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="f0017-172">如需有關如何 toocreate 和使用該範例，請參閱[最小值可行的規模調整集合](.\virtual-machine-scale-sets-mvss-start.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="f0017-173">從 Visual Studio 建立</span><span class="sxs-lookup"><span data-stu-id="f0017-173">Create from Visual Studio</span></span>

<span data-ttu-id="f0017-174">使用 Visual Studio 中，您可以建立 Azure 資源群組專案，並新增虛擬機器規模集範本 tooit。</span><span class="sxs-lookup"><span data-stu-id="f0017-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="f0017-175">您可以選擇是否要讓 tooimport 從 GitHub 或 hello Azure Web 應用程式庫。</span><span class="sxs-lookup"><span data-stu-id="f0017-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="f0017-176">系統也會為您產生部署 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0017-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="f0017-177">如需詳細資訊，請參閱[如何 toocreate 虛擬機器規模集與 Visual Studio](virtual-machine-scale-sets-vs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="f0017-178">建立從 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f0017-178">Create from hello Azure portal</span></span>

<span data-ttu-id="f0017-179">hello Azure 入口網站提供便利的方式 tooquickly 建立規模集。</span><span class="sxs-lookup"><span data-stu-id="f0017-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="f0017-180">如需詳細資訊，請參閱[如何 toocreate 虛擬機器規模集以 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0017-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0017-181">Next steps</span></span>

<span data-ttu-id="f0017-182">深入了解[資料磁碟](virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="f0017-183">了解如何太[管理您的應用程式](virtual-machine-scale-sets-deploy-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f0017-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
