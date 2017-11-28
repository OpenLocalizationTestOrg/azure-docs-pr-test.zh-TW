---
title: "aaaTroubleshoot Linux VM 部署 RM |Microsoft 文件"
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
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="905c2-103">針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="905c2-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="905c2-104">常見問題</span><span class="sxs-lookup"><span data-stu-id="905c2-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="905c2-105">如需了解其他 VM 部署問題，請參閱[針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解](troubleshoot-deploy-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="905c2-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="905c2-106">收集活動記錄</span><span class="sxs-lookup"><span data-stu-id="905c2-106">Collect activity logs</span></span>
<span data-ttu-id="905c2-107">疑難排解，toostart 收集 hello 活動與 hello 問題相關聯的 tooidentify hello 錯誤的記錄。</span><span class="sxs-lookup"><span data-stu-id="905c2-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="905c2-108">hello 下列連結包含 hello 程序 toofollow 的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="905c2-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="905c2-109">檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="905c2-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="905c2-110">檢視活動記錄檔 toomanage Azure 資源</span><span class="sxs-lookup"><span data-stu-id="905c2-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="905c2-111">**Y:**如果 hello 作業系統一般化，Linux 和它已上傳及/或所擷取的 hello 一般化設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="905c2-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="905c2-112">同樣地，如果 hello OS Linux 特製化，且它已上傳及/或所擷取的 hello 特製化的設定，則不會有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="905c2-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="905c2-113">**上傳錯誤：**</span><span class="sxs-lookup"><span data-stu-id="905c2-113">**Upload Errors:**</span></span>

<span data-ttu-id="905c2-114">**N<sup>1</sup>:**如果 hello OS Linux 一般化，而且會當做上傳的特製化，就會發生佈建的逾時錯誤因為 hello VM 停駐在 hello 佈建階段。</span><span class="sxs-lookup"><span data-stu-id="905c2-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="905c2-115">**N<sup>2</sup>:**如果 hello OS Linux 特製化，和上傳為一般化，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="905c2-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="905c2-116">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="905c2-116">**Resolution:**</span></span>

<span data-ttu-id="905c2-117">tooresolve 這兩個這些錯誤上, 傳 hello 原始 VHD，內部使用，與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="905c2-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="905c2-118">tooupload 為一般化，請記住 toorun-取消佈建第一次。</span><span class="sxs-lookup"><span data-stu-id="905c2-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="905c2-119">**擷取錯誤：**</span><span class="sxs-lookup"><span data-stu-id="905c2-119">**Capture Errors:**</span></span>

<span data-ttu-id="905c2-120">**N<sup>3</sup>:**如果 hello OS Linux 一般化，而且都擷取成特製化，就會發生佈建的逾時錯誤因為 hello 原始 VM 就無法使用為它標示為一般化。</span><span class="sxs-lookup"><span data-stu-id="905c2-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="905c2-121">**N<sup>4</sup>:**是否 hello OS Linux 特製化，然後為一般化擷取，就會發生佈建的失敗錯誤，因為 hello 新的 VM 正在執行 hello 原始電腦名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="905c2-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="905c2-122">此外，hello 原始 VM 並未使用因為它已標示為特製化。</span><span class="sxs-lookup"><span data-stu-id="905c2-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="905c2-123">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="905c2-123">**Resolution:**</span></span>

<span data-ttu-id="905c2-124">tooresolve 這兩個這些錯誤，從 hello 入口網站中，刪除 hello 目前映像和[收復 hello 從目前的 Vhd](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)與 hello 相同設定，與 hello OS （一般化/特製化）。</span><span class="sxs-lookup"><span data-stu-id="905c2-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="905c2-125">問題︰自訂/資源庫/Marketplace 映像；配置失敗</span><span class="sxs-lookup"><span data-stu-id="905c2-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="905c2-126">Hello 新 VM 要求時無法支援所要求的 hello VM 大小或沒有可用的空間 tooaccommodate hello 要求已釘選的 tooa 叢集的情況下發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="905c2-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="905c2-127">**原因 1:** hello 叢集無法支援 hello 要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="905c2-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="905c2-128">**解決方式 1：**</span><span class="sxs-lookup"><span data-stu-id="905c2-128">**Resolution 1:**</span></span>

* <span data-ttu-id="905c2-129">重試 hello 要求使用較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="905c2-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="905c2-130">如果 hello hello 的大小會要求無法變更 VM:</span><span class="sxs-lookup"><span data-stu-id="905c2-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="905c2-131">停止 hello 可用性設定組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="905c2-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="905c2-132">按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。</span><span class="sxs-lookup"><span data-stu-id="905c2-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="905c2-133">所有 hello Vm 停止之後，建立 hello hello 中新的 VM 所需的大小。</span><span class="sxs-lookup"><span data-stu-id="905c2-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="905c2-134">啟動第一次，hello 新的 VM，然後選取每個 hello 停止 Vm，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="905c2-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="905c2-135">**原因 2:** hello 叢集沒有釋出資源。</span><span class="sxs-lookup"><span data-stu-id="905c2-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="905c2-136">**解決方式 2：**</span><span class="sxs-lookup"><span data-stu-id="905c2-136">**Resolution 2:**</span></span>

* <span data-ttu-id="905c2-137">稍後，重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="905c2-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="905c2-138">如果 hello 新的 VM 可以屬於不同的可用性設定嗎</span><span class="sxs-lookup"><span data-stu-id="905c2-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="905c2-139">在不同的可用性設定組中建立新的 VM (hello 中相同的區域)。</span><span class="sxs-lookup"><span data-stu-id="905c2-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="905c2-140">加入新 VM toohello hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="905c2-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="905c2-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="905c2-141">Next steps</span></span>
<span data-ttu-id="905c2-142">如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有的 Linux VM 大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的 Resource Manager 部署問題進行疑難排解](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="905c2-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

