---
title: "aaaStatic 內部私用 IP-Azure VM-傳統"
description: "了解靜態內部 Ip (Dip) 以及 toomanage 它們"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="471e4-103">Tooset 靜態內部私用 IP 位址使用 PowerShell （傳統）</span><span class="sxs-lookup"><span data-stu-id="471e4-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="471e4-104">在大部分情況下，您不需要 toospecify 靜態內部 IP 位址的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="471e4-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="471e4-105">虛擬網路中的 VM 會從您指定的範圍自動接收內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="471e4-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="471e4-106">但在某些情況下，針對特定 VM 指定靜態 IP 位址是合理的。</span><span class="sxs-lookup"><span data-stu-id="471e4-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="471e4-107">例如，如果您的 VM 進行 toorun DNS 或將網域控制站。</span><span class="sxs-lookup"><span data-stu-id="471e4-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="471e4-108">即使歷經停止/解除佈建狀態 hello VM 會保持靜態內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="471e4-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="471e4-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="471e4-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="471e4-110">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="471e4-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="471e4-111">Microsoft 建議的最新的部署使用 hello [Resource Manager 部署模型](virtual-networks-static-private-ip-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="471e4-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="471e4-112">如何 tooverify 特定的 IP 位址是否可用</span><span class="sxs-lookup"><span data-stu-id="471e4-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="471e4-113">如果 hello tooverify IP 位址*10.0.0.7*位於名為 vnet *TestVnet*，執行下列 PowerShell 命令的 hello，並確認 hello 值*IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="471e4-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="471e4-114">如果您想 tootest hello 上述命令會在安全的環境中請依照下列中的 hello 指導方針[建立虛擬網路 （傳統）](virtual-networks-create-vnet-classic-pportal.md) toocreate 名為 vnet *TestVnet* ，並確保它會使用 hello *10.0.0.0/8*位址空間。</span><span class="sxs-lookup"><span data-stu-id="471e4-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="471e4-115">如何 toospecify 靜態內部 IP 建立 VM 時</span><span class="sxs-lookup"><span data-stu-id="471e4-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="471e4-116">hello 下列 PowerShell 指令碼會建立新的雲端服務，名為*TestService*，然後從 Azure 擷取映像，然後建立名為 VM *TestVM* hello 使用 hello 擷取映像，新雲端服務中設定 hello 名為的子網路的 VM toobe *subnet-1*，並設定*10.0.0.7* hello VM 的靜態內部 ip 位址為：</span><span class="sxs-lookup"><span data-stu-id="471e4-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="471e4-117">如何 tooretrieve 靜態內部 IP 資訊適用於 VM</span><span class="sxs-lookup"><span data-stu-id="471e4-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="471e4-118">執行下列 PowerShell 命令的 hello tooview hello 靜態內部 IP 資訊 hello 與 hello 指令碼，請在建立 VM，並觀察 hello 值*IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="471e4-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="471e4-119">如何 tooremove 從 VM 的靜態內部 IP</span><span class="sxs-lookup"><span data-stu-id="471e4-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="471e4-120">tooremove hello 的靜態內部 IP 加入 toohello VM 在 hello 指令碼，請執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="471e4-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="471e4-121">如何 tooadd 靜態內部 IP tooan 現有的 VM</span><span class="sxs-lookup"><span data-stu-id="471e4-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="471e4-122">tooadd 靜態的內部 IP toohello 下命令使用上述 runt hello 指令碼建立 VM:</span><span class="sxs-lookup"><span data-stu-id="471e4-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="471e4-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="471e4-123">Next steps</span></span>
[<span data-ttu-id="471e4-124">保留的 IP</span><span class="sxs-lookup"><span data-stu-id="471e4-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="471e4-125">執行個體層級公用 IP (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="471e4-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="471e4-126">保留的 IP REST API</span><span class="sxs-lookup"><span data-stu-id="471e4-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

