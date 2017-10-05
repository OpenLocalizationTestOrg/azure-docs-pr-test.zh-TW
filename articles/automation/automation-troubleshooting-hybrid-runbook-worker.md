---
title: "針對 Azure 自動化混合式 Runbook 背景工作角色進行疑難排解 | Microsoft Docs"
description: "說明 Azure 自動化中最常見混合式 Runbook 背景工作角色問題的徵狀、原因和解決方法。"
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
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 9d1ceda5a072f494651a751a25a8ccf66e4c72ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a><span data-ttu-id="90eb1-103">混合式 Runbook 背景工作角色的疑難排解提示</span><span class="sxs-lookup"><span data-stu-id="90eb1-103">Troubleshooting tips for Hybrid Runbook Worker</span></span>

<span data-ttu-id="90eb1-104">本文可協助您針對使用自動化混合式 Runbook 背景工作角色時可能遇到的錯誤進行疑難排解，並建議可能的解決方法。</span><span class="sxs-lookup"><span data-stu-id="90eb1-104">This article provides help troubleshooting errors you might experience with Automation Hybrid Runbook Workers and suggests possible solutions to resolve them.</span></span>

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a><span data-ttu-id="90eb1-105">Runbook 作業在暫止狀態下終止</span><span class="sxs-lookup"><span data-stu-id="90eb1-105">A runbook job terminates with a status of Suspended</span></span>

<span data-ttu-id="90eb1-106">Runbook 在嘗試執行三次後會馬上暫止。</span><span class="sxs-lookup"><span data-stu-id="90eb1-106">Your runbook is suspended shortly after attempting to execute it three times.</span></span> <span data-ttu-id="90eb1-107">在某些情況下，Runbook 可能會因為受到干擾而無法順利完成，而相關的錯誤訊息卻不含任何指出原因的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="90eb1-107">There are conditions which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why.</span></span> <span data-ttu-id="90eb1-108">本文提供 Hybrid Runbook Worker Runbook 執行失敗之相關問題的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="90eb1-108">This article provides troubleshooting steps for issues related to the Hybrid Runbook Worker runbook execution failures.</span></span>

