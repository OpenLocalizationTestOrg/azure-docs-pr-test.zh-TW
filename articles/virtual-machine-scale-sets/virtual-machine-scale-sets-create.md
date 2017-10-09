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
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>建立和部署虛擬機器擴展集
虛擬機器擴展集讓您輕鬆為您 toodeploy 和管理一組相同的虛擬機器。 調整集可為超大規模的應用程式提供高度擴充和可自訂的計算層，並且可支援 Windows 平台映像、Linux 平台映像、自訂映像和擴充。 如需調整集的詳細資訊，請參閱[虛擬機器擴展集](virtual-machine-scale-sets-overview.md)。

此教學課程會示範如何 toocreate 虛擬機器規模集**沒有**使用 hello Azure 入口網站。 如需如何 toouse hello Azure 入口網站資訊，請參閱[如何 toocreate 虛擬機器規模集以 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。

>[!NOTE]
>如需 Azure Resource Manager 資源的詳細資訊，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。

## <a name="sign-in-tooazure"></a>登入 tooAzure

如果您使用 Azure CLI 2.0 或 Azure PowerShell toocreate 縮放設定，您首先需要 toosign tooyour 訂用帳戶中的。

如需有關如何 tooinstall，設定，然後登入 tooAzure 使用 Azure CLI 或 PowerShell，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)或[開始使用 Azure PowerShell cmdlet](/powershell/azure/overview)。

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>建立資源群組

您必須先 toocreate hello 虛擬機器規模集資源群組相關聯。

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>從 Azure CLI 建立

使用 Azure CLI 建立虛擬機器擴展集最輕鬆。 如果您省略預設值，系統會為您提供預設值。 例如，如果您未指定任何虛擬網路資訊，則會為您建立虛擬網路。 如果您省略 hello 下列組件時，它們會為您建立： 
- 負載平衡器
- 虛擬網路
- 公用 IP 位址

如果選擇 hello 想 toouse hello 虛擬機器規模集上的虛擬機器映像，則會有幾個選項：

- URN  
資源 hello 識別項：  
**Win2012R2Datacenter**

- URN 別名  
URN 的好記名稱的 hello:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- 自訂資源識別碼  
hello 路徑 tooan Azure 資源：  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Web 資源  
hello 路徑 tooan HTTP URI:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>您可以使用 `az vm image list`取得可用的映像清單。

toocreate 的虛擬機器擴展集，您必須指定 hello 下列：

- 資源群組 
- 名稱
- 作業系統映像
- 驗證資訊 
 
hello 下列範例會建立基本的虛擬機器規模集 （此步驟可能需要幾分鐘的時間）。

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Hello 命令執行完成之後，您現在會有您的虛擬機器擴展集 建立。 因此，您可以連接 tooit，您可能需要 hello 虛擬機器 tooget hello IP 位址。 您可以使用下列命令的 hello 取得許多不同 hello 虛擬機器 （包括 hello IP 位址） 的相關資訊。 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>從 PowerShell 建立

PowerShell 是更複雜的 toouse 比 Azure CLI。 Azure CLI 會提供網路相關資源 (例如，負載平衡器、IP 位址和虛擬網路) 的預設值，PowerShell 不會提供。 使用 PowerShell 參考映像也有點複雜。 您可以取得映像以 hello 下列 cmdlet:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

hello cmdlet 工作可以使用管線傳送的順序。 以下是範例的所有 tooget hello 的映都像**美國西部 2**與 hello 名稱 「 發行者 」 的區域**microsoft**中。

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

用於建立虛擬機器規模集的 hello 工作流程如下所示：

1. 建立保留 hello 規模集的相關資訊的組態物件。
2. 參考 hello 基本 OS 映像。
3. Hello 作業系統設定： 驗證、 VM 名稱前置詞，以及使用者/密碼。
4. 設定網路功能。
5. 建立 hello 規模集。

這個範例為已安裝 Windows Server 2016 的電腦建立基本雙執行個體擴展集。

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

### <a name="using-a-custom-virtual-machine-image"></a>使用自訂虛擬機器映像
如果您要建立在擴展集從您自己的自訂映像，而不是從 hello 圖庫中，參考的虛擬機器映像 hello_組 AzureRmVmssStorageProfile_命令看起來像這樣：
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>從範本建立

您可以使用 Azure Resource Manager 範本部署虛擬機器擴展集。 您可以建立您自己的範本，或使用的 hello[範本儲存機制](https://azure.microsoft.com/resources/templates/?term=vmss)。 您可以部署這些範本直接 tooyour Azure 訂用帳戶。

>[!NOTE]
>toocreate 您自己的範本，建立 JSON 文字檔案。 如需有關的一般資訊 toocreate 和自訂範本，請參閱[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。

您可以[在 GitHub 上](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set)取得範本範例。 如需有關如何 toocreate 和使用該範例，請參閱[最小值可行的規模調整集合](.\virtual-machine-scale-sets-mvss-start.md)。

## <a name="create-from-visual-studio"></a>從 Visual Studio 建立

使用 Visual Studio 中，您可以建立 Azure 資源群組專案，並新增虛擬機器規模集範本 tooit。 您可以選擇是否要讓 tooimport 從 GitHub 或 hello Azure Web 應用程式庫。 系統也會為您產生部署 PowerShell 指令碼。 如需詳細資訊，請參閱[如何 toocreate 虛擬機器規模集與 Visual Studio](virtual-machine-scale-sets-vs-create.md)。

## <a name="create-from-hello-azure-portal"></a>建立從 hello Azure 入口網站

hello Azure 入口網站提供便利的方式 tooquickly 建立規模集。 如需詳細資訊，請參閱[如何 toocreate 虛擬機器規模集以 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。

## <a name="next-steps"></a>後續步驟

深入了解[資料磁碟](virtual-machine-scale-sets-attached-disks.md)。

了解如何太[管理您的應用程式](virtual-machine-scale-sets-deploy-app.md)。
