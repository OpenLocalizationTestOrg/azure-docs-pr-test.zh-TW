---
title: "靜態內部私人 IP - Azure VM - 傳統"
description: "了解靜態內部 IP (DIP) 以及如何管理"
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="b2ed6-103">如何使用 PowerShell 設定靜態內部私人 IP 位址 (傳統)</span><span class="sxs-lookup"><span data-stu-id="b2ed6-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="b2ed6-104">在大部分情況下，您不需要針對虛擬機器指定靜態內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="b2ed6-105">虛擬網路中的 VM 會從您指定的範圍自動接收內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="b2ed6-106">但在某些情況下，針對特定 VM 指定靜態 IP 位址是合理的。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="b2ed6-107">例如，如果您的 VM 即將執行 DNS 或將成為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="b2ed6-108">靜態內部 IP 位址會伴隨 VM 而存在，甚至是透過停止/取消佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b2ed6-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b2ed6-110">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="b2ed6-111">Microsoft 建議讓大部分的新部署使用 [Resource Manager 部署模型](virtual-networks-static-private-ip-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="b2ed6-112">如何驗證特定 IP 位址是否可用</span><span class="sxs-lookup"><span data-stu-id="b2ed6-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="b2ed6-113">若要驗證 IP 位址 10.0.0.7 在名為 TestVnet 的 VNet 中是否可用，請執行下列 PowerShell 命令，並驗證 IsAvailable 的值：</span><span class="sxs-lookup"><span data-stu-id="b2ed6-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="b2ed6-114">如果您想要在安全的環境中測試上述命令，請依照[建立虛擬網路 (傳統)](virtual-networks-create-vnet-classic-pportal.md) 中的指導方針，建立名為 *TestVnet* 的 VNet，並確保它使用 *10.0.0.0/8* 位址空間。</span><span class="sxs-lookup"><span data-stu-id="b2ed6-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="b2ed6-115">如何在建立 VM 時指定靜態內部 IP</span><span class="sxs-lookup"><span data-stu-id="b2ed6-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="b2ed6-116">下方 PowerShell 指令碼會建立名為 TestService 的新雲端服務，接著從 Azure 中擷取映像，然後在新的雲端服務中使用擷取的映像建立名為 TestVM 的 VM，接下來設定 VM 位於稱為 Subnet-1 子網路中，並設定 10.0.0.7 作為 VM 的靜態內部 IP：</span><span class="sxs-lookup"><span data-stu-id="b2ed6-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="b2ed6-117">如何擷取 VM 的靜態內部 IP 資訊</span><span class="sxs-lookup"><span data-stu-id="b2ed6-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="b2ed6-118">若要檢視使用上述指令碼建立之 VM 的 IP 資訊，請執行下列 PowerShell 命令，並觀察 *IpAddress*的值：</span><span class="sxs-lookup"><span data-stu-id="b2ed6-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="b2ed6-119">如何從 VM 移除靜態內部 IP</span><span class="sxs-lookup"><span data-stu-id="b2ed6-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="b2ed6-120">若要移除在上述指令碼中新增至 VM 的靜態內部 IP，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="b2ed6-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="b2ed6-121">如何將靜態內部 IP 位址新增至現有的 VM</span><span class="sxs-lookup"><span data-stu-id="b2ed6-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="b2ed6-122">若要將靜態內部 IP 新增至使用上述指令碼建立的 VM，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b2ed6-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="b2ed6-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2ed6-123">Next steps</span></span>
[<span data-ttu-id="b2ed6-124">保留的 IP</span><span class="sxs-lookup"><span data-stu-id="b2ed6-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="b2ed6-125">執行個體層級公用 IP (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="b2ed6-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="b2ed6-126">保留的 IP REST API</span><span class="sxs-lookup"><span data-stu-id="b2ed6-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

