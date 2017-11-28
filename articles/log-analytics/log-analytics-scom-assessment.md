---
title: "使用 Azure Log Analytics 最佳化 System Center Operations Manager 環境 | Microsoft Docs"
description: "您可以使用 System Center Operations Manager 評定解決方案，定期評估伺服器環境的風險和健康狀態。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4992d98397da409f7c1cfbdeb40fdb0cdd0d2f19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-environment-with-the-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="86e38-103">使用 System Center Operations Manager 評定 (預覽) 解決方案進行環境最佳化</span><span class="sxs-lookup"><span data-stu-id="86e38-103">Optimize your environment with the System Center Operations Manager Assessment (Preview) solution</span></span>

![System Center Operations Manager 評定符號](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

<span data-ttu-id="86e38-105">您可以使用 System Center Operations Manager 評定解決方案，定期評估 System Center Operations Manager 伺服器環境的風險和健康狀態。</span><span class="sxs-lookup"><span data-stu-id="86e38-105">You can use the System Center Operations Manager Assessment solution to assess the risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="86e38-106">本文協助您安裝、設定和使用此解決方案，讓您可以針對潛在問題採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="86e38-106">This article helps you install, configure, and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="86e38-107">此方案能針對已部署的伺服器基礎結構提供依照優先順序排列的具體建議清單。</span><span class="sxs-lookup"><span data-stu-id="86e38-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="86e38-108">建議分為四個焦點領域，幫助您快速了解風險並採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="86e38-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="86e38-109">智慧套件提供的建議乃源自 Microsoft 工程師數千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="86e38-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="86e38-110">每項建議均提供問題的影響層面，以及如何實作建議變更等相關指引。</span><span class="sxs-lookup"><span data-stu-id="86e38-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="86e38-111">您可以選擇對組織而言最重要的焦點區域，同時追蹤經營無風險且健康狀態良好之環境的進度。</span><span class="sxs-lookup"><span data-stu-id="86e38-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="86e38-112">新增解決方案並完成評估之後，焦點區域的摘要資訊會顯示在基礎結構的 [System Center Operations Manager 評定] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="86e38-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="86e38-113">下列章節說明如何使用 [System Center Operations Manager 評定] 儀表板上的資訊，您可以在這裡檢視並採用針對 SCOM 基礎結構建議的動作。</span><span class="sxs-lookup"><span data-stu-id="86e38-113">The following sections describe how to use the information on the **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager 解決方案圖格](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 評估儀表板](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="86e38-116">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="86e38-116">Installing and configuring the solution</span></span>

<span data-ttu-id="86e38-117">此解決方案適用於 Microsoft System Operations Manager 2012 R2 和 2012 SP1。</span><span class="sxs-lookup"><span data-stu-id="86e38-117">The solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="86e38-118">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="86e38-118">Use the following information to install and configure the solution.</span></span>

 - <span data-ttu-id="86e38-119">在使用 OMS 中的評估方案之前，您必須先安裝方案。</span><span class="sxs-lookup"><span data-stu-id="86e38-119">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="86e38-120">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) 或遵循[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中的指示，安裝解決方案。</span><span class="sxs-lookup"><span data-stu-id="86e38-120">Install the solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following the instructions in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="86e38-121">將解決方案新增至工作區之後，儀表板上的 System Center Operations Manager 評定圖格會顯示額外設定必要的訊息。</span><span class="sxs-lookup"><span data-stu-id="86e38-121">After adding the solution to the workspace, the System Center Operations Manager Assessment tile on the dashboard displays the additional configuration required message.</span></span> <span data-ttu-id="86e38-122">按一下圖格，然後遵循頁面中所述的設定步驟</span><span class="sxs-lookup"><span data-stu-id="86e38-122">Click on the tile and follow the configuration steps mentioned in the page</span></span>

 ![System Center Operations Manager 儀表板圖格](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 <span data-ttu-id="86e38-124">System Center Operations Manager 的組態可以透過指令碼完成，方法為遵循 OMS 中解決方案組態頁面中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="86e38-124">Configuration of the System Center Operations Manager can be done through the script by following the steps mentioned in the configuration page of the solution in OMS.</span></span>

 <span data-ttu-id="86e38-125">相反地，若要透過 SCOM 主控台設定評估，請以相同的順序遵循下列步驟</span><span class="sxs-lookup"><span data-stu-id="86e38-125">Instead, to configure the assessment through SCOM Console, follow the below steps in the same order</span></span>
1. [<span data-ttu-id="86e38-126">設定 System Center Operations Manager 評定的執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="86e38-126">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="86e38-127">設定 System Center Operations Manager 評定規則</span><span class="sxs-lookup"><span data-stu-id="86e38-127">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="86e38-128">收集 System Center Operations Manager 評定資料的詳細資料</span><span class="sxs-lookup"><span data-stu-id="86e38-128">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="86e38-129">System Center Operations Manager 評定會使用您已啟用的伺服器，透過 Windows PowerShell、SQL 查詢和檔案資訊收集器，以收集 WMI 資料、登錄資料、事件記錄檔資料和 Operations Manager 資料。</span><span class="sxs-lookup"><span data-stu-id="86e38-129">The System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using the server that you have enabled.</span></span>

<span data-ttu-id="86e38-130">下表顯示 System Center Operations Manager 評定的資料收集方法，以及代理程式收集資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="86e38-130">The following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="86e38-131">平台</span><span class="sxs-lookup"><span data-stu-id="86e38-131">platform</span></span> | <span data-ttu-id="86e38-132">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="86e38-132">Direct Agent</span></span> | <span data-ttu-id="86e38-133">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="86e38-133">SCOM agent</span></span> | <span data-ttu-id="86e38-134">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="86e38-134">Azure Storage</span></span> | <span data-ttu-id="86e38-135">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="86e38-135">SCOM required?</span></span> | <span data-ttu-id="86e38-136">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="86e38-136">SCOM agent data sent via management group</span></span> | <span data-ttu-id="86e38-137">收集頻率</span><span class="sxs-lookup"><span data-stu-id="86e38-137">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="86e38-138">Windows</span><span class="sxs-lookup"><span data-stu-id="86e38-138">Windows</span></span> | | | | <span data-ttu-id="86e38-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="86e38-139">&#8226;</span></span> | | <span data-ttu-id="86e38-140">7 天</span><span class="sxs-lookup"><span data-stu-id="86e38-140">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="86e38-141">OMS 的 Operations Manager 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="86e38-141">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="86e38-142">OMS 以工作負載的管理套件為基礎來提供加值服務。</span><span class="sxs-lookup"><span data-stu-id="86e38-142">OMS builds on management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="86e38-143">每個工作負載都需要具有特定的工作負載權限，才能在不同的安全性內容中執行管理套件，例如網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-143">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="86e38-144">設定 Operations Manager 執行身分帳戶來提供認證資訊。</span><span class="sxs-lookup"><span data-stu-id="86e38-144">Configure an Operations Manager Run As account to provide credential information.</span></span>

<span data-ttu-id="86e38-145">請使用下列資訊來設定 System Center Operations Manager 評定的 Operations Manager 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-145">Use the following information to set the Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-the-run-as-account"></a><span data-ttu-id="86e38-146">設定執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="86e38-146">Set the Run As account</span></span>

1. <span data-ttu-id="86e38-147">在 Operations Manager 主控台中，移至 [管理] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="86e38-147">In the Operations Manager Console, go to the **Administration** tab.</span></span>
2. <span data-ttu-id="86e38-148">在 [執行身分設定] 下，按一下 [帳戶]。</span><span class="sxs-lookup"><span data-stu-id="86e38-148">Under the **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="86e38-149">建立執行身分帳戶，經由精靈建立 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-149">Create the Run As Account, following through the Wizard, creating a Windows account.</span></span> <span data-ttu-id="86e38-150">要使用的帳戶是已識別且符合下列所有必要條件的帳戶︰</span><span class="sxs-lookup"><span data-stu-id="86e38-150">The account to use is the one identified and having all the prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="86e38-151">執行身分帳戶必須符合下列需求︰</span><span class="sxs-lookup"><span data-stu-id="86e38-151">The Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="86e38-152">環境中所有伺服器上本機 Administrators 群組的網域帳戶成員 (所有 Operations Manager 角色 - 管理伺服器、OpsMgr 資料庫、資料倉儲、報告、Web 主控台、閘道)</span><span class="sxs-lookup"><span data-stu-id="86e38-152">A domain account member of the local Administrators group on all servers in the environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="86e38-153">要評估的管理群組之 Operation Manager 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="86e38-153">Operation Manager Administrator Role for the management group being assessed</span></span>
    - <span data-ttu-id="86e38-154">執行[指令碼](#sql-script-to-grant-granular-permissions-to-the-run-as-account)，將細微權限授與 Operations Manager 所使用的 SQL 執行個體上的帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-154">Execute the [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) to grant granular permissions to the account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="86e38-155">注意︰如果此帳戶已有系統管理員權限，請略過指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="86e38-155">Note: If this account has sysadmin rights already, then skip the script execution.</span></span>

4. <span data-ttu-id="86e38-156">在 [散發安全性] 下，選取 [較安全]。</span><span class="sxs-lookup"><span data-stu-id="86e38-156">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="86e38-157">指定散發帳戶的管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="86e38-157">Specify the management server where the account is distributed.</span></span>
3. <span data-ttu-id="86e38-158">返回 [執行身分設定]，按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="86e38-158">Go back to the Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="86e38-159">搜尋「SCOM 評定設定檔」。</span><span class="sxs-lookup"><span data-stu-id="86e38-159">Search for the *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="86e38-160">設定檔名稱應該是︰「Microsoft System Center Advisor SCOM 評定執行身分設定檔」。</span><span class="sxs-lookup"><span data-stu-id="86e38-160">The profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="86e38-161">以滑鼠右鍵按一下其屬性並更新，然後新增您最近在步驟 3 中建立的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-161">Right-click and update its properties and add the recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-to-grant-granular-permissions-to-the-run-as-account"></a><span data-ttu-id="86e38-162">授與細微權限給執行身分帳戶的 SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="86e38-162">SQL script to grant granular permissions to the Run As account</span></span>

<span data-ttu-id="86e38-163">執行下列 SQL 指令碼，將必要權限授與 Operations Manager 所使用的 SQL 執行個體上的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="86e38-163">Execute the following SQL script to grant required permissions to the Run As account on the SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with the actual user name being used as Run As Account.
USE master

-- Create login for the user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions to user.
GRANT VIEW SERVER STATE TO [UserName]
GRANT VIEW ANY DEFINITION TO [UserName]
GRANT VIEW ANY DATABASE TO [UserName]

-- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
-- NOTE: This command must be run anytime new databases are added to SQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT To [UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace the Operations Manager database name with the one in your environment
Use [OperationsManager];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager DatawareHouse database name with the one in your environment
Use [OperationsManagerDW];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager Audit Collection database name with the one in your environment
Use [OperationsManagerAC];
GRANT SELECT To [UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace the Operations Manager database name with the one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-the-assessment-rule"></a><span data-ttu-id="86e38-164">設定評定規則</span><span class="sxs-lookup"><span data-stu-id="86e38-164">Configure the assessment rule</span></span>

<span data-ttu-id="86e38-165">System Center Operations Manager 評定解決方案的管理套件包含名為「Microsoft System Center Advisor SCOM 評定執行評定規則」的規則。</span><span class="sxs-lookup"><span data-stu-id="86e38-165">The System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="86e38-166">此規則負責執行評定。</span><span class="sxs-lookup"><span data-stu-id="86e38-166">This rule is responsible for running the assessment.</span></span> <span data-ttu-id="86e38-167">若要啟用規則和設定頻率，請使用下列程序。</span><span class="sxs-lookup"><span data-stu-id="86e38-167">To enable the rule and configure the frequency, use the procedures below.</span></span>

<span data-ttu-id="86e38-168">根據預設，Microsoft System Center Advisor SCOM 評定執行評定規則已停用。</span><span class="sxs-lookup"><span data-stu-id="86e38-168">By default, the Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="86e38-169">若要執行評定，您必須在管理伺服器上啟用此規則。</span><span class="sxs-lookup"><span data-stu-id="86e38-169">To run the assessment, you must enable the rule on a management server.</span></span> <span data-ttu-id="86e38-170">使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="86e38-170">Use the following steps.</span></span>

#### <a name="enable-the-rule-for-a-specific-management-server"></a><span data-ttu-id="86e38-171">針對特定的管理伺服器啟用此規則</span><span class="sxs-lookup"><span data-stu-id="86e38-171">Enable the rule for a specific management server</span></span>

1. <span data-ttu-id="86e38-172">在 Operations Manager 主控台的 [撰寫] 工作區中，在 [規則] 窗格中搜尋規則「Microsoft System Center Advisor SCOM 評定執行評定規則」。</span><span class="sxs-lookup"><span data-stu-id="86e38-172">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="86e38-173">在搜尋結果中，選取包含文字「類型︰管理伺服器」的規則。</span><span class="sxs-lookup"><span data-stu-id="86e38-173">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="86e38-174">以滑鼠右鍵按一下規則，然後按一下 [覆寫] > [針對以下類別的特定物件: 管理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="86e38-174">Right-click the rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="86e38-175">在可用的管理伺服器清單中，選取應該執行此規則的管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="86e38-175">In the available management servers list, select the management server where the rule should run.</span></span>
5.  <span data-ttu-id="86e38-176">針對 [已啟用] 參數值，務必將覆寫值變更為 [True]。</span><span class="sxs-lookup"><span data-stu-id="86e38-176">Ensure that you change override value to **True** for the **Enabled** parameter value.</span></span>  
    <span data-ttu-id="86e38-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="86e38-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="86e38-178">仍在此視窗中，使用下一個程序來設定執行頻率。</span><span class="sxs-lookup"><span data-stu-id="86e38-178">While still in this window, configure the frequency of the run using the next procedure.</span></span>

#### <a name="configure-the-run-frequency"></a><span data-ttu-id="86e38-179">設定執行頻率</span><span class="sxs-lookup"><span data-stu-id="86e38-179">Configure the run frequency</span></span>

<span data-ttu-id="86e38-180">評定設為每 10,080 分鐘 (或 7 天) 執行一次，此為預設間隔。</span><span class="sxs-lookup"><span data-stu-id="86e38-180">The assessment is configured to run every 10,080 minutes (or seven days), the default interval.</span></span> <span data-ttu-id="86e38-181">您可以將值覆寫為最小值 1440 分鐘 (或一天)。</span><span class="sxs-lookup"><span data-stu-id="86e38-181">You can override the value to a minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="86e38-182">此值代表連續執行評定之間所需的最短時間間隔。</span><span class="sxs-lookup"><span data-stu-id="86e38-182">The value represents the minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="86e38-183">若要覆寫間隔，請使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="86e38-183">To override the interval, use the steps below.</span></span>

1. <span data-ttu-id="86e38-184">在 Operations Manager 主控台的 [撰寫] 工作區中，在 [規則] 窗格中搜尋規則「Microsoft System Center Advisor SCOM 評定執行評定規則」。</span><span class="sxs-lookup"><span data-stu-id="86e38-184">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="86e38-185">在搜尋結果中，選取包含文字「類型︰管理伺服器」的規則。</span><span class="sxs-lookup"><span data-stu-id="86e38-185">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="86e38-186">以滑鼠右鍵按一下規則，然後按一下 [覆寫規則] > [針對以下類別的所有物件: 管理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="86e38-186">Right-click the rule and then click **Override the Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="86e38-187">將 [間隔] 參數值變更為您想要的間隔值。</span><span class="sxs-lookup"><span data-stu-id="86e38-187">Change the **Interval** parameter value to your desired interval value.</span></span> <span data-ttu-id="86e38-188">在下列範例中，此值設為 1440 分鐘 (一天)。</span><span class="sxs-lookup"><span data-stu-id="86e38-188">In the example below, the value is set to 1440 minutes (one day).</span></span>  
    <span data-ttu-id="86e38-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="86e38-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="86e38-190">如果此值設為 1440 分鐘內，則規則會每天執行一次。</span><span class="sxs-lookup"><span data-stu-id="86e38-190">If the value is set to less than 1440 minutes, then the rule runs at a one day interval.</span></span> <span data-ttu-id="86e38-191">在此範例中，此規則會忽略間隔值，且每天執行一次。</span><span class="sxs-lookup"><span data-stu-id="86e38-191">In this example, the rule ignores the interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="86e38-192">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="86e38-192">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="86e38-193">智慧套件會為每項建議指派加權值，該值能顯現建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="86e38-193">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="86e38-194">只會顯示最重要的 10 個建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-194">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="86e38-195">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="86e38-195">How weights are calculated</span></span>

<span data-ttu-id="86e38-196">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="86e38-196">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="86e38-197">識別之疑難引發問題的 *機率* 。</span><span class="sxs-lookup"><span data-stu-id="86e38-197">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="86e38-198">機率較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="86e38-198">A higher probability equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="86e38-199">疑難對組織的 *影響力* (如果確實引發問題)。</span><span class="sxs-lookup"><span data-stu-id="86e38-199">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="86e38-200">影響力較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="86e38-200">A higher impact equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="86e38-201">實作建議所需的 *勞力* 。</span><span class="sxs-lookup"><span data-stu-id="86e38-201">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="86e38-202">勞力較高等同於建議的整體分數較低。</span><span class="sxs-lookup"><span data-stu-id="86e38-202">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="86e38-203">每項建議之加權的表示採用每個焦點區域之總分的百分比。</span><span class="sxs-lookup"><span data-stu-id="86e38-203">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="86e38-204">例如，如果 [可用性與商務持續性] 焦點區域中的建議得分 5%，則實作該建議可讓整個「可用性與商務持續性」分數增加 5%。</span><span class="sxs-lookup"><span data-stu-id="86e38-204">For example, if a recommendation in the Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="86e38-205">焦點區域</span><span class="sxs-lookup"><span data-stu-id="86e38-205">Focus areas</span></span>

<span data-ttu-id="86e38-206">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="86e38-206">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="86e38-207">**效能和延展性** - 這個重點區域會顯示建議來協助貴組織的 IT 基礎結構成長、確定您的 IT 環境是否符合目前的效能需求，而且能夠回應不斷變動的基礎結構需求。</span><span class="sxs-lookup"><span data-stu-id="86e38-207">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="86e38-208">**升級、移轉和部署** - 這個焦點區域會顯示建議，協助您升級、移轉和將 SQL Server 部署至現有的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="86e38-208">**Upgrade, Migration, and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="86e38-209">**作業和監視** - 這個重點區域會顯示建議來協助您的 IT 作業更加順暢、執行預防性維護並將效能最大化。</span><span class="sxs-lookup"><span data-stu-id="86e38-209">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="86e38-210">我應該為每個焦點區域訂定 100% 的分數嗎？</span><span class="sxs-lookup"><span data-stu-id="86e38-210">Should you aim to score 100% in every focus area?</span></span>

<span data-ttu-id="86e38-211">不一定。</span><span class="sxs-lookup"><span data-stu-id="86e38-211">Not necessarily.</span></span> <span data-ttu-id="86e38-212">建議乃源自 Microsoft 工程師上千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="86e38-212">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="86e38-213">然而，世界上沒有兩個一模一樣的伺服器基礎結構，因此特定建議與您的關聯性可能會有所增減。</span><span class="sxs-lookup"><span data-stu-id="86e38-213">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="86e38-214">例如，如果您的虛擬機器並未暴露在網際網路中，某些安全性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="86e38-214">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="86e38-215">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="86e38-215">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="86e38-216">會對成熟企業造成重大影響的問題，不見得會對新公司造成同等嚴重的影響。</span><span class="sxs-lookup"><span data-stu-id="86e38-216">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="86e38-217">因此，建議您先找出自己的優先焦點區域，然後觀察一段時間內的分數變化。</span><span class="sxs-lookup"><span data-stu-id="86e38-217">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="86e38-218">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="86e38-218">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="86e38-219">根據您的 IT 服務性質和組織的商務需求，請使用本指引來評估是否適合實作建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-219">Use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="86e38-220">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="86e38-220">Use assessment focus area recommendations</span></span>

<span data-ttu-id="86e38-221">在使用 OMS 中的評估方案之前，您必須先安裝方案。</span><span class="sxs-lookup"><span data-stu-id="86e38-221">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="86e38-222">如需閱讀安裝方案的更多資訊，請參閱 [從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="86e38-222">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="86e38-223">安裝之後，您可以在 OMS 的 [概觀] 頁面上，使用 [System Center Operations Manager 評定] 圖格來檢視建議摘要。</span><span class="sxs-lookup"><span data-stu-id="86e38-223">After it is installed, you can view the summary of recommendations by using the System Center Operations Manager Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="86e38-224">檢視基礎結構的總結法務遵循評估結果，然後再深入鑽研建議事項。</span><span class="sxs-lookup"><span data-stu-id="86e38-224">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="86e38-225">檢視的焦點區域的建議並採取更正措施</span><span class="sxs-lookup"><span data-stu-id="86e38-225">To view recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="86e38-226">在 [概觀] 頁面上，按一下 [System Center Operations Manager 評定] 圖格。</span><span class="sxs-lookup"><span data-stu-id="86e38-226">On the **Overview** page, click the **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="86e38-227">在 [System Center Operations Manager 評定] 頁面上，檢閱其中一個焦點區域刀鋒視窗中的摘要資訊，然後按一下一個刀鋒視窗來檢視該焦點區域的建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-227">On the **System Center Operations Manager Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="86e38-228">在任一焦點區域頁面中，您可以檢視針對環境且按照優先順序排列的建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-228">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="86e38-229">按一下 [受影響的物件]  下方的建議，可檢視建議提出原因的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="86e38-229">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="86e38-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="86e38-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="86e38-231">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="86e38-231">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="86e38-232">當您解決某個項目後，後續評估會記錄您實施的建議動作並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="86e38-232">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="86e38-233">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="86e38-233">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="86e38-234">忽略建議</span><span class="sxs-lookup"><span data-stu-id="86e38-234">Ignore recommendations</span></span>

<span data-ttu-id="86e38-235">如果您有想要忽略的建議，您可以建立文字檔，供 OMS 用來防止建議出現在評定結果中。</span><span class="sxs-lookup"><span data-stu-id="86e38-235">If you have recommendations that you want to ignore, you can create a text file that OMS uses to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-want-to-ignore"></a><span data-ttu-id="86e38-236">若要識別您想要忽略的建議</span><span class="sxs-lookup"><span data-stu-id="86e38-236">To identify recommendations that you want to ignore</span></span>

1. <span data-ttu-id="86e38-237">登入您的工作區，並開啟記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="86e38-237">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="86e38-238">使用下列查詢來列出您環境中電腦的失敗建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-238">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="86e38-239">以下是顯示記錄檔搜尋查詢的螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="86e38-239">Here's a screen shot showing the Log Search query:</span></span>  
    ![log search](./media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="86e38-241">選擇您想要忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-241">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="86e38-242">在下一個程序中，您將使用 RecommendationId 的值。</span><span class="sxs-lookup"><span data-stu-id="86e38-242">You'll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="86e38-243">建立及使用 IgnoreRecommendations.txt 文字檔案</span><span class="sxs-lookup"><span data-stu-id="86e38-243">To create and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="86e38-244">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="86e38-244">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="86e38-245">在個別行上貼上或輸入您想要 OMS 忽略之每個建議的各個 RecommendationId，然後儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="86e38-245">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="86e38-246">將檔案放在您想要 OMS 忽略建議之每一部電腦的下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="86e38-246">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
4. <span data-ttu-id="86e38-247">在 Operations Manager 管理伺服器上 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server。</span><span class="sxs-lookup"><span data-stu-id="86e38-247">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="86e38-248">驗證已忽略建議</span><span class="sxs-lookup"><span data-stu-id="86e38-248">To verify that recommendations are ignored</span></span>

1. <span data-ttu-id="86e38-249">在執行下一個排定的評估之後 (依預設是每隔 7 天)，指定的建議會標示為 [已略過]，且不會出現在評定儀表板中。</span><span class="sxs-lookup"><span data-stu-id="86e38-249">After the next scheduled assessment runs, by default every seven days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="86e38-250">您可以使用下列記錄搜尋查詢列出所有已忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-250">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="86e38-251">如果您稍後決定想要查看忽略的建議，請移除任何 IgnoreRecommendations.txt 檔案，或從中移除 RecommendationID。</span><span class="sxs-lookup"><span data-stu-id="86e38-251">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="86e38-252">System Center Operations Manager 評定解決方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="86e38-252">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="86e38-253">*我已將評定解決方案新增至 OMS 工作區。但沒看到建議。為什麼？*</span><span class="sxs-lookup"><span data-stu-id="86e38-253">*I added the assessment solution to my OMS workspace. But I don’t see the recommendations. Why not?*</span></span> <span data-ttu-id="86e38-254">新增解決方案之後，請使用下列步驟在 OMS 儀表板上檢視建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-254">After adding the solution, use the following steps view the recommendations on the OMS dashboard.</span></span>  

- [<span data-ttu-id="86e38-255">設定 System Center Operations Manager 評定的執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="86e38-255">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="86e38-256">設定 System Center Operations Manager 評定規則</span><span class="sxs-lookup"><span data-stu-id="86e38-256">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="86e38-257">*是否有設定評估執行頻率的方法？*</span><span class="sxs-lookup"><span data-stu-id="86e38-257">*Is there a way to configure how often the assessment runs?*</span></span> <span data-ttu-id="86e38-258">是。</span><span class="sxs-lookup"><span data-stu-id="86e38-258">Yes.</span></span> <span data-ttu-id="86e38-259">請參閱[設定執行頻率](#configure-the-run-frequency)。</span><span class="sxs-lookup"><span data-stu-id="86e38-259">See [Configure the run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="86e38-260">如果在我新增 System Center Operations Manager 評定解決方案之後探索到另一部伺服器，也會評估這部伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="86e38-260">*If another server is discovered after I’ve added the System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="86e38-261">是，在探索之後，從那時起也會評估它 -- 預設是每隔 7 天。</span><span class="sxs-lookup"><span data-stu-id="86e38-261">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="86e38-262">*負責收集資料之處理序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="86e38-262">*What is the name of the process that does the data collection?*</span></span> <span data-ttu-id="86e38-263">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="86e38-263">AdvisorAssessment.exe</span></span>

<span data-ttu-id="86e38-264">AdvisorAssessment.exe 程序在哪裡執行？</span><span class="sxs-lookup"><span data-stu-id="86e38-264">*Where does the AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="86e38-265">AdvisorAssessment.exe 會在啟用評定規則的管理伺服器的 HealthService 之下執行。</span><span class="sxs-lookup"><span data-stu-id="86e38-265">AdvisorAssessment.exe runs under the HealthService of the management server where the assessment rule is enabled.</span></span> <span data-ttu-id="86e38-266">使用這個程序時，將會透過遠端資料收集來探索您的整個環境。</span><span class="sxs-lookup"><span data-stu-id="86e38-266">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="86e38-267">收集資料需要花費多少時間？</span><span class="sxs-lookup"><span data-stu-id="86e38-267">*How long does it take for data collection?*</span></span> <span data-ttu-id="86e38-268">在伺服器上資料收集需要花費約 1 小時。</span><span class="sxs-lookup"><span data-stu-id="86e38-268">Data collection on the server takes about one hour.</span></span> <span data-ttu-id="86e38-269">在有許多 Operations Manager 執行個體或資料庫的環境中可能更久。</span><span class="sxs-lookup"><span data-stu-id="86e38-269">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="86e38-270">如果我將評定間隔設為少於 1440 分鐘會怎樣？</span><span class="sxs-lookup"><span data-stu-id="86e38-270">*What if I set the interval of the assessment to less than 1440 minutes?*</span></span> <span data-ttu-id="86e38-271">評定已預先設定為最多一天執行一次。</span><span class="sxs-lookup"><span data-stu-id="86e38-271">The assessment is pre-configured to run at a maximum of once per day.</span></span> <span data-ttu-id="86e38-272">如果您將間隔值覆寫為少於 1440 分鐘的值，則評定會使用 1440 分鐘做為間隔值。</span><span class="sxs-lookup"><span data-stu-id="86e38-272">If you override the interval value to a value less than 1440 minutes, then the assessment uses 1440 minutes as the interval value.</span></span>

<span data-ttu-id="86e38-273">如何知道是否未通過必要條件？</span><span class="sxs-lookup"><span data-stu-id="86e38-273">*How to know if there are pre-requisite failures?*</span></span> <span data-ttu-id="86e38-274">如果評定已執行，但您沒有看到結果，很可能是評定的某些必要條件未通過。</span><span class="sxs-lookup"><span data-stu-id="86e38-274">If the assessment ran and you don't see results, then it is likely that some of the pre-requisites for the assessment failed.</span></span> <span data-ttu-id="86e38-275">您可以在記錄檔搜尋中執行查詢︰`Type=Operation Solution=SCOMAssessment` 和 `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites`，以查看未通過的必要條件。</span><span class="sxs-lookup"><span data-stu-id="86e38-275">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search to see the failed pre-requisites.</span></span>

<span data-ttu-id="86e38-276">*必要條件未通過中出現 `Failed to connect to the SQL Instance (….).` 訊息。有什麼問題？*</span><span class="sxs-lookup"><span data-stu-id="86e38-276">*There is a `Failed to connect to the SQL Instance (….).` message in pre-requisite failures. What is the issue?*</span></span> <span data-ttu-id="86e38-277">管理伺服器的 HealthService 之下會執行資料收集程序 AdvisorAssessment.exe。</span><span class="sxs-lookup"><span data-stu-id="86e38-277">AdvisorAssessment.exe, the process that collects data, runs under the HealthService of the management server.</span></span> <span data-ttu-id="86e38-278">在評定過程中，此程序會嘗試連接至 Operations Manager 資料庫所在的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="86e38-278">As part of the assessment, the process attempts to connect to the SQL Server where the Operations Manager database is present.</span></span> <span data-ttu-id="86e38-279">當防火牆規則封鎖 SQL Server 執行個體的連接時，就會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="86e38-279">This error can occur when firewall rules block the connection to the SQL Server instance.</span></span>

<span data-ttu-id="86e38-280">*收集的資料類型為何？*</span><span class="sxs-lookup"><span data-stu-id="86e38-280">*What type of data is collected?*</span></span> <span data-ttu-id="86e38-281">透過 Windows PowerShell、SQL 查詢和檔案資訊收集器收集的資料類型如下︰WMI 資料 - 登錄資料 - 事件記錄檔資料 - Operations Manager 資料。</span><span class="sxs-lookup"><span data-stu-id="86e38-281">The following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="86e38-282">*為什麼我必須設定執行身分帳戶？*</span><span class="sxs-lookup"><span data-stu-id="86e38-282">*Why do I have to configure a Run As Account?*</span></span> <span data-ttu-id="86e38-283">Operations Manager 伺服器上會執行各種 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="86e38-283">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="86e38-284">您必須使用具有必要權限的執行身分帳戶，它們才能夠執行。</span><span class="sxs-lookup"><span data-stu-id="86e38-284">In order for them to run, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="86e38-285">此外，查詢 WMI 還需要本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="86e38-285">In addition, local administrator credentials are required to query WMI.</span></span>

<span data-ttu-id="86e38-286">*為什麼只顯示前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="86e38-286">*Why display only the top 10 recommendations?*</span></span> <span data-ttu-id="86e38-287">與其列出鉅細靡遺的工作清單，我們建議您先專注於解決優先的建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-287">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="86e38-288">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-288">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="86e38-289">如果您想要查看詳細清單，可以使用記錄檔搜尋來檢視所有建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-289">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="86e38-290">*是否有忽略建議的方法？*</span><span class="sxs-lookup"><span data-stu-id="86e38-290">*Is there a way to ignore a recommendation?*</span></span> <span data-ttu-id="86e38-291">是，請參閱[忽略建議](#Ignore-recommendations)。</span><span class="sxs-lookup"><span data-stu-id="86e38-291">Yes, see the [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="86e38-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86e38-292">Next steps</span></span>

- <span data-ttu-id="86e38-293">[搜尋記錄檔](log-analytics-log-searches.md)，以檢視詳細的 System Center Operations Manager 評定資料和建議。</span><span class="sxs-lookup"><span data-stu-id="86e38-293">[Search logs](log-analytics-log-searches.md) to view detailed System Center Operations Manager Assessment data and recommendations.</span></span>
