---
title: "aaaTroubleshoot Linux VM 部署傳統 |Microsoft 文件"
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
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="c9f9c-103">針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c9f9c-103">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> <span data-ttu-id="c9f9c-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c9f9c-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c9f9c-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c9f9c-107">如需這篇文章 hello 資源管理員版本，請參閱[這裡](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-107">For hello Resource Manager version of this article, see [here](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="c9f9c-108">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="c9f9c-108">Collect audit logs</span></span>
<span data-ttu-id="c9f9c-109">troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-109">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="c9f9c-110">在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Windows 虛擬機器* >  **設定** > **稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-110">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="c9f9c-111">**Y:**如果 hello 作業系統一般化，Linux 和它已上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="c9f9c-112">同樣地，如果 hello OS Linux 特製化，且它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="c9f9c-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-113">**Upload Errors:**</span></span>

<span data-ttu-id="c9f9c-114">**N<sup>1</sup>:**如果 hello OS Linux 一般化，而且會當做上傳的特製化，就會發生佈建的逾時錯誤因為 hello VM 停駐在 hello 佈建階段。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="c9f9c-115">**N<sup>2</sup>:**如果 hello OS Linux 特製化，和上傳為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="c9f9c-116">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-116">**Resolution:**</span></span>

<span data-ttu-id="c9f9c-117">tooresolve 這兩個這些錯誤上, 傳 hello 原始 VHD，內部使用，與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="c9f9c-118">tooupload 為一般化，請記住 toorun-取消佈建第一次。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-118">tooupload as generalized, remember toorun -deprovision first.</span></span> <span data-ttu-id="c9f9c-119">請參閱[建立及上傳虛擬硬碟的 Contains hello Linux Operating System](create-upload-vhd.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-119">See [Create and Upload a Virtual Hard Disk that Contains hello Linux Operating System](create-upload-vhd.md) for more information.</span></span>

<span data-ttu-id="c9f9c-120">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-120">**Capture Errors:**</span></span>

<span data-ttu-id="c9f9c-121">**N<sup>3</sup>:**如果 hello OS Linux 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-121">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="c9f9c-122">**N<sup>4</sup>:**是否 hello OS Linux 特製化，然後為一般化擷取，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-122">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="c9f9c-123">此外，hello 原始 VM 並未使用因為它已標示為特製化。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-123">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="c9f9c-124">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-124">**Resolution:**</span></span>

<span data-ttu-id="c9f9c-125">tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](capture-image.md)與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-125">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="c9f9c-126">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="c9f9c-126">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="c9f9c-127">會發生這個錯誤情況時傳送 hello 新的 VM 要求 tooa 叢集可能沒有可用的空間 tooaccommodate hello 要求，或無法支援所要求的 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-127">This error arises in situations when hello new VM request is sent tooa cluster that either does not have available free space tooaccommodate hello request, or cannot support hello VM size being requested.</span></span> <span data-ttu-id="c9f9c-128">不可能 toomix 不同序列 hello 中 Vm 的相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-128">It is not possible toomix different series of VMs in hello same cloud service.</span></span> <span data-ttu-id="c9f9c-129">因此如果您想 toocreate 比您的雲端服務可支援不同大小的新的 VM，hello 計算要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-129">So if you want toocreate a new VM of a different size than what your cloud service can support, hello compute request will fail.</span></span>

<span data-ttu-id="c9f9c-130">您可以根據 hello hello 雲端服務的條件約束使用 toocreate hello 新的 VM，您可能會遇到的其中兩個情況造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-130">Depending on hello constraints of hello cloud service you use toocreate hello new VM, you might encounter an error caused by one of two situations.</span></span>

<span data-ttu-id="c9f9c-131">**原因 1:** hello 雲端服務是已釘選的 tooa 特定叢集，或者它是連結的 tooan 同質群組，並因此釘選的 tooa 特定群集的設計。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-131">**Cause 1:** hello cloud service is pinned tooa specific cluster, or it is linked tooan affinity group, and hence pinned tooa specific cluster by design.</span></span> <span data-ttu-id="c9f9c-132">因此在該同質群組中，要求新的計算資源會嘗試在 hello 相同叢集 hello 現有資源的裝載位置。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-132">So new compute resource requests in that affinity group are tried in hello same cluster where hello existing resources are hosted.</span></span> <span data-ttu-id="c9f9c-133">不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-133">However, hello same cluster may either not support hello requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="c9f9c-134">透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-134">This is true whether hello new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="c9f9c-135">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-135">**Resolution 1:**</span></span>

* <span data-ttu-id="c9f9c-136">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-136">Create a new cloud service and associate it with either a region or a region-based virtual network.</span></span>
* <span data-ttu-id="c9f9c-137">Hello 新的雲端服務中建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-137">Create a new VM in hello new cloud service.</span></span>
  <span data-ttu-id="c9f9c-138">如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，稍後再試一次，或變更 hello 雲端服務的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-138">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9f9c-139">如果您嘗試 toocreate 中現有的雲端服務的新 VM，但無法，而且產生 toocreate 新的雲端服務，新的 vm，您可以選擇 tooconsolidate 您所有的 Vm 中 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-139">If you were trying toocreate a new VM in an existing cloud service but couldn’t, and had toocreate a new cloud service for your new VM, you can choose tooconsolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="c9f9c-140">因此 toodo 刪除 hello 現有雲端服務中的 hello Vm，然後重新加以擷取其 hello 新的雲端服務中的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-140">toodo so, delete hello VMs in hello existing cloud service, and recapture them from their disks in hello new cloud service.</span></span> <span data-ttu-id="c9f9c-141">不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>
> 
> 

<span data-ttu-id="c9f9c-142">**原因 2:** hello 雲端服務可以是連結的 tooan 同質群組，所以它是已釘選的 tooa 所設計的特定叢集的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-142">**Cause 2:** hello cloud service is associated with a virtual network that is linked tooan affinity group, so it is pinned tooa specific cluster by design.</span></span> <span data-ttu-id="c9f9c-143">相同叢集 hello 現有資源的裝載位置的 hello 因此會嘗試在該同質群組中的所有新計算資源要求。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-143">All new compute resource requests in that affinity group are therefore tried in hello same cluster where hello existing resources are hosted.</span></span> <span data-ttu-id="c9f9c-144">不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-144">However, hello same cluster may either not support hello requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="c9f9c-145">透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-145">This is true whether hello new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="c9f9c-146">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="c9f9c-146">**Resolution 2:**</span></span>

* <span data-ttu-id="c9f9c-147">建立新的區域虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-147">Create a new regional virtual network.</span></span>
* <span data-ttu-id="c9f9c-148">建立 hello hello 新的虛擬網路中的新 VM。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-148">Create hello new VM in hello new virtual network.</span></span>
* <span data-ttu-id="c9f9c-149">[您現有的虛擬網路連線](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)toohello 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-149">[Connect your existing virtual network](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello new virtual network.</span></span> <span data-ttu-id="c9f9c-150">深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-150">See more about [regional virtual networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).</span></span> <span data-ttu-id="c9f9c-151">或者，您可以[將同質群組為基礎的虛擬網路 tooa 地區虛擬網路移轉](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)，然後再建立 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-151">Alternatively, you can [migrate your affinity-group-based virtual network tooa regional virtual network](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), and then create hello new VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9f9c-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9f9c-152">Next steps</span></span>
<span data-ttu-id="c9f9c-153">如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有 Linux VM 的大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解](restart-resize-error-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="c9f9c-153">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md).</span></span>

