---
title: "aaaCreate 多部虛擬機器 |Microsoft 文件"
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
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a><span data-ttu-id="8426f-103">建立多部 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8426f-103">Create multiple Azure virtual machines</span></span>
<span data-ttu-id="8426f-104">有許多案例中您需要 toocreate 大量的類似的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="8426f-104">There are many scenarios where you need toocreate a large number of similar virtual machines (VMs).</span></span> <span data-ttu-id="8426f-105">部分範例包括高效能運算 (HPC)、大規模資料分析、可調整且通常是無狀態的中介層或後端伺服器 (例如 Web 伺服器)，以及分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="8426f-105">Some examples include high-performance computing (HPC), large-scale data analysis, scalable and often stateless middle-tier or backend servers (such as webservers), and distributed databases.</span></span>

<span data-ttu-id="8426f-106">這篇文章討論 hello 可用的選項 toocreate 在 Azure 中的多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="8426f-106">This article discusses hello available options toocreate multiple VMs in Azure.</span></span> <span data-ttu-id="8426f-107">這些選項超越 hello 簡單案例中手動建立一系列的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8426f-107">These options go beyond hello simple cases where you manually create a series of VMs.</span></span> <span data-ttu-id="8426f-108">如果您需要 toocreate 多個 Vm 的少數許多 Vm，您通常使用 hello 處理程序不縮放 toocreate。</span><span class="sxs-lookup"><span data-stu-id="8426f-108">toocreate many VMs, hello processes that you typically use don't scale well if you need toocreate more than a handful of VMs.</span></span>

<span data-ttu-id="8426f-109">許多類似的 Vm 是 toouse hello Azure 資源管理員結構的其中一種方式 toocreate*資源迴圈*。</span><span class="sxs-lookup"><span data-stu-id="8426f-109">One way toocreate many similar VMs is toouse hello Azure Resource Manager construct of *resource loops*.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="8426f-110">資源迴圈</span><span class="sxs-lookup"><span data-stu-id="8426f-110">Resource loops</span></span>
<span data-ttu-id="8426f-111">資源迴圈是 Azure Resource Manager 範本中的速記語法，</span><span class="sxs-lookup"><span data-stu-id="8426f-111">Resource loops are a syntactical shorthand in Azure Resource Manager templates.</span></span> <span data-ttu-id="8426f-112">它能您在迴圈中建立一組設定相似的資源。</span><span class="sxs-lookup"><span data-stu-id="8426f-112">Resource loops can create a set of similarly configured resources in a loop.</span></span> <span data-ttu-id="8426f-113">您可以使用資源迴圈 toocreate 多個儲存體帳戶、 網路介面或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8426f-113">You can use resource loops toocreate multiple storage accounts, network interfaces, or virtual machines.</span></span> <span data-ttu-id="8426f-114">如需資源迴圈的詳細資訊，請參閱太[使用資源迴圈的可用性設定組中的 建立 Vm](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)。</span><span class="sxs-lookup"><span data-stu-id="8426f-114">For more information about resource loops, refer too[Create VMs in availability sets using resource loops](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).</span></span>

## <a name="challenges-of-scale"></a><span data-ttu-id="8426f-115">規模的挑戰</span><span class="sxs-lookup"><span data-stu-id="8426f-115">Challenges of scale</span></span>
<span data-ttu-id="8426f-116">雖然資源迴圈在標尺將更容易 toobuild 出雲端基礎結構，而且會產生更精確的範本，就會保留特定的挑戰。</span><span class="sxs-lookup"><span data-stu-id="8426f-116">Although resource loops make it easier toobuild out a cloud infrastructure at scale and produce more concise templates, certain challenges remain.</span></span> <span data-ttu-id="8426f-117">例如，如果您使用資源迴圈 toocreate 100 部虛擬機器，您會需要 toocorrelate 網路介面控制器 (Nic) 對應的 Vm 與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8426f-117">For example, if you use a resource loop toocreate 100 virtual machines, you need toocorrelate network interface controllers (NICs) with corresponding VMs and storage accounts.</span></span> <span data-ttu-id="8426f-118">Hello Vm 數目是可能 toobe hello 儲存體帳戶數目不同，因為您必須具有不同的資源迴圈大小，toodeal 太。</span><span class="sxs-lookup"><span data-stu-id="8426f-118">Because hello number of VMs is likely toobe different from hello number of storage accounts, you'll have toodeal with different resource loop sizes, too.</span></span> <span data-ttu-id="8426f-119">這些都是可解決的問題，但是 hello 複雜性會大幅增加小數位數。</span><span class="sxs-lookup"><span data-stu-id="8426f-119">These are solvable problems, but hello complexity increases significantly with scale.</span></span>

