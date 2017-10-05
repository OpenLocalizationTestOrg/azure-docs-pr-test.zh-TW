---
title: "VM 重新啟動或調整大小的問題 | Microsoft 文件"
description: "針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 7fe0636366c60d4679cfc69bd96cd532695b080e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="e4981-103">針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e4981-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4981-104">傳統</span><span class="sxs-lookup"><span data-stu-id="e4981-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="e4981-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="e4981-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="e4981-106">當您嘗試啟動已停止的 Azure 虛擬機器 (VM)，或調整現有 Azure VM 的大小時，常會遇到的錯誤是配置失敗。</span><span class="sxs-lookup"><span data-stu-id="e4981-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="e4981-107">當叢集或區域沒有可用的資源或無法支援所要求的 VM 大小，就會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4981-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4981-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="e4981-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="e4981-109">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="e4981-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e4981-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="e4981-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="e4981-111">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="e4981-111">Collect audit logs</span></span>
<span data-ttu-id="e4981-112">若要開始進行排解疑難，請收集稽核記錄，識別與問題相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4981-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="e4981-113">在 Azure 入口網站中，依序按一下 [瀏覽] > [虛擬機器] > 您的 Windows 虛擬機器 > [設定] > [稽核記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="e4981-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="e4981-114">問題：啟動已停止的 VM 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="e4981-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="e4981-115">您嘗試啟動已停止的 VM，但是發現配置失敗。</span><span class="sxs-lookup"><span data-stu-id="e4981-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e4981-116">原因</span><span class="sxs-lookup"><span data-stu-id="e4981-116">Cause</span></span>
<span data-ttu-id="e4981-117">必須在架設雲端服務的原始叢集上嘗試提出啟動已停止的 VM 要求。</span><span class="sxs-lookup"><span data-stu-id="e4981-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="e4981-118">不過，叢集沒有足夠空間可完成要求。</span><span class="sxs-lookup"><span data-stu-id="e4981-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="e4981-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="e4981-119">Resolution</span></span>
* <span data-ttu-id="e4981-120">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯，但不是和同質群組。</span><span class="sxs-lookup"><span data-stu-id="e4981-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="e4981-121">刪除已停止的 VM。</span><span class="sxs-lookup"><span data-stu-id="e4981-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="e4981-122">使用磁碟在新的雲端服務中重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="e4981-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="e4981-123">啟動重新建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="e4981-123">Start the re-created VM.</span></span>

<span data-ttu-id="e4981-124">如果您在嘗試建立新的雲端服務時收到錯誤，請稍後再試一次，或變更雲端服務的區域。</span><span class="sxs-lookup"><span data-stu-id="e4981-124">If you get an error when trying to create a new cloud service, either retry later or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4981-125">新的雲端服務將會有新的名稱和 VIP，因此您需要為所有將資訊用於現有雲端服務的相依性變更該資訊。</span><span class="sxs-lookup"><span data-stu-id="e4981-125">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="e4981-126">問題：調整現有 VM 的大小時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="e4981-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="e4981-127">您嘗試調整現有 VM 的大小，但是發現配置失敗。</span><span class="sxs-lookup"><span data-stu-id="e4981-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e4981-128">原因</span><span class="sxs-lookup"><span data-stu-id="e4981-128">Cause</span></span>
<span data-ttu-id="e4981-129">必須在架設雲端服務的原始叢集上嘗試提出調整 VM 大小的要求。</span><span class="sxs-lookup"><span data-stu-id="e4981-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="e4981-130">不過，叢集不支援要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="e4981-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="e4981-131">解決方案</span><span class="sxs-lookup"><span data-stu-id="e4981-131">Resolution</span></span>
<span data-ttu-id="e4981-132">減少要求的 VM 大小，並再試一次調整大小要求。</span><span class="sxs-lookup"><span data-stu-id="e4981-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="e4981-133">按一下 [全部瀏覽]  >  [虛擬機器 (傳統)]  >  *您的虛擬機器*  >  [設定]  >  [大小]。</span><span class="sxs-lookup"><span data-stu-id="e4981-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="e4981-134">如需詳細步驟，請參閱 [調整虛擬機器的大小](https://msdn.microsoft.com/library/dn168976.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e4981-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="e4981-135">如果您無法減少 VM 大小，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="e4981-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="e4981-136">建立新的雲端服務，確保不會連結至同質群組，以及未與連結至同質群組的虛擬網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="e4981-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="e4981-137">在其中建立新的、較大的 VM。</span><span class="sxs-lookup"><span data-stu-id="e4981-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="e4981-138">您可以在相同的雲端服務中合併所有 VM。</span><span class="sxs-lookup"><span data-stu-id="e4981-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="e4981-139">如果現有的雲端服務和以區域為基礎的虛擬網路相關聯，您可以將新的雲端服務連接到現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4981-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="e4981-140">如果現有的雲端服務未和以區域為基礎的虛擬網路相關聯，您必須刪除現有雲端服務中的 VM，並從其磁碟在新的雲端服務中將其重新建立。</span><span class="sxs-lookup"><span data-stu-id="e4981-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="e4981-141">然而，請務必記得新的雲端服務將會有新的名稱和 VIP，因此您需要為所有目前將此資訊用於現有雲端服務的相依性更新該資訊。</span><span class="sxs-lookup"><span data-stu-id="e4981-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4981-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4981-142">Next steps</span></span>
<span data-ttu-id="e4981-143">如果您在 Azure 中建立 Windows VM 時遇到問題，請參閱[針對在 Azure 中建立 Windows 虛擬機器的部署問題進行疑難排解](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e4981-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
