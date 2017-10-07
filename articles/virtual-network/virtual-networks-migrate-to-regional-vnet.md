---
title: "Azure 虛擬網路 （傳統） 的同質群組 tooa 區域 aaaMigrate |Microsoft 文件"
description: "了解如何 toomigrate 虛擬網路 （傳統） 從親和性群組 tooa 區域。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="49ee4-103">移轉的同質群組 tooa 區域虛擬網路 （傳統）</span><span class="sxs-lookup"><span data-stu-id="49ee4-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49ee4-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="49ee4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="49ee4-105">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="49ee4-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="49ee4-106">Microsoft 建議最新的部署使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="49ee4-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="49ee4-107">同質群組確保的 hello 很遠，啟用這些資源 toocommunicate 速度較快的伺服器實體裝載相同同質群組內建立資源。</span><span class="sxs-lookup"><span data-stu-id="49ee4-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="49ee4-108">Hello 過去，同質群組是建立虛擬網路 （傳統） 的需求。</span><span class="sxs-lookup"><span data-stu-id="49ee4-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="49ee4-109">執行之後，受管理虛擬網路 （傳統） 的 hello 網路管理員服務只能在一組實體伺服器或延展單位。</span><span class="sxs-lookup"><span data-stu-id="49ee4-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="49ee4-110">結構改進增加 hello 範圍的網路管理 tooa 區域。</span><span class="sxs-lookup"><span data-stu-id="49ee4-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="49ee4-111">由於這些架構的改進，因而導致不再建議使用同質群組，或不再需要虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="49ee4-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="49ee4-112">區域取代 hello 使用同質群組的虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="49ee4-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="49ee4-113">與區域相關聯的虛擬網路 (傳統) 稱為地區虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="49ee4-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="49ee4-114">我們建議您在一般情況下不要使用同質群組。</span><span class="sxs-lookup"><span data-stu-id="49ee4-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="49ee4-115">除了 hello 虛擬網路需求，同質群組也是重要 toouse tooensure 資源，例如計算 （傳統） 和儲存體 （傳統），已放置彼此的附近。</span><span class="sxs-lookup"><span data-stu-id="49ee4-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="49ee4-116">不過，與目前 Azure 網路架構 hello，這些位置需求不再需要。</span><span class="sxs-lookup"><span data-stu-id="49ee4-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49ee4-117">雖然技術上仍然可以 toocreate 與同質群組相關聯的虛擬網路，沒有任何令人信服原因 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="49ee4-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="49ee4-118">許多虛擬網路功能 (例如網路安全性群組) 只有在使用區域虛擬網路時才能使用，且不適用於與同質群組相關聯的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="49ee4-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="49ee4-119">編輯 hello 網路組態檔</span><span class="sxs-lookup"><span data-stu-id="49ee4-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="49ee4-120">匯出 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="49ee4-120">Export hello network configuration file.</span></span> <span data-ttu-id="49ee4-121">toolearn 如何 tooexport 網路組態檔使用 PowerShell 或 hello Azure 命令列介面 (CLI) 1.0，請參閱[設定虛擬網路使用網路組態檔](virtual-networks-using-network-configuration-file.md#export)。</span><span class="sxs-lookup"><span data-stu-id="49ee4-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="49ee4-122">編輯 hello 網路組態檔，取代**AffinityGroup**與**位置**。</span><span class="sxs-lookup"><span data-stu-id="49ee4-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="49ee4-123">您需針對 **Location** 指定 Azure [區域](https://azure.microsoft.com/regions)。</span><span class="sxs-lookup"><span data-stu-id="49ee4-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="49ee4-124">hello**位置**是您指定 hello 與虛擬網路 （傳統） 相關聯的同質群組的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="49ee4-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="49ee4-125">例如，如果您的虛擬網路 （傳統） 與移轉時，位於美國西部、 同質群組相關聯您**位置**必須指向 tooWest 美國。</span><span class="sxs-lookup"><span data-stu-id="49ee4-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="49ee4-126">編輯 hello 遵循您的網路組態檔中的程式行、 取代您自己 hello 值：</span><span class="sxs-lookup"><span data-stu-id="49ee4-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="49ee4-127">**舊值：**\<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="49ee4-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="49ee4-128">**新值：**\<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span><span class="sxs-lookup"><span data-stu-id="49ee4-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="49ee4-129">儲存您的變更和[匯入](virtual-networks-using-network-configuration-file.md#import)hello 網路組態 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="49ee4-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="49ee4-130">這項移轉不會產生任何停機時間 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="49ee4-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="49ee4-131">如果您在同質群組 （傳統） 的 VM 哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="49ee4-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="49ee4-132">Vm （傳統），目前正在同質群組中不需要 toobe 從 hello 同質群組中移除。</span><span class="sxs-lookup"><span data-stu-id="49ee4-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="49ee4-133">一旦部署 VM 時，就會是已部署的 tooa 單一延展單位。</span><span class="sxs-lookup"><span data-stu-id="49ee4-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="49ee4-134">同質群組可限制 hello 的可用 VM 集合大小為新的 VM 部署，但是已部署的任何現有 VM 已經限制 toohello 組的 VM 大小可用 hello 縮放單位中的 hello 部署 VM。</span><span class="sxs-lookup"><span data-stu-id="49ee4-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="49ee4-135">因為 hello VM 已部署 tooa 擴充單元，從同質群組中移除 VM 沒有 hello VM 上的任何作用。</span><span class="sxs-lookup"><span data-stu-id="49ee4-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