<span data-ttu-id="8426f-120">另一項挑戰發生於當您需要彈性調整的基礎結構時，</span><span class="sxs-lookup"><span data-stu-id="8426f-120">Another challenge occurs when you need an infrastructure that scales elastically.</span></span> <span data-ttu-id="8426f-121">例如，您可以自動調整規模基礎結構會自動增加或減少 Vm 中回應 tooworkload hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8426f-121">For example, you might want an autoscale infrastructure that automatically increases or decreases hello number of VMs in response tooworkload.</span></span> <span data-ttu-id="8426f-122">Vm 未提供的整合的機制 toovary 中數字 （向外的延展和中的小數位數）。</span><span class="sxs-lookup"><span data-stu-id="8426f-122">VMs don't provide an integrated mechanism toovary in number (scale out and scale in).</span></span> <span data-ttu-id="8426f-123">如果您藉由移除 Vm 中調整規模，請藉由確定更新和錯誤網域之間平衡的 Vm 是難以 tooguarantee 高可用性。</span><span class="sxs-lookup"><span data-stu-id="8426f-123">If you scale in by removing VMs, it's difficult tooguarantee high availability by making sure that VMs are balanced across update and fault domains.</span></span>

<span data-ttu-id="8426f-124">最後，當您使用的資源迴圈時，多個呼叫 toocreate 資源移 toohello 基礎網狀架構。</span><span class="sxs-lookup"><span data-stu-id="8426f-124">Finally, when you use a resource loop, multiple calls toocreate resources go toohello underlying fabric.</span></span> <span data-ttu-id="8426f-125">當多個呼叫會建立類似的資源時，Azure 有隱含的機會 tooimprove，在這項設計時，並最佳化部署可靠性和效能。</span><span class="sxs-lookup"><span data-stu-id="8426f-125">When multiple calls create similar resources, Azure has an implicit opportunity tooimprove upon this design and optimize deployment reliability and performance.</span></span> <span data-ttu-id="8426f-126">這正是我們引進「虛擬機器擴展集」  的契機。</span><span class="sxs-lookup"><span data-stu-id="8426f-126">This is where *virtual machine scale sets* come in.</span></span>

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="8426f-127">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="8426f-127">Virtual machine scale sets</span></span>
<span data-ttu-id="8426f-128">虛擬機器擴展集是 Azure 計算資源 toodeploy 和管理一組相同的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8426f-128">Virtual machine scale sets are an Azure Compute resource toodeploy and manage a set of identical VMs.</span></span> <span data-ttu-id="8426f-129">並將所有的 Vm 設定 hello 相同，則 VM 規模集為中的簡單 tooscale 及向外的延展。您只需變更 hello Vm 數目在 hello 集合中。</span><span class="sxs-lookup"><span data-stu-id="8426f-129">With all VMs configured hello same, VM scale sets are easy tooscale in and scale out. You simply change hello number of VMs in hello set.</span></span> <span data-ttu-id="8426f-130">您也可以設定 VM 規模集 tooautoscale hello hello 工作負載需求為基礎。</span><span class="sxs-lookup"><span data-stu-id="8426f-130">You can also configure VM scale sets tooautoscale based on hello demands of hello workload.</span></span>

<span data-ttu-id="8426f-131">需要 tooscale 計算資源，且在標尺的應用程式的作業會隱含地平衡容錯網域和更新網域。</span><span class="sxs-lookup"><span data-stu-id="8426f-131">For applications that need tooscale Compute resources out and in, scale operations are implicitly balanced across fault and update domains.</span></span>

<span data-ttu-id="8426f-132">VM 擴展集擁有網路、儲存體、虛擬機器和擴充功能等供您集中設定的屬性，而不需建立 NIC 和 VM 等多種資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="8426f-132">Instead of correlating multiple resources such as NICs and VMs, a VM scale set has network, storage, virtual machine, and extension properties that you can configure centrally.</span></span>

<span data-ttu-id="8426f-133">設定簡介 tooVM 的小數位數，參閱 toohello[虛擬機器規模設定產品頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="8426f-133">For an introduction tooVM scale sets, refer toohello [Virtual machine scale sets product page](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span> <span data-ttu-id="8426f-134">如需詳細資訊，請移 toohello[虛擬機器規模設定文件](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="8426f-134">For more detailed information, go toohello [Virtual machines scale sets documentation](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).</span></span>

