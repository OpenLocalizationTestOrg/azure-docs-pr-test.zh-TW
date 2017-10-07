---
title: "Hybrid Runbook 背景工作角色：Runbook 作業在暫止狀態下終止 | Microsoft Docs"
description: "Hybrid Runbook Worker 作業終止錯誤的徵兆原因和解決方式。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a><span data-ttu-id="5ccdf-103">Hybrid Runbook Worker：Runbook 作業在暫止狀態下終止</span><span class="sxs-lookup"><span data-stu-id="5ccdf-103">Hybrid Runbook Worker: A runbook job terminates with a status of Suspended</span></span>
## <a name="summary"></a><span data-ttu-id="5ccdf-104">摘要</span><span class="sxs-lookup"><span data-stu-id="5ccdf-104">Summary</span></span>
<span data-ttu-id="5ccdf-105">您的 runbook 會暫停嘗試 tooexecute 後，馬上它三次。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-105">Your runbook is suspended shortly after attempting tooexecute it three times.</span></span> <span data-ttu-id="5ccdf-106">可能會干擾 hello runbook 無法順利完成的情況，而且 hello 相關的錯誤訊息不包含任何表示原因的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-106">There are conditions which may interrupt hello runbook from completing successfully and hello related error message does not include any additional information indicating why.</span></span> <span data-ttu-id="5ccdf-107">本文章提供問題相關的 toohello Hybrid Runbook Worker runbook 執行失敗的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-107">This article provides troubleshooting steps for issues related toohello Hybrid Runbook Worker runbook execution failures.</span></span>

