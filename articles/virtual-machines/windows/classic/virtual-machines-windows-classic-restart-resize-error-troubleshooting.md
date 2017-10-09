---
title: "重新啟動或調整大小問題 aaaVM |Microsoft 文件"
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
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="fd719-103">針對在 Azure 中重新啟動或調整現有 Windows 虛擬機器大小的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="fd719-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd719-104">傳統</span><span class="sxs-lookup"><span data-stu-id="fd719-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="fd719-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="fd719-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="fd719-106">當您嘗試 toostart 停止 Azure 虛擬機器 (VM)，或將現有的 Azure VM 調整時，hello 常見的錯誤，您會遇到為配置失敗。</span><span class="sxs-lookup"><span data-stu-id="fd719-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="fd719-107">當 hello 叢集或區域可能沒有可用的資源或無法支援 hello 要求的 VM 大小，就會產生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd719-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd719-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="fd719-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fd719-109">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fd719-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="fd719-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="fd719-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="fd719-111">收集稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="fd719-111">Collect audit logs</span></span>
<span data-ttu-id="fd719-112">troubleshooting，toostart 收集 hello 稽核記錄與 hello 問題相關聯的 tooidentify hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd719-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="fd719-113">在 hello Azure 入口網站，按一下 **瀏覽** > **虛擬機器** > *Windows 虛擬機器* >  **設定** > **稽核記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="fd719-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="fd719-114">問題：啟動已停止的 VM 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="fd719-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="fd719-115">您嘗試 toostart 已停止的 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="fd719-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fd719-116">原因</span><span class="sxs-lookup"><span data-stu-id="fd719-116">Cause</span></span>
<span data-ttu-id="fd719-117">hello 要求 toostart hello 停止 VM 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。</span><span class="sxs-lookup"><span data-stu-id="fd719-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="fd719-118">不過，hello 叢集沒有可用的空間可用 toofulfill hello 要求。</span><span class="sxs-lookup"><span data-stu-id="fd719-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="fd719-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="fd719-119">Resolution</span></span>
* <span data-ttu-id="fd719-120">建立新的雲端服務，並將它和區域或以區域為基礎的虛擬網路相關聯，但不是和同質群組。</span><span class="sxs-lookup"><span data-stu-id="fd719-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="fd719-121">刪除 hello 停止 VM。</span><span class="sxs-lookup"><span data-stu-id="fd719-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="fd719-122">使用 hello 磁碟重新建立 hello 新的雲端服務中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="fd719-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="fd719-123">啟動 hello 重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="fd719-123">Start hello re-created VM.</span></span>

<span data-ttu-id="fd719-124">如果嘗試 toocreate 新的雲端服務時，您會收到錯誤，請稍後重試，或變更 hello 雲端服務的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="fd719-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd719-125">hello 新的雲端服務必須在新的名稱和 VIP，因此您需要 toochange 該資訊的所有使用該資訊 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="fd719-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="fd719-126">問題：調整現有 VM 的大小時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="fd719-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="fd719-127">您嘗試 tooresize 現有 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="fd719-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="fd719-128">原因</span><span class="sxs-lookup"><span data-stu-id="fd719-128">Cause</span></span>
<span data-ttu-id="fd719-129">hello 要求 tooresize hello VM 有 toobe 嘗試 hello 原始叢集在該主機 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd719-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="fd719-130">不過，不支援 hello 叢集 hello 要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="fd719-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="fd719-131">解決方案</span><span class="sxs-lookup"><span data-stu-id="fd719-131">Resolution</span></span>
<span data-ttu-id="fd719-132">減少 hello 要求的 VM 大小和重試 hello 調整大小的要求。</span><span class="sxs-lookup"><span data-stu-id="fd719-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="fd719-133">按一下 [全部瀏覽]  >  [虛擬機器 (傳統)]  >  *您的虛擬機器*  >  [設定]  >  [大小]。</span><span class="sxs-lookup"><span data-stu-id="fd719-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="fd719-134">如需詳細步驟，請參閱[調整 hello 虛擬機器大小](https://msdn.microsoft.com/library/dn168976.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd719-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="fd719-135">如果不可能 tooreduce hello VM 大小，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fd719-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="fd719-136">建立新的雲端服務中，確定它不連結 tooan 同質群組不相關聯的虛擬網路，且連結的 tooan 同質群組。</span><span class="sxs-lookup"><span data-stu-id="fd719-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="fd719-137">在其中建立新的、較大的 VM。</span><span class="sxs-lookup"><span data-stu-id="fd719-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="fd719-138">您可以將合併所有 Vm 都在 hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd719-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="fd719-139">如果您現有的雲端服務與區域為基礎的虛擬網路相關聯，您可以連接 hello 新雲端服務 toohello 現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fd719-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="fd719-140">如果找不到與區域為基礎的虛擬網路相關聯的 hello 現有雲端服務，您擁有 toodelete hello Vm hello 現有雲端服務中的，並且在 hello 新的雲端服務從其磁碟重新建立它們。</span><span class="sxs-lookup"><span data-stu-id="fd719-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="fd719-141">不過，它是重要 tooremember，hello 新的雲端服務會有新名稱和 VIP，因此您需要 tooupdate 供所有目前使用這項資訊為 hello 現有雲端服務的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="fd719-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd719-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd719-142">Next steps</span></span>
<span data-ttu-id="fd719-143">如果您在 Azure 中建立 Windows VM 時遇到問題，請參閱[針對在 Azure 中建立 Windows 虛擬機器的部署問題進行疑難排解](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fd719-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

