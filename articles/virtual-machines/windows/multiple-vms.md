---
title: "建立多部虛擬機器 | Microsoft Docs"
description: "在 Windows 上建立多部虛擬機器的選項"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 5e96805f8880a30a5fc8779d8f07addb6d068c09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-multiple-azure-virtual-machines"></a><span data-ttu-id="e25ce-103">建立多部 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e25ce-103">Create multiple Azure virtual machines</span></span>
<span data-ttu-id="e25ce-104">需要建立大量類似虛擬機器 (VM) 的案例不勝枚舉，</span><span class="sxs-lookup"><span data-stu-id="e25ce-104">There are many scenarios where you need to create a large number of similar virtual machines (VMs).</span></span> <span data-ttu-id="e25ce-105">部分範例包括高效能運算 (HPC)、大規模資料分析、可調整且通常是無狀態的中介層或後端伺服器 (例如 Web 伺服器)，以及分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="e25ce-105">Some examples include high-performance computing (HPC), large-scale data analysis, scalable and often stateless middle-tier or backend servers (such as webservers), and distributed databases.</span></span>

<span data-ttu-id="e25ce-106">本文章討論在 Azure 中建立多部 VM 的可用選項，</span><span class="sxs-lookup"><span data-stu-id="e25ce-106">This article discusses the available options to create multiple VMs in Azure.</span></span> <span data-ttu-id="e25ce-107">這些選項超越手動建立一系列 VM 的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="e25ce-107">These options go beyond the simple cases where you manually create a series of VMs.</span></span> <span data-ttu-id="e25ce-108">畢竟，在建立數量較多的 VM 時，如果按照平常使用的程序進行將無法妥善調整。</span><span class="sxs-lookup"><span data-stu-id="e25ce-108">To create many VMs, the processes that you typically use don't scale well if you need to create more than a handful of VMs.</span></span>

<span data-ttu-id="e25ce-109">其中一個可建立許多類似 VM 的方法，就是使用 Azure Resource Manager 資源迴圈 建構。</span><span class="sxs-lookup"><span data-stu-id="e25ce-109">One way to create many similar VMs is to use the Azure Resource Manager construct of *resource loops*.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="e25ce-110">資源迴圈</span><span class="sxs-lookup"><span data-stu-id="e25ce-110">Resource loops</span></span>
<span data-ttu-id="e25ce-111">資源迴圈是 Azure Resource Manager 範本中的速記語法，</span><span class="sxs-lookup"><span data-stu-id="e25ce-111">Resource loops are a syntactical shorthand in Azure Resource Manager templates.</span></span> <span data-ttu-id="e25ce-112">它能您在迴圈中建立一組設定相似的資源。</span><span class="sxs-lookup"><span data-stu-id="e25ce-112">Resource loops can create a set of similarly configured resources in a loop.</span></span> <span data-ttu-id="e25ce-113">您可以使用資源迴圈來建立多個儲存體帳戶、網路介面或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e25ce-113">You can use resource loops to create multiple storage accounts, network interfaces, or virtual machines.</span></span> <span data-ttu-id="e25ce-114">如需資源迴圈的詳細資訊，請參考[使用資源迴圈在可用性設定組中建立 VM](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)。</span><span class="sxs-lookup"><span data-stu-id="e25ce-114">For more information about resource loops, refer to [Create VMs in availability sets using resource loops](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).</span></span>

## <a name="challenges-of-scale"></a><span data-ttu-id="e25ce-115">規模的挑戰</span><span class="sxs-lookup"><span data-stu-id="e25ce-115">Challenges of scale</span></span>
<span data-ttu-id="e25ce-116">儘管資源迴圈讓建置大規模雲端基礎結構變得更簡單，也可以產生更精確的範本，不過仍有一些難題有待克服。</span><span class="sxs-lookup"><span data-stu-id="e25ce-116">Although resource loops make it easier to build out a cloud infrastructure at scale and produce more concise templates, certain challenges remain.</span></span> <span data-ttu-id="e25ce-117">例如，如果要使用資源迴圈建立 100 部虛擬機器，您需要建立網路介面控制器 (NIC) 與對應 VM 和儲存體帳戶之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="e25ce-117">For example, if you use a resource loop to create 100 virtual machines, you need to correlate network interface controllers (NICs) with corresponding VMs and storage accounts.</span></span> <span data-ttu-id="e25ce-118">由於 VM 的數目和儲存體帳戶的數目可能會不同，因此會造就不同大小的資源迴圈。</span><span class="sxs-lookup"><span data-stu-id="e25ce-118">Because the number of VMs is likely to be different from the number of storage accounts, you'll have to deal with different resource loop sizes, too.</span></span> <span data-ttu-id="e25ce-119">這些是可解決的問題，不過會讓複雜度隨著規模擴大而大幅增長。</span><span class="sxs-lookup"><span data-stu-id="e25ce-119">These are solvable problems, but the complexity increases significantly with scale.</span></span>

