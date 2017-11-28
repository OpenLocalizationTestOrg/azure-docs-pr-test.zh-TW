---
title: "Azure 自動化帳戶的記錄分析 aaaUnlink |Microsoft 文件"
description: "本文章提供如何 toounlink Azure 自動化帳戶從 OMS 工作區的概觀。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="6271b-103">如何 toounlink 您的自動化帳戶從記錄分析工作區</span><span class="sxs-lookup"><span data-stu-id="6271b-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="6271b-104">Azure 自動化整合記錄分析 toonot 只支援主動式監視之 runbook 工作的所有的自動化帳戶，但也是必要時您匯入下列相依於記錄分析解決方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="6271b-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="6271b-105">更新管理</span><span class="sxs-lookup"><span data-stu-id="6271b-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="6271b-106">變更追蹤</span><span class="sxs-lookup"><span data-stu-id="6271b-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="6271b-107">於下班時間啟動/停止 VM</span><span class="sxs-lookup"><span data-stu-id="6271b-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="6271b-108">如果您決定您不再想 toointegrate 記錄分析您的自動化帳戶，您可以取消連結您的帳戶，直接從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6271b-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="6271b-109">在繼續之前，您需要先 tooremove hello 解決方案稍早所提及，否則此程序將無法再繼續。</span><span class="sxs-lookup"><span data-stu-id="6271b-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="6271b-110">Hello 特定方案的檢閱 hello 主題您已匯入所需的 toounderstand hello 步驟 tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="6271b-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="6271b-111">移除這些方案之後可以執行下列步驟 toounlink hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="6271b-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="6271b-112">取消連結工作區</span><span class="sxs-lookup"><span data-stu-id="6271b-112">Unlink workspace</span></span>

1. <span data-ttu-id="6271b-113">從 hello Azure 入口網站，開啟您的自動化帳戶，然後在 hello 自動化帳戶 刀鋒視窗，在 hello 帳戶 刀鋒視窗中，選取**取消連結工作區**。</span><span class="sxs-lookup"><span data-stu-id="6271b-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="6271b-114">![取消連結工作區選項](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="6271b-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="6271b-115">在 hello 取消連結工作區刀鋒視窗中，按一下 **取消連結 worksapce**。</span><span class="sxs-lookup"><span data-stu-id="6271b-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="6271b-116">![取消連結工作區刀鋒視窗](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png)。</span><span class="sxs-lookup"><span data-stu-id="6271b-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="6271b-117">您會收到確認您想 tooproceed 提示。</span><span class="sxs-lookup"><span data-stu-id="6271b-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="6271b-118">但是 Azure 自動化會嘗試 toounlink hello 帳戶記錄分析工作區，您可以追蹤在 hello 進度**通知**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="6271b-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="6271b-119">如果您使用 hello 更新管理解決方案，或者您可能想 tooremove hello 下列 hello 方案中移除之後不再需要的項目。</span><span class="sxs-lookup"><span data-stu-id="6271b-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="6271b-120">更新排程。</span><span class="sxs-lookup"><span data-stu-id="6271b-120">Update schedules.</span></span>  <span data-ttu-id="6271b-121">每個都會有名稱符合您所建立的 hello 更新部署）</span><span class="sxs-lookup"><span data-stu-id="6271b-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="6271b-122">建立 hello 方案的混合式背景工作群組。</span><span class="sxs-lookup"><span data-stu-id="6271b-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="6271b-123">每個將命名為同樣的太 machine1.contoso.com_9ceb8108-26 c 9-4051-b6b3-227600d715c8)。</span><span class="sxs-lookup"><span data-stu-id="6271b-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="6271b-124">如果您在離峰時間方案時使用 hello 啟動/停止 Vm，或者您可能想 tooremove hello 下列 hello 方案中移除之後不再需要的項目。</span><span class="sxs-lookup"><span data-stu-id="6271b-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="6271b-125">啟動及停止 VM Runbook 排程</span><span class="sxs-lookup"><span data-stu-id="6271b-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="6271b-126">啟動及停止 VM Runbook</span><span class="sxs-lookup"><span data-stu-id="6271b-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="6271b-127">變數</span><span class="sxs-lookup"><span data-stu-id="6271b-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6271b-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6271b-128">Next steps</span></span>

<span data-ttu-id="6271b-129">tooreconfigure 您自動化帳戶 toointegrate，OMS 記錄分析，請參閱[自動化 tooLog 分析 (OMS) 從轉寄工作狀態和作業資料流](automation-manage-send-joblogs-log-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="6271b-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