<span data-ttu-id="5ccdf-108">如果這份文件中並未提及您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和 hello 堆疊溢位](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-108">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5ccdf-109">您可以在這些論壇張貼您的問題或太[@AzureSupport Twitter 上](https://twitter.com/AzureSupport)。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-109">You can post your issue on these forums or too[@AzureSupport on Twitter](https://twitter.com/AzureSupport).</span></span> <span data-ttu-id="5ccdf-110">此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-110">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptom"></a><span data-ttu-id="5ccdf-111">徵狀</span><span class="sxs-lookup"><span data-stu-id="5ccdf-111">Symptom</span></span>
<span data-ttu-id="5ccdf-112">Runbook 執行會失敗並會傳回錯誤的 hello，"hello 作業動作 'Activate' 無法執行，因為 hello 處理序意外停止。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-112">Runbook execution fails and hello error returned is, "hello job action 'Activate' cannot be run, because hello process stopped unexpectedly.</span></span> <span data-ttu-id="5ccdf-113">hello 工作動作嘗試 3 次。 」</span><span class="sxs-lookup"><span data-stu-id="5ccdf-113">hello job action was attempted 3 times."</span></span>

## <a name="cause"></a><span data-ttu-id="5ccdf-114">原因</span><span class="sxs-lookup"><span data-stu-id="5ccdf-114">Cause</span></span>
<span data-ttu-id="5ccdf-115">有幾個 hello 錯誤可能原因：</span><span class="sxs-lookup"><span data-stu-id="5ccdf-115">There are several possible causes for hello error:</span></span> 

1. <span data-ttu-id="5ccdf-116">hello 混合式背景工作會在 proxy 或防火牆後面</span><span class="sxs-lookup"><span data-stu-id="5ccdf-116">hello hybrid worker is behind a proxy or firewall</span></span>
2. <span data-ttu-id="5ccdf-117">hello 電腦 hello 混合式背景工作上執行小於比 hello 最低硬體[需求](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span><span class="sxs-lookup"><span data-stu-id="5ccdf-117">hello computer hello hybrid worker is running on has less than hello minimum hardware [requirements](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span></span> 
3. <span data-ttu-id="5ccdf-118">hello runbook 無法向本機資源</span><span class="sxs-lookup"><span data-stu-id="5ccdf-118">hello runbooks cannot authenticate with local resources</span></span>

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a><span data-ttu-id="5ccdf-119">原因 1︰Hybrid Runbook Worker 位在 Proxy 或防火牆後方</span><span class="sxs-lookup"><span data-stu-id="5ccdf-119">Cause 1: Hybrid Runbook Worker is behind proxy or firewall</span></span>
<span data-ttu-id="5ccdf-120">混合式 Runbook 背景工作執行的 hello 電腦 hello 位於防火牆或 proxy 伺服器並不能允許或正確設定傳出的網路存取。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-120">hello computer hello Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.</span></span>

### <a name="solution"></a><span data-ttu-id="5ccdf-121">方案</span><span class="sxs-lookup"><span data-stu-id="5ccdf-121">Solution</span></span>
<span data-ttu-id="5ccdf-122">請確認 hello 電腦有 too*.cloudapp 對外存取連接埠 443、 9354 和 30000 30199 上的.net。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-122">Verify hello computer has outbound access too*.cloudapp.net on ports 443, 9354, and 30000-30199.</span></span> 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a><span data-ttu-id="5ccdf-123">原因 2︰電腦未滿足最低硬體需求</span><span class="sxs-lookup"><span data-stu-id="5ccdf-123">Cause 2: Computer has less than minimum hardware requirements</span></span>
<span data-ttu-id="5ccdf-124">執行的 hello 應該符合 Hybrid Runbook Worker 的電腦 hello 最低硬體需求，再指定它 toohost 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-124">Computers running hello Hybrid Runbook Worker should meet hello minimum hardware requirements before designating it toohost this feature.</span></span> <span data-ttu-id="5ccdf-125">否則，根據 hello 資源使用的其他背景處理序和執行期間，runbook 所造成的競爭情形，hello 電腦會變得過度使用，並會造成 runbook 作業延遲或逾時。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-125">Otherwise, depending on hello resource utilization of other background processes and contention caused by runbooks during execution, hello computer will become over utilized and cause runbook job delays or timeouts.</span></span> 

### <a name="solution"></a><span data-ttu-id="5ccdf-126">方案</span><span class="sxs-lookup"><span data-stu-id="5ccdf-126">Solution</span></span>
<span data-ttu-id="5ccdf-127">先確認 hello 電腦指定 toorun hello Hybrid Runbook Worker 的功能符合 hello 最低硬體需求。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-127">First confirm hello computer designated toorun hello Hybrid Runbook Worker feature meets hello minimum hardware requirements.</span></span>  <span data-ttu-id="5ccdf-128">若是如此，監視 CPU 和記憶體使用率 toodetermine Windows hello 的混合式 Runbook 背景工作處理序的效能之間的任何相互關聯。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-128">If it does, monitor CPU and memory utilization toodetermine any correlation between hello performance of Hybrid Runbook Worker processes and Windows.</span></span>  <span data-ttu-id="5ccdf-129">如果沒有記憶體或 CPU 不足的壓力，這可能表示 hello 需要 tooupgrade 或加入額外的處理器或增加記憶體 tooaddress hello 資源瓶頸並解決 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-129">If there is memory or CPU pressure, this may indicate hello need tooupgrade or add additional processors, or increase memory tooaddress hello resource bottleneck and resolve hello error.</span></span> <span data-ttu-id="5ccdf-130">或者，選取不同的計算資源可支援 hello 最小需求並縮放工作負載需求指出是必要的增加時。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-130">Alternatively, select a different compute resource that can support hello minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a><span data-ttu-id="5ccdf-131">原因 3：Runbook 無法使用本機資源驗證</span><span class="sxs-lookup"><span data-stu-id="5ccdf-131">Cause 3: Runbooks cannot authenticate with local resources</span></span>
### <a name="solution"></a><span data-ttu-id="5ccdf-132">方案</span><span class="sxs-lookup"><span data-stu-id="5ccdf-132">Solution</span></span>
<span data-ttu-id="5ccdf-133">檢查 hello **Microsoft SMA**事件記錄檔中描述的對應事件*Win32 處理序已結束，代碼 [4294967295]*。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-133">Check hello **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span>  <span data-ttu-id="5ccdf-134">hello 這個錯誤的原因是您未在 runbook 中設定驗證或未指定 hello 執行身分認證的 hello Hybrid worker 群組。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-134">hello cause of this error is you haven't configured authentication in your runbooks or specified hello Run As credentials for hello Hybrid worker group.</span></span>  <span data-ttu-id="5ccdf-135">請檢閱[Runbook 權限](automation-hybrid-runbook-worker.md#runbook-permissions)tooconfirm 您已正確設定驗證您的 runbook。</span><span class="sxs-lookup"><span data-stu-id="5ccdf-135">Please review [Runbook permissions](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm you have correctly configured authentication for your runbooks.</span></span>  

