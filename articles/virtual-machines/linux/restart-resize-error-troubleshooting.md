---
title: "在 Azure 中發出重新啟動或調整大小的 aaaVM |Microsoft 文件"
description: "針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="8a2cb-103">針對在 Azure 中重新啟動或調整現有 Linux VM 大小的部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8a2cb-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="8a2cb-104">當您嘗試 toostart 停止 Azure 虛擬機器 (VM)，或將現有的 Azure VM 調整時，hello 常見的錯誤，您會遇到為配置失敗。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="8a2cb-105">當 hello 叢集或區域可能沒有可用的資源或無法支援 hello 要求的 VM 大小，就會產生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="8a2cb-106">收集活動記錄</span><span class="sxs-lookup"><span data-stu-id="8a2cb-106">Collect activity logs</span></span>
<span data-ttu-id="8a2cb-107">疑難排解，toostart 收集 hello 活動與 hello 問題相關聯的 tooidentify hello 錯誤的記錄。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="8a2cb-108">下列連結查看 hello 包含 hello 程序的詳細的資訊：</span><span class="sxs-lookup"><span data-stu-id="8a2cb-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="8a2cb-109">檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="8a2cb-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="8a2cb-110">檢視活動記錄檔 toomanage Azure 資源</span><span class="sxs-lookup"><span data-stu-id="8a2cb-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="8a2cb-111">問題：啟動已停止的 VM 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="8a2cb-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="8a2cb-112">您嘗試 toostart 已停止的 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="8a2cb-113">原因</span><span class="sxs-lookup"><span data-stu-id="8a2cb-113">Cause</span></span>
<span data-ttu-id="8a2cb-114">hello 要求 toostart hello 停止 VM 有 toobe 嘗試裝載 hello 雲端服務的 hello 原始叢集中。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="8a2cb-115">不過，hello 叢集沒有可用的空間可用 toofulfill hello 要求。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="8a2cb-116">解決方案</span><span class="sxs-lookup"><span data-stu-id="8a2cb-116">Resolution</span></span>
* <span data-ttu-id="8a2cb-117">停止所有 hello hello 可用性中的 Vm 設定，然後再重新啟動每個 VM。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="8a2cb-118">按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="8a2cb-119">在所有 hello Vm 停止，並選取每個 hello 停止 Vm，然後按一下 開始。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="8a2cb-120">稍後，重試 hello 重新啟動要求。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="8a2cb-121">問題：調整現有 VM 的大小時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="8a2cb-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="8a2cb-122">您嘗試 tooresize 現有 VM，但配置失敗。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="8a2cb-123">原因</span><span class="sxs-lookup"><span data-stu-id="8a2cb-123">Cause</span></span>
<span data-ttu-id="8a2cb-124">hello 要求 tooresize hello VM 有 toobe 嘗試 hello 原始叢集在該主機 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="8a2cb-125">不過，不支援 hello 叢集 hello 要求的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="8a2cb-126">解決方案</span><span class="sxs-lookup"><span data-stu-id="8a2cb-126">Resolution</span></span>
* <span data-ttu-id="8a2cb-127">重試 hello 要求使用較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="8a2cb-128">如果 hello hello 的大小會要求無法變更 VM:</span><span class="sxs-lookup"><span data-stu-id="8a2cb-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="8a2cb-129">停止 hello 可用性設定組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="8a2cb-130">按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="8a2cb-131">在所有 hello Vm 停止，調整大小所需的 hello VM tooa 較大的大小。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="8a2cb-132">選取 hello 調整大小的 VM，然後按一下**啟動**，然後啟動每一部 hello 停止 Vm。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a2cb-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a2cb-133">Next steps</span></span>
<span data-ttu-id="8a2cb-134">如果您在 Azure 中建立新的 Linux VM 時遇到問題，請參閱[針對在 Azure 中建立新 Linux 虛擬機器的部署問題進行疑難排解](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8a2cb-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

