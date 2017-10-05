---
title: "從 Log Analytics 取消 Azure 自動化帳戶連結 | Microsoft Docs"
description: "此文章提供如何將 Azure 自動化帳戶從 OMS 工作區取消連結的概觀。"
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="a034e-103">如何將自動化帳戶從 Log Analytics 工作區取消連結</span><span class="sxs-lookup"><span data-stu-id="a034e-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="a034e-104">Azure 自動化與 Log Analytics 整合，不僅支援所有自動化帳戶 Runbook 作業的主動式監視，而且是在您匯入下列相依於 Log Analytics 的解決方案時所必須的：</span><span class="sxs-lookup"><span data-stu-id="a034e-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="a034e-105">更新管理</span><span class="sxs-lookup"><span data-stu-id="a034e-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="a034e-106">變更追蹤</span><span class="sxs-lookup"><span data-stu-id="a034e-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="a034e-107">於下班時間啟動/停止 VM</span><span class="sxs-lookup"><span data-stu-id="a034e-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="a034e-108">若決定不想再讓自動化帳戶與 Log Analytics 整合，您可以直接從 Azure 入口網站將您的帳戶取消連結。</span><span class="sxs-lookup"><span data-stu-id="a034e-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="a034e-109">繼續之前，您必須先移除稍早所述的解決方案，否則此程序將無法完成。</span><span class="sxs-lookup"><span data-stu-id="a034e-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="a034e-110">檢閱您已匯入之特定解決方案的主題，以了解移除解決方案所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="a034e-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="a034e-111">移除這些解決方案之後，您可以執行下列步驟以將您的自動化帳戶取消連結。</span><span class="sxs-lookup"><span data-stu-id="a034e-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="a034e-112">取消連結工作區</span><span class="sxs-lookup"><span data-stu-id="a034e-112">Unlink workspace</span></span>

1. <span data-ttu-id="a034e-113">從 Azure 入口網站，開啟您的自動化帳戶，然後在 [自動化帳戶] 刀鋒視窗的 [帳戶] 刀鋒視窗中選取 [取消連結工作區]。</span><span class="sxs-lookup"><span data-stu-id="a034e-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="a034e-114">![取消連結工作區選項](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="a034e-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="a034e-115">在 [取消連結工作區] 刀鋒視窗上，按一下 [取消連結工作區]。</span><span class="sxs-lookup"><span data-stu-id="a034e-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="a034e-116">![取消連結工作區刀鋒視窗](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png)。</span><span class="sxs-lookup"><span data-stu-id="a034e-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="a034e-117">您會收到提示，確認您想要繼續。</span><span class="sxs-lookup"><span data-stu-id="a034e-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="a034e-118">當 Azure 自動化嘗試將您的帳戶從 Log Analytics 工作區取消連結時，您可以從功能表在 [通知] 下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="a034e-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="a034e-119">若使用「更新管理」解決方案，您可以在移除解決方案之後選擇移除已不再需要的下列項目。</span><span class="sxs-lookup"><span data-stu-id="a034e-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="a034e-120">更新排程。</span><span class="sxs-lookup"><span data-stu-id="a034e-120">Update schedules.</span></span>  <span data-ttu-id="a034e-121">每個都會有符合您建立之更新部署的名稱)</span><span class="sxs-lookup"><span data-stu-id="a034e-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="a034e-122">針對解決方案建立的混合式背景工作角色群組。</span><span class="sxs-lookup"><span data-stu-id="a034e-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="a034e-123">每個都會具有如下名稱：machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8)。</span><span class="sxs-lookup"><span data-stu-id="a034e-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="a034e-124">若使用「於下班時間啟動/停止 VM」解決方案，您可以在移除解決方案之後選擇移除已不再需要的下列項目。</span><span class="sxs-lookup"><span data-stu-id="a034e-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="a034e-125">啟動及停止 VM Runbook 排程</span><span class="sxs-lookup"><span data-stu-id="a034e-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="a034e-126">啟動及停止 VM Runbook</span><span class="sxs-lookup"><span data-stu-id="a034e-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="a034e-127">變數</span><span class="sxs-lookup"><span data-stu-id="a034e-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="a034e-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a034e-128">Next steps</span></span>

<span data-ttu-id="a034e-129">若要重新設定您的自動化帳戶以與 OMS Log Analytics 整合，請參閱[從自動化將作業狀態和作業串流轉送到 Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="a034e-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 