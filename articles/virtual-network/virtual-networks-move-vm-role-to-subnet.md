---
title: "將 VM (傳統) 或雲端服務角色執行個體移至不同的子網路 - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 將 VM (傳統) 和雲端服務角色執行個體移至不同的子網路。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="b7cd5-103">使用 PowerShell 將 VM (傳統) 或雲端服務角色執行個體移至不同的子網路</span><span class="sxs-lookup"><span data-stu-id="b7cd5-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="b7cd5-104">您可以使用 PowerShell 將 VM (傳統) 從一個子網路移至相同虛擬網路 (VNet) 中的另一個子網路。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="b7cd5-105">您可以藉由編輯 CSCFG 檔案，而非使用 PowerShell 來移動角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b7cd5-106">本文說明如何移動只透過傳統部署模型部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="b7cd5-107">為什麼要將 VM 移到另一個子網路？</span><span class="sxs-lookup"><span data-stu-id="b7cd5-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="b7cd5-108">當較舊的子網路太小，且由於在該子網路中執行的現有 VM 而無法擴充時，子網路移轉相當實用。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="b7cd5-109">在此案例中，您可以建立較新且較大的子網路，並將 VM 移轉至新的子網路，然後在完成移轉之後，您可以刪除舊的空白子網路。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="b7cd5-110">如何將 VM 移至另一個子網路</span><span class="sxs-lookup"><span data-stu-id="b7cd5-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="b7cd5-111">若要移動 VM，請執行 Set AzureSubnet PowerShell Cmdlet，並使用下方範例作為範本。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="b7cd5-112">在下列範例中，我們會將 TestVM 從其目前的子網路移到 Subnet-2。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="b7cd5-113">請務必編輯該範例來反映您的環境。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="b7cd5-114">請注意，每當您執行 Update-azurevm Cmdlet 作為程序的一部分，其會重新啟動您的 VM 作為更新程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="b7cd5-115">如果您針對 VM 指定靜態內部私人 DIP，您必須清除該設定，才能將 VM 移至新的子網路。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="b7cd5-116">在此案例中，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="b7cd5-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="b7cd5-117">若要將角色執行個體移至另一個子網路</span><span class="sxs-lookup"><span data-stu-id="b7cd5-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="b7cd5-118">若要移動角色執行個體，請編輯 CSCFG 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="b7cd5-119">在下方範例中，我們會將虛擬網路 VNETName 中的「Role0」從其目前的子網路移至 Subnet-2。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="b7cd5-120">因為已部署角色執行個體，您僅需變更 Subnet name = Subnet-2 的部份。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="b7cd5-121">請務必編輯該範例來反映您的環境。</span><span class="sxs-lookup"><span data-stu-id="b7cd5-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
