---
title: "aaaTroubleshoot Windows VM 部署傳統 |Microsoft 文件"
description: "針對在 Azure 中建立新 Windows 虛擬機器的傳統部署問題進行疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cjiang
ms.openlocfilehash: aa12cb013a18e0572fbef8b7ea69106dd47c1fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a><span data-ttu-id="632ab-103">針對在 Azure 中建立新 Windows 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="632ab-103">Troubleshoot classic deployment issues with creating a new Windows virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> <span data-ttu-id="632ab-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="632ab-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="632ab-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="632ab-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="632ab-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="632ab-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="632ab-107">如需這篇文章 hello 資源管理員版本，請參閱[這裡](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="632ab-107">For hello Resource Manager version of this article, see [here](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="632ab-108">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="632ab-108">Collect audit logs</span></span>
<span data-ttu-id="632ab-109">troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-109">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="632ab-110">在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Windows 虛擬機器* >  **設定** > **稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="632ab-110">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="632ab-111">**Y:**如果 hello 作業系統是 Windows 一般化，而且它是上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="632ab-112">同樣地，如果 hello 作業系統是 Windows 的特製化，和它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="632ab-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="632ab-113">**Upload Errors:**</span></span>

<span data-ttu-id="632ab-114">**N<sup>1</sup>:**如果 hello 作業系統是 Windows 一般化，而且會當做上傳的特製化，就會以 VM 停駐在 hello OOBE 螢幕 hello 佈建的逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="632ab-115">**N<sup>2</sup>:**如果 hello 作業系統是 Windows 的特製化，和上傳為一般化，就會以 hello VM 停駐在 hello OOBE 畫面，因為 hello 新的 VM 正在執行與 hello 原始電腦的佈建失敗錯誤名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="632ab-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="632ab-116">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="632ab-116">**Resolution:**</span></span>

<span data-ttu-id="632ab-117">tooresolve 這兩個這些錯誤上, 傳 hello 原始 VHD，內部使用，與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="632ab-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="632ab-118">tooupload 為一般化，請記住 toorun sysprep 第一次。</span><span class="sxs-lookup"><span data-stu-id="632ab-118">tooupload as generalized, remember toorun sysprep first.</span></span> <span data-ttu-id="632ab-119">請參閱[建立並上傳 Windows Server VHD tooAzure](createupload-vhd.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="632ab-119">See [Create and upload a Windows Server VHD tooAzure](createupload-vhd.md) for more information.</span></span>

<span data-ttu-id="632ab-120">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="632ab-120">**Capture Errors:**</span></span>

<span data-ttu-id="632ab-121">**N<sup>3</sup>:**如果 hello 作業系統是 Windows 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。</span><span class="sxs-lookup"><span data-stu-id="632ab-121">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="632ab-122">**N<sup>4</sup>:**如果 hello 作業系統是 Windows 的特製化，和擷取為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="632ab-122">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="632ab-123">此外，hello 原始 VM 並未使用因為它已標示為特製化。</span><span class="sxs-lookup"><span data-stu-id="632ab-123">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="632ab-124">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="632ab-124">**Resolution:**</span></span>

<span data-ttu-id="632ab-125">tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](capture-image.md)與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="632ab-125">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="632ab-126">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="632ab-126">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="632ab-127">會發生這個錯誤情況時傳送 hello 新的 VM 要求 tooa 叢集可能沒有可用的空間 tooaccommodate hello 要求，或無法支援所要求的 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="632ab-127">This error arises in situations when hello new VM request is sent tooa cluster that either does not have available free space tooaccommodate hello request, or cannot support hello VM size being requested.</span></span> <span data-ttu-id="632ab-128">不可能 toomix 不同序列 hello 中 Vm 的相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="632ab-128">It is not possible toomix different series of VMs in hello same cloud service.</span></span> <span data-ttu-id="632ab-129">因此如果您想 toocreate 比您的雲端服務可支援不同大小的新的 VM，hello 計算要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="632ab-129">So if you want toocreate a new VM of a different size than what your cloud service can support, hello compute request will fail.</span></span>

<span data-ttu-id="632ab-130">您可以根據 hello hello 雲端服務的條件約束使用 toocreate hello 新的 VM，您可能會遇到的其中兩個情況造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-130">Depending on hello constraints of hello cloud service you use toocreate hello new VM, you might encounter an error caused by one of two situations.</span></span>

<span data-ttu-id="632ab-131">**原因 1:** hello 雲端服務是已釘選的 tooa 特定叢集，或者它是連結的 tooan 同質群組，並因此釘選的 tooa 特定群集的設計。</span><span class="sxs-lookup"><span data-stu-id="632ab-131">**Cause 1:** hello cloud service is pinned tooa specific cluster, or it is linked tooan affinity group, and hence pinned tooa specific cluster by design.</span></span> <span data-ttu-id="632ab-132">因此在該同質群組中，要求新的計算資源會嘗試在 hello 相同叢集 hello 現有資源的裝載位置。</span><span class="sxs-lookup"><span data-stu-id="632ab-132">So new compute resource requests in that affinity group are tried in hello same cluster where hello existing resources are hosted.</span></span> <span data-ttu-id="632ab-133">不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-133">However, hello same cluster may either not support hello requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="632ab-134">透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。</span><span class="sxs-lookup"><span data-stu-id="632ab-134">This is true whether hello new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="632ab-135">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="632ab-135">**Resolution 1:**</span></span>

* <span data-ttu-id="632ab-136">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="632ab-136">Create a new cloud service and associate it with either a region or a region-based virtual network.</span></span>
* <span data-ttu-id="632ab-137">Hello 新的雲端服務中建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="632ab-137">Create a new VM in hello new cloud service.</span></span>
  <span data-ttu-id="632ab-138">如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，稍後再試一次，或變更 hello 雲端服務的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="632ab-138">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="632ab-139">如果您嘗試 toocreate 中現有的雲端服務的新 VM，但無法，而且產生 toocreate 新的雲端服務，新的 vm，您可以選擇 tooconsolidate 您所有的 Vm 中 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="632ab-139">If you were trying toocreate a new VM in an existing cloud service but couldn’t, and had toocreate a new cloud service for your new VM, you can choose tooconsolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="632ab-140">因此 toodo 刪除 hello 現有雲端服務中的 hello Vm，然後重新加以擷取其 hello 新的雲端服務中的磁碟。</span><span class="sxs-lookup"><span data-stu-id="632ab-140">toodo so, delete hello VMs in hello existing cloud service, and recapture them from their disks in hello new cloud service.</span></span> <span data-ttu-id="632ab-141">不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="632ab-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>
> 
> 

<span data-ttu-id="632ab-142">**原因 2:** hello 雲端服務可以是連結的 tooan 同質群組，所以它是已釘選的 tooa 所設計的特定叢集的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="632ab-142">**Cause 2:** hello cloud service is associated with a virtual network that is linked tooan affinity group, so it is pinned tooa specific cluster by design.</span></span> <span data-ttu-id="632ab-143">相同叢集 hello 現有資源的裝載位置的 hello 因此會嘗試在該同質群組中的所有新計算資源要求。</span><span class="sxs-lookup"><span data-stu-id="632ab-143">All new compute resource requests in that affinity group are therefore tried in hello same cluster where hello existing resources are hosted.</span></span> <span data-ttu-id="632ab-144">不過，hello 相同叢集可能不支援 hello 要求的 VM 大小，或有可用空間不足，造成配置錯誤。</span><span class="sxs-lookup"><span data-stu-id="632ab-144">However, hello same cluster may either not support hello requested VM size or have insufficient available space, resulting in an allocation error.</span></span> <span data-ttu-id="632ab-145">透過新的雲端服務或透過現有的雲端服務的 hello 新資源建立是否為 true。</span><span class="sxs-lookup"><span data-stu-id="632ab-145">This is true whether hello new resources are created through a new cloud service or through an existing cloud service.</span></span>

<span data-ttu-id="632ab-146">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="632ab-146">**Resolution 2:**</span></span>

* <span data-ttu-id="632ab-147">建立新的區域虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="632ab-147">Create a new regional virtual network.</span></span>
* <span data-ttu-id="632ab-148">建立 hello hello 新的虛擬網路中的新 VM。</span><span class="sxs-lookup"><span data-stu-id="632ab-148">Create hello new VM in hello new virtual network.</span></span>
* <span data-ttu-id="632ab-149">[您現有的虛擬網路連線](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/)toohello 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="632ab-149">[Connect your existing virtual network](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello new virtual network.</span></span> <span data-ttu-id="632ab-150">深入了解 [區域虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)。</span><span class="sxs-lookup"><span data-stu-id="632ab-150">See more about [regional virtual networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).</span></span> <span data-ttu-id="632ab-151">或者，您可以[將同質群組為基礎的虛擬網路 tooa 地區虛擬網路移轉](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)，然後再建立 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="632ab-151">Alternatively, you can [migrate your affinity-group-based virtual network tooa regional virtual network](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), and then create hello new VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="632ab-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="632ab-152">Next steps</span></span>
<span data-ttu-id="632ab-153">如果您在啟動已停止的 Windows VM，或重新調整 Azure 中現有的 Windows VM 大小時遇到問題，請參閱 [Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure (針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解)](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="632ab-153">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).</span></span>

