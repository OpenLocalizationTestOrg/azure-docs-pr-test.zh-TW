---
title: "使用 Azure Log Analytics 最佳化 SQL Server 環境 | Microsoft Docs"
description: "透過 Azure Log Analytics，您可以使用 SQL 評估方案，定期評估 SQL 伺服器環境的風險和健全狀況。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="8c598-103">在 Log Analytics 中使用 SQL 評估方案最佳化 SQL Server 環境</span><span class="sxs-lookup"><span data-stu-id="8c598-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![SQL 評定符號](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="8c598-105">您可以使用 SQL 評估方案定期評估伺服器環境的風險和健全狀況。</span><span class="sxs-lookup"><span data-stu-id="8c598-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="8c598-106">本文將協助您安裝方案，讓您可以針對潛在問題採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="8c598-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="8c598-107">此方案能針對已部署的伺服器基礎結構提供依照優先順序排列的具體建議清單。</span><span class="sxs-lookup"><span data-stu-id="8c598-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="8c598-108">建議分為六個焦點領域，它們可以幫助您快速了解風險並採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="8c598-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="8c598-109">智慧套件提供的建議乃源自 Microsoft 工程師數千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="8c598-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="8c598-110">每項建議均提供問題的影響層面，以及如何實作建議變更等相關指引。</span><span class="sxs-lookup"><span data-stu-id="8c598-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="8c598-111">您可以選擇對組織而言最重要的焦點區域，同時追蹤經營無風險且健康狀態良好之環境的進度。</span><span class="sxs-lookup"><span data-stu-id="8c598-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="8c598-112">加入方案且評估完成之後，系統會將焦點區域的摘要資訊顯示在環境之基礎結構的 [SQL 評估]  儀表板中。</span><span class="sxs-lookup"><span data-stu-id="8c598-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="8c598-113">下列章節說明如何使用 [SQL 評估]  儀表板上的資訊，您可以在這裡檢視 SQL 伺服器基礎結構的建議動作並予以實施。</span><span class="sxs-lookup"><span data-stu-id="8c598-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL 評估磚的影像](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="8c598-116">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="8c598-116">Installing and configuring the solution</span></span>
<span data-ttu-id="8c598-117">SQL 評估適用於 Standard、Developer 和 Enterprise 版本之 SQL Server 目前支援的所有版本。</span><span class="sxs-lookup"><span data-stu-id="8c598-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="8c598-118">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="8c598-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="8c598-119">代理程式必須安裝於已安裝 SQL Server 的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8c598-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="8c598-120">SQL 評估方案需要在具有 OMS 代理程式的每部電腦上安裝 .NET Framework 4 的支援版本。</span><span class="sxs-lookup"><span data-stu-id="8c598-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="8c598-121">若要安裝方案，使用者在使用 Azure 入口網站時必須是系統管理員或是 Azure 訂用帳戶的參與者。</span><span class="sxs-lookup"><span data-stu-id="8c598-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="8c598-122">此外，使用者必須是 OMS 入口網站中 OMS 工作區參與者或系統管理員角色的成員。</span><span class="sxs-lookup"><span data-stu-id="8c598-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="8c598-123">搭配使用 Operations Manager 代理程式和 SQL 評估時，您必須使用 Operations Manager 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="8c598-124">如需詳細資訊，請參閱底下的 [OMS 的 Operations Manager 執行身分帳戶](#operations-manager-run-as-accounts-for-oms) 。</span><span class="sxs-lookup"><span data-stu-id="8c598-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8c598-125">MMA 代理程式不支援 Operations Manager 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="8c598-126">使用 [從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)中的程序，將 SQL 評估方案加入您的 OMS 工作區中。</span><span class="sxs-lookup"><span data-stu-id="8c598-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="8c598-127">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="8c598-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="8c598-128">您加入方案之後，AdvisorAssessment.exe 檔案會以代理程式加入伺服器中。</span><span class="sxs-lookup"><span data-stu-id="8c598-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="8c598-129">組態資料會先讀取後再傳送至雲端中的 OMS 服務，以便進行處理。</span><span class="sxs-lookup"><span data-stu-id="8c598-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="8c598-130">會將邏輯套用至接收的資料，且雲端服務會記錄資料。</span><span class="sxs-lookup"><span data-stu-id="8c598-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="8c598-131">SQL 評估資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="8c598-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="8c598-132">SQL 評估會使用您已啟用的代理程式，來收集 WMI 資料、登錄資料、效能資料和 SQL Server 動態管理檢視結果。</span><span class="sxs-lookup"><span data-stu-id="8c598-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="8c598-133">下表顯示代理程式的資料收集方法、是否需要 Operations Manager (SCOM)，以及如何代理程式收集資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="8c598-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="8c598-134">平台</span><span class="sxs-lookup"><span data-stu-id="8c598-134">platform</span></span> | <span data-ttu-id="8c598-135">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="8c598-135">Direct Agent</span></span> | <span data-ttu-id="8c598-136">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="8c598-136">SCOM agent</span></span> | <span data-ttu-id="8c598-137">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="8c598-137">Azure Storage</span></span> | <span data-ttu-id="8c598-138">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="8c598-138">SCOM required?</span></span> | <span data-ttu-id="8c598-139">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="8c598-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="8c598-140">收集頻率</span><span class="sxs-lookup"><span data-stu-id="8c598-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8c598-141">Windows</span><span class="sxs-lookup"><span data-stu-id="8c598-141">Windows</span></span> | <span data-ttu-id="8c598-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="8c598-142">&#8226;</span></span> | <span data-ttu-id="8c598-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="8c598-143">&#8226;</span></span> |  |  | <span data-ttu-id="8c598-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="8c598-144">&#8226;</span></span> |<span data-ttu-id="8c598-145">7 天</span><span class="sxs-lookup"><span data-stu-id="8c598-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="8c598-146">OMS 的 Operations Manager 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="8c598-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="8c598-147">OMS 中的 Log Analytics 會使用 Operations Manager 代理程式及管理群組，收集資料並將資料傳送給 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="8c598-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="8c598-148">OMS 會建立工作負載的管理套件以提供加值服務。</span><span class="sxs-lookup"><span data-stu-id="8c598-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="8c598-149">每個工作負載都需要具有特定的工作負載權限，才能在不同的安全性內容中執行管理套件，例如網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="8c598-150">您需要藉由設定 Operations Manager 執行身分帳戶來提供認證資訊。</span><span class="sxs-lookup"><span data-stu-id="8c598-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="8c598-151">請使用下列資訊來設定 SQL 評估的 Operations Manager 執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="8c598-152">設定 SQL 評估的執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="8c598-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="8c598-153">如果您已經在使用 SQL Server 管理套件，您應該使用該執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="8c598-154">在 Operations 主控台中設定 SQL 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="8c598-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="8c598-155">如果您使用 OMS 直接代理程式，而不是 SCOM 代理程式，則管理組件一律會在本機系統帳戶的安全性內容中執行。</span><span class="sxs-lookup"><span data-stu-id="8c598-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="8c598-156">略過下列的步驟 1-5，並執行 T-SQL 或 Powershell 範例，指定 NT AUTHORITY\SYSTEM 做為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8c598-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="8c598-157">在 Operations Manager 中開啟 Operations 主控台，然後按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="8c598-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="8c598-158">在 [執行身分組態] 下方，按一下 [設定檔]，並開啟 [OMS SQL 評估執行身分設定檔]。</span><span class="sxs-lookup"><span data-stu-id="8c598-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="8c598-159">在 [執行身分帳戶] 頁面上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8c598-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="8c598-160">選取包含 SQL Server 所需認證的 Windows 執行身分帳戶，或按一下 [新增]  建立一個。</span><span class="sxs-lookup"><span data-stu-id="8c598-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c598-161">執行身分帳戶類型必須是 Windows。</span><span class="sxs-lookup"><span data-stu-id="8c598-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="8c598-162">執行身分帳戶也必須屬於裝載 SQL Server 執行個體的所有 Windows 伺服器上的本機系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="8c598-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="8c598-163">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8c598-163">Click **Save**.</span></span>
6. <span data-ttu-id="8c598-164">修改，然後在每個 SQL Server 執行個體上執行下列 T-SQL 範例，授與執行身分帳戶所需的最小權限授以執行 SQL 評估。</span><span class="sxs-lookup"><span data-stu-id="8c598-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="8c598-165">不過，如果執行身分帳戶已是 SQL Server 執行個體上 sysadmin 伺服器角色的一部分，您就不需要這樣做。</span><span class="sxs-lookup"><span data-stu-id="8c598-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="8c598-166">使用 Windows PowerShell 設定 SQL 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="8c598-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="8c598-167">以您的資訊更新它之後，開啟 PowerShell 視窗並執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="8c598-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="8c598-168">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="8c598-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="8c598-169">智慧套件會為每項建議指派加權值，該值能顯現建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="8c598-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="8c598-170">唯有重要性排行前十名的建議會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="8c598-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="8c598-171">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="8c598-171">How weights are calculated</span></span>
<span data-ttu-id="8c598-172">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="8c598-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="8c598-173">識別之疑難引發問題的 *機率* 。</span><span class="sxs-lookup"><span data-stu-id="8c598-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="8c598-174">機率較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="8c598-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="8c598-175">疑難對組織的 *影響力* (如果確實引發問題)。</span><span class="sxs-lookup"><span data-stu-id="8c598-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="8c598-176">影響力較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="8c598-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="8c598-177">實作建議所需的 *勞力* 。</span><span class="sxs-lookup"><span data-stu-id="8c598-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="8c598-178">勞力較高等同於建議的整體分數較低。</span><span class="sxs-lookup"><span data-stu-id="8c598-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="8c598-179">每項建議之加權的表示採用每個焦點區域之總分的百分比。</span><span class="sxs-lookup"><span data-stu-id="8c598-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="8c598-180">例如，如果針對安全性和法務遵循焦點區域之建議的分數為 5%，代表實作該項建議能增加 5% 的安全性和法務遵循整體分數。</span><span class="sxs-lookup"><span data-stu-id="8c598-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="8c598-181">焦點區域</span><span class="sxs-lookup"><span data-stu-id="8c598-181">Focus areas</span></span>
<span data-ttu-id="8c598-182">**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。</span><span class="sxs-lookup"><span data-stu-id="8c598-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="8c598-183">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="8c598-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="8c598-184">**效能和延展性** - 這個重點區域會顯示建議來協助貴組織的 IT 基礎結構成長、確定您的 IT 環境是否符合目前的效能需求，而且能夠回應不斷變動的基礎結構需求。</span><span class="sxs-lookup"><span data-stu-id="8c598-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="8c598-185">**升級、移轉和部署** - 這個重點區域會顯示建議來協助您升級、移轉和將 SQL Server 部署到您的現有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="8c598-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="8c598-186">**作業和監視** - 這個重點區域會顯示建議來協助您的 IT 作業更加順暢、執行預防性維護並將效能最大化。</span><span class="sxs-lookup"><span data-stu-id="8c598-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="8c598-187">**變更和組態管理** - 這個重點區域會顯示建議來協助保護每日作業，確保變更不會對您的基礎結構造成負面影響，同時建立變更控管程序，並追蹤及審核系統組態。</span><span class="sxs-lookup"><span data-stu-id="8c598-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="8c598-188">我應該為每個焦點區域訂定 100% 的分數嗎？</span><span class="sxs-lookup"><span data-stu-id="8c598-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="8c598-189">不一定。</span><span class="sxs-lookup"><span data-stu-id="8c598-189">Not necessarily.</span></span> <span data-ttu-id="8c598-190">建議乃源自 Microsoft 工程師上千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="8c598-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="8c598-191">然而，世界上沒有兩個一模一樣的伺服器基礎結構，因此特定建議與您的關聯性可能會有所增減。</span><span class="sxs-lookup"><span data-stu-id="8c598-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="8c598-192">例如，如果您的虛擬機器並未暴露在網際網路中，某些安全性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="8c598-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="8c598-193">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="8c598-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="8c598-194">會對成熟企業造成重大影響的問題，不見得會對新公司造成同等嚴重的影響。</span><span class="sxs-lookup"><span data-stu-id="8c598-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="8c598-195">因此，建議您先找出自己的優先焦點區域，然後觀察一段時間內的分數變化。</span><span class="sxs-lookup"><span data-stu-id="8c598-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="8c598-196">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="8c598-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="8c598-197">在已知 IT 服務之本質和組織之商務需求的情況下，您應使用該指引來評估實作建議的適當性。</span><span class="sxs-lookup"><span data-stu-id="8c598-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="8c598-198">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="8c598-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="8c598-199">在使用 OMS 中的評估方案之前，您必須先安裝方案。</span><span class="sxs-lookup"><span data-stu-id="8c598-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="8c598-200">如需閱讀安裝方案的更多資訊，請參閱 [從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="8c598-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="8c598-201">安裝之後，您可以在 OMS 中使用 [概觀] 頁面上的 [SQL 評估] 圖格檢視建議摘要。</span><span class="sxs-lookup"><span data-stu-id="8c598-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="8c598-202">檢視基礎結構的總結法務遵循評估結果，然後再深入鑽研建議事項。</span><span class="sxs-lookup"><span data-stu-id="8c598-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="8c598-203">檢視的焦點區域的建議並採取更正措施</span><span class="sxs-lookup"><span data-stu-id="8c598-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="8c598-204">在 [概觀] 頁面上，按一下 [SQL 評估] 圖格。</span><span class="sxs-lookup"><span data-stu-id="8c598-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="8c598-205">在 [SQL 評估] 頁面中，檢閱任一焦點區域刀鋒視窗中的摘要資訊，然後按一下焦點區域以檢視建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="8c598-206">在任一焦點區域頁面中，您可以檢視針對環境且按照優先順序排列的建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="8c598-207">按一下 [受影響的物件]  下方的建議，可檢視建議提出原因的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8c598-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="8c598-208">![SQL 評定建議圖片](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="8c598-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="8c598-209">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="8c598-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="8c598-210">當您解決某個項目後，後續評估會記錄您實施的建議動作並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="8c598-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="8c598-211">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="8c598-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="8c598-212">忽略建議</span><span class="sxs-lookup"><span data-stu-id="8c598-212">Ignore recommendations</span></span>
<span data-ttu-id="8c598-213">如果您有想要忽略的建議，則可以建立 OMS 將用來防止建議出現在您評估結果的文字檔。</span><span class="sxs-lookup"><span data-stu-id="8c598-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="8c598-214">識別您將忽略的建議</span><span class="sxs-lookup"><span data-stu-id="8c598-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="8c598-215">登入您的工作區，並開啟記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="8c598-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="8c598-216">使用下列查詢來列出您環境中電腦的失敗建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="8c598-217">以下是顯示記錄檔搜尋查詢的螢幕擷取畫面︰![失敗的建議](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="8c598-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="8c598-218">選擇您想要忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="8c598-219">您將使用下一個程序中的 RecommendationId 值。</span><span class="sxs-lookup"><span data-stu-id="8c598-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="8c598-220">建立及使用 IgnoreRecommendations.txt 文字檔案</span><span class="sxs-lookup"><span data-stu-id="8c598-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="8c598-221">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="8c598-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="8c598-222">在個別行上貼上或輸入您想要 OMS 忽略之每個建議的各個 RecommendationId，然後儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="8c598-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="8c598-223">將檔案放在您想要 OMS 忽略建議之每一部電腦的下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8c598-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="8c598-224">在具有 Microsoft Monitoring Agent 的電腦 (直接連線或透過 Operations Manager 連線) 上 - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="8c598-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="8c598-225">在 Operations Manager 管理伺服器上 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="8c598-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="8c598-226">驗證已忽略建議</span><span class="sxs-lookup"><span data-stu-id="8c598-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="8c598-227">在執行下一個排定的評估之後，依預設是每隔 7 天執行一次，指定的建議會標示為忽略，且不會出現在評估儀表板。</span><span class="sxs-lookup"><span data-stu-id="8c598-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="8c598-228">您可以使用下列記錄搜尋查詢列出所有已忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="8c598-229">如果您稍後決定想要查看忽略的建議，請移除任何 IgnoreRecommendations.txt 檔案，或從中移除 RecommendationID。</span><span class="sxs-lookup"><span data-stu-id="8c598-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="8c598-230">SQL 評估方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="8c598-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="8c598-231">*評估的執行頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="8c598-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="8c598-232">評估會每隔 7 天執行一次。</span><span class="sxs-lookup"><span data-stu-id="8c598-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="8c598-233">*是否有設定評估執行頻率的方法？*</span><span class="sxs-lookup"><span data-stu-id="8c598-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="8c598-234">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="8c598-234">Not at this time.</span></span>

<span data-ttu-id="8c598-235">*如果我在加入 SQL 評估方案後探索到另一部伺服器，方案也會評估這部伺服器嗎？*</span><span class="sxs-lookup"><span data-stu-id="8c598-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="8c598-236">是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。</span><span class="sxs-lookup"><span data-stu-id="8c598-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="8c598-237">*如果把伺服器除役，何時能將它從評估中移除？*</span><span class="sxs-lookup"><span data-stu-id="8c598-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="8c598-238">如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。</span><span class="sxs-lookup"><span data-stu-id="8c598-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="8c598-239">*負責收集資料之處理序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="8c598-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="8c598-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="8c598-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="8c598-241">*收集資料需要花費多少時間？*</span><span class="sxs-lookup"><span data-stu-id="8c598-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="8c598-242">伺服器上的實際資料收集需費時約 1 小時。</span><span class="sxs-lookup"><span data-stu-id="8c598-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="8c598-243">對於擁有大量 SQL 執行個體或資料庫的伺服器，資料收集可能需要花費更久的時間。</span><span class="sxs-lookup"><span data-stu-id="8c598-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="8c598-244">*收集的資料類型為何？*</span><span class="sxs-lookup"><span data-stu-id="8c598-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="8c598-245">收集的資料類型如下：</span><span class="sxs-lookup"><span data-stu-id="8c598-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="8c598-246">WMI</span><span class="sxs-lookup"><span data-stu-id="8c598-246">WMI</span></span>
  * <span data-ttu-id="8c598-247">登錄</span><span class="sxs-lookup"><span data-stu-id="8c598-247">Registry</span></span>
  * <span data-ttu-id="8c598-248">效能計數器</span><span class="sxs-lookup"><span data-stu-id="8c598-248">Performance counters</span></span>
  * <span data-ttu-id="8c598-249">SQL 動態管理檢視 (DMV)。</span><span class="sxs-lookup"><span data-stu-id="8c598-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="8c598-250">*是否有設定資料收集時間的方法？*</span><span class="sxs-lookup"><span data-stu-id="8c598-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="8c598-251">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="8c598-251">Not at this time.</span></span>

<span data-ttu-id="8c598-252">*為什麼我必須設定執行身分帳戶？*</span><span class="sxs-lookup"><span data-stu-id="8c598-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="8c598-253">智慧套件會針對 SQL Server 執行少量的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="8c598-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="8c598-254">為了要執行 SQL 查詢，智慧套件必須使用具備「檢視伺服器狀態」權限的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c598-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="8c598-255">此外，為了要查詢 WMI，智慧套件還需要本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="8c598-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="8c598-256">*為什麼只顯示前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="8c598-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="8c598-257">與其提供鉅細靡遺的工作清單，我們建議您先著重於解決優先建議事項。</span><span class="sxs-lookup"><span data-stu-id="8c598-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="8c598-258">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="8c598-259">如果您想要查看詳細清單，可以使用 OMS 記錄搜尋來檢視所有建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="8c598-260">*是否有忽略建議的方法？*</span><span class="sxs-lookup"><span data-stu-id="8c598-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="8c598-261">是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。</span><span class="sxs-lookup"><span data-stu-id="8c598-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c598-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c598-262">Next steps</span></span>
* <span data-ttu-id="8c598-263">[搜尋記錄檔](log-analytics-log-searches.md) 以檢視詳細的 SQL 評估資料和建議。</span><span class="sxs-lookup"><span data-stu-id="8c598-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
