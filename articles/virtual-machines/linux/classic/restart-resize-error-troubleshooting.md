---
title: "VM 重新啟動或調整大小的問題 | Microsoft 文件"
description: "針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="0056f-103">針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0056f-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0056f-104">傳統</span><span class="sxs-lookup"><span data-stu-id="0056f-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="0056f-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="0056f-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="0056f-106">當您嘗試啟動已停止的 Azure 虛擬機器 (VM)，或調整現有 Azure VM 的大小時，常會遇到的錯誤是配置失敗。</span><span class="sxs-lookup"><span data-stu-id="0056f-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="0056f-107">當叢集或區域沒有可用的資源或無法支援所要求的 VM 大小，就會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0056f-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0056f-108">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0056f-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0056f-109">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0056f-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0056f-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="0056f-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0056f-111">如需 Resource Manager 版本，請參閱[這裡](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0056f-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="0056f-112">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="0056f-112">Collect audit logs</span></span>
<span data-ttu-id="0056f-113">若要開始進行排解疑難，請收集稽核記錄，識別與問題相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0056f-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="0056f-114">在 Azure 入口網站中，依序按一下 [瀏覽] > [虛擬機器] > 您的 Linux 虛擬機器 > [設定] > [稽核記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="0056f-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="0056f-115">問題：啟動已停止的 VM 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="0056f-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="0056f-116">您嘗試啟動已停止的 VM，但是發現配置失敗。</span><span class="sxs-lookup"><span data-stu-id="0056f-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="0056f-117">原因</span><span class="sxs-lookup"><span data-stu-id="0056f-117">Cause</span></span>
<span data-ttu-id="0056f-118">必須在架設雲端服務的原始叢集上嘗試提出啟動已停止的 VM 要求。</span><span class="sxs-lookup"><span data-stu-id="0056f-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="0056f-119">不過，叢集沒有足夠空間可完成要求。</span><span class="sxs-lookup"><span data-stu-id="0056f-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="0056f-120">解決方案</span><span class="sxs-lookup"><span data-stu-id="0056f-120">Resolution</span></span>
* <span data-ttu-id="0056f-121">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯，但不是和同質群組。</span><span class="sxs-lookup"><span data-stu-id="0056f-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="0056f-122">刪除已停止的 VM。</span><span class="sxs-lookup"><span data-stu-id="0056f-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="0056f-123">使用磁碟在新的雲端服務中重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="0056f-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="0056f-124">啟動重新建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="0056f-124">Start the re-created VM.</span></span>

<span data-ttu-id="0056f-125">如果您在嘗試建立新的雲端服務時收到錯誤，請稍後再試一次，或變更雲端服務的區域。</span><span class="sxs-lookup"><span data-stu-id="0056f-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0056f-126">新的雲端服務將會有新的名稱和 VIP，因此您需要為所有將資訊用於現有雲端服務的相依性變更該資訊。</span><span class="sxs-lookup"><span data-stu-id="0056f-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="0056f-127">問題：調整現有 VM 的大小時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="0056f-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="0056f-128">您嘗試調整現有 VM 的大小，但是發現配置失敗。</span><span class="sxs-lookup"><span data-stu-id="0056f-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="0056f-129">原因</span><span class="sxs-lookup"><span data-stu-id="0056f-129">Cause</span></span>
<span data-ttu-id="0056f-130">必須在架設雲端服務的原始叢集上嘗試提出調整 VM 大小的要求。</span><span class="sxs-lookup"><span data-stu-id="0056f-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="0056f-131">不過，叢集不支援要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="0056f-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="0056f-132">解決方案</span><span class="sxs-lookup"><span data-stu-id="0056f-132">Resolution</span></span>
<span data-ttu-id="0056f-133">減少要求的 VM 大小，並再試一次調整大小要求。</span><span class="sxs-lookup"><span data-stu-id="0056f-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="0056f-134">按一下 [全部瀏覽]  >  [虛擬機器 (傳統)]  >  *您的虛擬機器*  >  [設定]  >  [大小]。</span><span class="sxs-lookup"><span data-stu-id="0056f-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="0056f-135">如需詳細步驟，請參閱 [調整虛擬機器的大小](https://msdn.microsoft.com/library/dn168976.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0056f-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="0056f-136">如果您無法減少 VM 大小，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="0056f-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="0056f-137">建立新的雲端服務，確保不會連結至同質群組，以及未與連結至同質群組的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="0056f-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="0056f-138">在其中建立新的、較大的 VM。</span><span class="sxs-lookup"><span data-stu-id="0056f-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="0056f-139">您可以在相同的雲端服務中合併所有 VM。</span><span class="sxs-lookup"><span data-stu-id="0056f-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="0056f-140">如果現有的雲端服務和以區域為基礎的虛擬網路相關聯，您可以將新的雲端服務連接到現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0056f-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="0056f-141">如果現有的雲端服務未和以區域為基礎的虛擬網路相關聯，您必須刪除現有雲端服務中的 VM，並從其磁碟在新的雲端服務中將其重新建立。</span><span class="sxs-lookup"><span data-stu-id="0056f-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="0056f-142">然而，請務必記得新的雲端服務將會有新的名稱和 VIP，因此您需要為所有目前將此資訊用於現有雲端服務的相依性更新該資訊。</span><span class="sxs-lookup"><span data-stu-id="0056f-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0056f-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0056f-143">Next steps</span></span>
<span data-ttu-id="0056f-144">如果您在 Azure 中建立新的 Linux VM 時遇到問題，請參閱[針對在 Azure 中建立新 Linux 虛擬機器的部署問題進行疑難排解](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0056f-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

