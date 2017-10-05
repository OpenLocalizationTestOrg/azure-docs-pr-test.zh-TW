---
title: "針對 Linux VM 部署-RM 進行疑難排解 | Microsoft Docs"
description: "針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: aea5db05843b0175b8ef8b713944e12262e33010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="69e5a-103">針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="69e5a-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="69e5a-104">常見問題</span><span class="sxs-lookup"><span data-stu-id="69e5a-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="69e5a-105">如需了解其他 VM 部署問題，請參閱[針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解](troubleshoot-deploy-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="69e5a-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="69e5a-106">收集活動記錄</span><span class="sxs-lookup"><span data-stu-id="69e5a-106">Collect activity logs</span></span>
<span data-ttu-id="69e5a-107">若要開始進行排解疑難，請收集活動記錄，以識別與問題相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="69e5a-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="69e5a-108">下列連結提供此程序該遵循的更多詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="69e5a-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="69e5a-109">檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="69e5a-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="69e5a-110">檢視活動記錄以管理 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="69e5a-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="69e5a-111">**Y：** 如果作業系統是一般化的 Linux，且上傳和 (或) 擷取它時使用的是一般化設定，就不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="69e5a-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="69e5a-112">同樣地，如果作業系統是特殊化的 Linux，且上傳和 (或) 擷取它時使用的是特殊化設定，就不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="69e5a-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="69e5a-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-113">**Upload Errors:**</span></span>

<span data-ttu-id="69e5a-114">**N<sup>1</sup>：**如果作業系統是一般化的 Linux，但是上傳它時是以特殊化形式上傳，就會發生佈建逾時錯誤，因為 VM 會卡在佈建階段。</span><span class="sxs-lookup"><span data-stu-id="69e5a-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="69e5a-115">**N<sup>2</sup>：**如果作業系統是特殊化的 Linux，但是上傳它時是以一般化形式上傳，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。</span><span class="sxs-lookup"><span data-stu-id="69e5a-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="69e5a-116">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-116">**Resolution:**</span></span>

<span data-ttu-id="69e5a-117">若要解決這兩個錯誤，請使用與作業系統相同的設定 (一般化/特殊化) 來上傳原始 VHD (可從內部部署環境取得)。</span><span class="sxs-lookup"><span data-stu-id="69e5a-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="69e5a-118">若要以一般化形式上傳，請務必先執行 -deprovision。</span><span class="sxs-lookup"><span data-stu-id="69e5a-118">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="69e5a-119">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-119">**Capture Errors:**</span></span>

<span data-ttu-id="69e5a-120">**N<sup>3</sup>：**如果作業系統是一般化的 Linux，但是擷取它時是以特殊化形式擷取，就會發生佈建逾時錯誤，因為原始 VM 會因被標示為一般化而無法供使用。</span><span class="sxs-lookup"><span data-stu-id="69e5a-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="69e5a-121">**N<sup>4</sup>：**如果作業系統是特殊化的 Linux，但是擷取它時是以一般化形式擷取，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。</span><span class="sxs-lookup"><span data-stu-id="69e5a-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="69e5a-122">此外，原始 VM 會因被標示為特殊化而無法供使用。</span><span class="sxs-lookup"><span data-stu-id="69e5a-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="69e5a-123">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-123">**Resolution:**</span></span>

<span data-ttu-id="69e5a-124">若要解決這兩個錯誤，請從入口網站中刪除目前的映像，然後使用與作業系統相同的設定 (一般化/特殊化) [從目前的 VHD 重新擷取映像](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="69e5a-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="69e5a-125">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="69e5a-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="69e5a-126">當新的 VM 要求被釘選到不支援所要求的 VM 大小、或沒有可用空間可處理要求的叢集，便會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="69e5a-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="69e5a-127">**原因 1：** 叢集無法支援要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="69e5a-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="69e5a-128">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-128">**Resolution 1:**</span></span>

* <span data-ttu-id="69e5a-129">以較小的 VM 大小重試要求。</span><span class="sxs-lookup"><span data-stu-id="69e5a-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="69e5a-130">如果無法變更要求的 VM 的大小︰</span><span class="sxs-lookup"><span data-stu-id="69e5a-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="69e5a-131">停止可用性設定組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="69e5a-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="69e5a-132">按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。</span><span class="sxs-lookup"><span data-stu-id="69e5a-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="69e5a-133">所有 VM 都停止後，建立所需大小的新 VM。</span><span class="sxs-lookup"><span data-stu-id="69e5a-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="69e5a-134">先啟動新 VM，然後選取每個已停止的 VM 並按一下 [啟動] 。</span><span class="sxs-lookup"><span data-stu-id="69e5a-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="69e5a-135">**原因 2：** 叢集沒有可用的資源。</span><span class="sxs-lookup"><span data-stu-id="69e5a-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="69e5a-136">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="69e5a-136">**Resolution 2:**</span></span>

* <span data-ttu-id="69e5a-137">稍後再重試要求。</span><span class="sxs-lookup"><span data-stu-id="69e5a-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="69e5a-138">如果新的 VM 可以屬於不同的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="69e5a-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="69e5a-139">在不同的可用性設定組 (位於相同區域) 中建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="69e5a-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="69e5a-140">將新的 VM 加入相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="69e5a-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69e5a-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69e5a-141">Next steps</span></span>
<span data-ttu-id="69e5a-142">如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有的 Linux VM 大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的 Resource Manager 部署問題進行疑難排解](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="69e5a-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