<span data-ttu-id="e25ce-120">另一項挑戰發生於當您需要彈性調整的基礎結構時，</span><span class="sxs-lookup"><span data-stu-id="e25ce-120">Another challenge occurs when you need an infrastructure that scales elastically.</span></span> <span data-ttu-id="e25ce-121">例如您可能想自動調整基礎結構，以自動因應工作負載而增加或減少 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="e25ce-121">For example, you might want an autoscale infrastructure that automatically increases or decreases the number of VMs in response to workload.</span></span> <span data-ttu-id="e25ce-122">VM 不提供改變數目 (相應放大和相應縮小) 的整合式機制。</span><span class="sxs-lookup"><span data-stu-id="e25ce-122">VMs don't provide an integrated mechanism to vary in number (scale out and scale in).</span></span> <span data-ttu-id="e25ce-123">假設您想透過移除 VM 來達到相應縮小的目的，但即使 VM 在更新和容錯網域之間保持平衡，依然很難保證高可用性。</span><span class="sxs-lookup"><span data-stu-id="e25ce-123">If you scale in by removing VMs, it's difficult to guarantee high availability by making sure that VMs are balanced across update and fault domains.</span></span>

<span data-ttu-id="e25ce-124">最後，當您使用一個資源迴圈時，就會產生許多涉及基礎網狀架構的資源建立訴求。</span><span class="sxs-lookup"><span data-stu-id="e25ce-124">Finally, when you use a resource loop, multiple calls to create resources go to the underlying fabric.</span></span> <span data-ttu-id="e25ce-125">一旦有許多建立類似資源的訴求出現，Azure 就有潛在機會可以改善設計和實施最佳化，藉此提升部署可靠性和效能。</span><span class="sxs-lookup"><span data-stu-id="e25ce-125">When multiple calls create similar resources, Azure has an implicit opportunity to improve upon this design and optimize deployment reliability and performance.</span></span> <span data-ttu-id="e25ce-126">這正是我們引進「虛擬機器擴展集」  的契機。</span><span class="sxs-lookup"><span data-stu-id="e25ce-126">This is where *virtual machine scale sets* come in.</span></span>

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="e25ce-127">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="e25ce-127">Virtual machine scale sets</span></span>
<span data-ttu-id="e25ce-128">虛擬機器擴展集是用來部署及管理一組相同 VM 的 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="e25ce-128">Virtual machine scale sets are an Azure Compute resource to deploy and manage a set of identical VMs.</span></span> <span data-ttu-id="e25ce-129">由於所有 VM 的設定均相同，所以能輕鬆相應縮小和增加 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="e25ce-129">With all VMs configured the same, VM scale sets are easy to scale in and scale out.</span></span> <span data-ttu-id="e25ce-130">您只要變更集合中的 VM 數目即可。</span><span class="sxs-lookup"><span data-stu-id="e25ce-130">You simply change the number of VMs in the set.</span></span> <span data-ttu-id="e25ce-131">您也可以根據工作負載的需求自動調整 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="e25ce-131">You can also configure VM scale sets to autoscale based on the demands of the workload.</span></span>

<span data-ttu-id="e25ce-132">對於需要相應放大計算資源的應用程式，調整作業會隱含地平衡分散到容錯網域和更新網域。</span><span class="sxs-lookup"><span data-stu-id="e25ce-132">For applications that need to scale Compute resources out and in, scale operations are implicitly balanced across fault and update domains.</span></span>

<span data-ttu-id="e25ce-133">VM 擴展集擁有網路、儲存體、虛擬機器和擴充功能等供您集中設定的屬性，而不需建立 NIC 和 VM 等多種資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="e25ce-133">Instead of correlating multiple resources such as NICs and VMs, a VM scale set has network, storage, virtual machine, and extension properties that you can configure centrally.</span></span>

<span data-ttu-id="e25ce-134">如需 VM 擴展集的簡介，請參閱 [虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)的產品頁面。</span><span class="sxs-lookup"><span data-stu-id="e25ce-134">For an introduction to VM scale sets, refer to the [Virtual machine scale sets product page](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span> <span data-ttu-id="e25ce-135">如需詳細資訊，請參閱 [虛擬機器擴展集](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)的文件。</span><span class="sxs-lookup"><span data-stu-id="e25ce-135">For more detailed information, go to the [Virtual machines scale sets documentation](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).</span></span>

