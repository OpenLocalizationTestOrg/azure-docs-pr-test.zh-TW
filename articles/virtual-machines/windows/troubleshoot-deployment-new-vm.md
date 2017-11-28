---
title: "在 Azure 中的 Windows VM 部署 aaaTroubleshoot |Microsoft 文件"
description: "針對在 Azure 中建立新 Windows 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="669ef-103">針對在 Azure 中建立新 Windows VM 時的部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="669ef-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="669ef-104">常見問題</span><span class="sxs-lookup"><span data-stu-id="669ef-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="669ef-105">如需了解其他 VM 部署問題，請參閱[針對 Azure 中的 Windows 虛擬機器部署問題進行疑難排解](troubleshoot-deploy-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="669ef-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="669ef-106">收集活動記錄</span><span class="sxs-lookup"><span data-stu-id="669ef-106">Collect activity logs</span></span>
<span data-ttu-id="669ef-107">疑難排解，toostart 收集 hello 活動與 hello 問題相關聯的 tooidentify hello 錯誤的記錄。</span><span class="sxs-lookup"><span data-stu-id="669ef-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="669ef-108">hello 下列連結包含 hello 程序 toofollow 的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="669ef-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="669ef-109">檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="669ef-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="669ef-110">檢視活動記錄檔 toomanage Azure 資源</span><span class="sxs-lookup"><span data-stu-id="669ef-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="669ef-111">**Y:**如果 hello 作業系統是 Windows 一般化，而且它是上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="669ef-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="669ef-112">同樣地，如果 hello 作業系統是 Windows 的特製化，和它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="669ef-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="669ef-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="669ef-113">**Upload Errors:**</span></span>

<span data-ttu-id="669ef-114">**N<sup>1</sup>:**如果 hello 作業系統是 Windows 一般化，而且會當做上傳的特製化，就會以 VM 停駐在 hello OOBE 螢幕 hello 佈建的逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="669ef-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="669ef-115">**N<sup>2</sup>:**如果 hello 作業系統是 Windows 的特製化，和上傳為一般化，就會以 hello VM 停駐在 hello OOBE 畫面，因為 hello 新的 VM 正在執行與 hello 原始電腦的佈建失敗錯誤名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="669ef-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="669ef-116">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="669ef-116">**Resolution**</span></span>

<span data-ttu-id="669ef-117">tooresolve 這兩個這些錯誤，使用[新增 AzureRmVhd tooupload hello 原始 VHD](https://msdn.microsoft.com/library/mt603554.aspx)，可以使用內部部署，以 hello 相同的設定值，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="669ef-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="669ef-118">tooupload 為一般化，請記住 toorun sysprep 第一次。</span><span class="sxs-lookup"><span data-stu-id="669ef-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="669ef-119">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="669ef-119">**Capture Errors:**</span></span>

<span data-ttu-id="669ef-120">**N<sup>3</sup>:**如果 hello 作業系統是 Windows 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。</span><span class="sxs-lookup"><span data-stu-id="669ef-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="669ef-121">**N<sup>4</sup>:**如果 hello 作業系統是 Windows 的特製化，和擷取為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行與 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="669ef-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="669ef-122">此外，hello 原始 VM 並未使用因為它已標示為特製化。</span><span class="sxs-lookup"><span data-stu-id="669ef-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="669ef-123">**解決方案**</span><span class="sxs-lookup"><span data-stu-id="669ef-123">**Resolution**</span></span>

<span data-ttu-id="669ef-124">tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="669ef-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="669ef-125">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="669ef-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="669ef-126">Hello 新 VM 要求時無法支援所要求的 hello VM 大小或沒有可用的空間 tooaccommodate hello 要求已釘選的 tooa 叢集的情況下發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="669ef-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="669ef-127">**原因 1:** hello 叢集無法支援 hello 要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="669ef-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="669ef-128">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="669ef-128">**Resolution 1:**</span></span>

* <span data-ttu-id="669ef-129">重試 hello 要求使用較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="669ef-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="669ef-130">如果 hello hello 的大小會要求無法變更 VM:</span><span class="sxs-lookup"><span data-stu-id="669ef-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="669ef-131">停止 hello 可用性設定組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="669ef-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="669ef-132">按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。</span><span class="sxs-lookup"><span data-stu-id="669ef-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="669ef-133">所有 hello Vm 停止之後，建立 hello hello 中新的 VM 所需的大小。</span><span class="sxs-lookup"><span data-stu-id="669ef-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="669ef-134">啟動第一次，hello 新的 VM，然後選取每個 hello 停止 Vm，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="669ef-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="669ef-135">**原因 2:** hello 叢集沒有釋出資源。</span><span class="sxs-lookup"><span data-stu-id="669ef-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="669ef-136">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="669ef-136">**Resolution 2:**</span></span>

* <span data-ttu-id="669ef-137">稍後，重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="669ef-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="669ef-138">如果 hello 新的 VM 可以屬於不同的可用性設定嗎</span><span class="sxs-lookup"><span data-stu-id="669ef-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="669ef-139">在不同的可用性設定組中建立新的 VM (hello 中相同的區域)。</span><span class="sxs-lookup"><span data-stu-id="669ef-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="669ef-140">加入新 VM toohello hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="669ef-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="669ef-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="669ef-141">Next steps</span></span>
<span data-ttu-id="669ef-142">如果您在啟動已停止的 Windows VM，或重新調整 Azure 中現有 Windows VM 的大小時遇到問題，請參閱 [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure (針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器的 Resource Manager 部署問題進行疑難排解)](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="669ef-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

