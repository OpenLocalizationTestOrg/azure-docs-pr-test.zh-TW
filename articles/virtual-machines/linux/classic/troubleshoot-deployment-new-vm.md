---
title: "針對 Linux VM 部署-傳統進行疑難排解 | Microsoft Docs"
description: "針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: 35b8ae033425e16fb53cc3127f300e1fb919a2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="45d19-103">針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="45d19-103">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> <span data-ttu-id="45d19-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="45d19-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="45d19-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="45d19-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="45d19-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="45d19-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="45d19-107">如需本文的 Resource Manager 版本，請參閱[這裡](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="45d19-107">For the Resource Manager version of this article, see [here](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="45d19-108">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="45d19-108">Collect audit logs</span></span>
<span data-ttu-id="45d19-109">若要開始進行排解疑難，請收集稽核記錄，識別與問題相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-109">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="45d19-110">在 Azure 入口網站中，依序按一下 [瀏覽] > [虛擬機器] > 您的 Windows 虛擬機器 > [設定] > [稽核記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="45d19-110">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="45d19-111">**Y：** 如果作業系統是一般化的 Linux，且上傳和 (或) 擷取它時使用的是一般化設定，就不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="45d19-112">同樣地，如果作業系統是特殊化的 Linux，且上傳和 (或) 擷取它時使用的是特殊化設定，就不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="45d19-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="45d19-113">**Upload Errors:**</span></span>

<span data-ttu-id="45d19-114">**N<sup>1</sup>：**如果作業系統是一般化的 Linux，但是上傳它時是以特殊化形式上傳，就會發生佈建逾時錯誤，因為 VM 會卡在佈建階段。</span><span class="sxs-lookup"><span data-stu-id="45d19-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="45d19-115">**N<sup>2</sup>：**如果作業系統是特殊化的 Linux，但是上傳它時是以一般化形式上傳，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。</span><span class="sxs-lookup"><span data-stu-id="45d19-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="45d19-116">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="45d19-116">**Resolution:**</span></span>

<span data-ttu-id="45d19-117">若要解決這兩個錯誤，請使用與作業系統相同的設定 (一般化/特殊化) 來上傳原始 VHD (可從內部部署環境取得)。</span><span class="sxs-lookup"><span data-stu-id="45d19-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="45d19-118">若要以一般化上傳，請務必先執行 -deprovision。</span><span class="sxs-lookup"><span data-stu-id="45d19-118">To upload as generalized, remember to run -deprovision first.</span></span> <span data-ttu-id="45d19-119">如需詳細資訊，請參閱 [建立及上傳包含 Linux 作業系統的虛擬硬碟](create-upload-vhd.md) 。</span><span class="sxs-lookup"><span data-stu-id="45d19-119">See [Create and Upload a Virtual Hard Disk that Contains the Linux Operating System](create-upload-vhd.md) for more information.</span></span>

<span data-ttu-id="45d19-120">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="45d19-120">**Capture Errors:**</span></span>

<span data-ttu-id="45d19-121">**N<sup>3</sup>：**如果作業系統是一般化的 Linux，但是擷取它時是以特殊化形式擷取，就會發生佈建逾時錯誤，因為原始 VM 會因被標示為一般化而無法供使用。</span><span class="sxs-lookup"><span data-stu-id="45d19-121">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="45d19-122">**N<sup>4</sup>：**如果作業系統是特殊化的 Linux，但是擷取它時是以一般化形式擷取，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。</span><span class="sxs-lookup"><span data-stu-id="45d19-122">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="45d19-123">此外，原始 VM 會因被標示為特殊化而無法供使用。</span><span class="sxs-lookup"><span data-stu-id="45d19-123">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="45d19-124">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="45d19-124">**Resolution:**</span></span>

<span data-ttu-id="45d19-125">若要解決這兩個錯誤，請從入口網站中刪除目前的映像，然後使用與作業系統相同的設定 (一般化/特殊化) [從目前的 VHD 重新擷取映像](capture-image.md) 。</span><span class="sxs-lookup"><span data-stu-id="45d19-125">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="45d19-126">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="45d19-126">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="45d19-127">當新的 VM 要求被傳送到沒有可用空間可處理要求、或不支援所要求的 VM 大小的叢集，便會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-127">This error arises in situations when the new VM request is sent to a cluster that either does not have available free space to accommodate the request, or cannot support the VM size being requested.</span></span> <span data-ttu-id="45d19-128">在相同的雲端服務中不可混合不同系列的 VM。</span><span class="sxs-lookup"><span data-stu-id="45d19-128">It is not possible to mix different series of VMs in the same cloud service.</span></span> <span data-ttu-id="45d19-129">因此，如果您想要建立和您的雲端服務可支援大小不同的新 VM，計算要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="45d19-129">So if you want to create a new VM of a different size than what your cloud service can support, the compute request will fail.</span></span>

<span data-ttu-id="45d19-130">您可能會遇到因兩種情況造成的錯誤，取決於您用於建立新 VM 的雲端服務的條件約束。</span><span class="sxs-lookup"><span data-stu-id="45d19-130">Depending on the constraints of the cloud service you use to create the new VM, you might encounter an error caused by one of two situations.</span></span>

