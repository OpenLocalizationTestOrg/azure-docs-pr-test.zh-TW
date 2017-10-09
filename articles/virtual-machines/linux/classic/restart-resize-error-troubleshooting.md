---
title: "重新啟動或調整大小問題 aaaVM |Microsoft 文件"
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
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="1932b-103">針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1932b-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1932b-104">傳統</span><span class="sxs-lookup"><span data-stu-id="1932b-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="1932b-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="1932b-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="1932b-106">當您嘗試 toostart 停止 Azure 虛擬機器 (VM)，或將現有的 Azure VM 調整時，hello 常見的錯誤，您會遇到為配置失敗。</span><span class="sxs-lookup"><span data-stu-id="1932b-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="1932b-107">當 hello 叢集或區域可能沒有可用的資源或無法支援 hello 要求的 VM 大小，就會產生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="1932b-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1932b-108">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1932b-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1932b-109">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1932b-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1932b-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="1932b-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1932b-111">Hello 資源管理員版本，請參閱[這裡](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1932b-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="1932b-112">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="1932b-112">Collect audit logs</span></span>
<span data-ttu-id="1932b-113">troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="1932b-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="1932b-114">在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Linux 虛擬機器* >  **設定** > **稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="1932b-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="1932b-115">問題：啟動已停止的 VM 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="1932b-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="1932b-116">您嘗試 toostart 已停止的 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="1932b-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="1932b-117">原因</span><span class="sxs-lookup"><span data-stu-id="1932b-117">Cause</span></span>
<span data-ttu-id="1932b-118">hello 要求 toostart hello 停止 VM 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。</span><span class="sxs-lookup"><span data-stu-id="1932b-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="1932b-119">不過，hello 叢集沒有可用的空間可用 toofulfill hello 要求。</span><span class="sxs-lookup"><span data-stu-id="1932b-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="1932b-120">解決方案</span><span class="sxs-lookup"><span data-stu-id="1932b-120">Resolution</span></span>
* <span data-ttu-id="1932b-121">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯，但不是和同質群組。</span><span class="sxs-lookup"><span data-stu-id="1932b-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="1932b-122">刪除 hello 停止 VM。</span><span class="sxs-lookup"><span data-stu-id="1932b-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="1932b-123">使用 hello 磁碟重新建立 hello 新的雲端服務中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1932b-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="1932b-124">啟動 hello 重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1932b-124">Start hello re-created VM.</span></span>

<span data-ttu-id="1932b-125">如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，稍後再試一次，或變更 hello 雲端服務的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="1932b-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1932b-126">hello 新的雲端服務必須在新的名稱和 VIP，因此您需要 toochange 該資訊的所有使用該資訊 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="1932b-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="1932b-127">問題：調整現有 VM 的大小時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="1932b-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="1932b-128">您嘗試 tooresize 現有 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="1932b-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="1932b-129">原因</span><span class="sxs-lookup"><span data-stu-id="1932b-129">Cause</span></span>
<span data-ttu-id="1932b-130">hello 要求 tooresize hello VM 有 toobe 嘗試 hello 原始叢集在該主機 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1932b-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="1932b-131">不過，不支援 hello 叢集 hello 要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="1932b-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="1932b-132">解決方案</span><span class="sxs-lookup"><span data-stu-id="1932b-132">Resolution</span></span>
<span data-ttu-id="1932b-133">減少 hello 要求的 VM 大小和重試 hello 調整大小的要求。</span><span class="sxs-lookup"><span data-stu-id="1932b-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="1932b-134">按一下 [全部瀏覽]  >  [虛擬機器 (傳統)]  >  *您的虛擬機器*  >  [設定]  >  [大小]。</span><span class="sxs-lookup"><span data-stu-id="1932b-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="1932b-135">如需詳細步驟，請參閱[調整 hello 虛擬機器大小](https://msdn.microsoft.com/library/dn168976.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1932b-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="1932b-136">如果不可能 tooreduce hello VM 大小，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1932b-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="1932b-137">建立新的雲端服務中，確定它不連結 tooan 同質群組不相關聯的虛擬網路，且連結的 tooan 同質群組。</span><span class="sxs-lookup"><span data-stu-id="1932b-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="1932b-138">在其中建立新的、較大的 VM。</span><span class="sxs-lookup"><span data-stu-id="1932b-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="1932b-139">您可以將合併所有 Vm 都在 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1932b-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="1932b-140">如果您現有的雲端服務與區域為基礎的虛擬網路相關聯，您可以連接 hello 新雲端服務 toohello 現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1932b-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="1932b-141">如果找不到與區域為基礎的虛擬網路相關聯的 hello 現有雲端服務，您擁有 toodelete hello Vm hello 現有雲端服務中的，並且在 hello 新的雲端服務從其磁碟重新建立它們。</span><span class="sxs-lookup"><span data-stu-id="1932b-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="1932b-142">不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="1932b-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1932b-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1932b-143">Next steps</span></span>
<span data-ttu-id="1932b-144">如果您在 Azure 中建立新的 Linux VM 時遇到問題，請參閱[針對在 Azure 中建立新 Linux 虛擬機器的部署問題進行疑難排解](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1932b-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