<span data-ttu-id="90eb1-109">若本文中未提及您的 Azure 問題，請造訪 [MSDN 及 Stack Overflow 上的 Azure 論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="90eb1-109">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="90eb1-110">您可以在這些論壇上張貼您的問題，或將問題貼到 Twitter [@AzureSupport上的](https://twitter.com/AzureSupport) 。</span><span class="sxs-lookup"><span data-stu-id="90eb1-110">You can post your issue on these forums or to [@AzureSupport on Twitter](https://twitter.com/AzureSupport).</span></span> <span data-ttu-id="90eb1-111">此外，您也可以選取 [Azure 支援](https://azure.microsoft.com/support/options/)網站上的 [取得支援]，來提出 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="90eb1-111">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

### <a name="symptom"></a><span data-ttu-id="90eb1-112">徵狀</span><span class="sxs-lookup"><span data-stu-id="90eb1-112">Symptom</span></span>
<span data-ttu-id="90eb1-113">Runbook 執行失敗且傳回的錯誤是「作業動作 'Activate' 無法執行，因為處理序意外停止。</span><span class="sxs-lookup"><span data-stu-id="90eb1-113">Runbook execution fails and the error returned is, "The job action 'Activate' cannot be run, because the process stopped unexpectedly.</span></span> <span data-ttu-id="90eb1-114">作業動作已嘗試 3 次」。</span><span class="sxs-lookup"><span data-stu-id="90eb1-114">The job action was attempted 3 times."</span></span>

<span data-ttu-id="90eb1-115">這個錯誤的可能原因有幾個，包括︰</span><span class="sxs-lookup"><span data-stu-id="90eb1-115">There are several possible causes for the error:</span></span> 

1. <span data-ttu-id="90eb1-116">Hybrid Worker 位於 Proxy 或防火牆後方</span><span class="sxs-lookup"><span data-stu-id="90eb1-116">The hybrid worker is behind a proxy or firewall</span></span>
2. <span data-ttu-id="90eb1-117">混合式背景工作角色執行所在的電腦未滿足最低硬體[需求](automation-offering-get-started.md#hybrid-runbook-worker)</span><span class="sxs-lookup"><span data-stu-id="90eb1-117">The computer the hybrid worker is running on has less than the minimum [hardware  requirements](automation-offering-get-started.md#hybrid-runbook-worker)</span></span>  
3. <span data-ttu-id="90eb1-118">Runbook 無法使用本機資源驗證</span><span class="sxs-lookup"><span data-stu-id="90eb1-118">The runbooks cannot authenticate with local resources</span></span>

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a><span data-ttu-id="90eb1-119">原因 1︰Hybrid Runbook Worker 位在 Proxy 或防火牆後方</span><span class="sxs-lookup"><span data-stu-id="90eb1-119">Cause 1: Hybrid Runbook Worker is behind proxy or firewall</span></span>
<span data-ttu-id="90eb1-120">Hybrid Runbook Worker 執行所在的電腦位於防火牆或 Proxy 伺服器後方，因此輸出網路存取未獲得允許或設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="90eb1-120">The computer the Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.</span></span>

#### <a name="solution"></a><span data-ttu-id="90eb1-121">方案</span><span class="sxs-lookup"><span data-stu-id="90eb1-121">Solution</span></span>
<span data-ttu-id="90eb1-122">確認電腦可透過連接埠 443 輸出存取 *.azure-automation.net。</span><span class="sxs-lookup"><span data-stu-id="90eb1-122">Verify the computer has outbound access to *.azure-automation.net on port 443.</span></span> 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a><span data-ttu-id="90eb1-123">原因 2︰電腦未滿足最低硬體需求</span><span class="sxs-lookup"><span data-stu-id="90eb1-123">Cause 2: Computer has less than minimum hardware requirements</span></span>
<span data-ttu-id="90eb1-124">執行 Hybrid Runbook Worker 的電腦應滿足最低硬體需求，您才能指派它來裝載這項功能。</span><span class="sxs-lookup"><span data-stu-id="90eb1-124">Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature.</span></span> <span data-ttu-id="90eb1-125">否則，根據其他背景處理序的資源使用率和 Runbook 在執行期間造成的競爭，電腦可能會變得過度使用，導致 Runbook 作業延遲或逾時。</span><span class="sxs-lookup"><span data-stu-id="90eb1-125">Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer will become over utilized and cause runbook job delays or timeouts.</span></span> 

#### <a name="solution"></a><span data-ttu-id="90eb1-126">方案</span><span class="sxs-lookup"><span data-stu-id="90eb1-126">Solution</span></span>
<span data-ttu-id="90eb1-127">先確認指派來執行 Hybrid Runbook Worker 功能的電腦滿足最低硬體需求。</span><span class="sxs-lookup"><span data-stu-id="90eb1-127">First confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span></span>  <span data-ttu-id="90eb1-128">如果滿足最低硬體需求，請監視 CPU 和記憶體使用率，判斷 Hybrid Runbook Worker 處理序之效能和 Windows 之間是否有任何相互關聯。</span><span class="sxs-lookup"><span data-stu-id="90eb1-128">If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.</span></span>  <span data-ttu-id="90eb1-129">如果有記憶體或 CPU 壓力，這表示電腦可能需要升級或增加額外處理器，或增加記憶體來解決資源瓶頸及解決錯誤。</span><span class="sxs-lookup"><span data-stu-id="90eb1-129">If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error.</span></span> <span data-ttu-id="90eb1-130">您也可以選擇其他可支援最低需求，也能在工作負載需求指出需要增加資源時擴充的計算資源。</span><span class="sxs-lookup"><span data-stu-id="90eb1-130">Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a><span data-ttu-id="90eb1-131">原因 3：Runbook 無法使用本機資源驗證</span><span class="sxs-lookup"><span data-stu-id="90eb1-131">Cause 3: Runbooks cannot authenticate with local resources</span></span>

#### <a name="solution"></a><span data-ttu-id="90eb1-132">方案</span><span class="sxs-lookup"><span data-stu-id="90eb1-132">Solution</span></span>
<span data-ttu-id="90eb1-133">查閱 **Microsoft-SMA** 事件記錄檔，找出描述為「Win32 處理序結束，代碼為 [4294967295]」的對應事件。</span><span class="sxs-lookup"><span data-stu-id="90eb1-133">Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span>  <span data-ttu-id="90eb1-134">此錯誤的原因是您尚未在 Runbook 中設定驗證，或尚未指定混合式背景工作角色群組的執行身分認證。</span><span class="sxs-lookup"><span data-stu-id="90eb1-134">The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.</span></span>  <span data-ttu-id="90eb1-135">請檢閱 [Runbook 權限](automation-hrw-run-runbooks.md#runbook-permissions) ，確認 Runbook 的驗證設定正確無誤。</span><span class="sxs-lookup"><span data-stu-id="90eb1-135">Please review [Runbook permissions](automation-hrw-run-runbooks.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="90eb1-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90eb1-136">Next steps</span></span>

<span data-ttu-id="90eb1-137">如需針對自動化中的其他問題進行疑難排解的協助，請參閱[針對 Azure 自動化進行疑難排解](automation-troubleshooting-automation-errors.md)</span><span class="sxs-lookup"><span data-stu-id="90eb1-137">For help troubleshooting other issues in Automation, see [Troubleshooting common Azure Automation issues](automation-troubleshooting-automation-errors.md)</span></span> 