<span data-ttu-id="45d19-131">**原因 1：** 雲端服務已釘選到特定叢集，或是連結到同質群組，因而釘選到所設計的特定叢集。</span><span class="sxs-lookup"><span data-stu-id="45d19-131">**Cause 1:** The cloud service is pinned to a specific cluster, or it is linked to an affinity group, and hence pinned to a specific cluster by design.</span></span> <span data-ttu-id="45d19-132">因此，系統會在裝載現有資源的相同叢集中，嘗試執行該同質群組中的新計算資源要求。</span><span class="sxs-lookup"><span data-stu-id="45d19-132">So new compute resource requests in that affinity group are tried in the same cluster where the existing resources are hosted.</span></span> <span data-ttu-id="45d19-133">不過，同一叢集可能不支援要求的 VM 大小，或者可用空間不足，導致配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-133">However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="45d19-134">無論新的資源是透過新的雲端服務，或是透過現有的雲端服務來建立，都是如此。</span><span class="sxs-lookup"><span data-stu-id="45d19-134">This is true whether the new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="45d19-135">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="45d19-135">**Resolution 1:**</span></span>

* <span data-ttu-id="45d19-136">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="45d19-136">Create a new cloud service and associate it with either a region or a region-based virtual network.</span></span>
* <span data-ttu-id="45d19-137">在新的雲端服務中建立新 VM。</span><span class="sxs-lookup"><span data-stu-id="45d19-137">Create a new VM in the new cloud service.</span></span>
  <span data-ttu-id="45d19-138">如果您在嘗試建立新的雲端服務時收到錯誤，請稍後再試一次，或變更雲端服務的區域。</span><span class="sxs-lookup"><span data-stu-id="45d19-138">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45d19-139">如果您嘗試在現有的雲端服務中建立新的 VM，但無法建立，而您又必須為新的 VM 建立新的雲端服務，則可以選擇合併相同雲端服務中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="45d19-139">If you were trying to create a new VM in an existing cloud service but couldn’t, and had to create a new cloud service for your new VM, you can choose to consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="45d19-140">若要這樣做，請刪除現有雲端服務中的 VM，然後從它們位於新雲端服務中的磁碟重新擷取它們。</span><span class="sxs-lookup"><span data-stu-id="45d19-140">To do so, delete the VMs in the existing cloud service, and recapture them from their disks in the new cloud service.</span></span> <span data-ttu-id="45d19-141">然而，請務必記得新的雲端服務將會有新的名稱和 VIP，因此您需要為所有目前將此資訊用於現有雲端服務的相依性更新該資訊。</span><span class="sxs-lookup"><span data-stu-id="45d19-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>
> 
> 

<span data-ttu-id="45d19-142">**原因 2：** 雲端服務已經與連結到同質群組的虛擬網路關聯，因而釘選到所設計的特定叢集。</span><span class="sxs-lookup"><span data-stu-id="45d19-142">**Cause 2:** The cloud service is associated with a virtual network that is linked to an affinity group, so it is pinned to a specific cluster by design.</span></span> <span data-ttu-id="45d19-143">因此，系統會在裝載現有資源的相同叢集中，嘗試執行該同質群組中的所有新計算資源要求。</span><span class="sxs-lookup"><span data-stu-id="45d19-143">All new compute resource requests in that affinity group are therefore tried in the same cluster where the existing resources are hosted.</span></span> <span data-ttu-id="45d19-144">不過，同一叢集可能不支援要求的 VM 大小，或者可用空間不足，導致配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="45d19-144">However, the same cluster may either not support the requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="45d19-145">無論新的資源是透過新的雲端服務，或是透過現有的雲端服務來建立，都是如此。</span><span class="sxs-lookup"><span data-stu-id="45d19-145">This is true whether the new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="45d19-146">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="45d19-146">**Resolution 2:**</span></span>

* <span data-ttu-id="45d19-147">建立新的區域虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45d19-147">Create a new regional virtual network.</span></span>
* <span data-ttu-id="45d19-148">在新的虛擬網路中建立新 VM。</span><span class="sxs-lookup"><span data-stu-id="45d19-148">Create the new VM in the new virtual network.</span></span>
* <span data-ttu-id="45d19-149">[連接您現有的虛擬網路](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) 到新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="45d19-149">[Connect your existing virtual network](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) to the new virtual network.</span></span> <span data-ttu-id="45d19-150">深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。</span><span class="sxs-lookup"><span data-stu-id="45d19-150">See more about [regional virtual networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).</span></span> <span data-ttu-id="45d19-151">此外，也可以 [將同質群組式虛擬網路移轉至區域虛擬網路](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)，然後建立新 VM。</span><span class="sxs-lookup"><span data-stu-id="45d19-151">Alternatively, you can [migrate your affinity-group-based virtual network to a regional virtual network](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), and then create the new VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45d19-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45d19-152">Next steps</span></span>
<span data-ttu-id="45d19-153">如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有 Linux VM 的大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解](restart-resize-error-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="45d19-153">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md).</span></span>

