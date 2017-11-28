---
title: "aaaOptimize Azure 記錄分析 SQL Server 環境 |Microsoft 文件"
description: "Azure 記錄分析，您可以使用 hello SQL 評估解決方案 tooassess hello 風險和 SQL server 環境的健全狀況規則的間隔。"
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
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="30bed-103">最佳化 SQL Server 環境以 hello 記錄分析中的 SQL 評估解決方案</span><span class="sxs-lookup"><span data-stu-id="30bed-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![SQL 評定符號](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="30bed-105">您可以使用 SQL 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="30bed-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="30bed-106">本文將協助您安裝 hello 解決方案，讓您可以採取修正動作，可能的問題。</span><span class="sxs-lookup"><span data-stu-id="30bed-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="30bed-107">此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。</span><span class="sxs-lookup"><span data-stu-id="30bed-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="30bed-108">hello 建議是跨六個焦點領域，它們可以協助您快速了解 hello 風險並採取更正措施分類。</span><span class="sxs-lookup"><span data-stu-id="30bed-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="30bed-109">hello 所提供的建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。</span><span class="sxs-lookup"><span data-stu-id="30bed-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="30bed-110">每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。</span><span class="sxs-lookup"><span data-stu-id="30bed-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="30bed-111">您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。</span><span class="sxs-lookup"><span data-stu-id="30bed-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="30bed-112">焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **SQL 評估**hello 基礎結構，您的環境中的儀表板。</span><span class="sxs-lookup"><span data-stu-id="30bed-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="30bed-113">hello 下列各節說明如何 toouse hello 有關 hello **SQL 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 SQL server 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="30bed-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL 評估磚的影像](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="30bed-116">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="30bed-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="30bed-117">SQL 評估適用於所有目前支援的 hello Standard、 Developer 和 Enterprise 版本的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="30bed-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="30bed-118">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="30bed-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="30bed-119">代理程式必須安裝於已安裝 SQL Server 的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="30bed-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="30bed-120">hello SQL 評估解決方案需要內含的 OMS 代理程式的每部電腦上安裝的.NET Framework 4 支援的版本。</span><span class="sxs-lookup"><span data-stu-id="30bed-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="30bed-121">在訂單 tooinstall hello 解決方案中，hello 使用者 Azure 訂用帳戶系統管理員或參與者 toohello 時必須使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="30bed-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="30bed-122">此外，hello 使用者必須是 hello OMS 工作區參與者或系統管理員角色 hello OMS 入口網站中的成員。</span><span class="sxs-lookup"><span data-stu-id="30bed-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="30bed-123">當使用 SQL 評估 hello Operations Manager 代理程式，您將需要 toouse Operations Manager Run-As 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30bed-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="30bed-124">如需詳細資訊，請參閱底下的 [OMS 的 Operations Manager 執行身分帳戶](#operations-manager-run-as-accounts-for-oms) 。</span><span class="sxs-lookup"><span data-stu-id="30bed-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="30bed-125">hello MMA 代理程式不支援 Operations Manager Run-As 帳戶。</span><span class="sxs-lookup"><span data-stu-id="30bed-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="30bed-126">新增使用 hello 程序的 OMS 工作區中所述的 hello SQL 評估解決方案 tooyour [hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="30bed-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="30bed-127">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="30bed-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="30bed-128">您加入 hello 方案之後，hello AdvisorAssessment.exe 檔案加入 tooservers 與代理程式。</span><span class="sxs-lookup"><span data-stu-id="30bed-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="30bed-129">讀取組態資料及傳送 toohello OMS 服務進行處理的 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="30bed-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="30bed-130">邏輯是套用的 toohello 接收資料，而 hello 雲端服務會記錄 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="30bed-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="30bed-131">SQL 評估資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="30bed-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="30bed-132">SQL 評估收集 WMI 資料、 登錄資料、 效能資料，以及使用您已啟用的 hello 代理程式的 SQL Server 動態管理檢視結果。</span><span class="sxs-lookup"><span data-stu-id="30bed-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="30bed-133">hello 下表顯示資料收集方法，代理程式是否 Operations Manager (SCOM) 為必要項，以及如何通常資料會收集代理程式。</span><span class="sxs-lookup"><span data-stu-id="30bed-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="30bed-134">平台</span><span class="sxs-lookup"><span data-stu-id="30bed-134">platform</span></span> | <span data-ttu-id="30bed-135">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="30bed-135">Direct Agent</span></span> | <span data-ttu-id="30bed-136">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="30bed-136">SCOM agent</span></span> | <span data-ttu-id="30bed-137">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="30bed-137">Azure Storage</span></span> | <span data-ttu-id="30bed-138">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="30bed-138">SCOM required?</span></span> | <span data-ttu-id="30bed-139">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="30bed-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="30bed-140">收集頻率</span><span class="sxs-lookup"><span data-stu-id="30bed-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="30bed-141">Windows</span><span class="sxs-lookup"><span data-stu-id="30bed-141">Windows</span></span> | <span data-ttu-id="30bed-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="30bed-142">&#8226;</span></span> | <span data-ttu-id="30bed-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="30bed-143">&#8226;</span></span> |  |  | <span data-ttu-id="30bed-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="30bed-144">&#8226;</span></span> |<span data-ttu-id="30bed-145">7 天</span><span class="sxs-lookup"><span data-stu-id="30bed-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="30bed-146">OMS 的 Operations Manager 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="30bed-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="30bed-147">在 OMS 中的記錄分析會使用 hello Operations Manager 代理程式和管理群組 toocollect，並傳送資料 toohello OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="30bed-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="30bed-148">OMS 會在工作負載 tooprovide 的管理組件時建立具有附加價值的服務。</span><span class="sxs-lookup"><span data-stu-id="30bed-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="30bed-149">每個工作負載需要在不同的安全性內容中，例如網域帳戶的工作負載特定權限 toorun 管理組件。</span><span class="sxs-lookup"><span data-stu-id="30bed-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="30bed-150">您藉由設定 Operations Manager 執行身分帳戶需要 tooprovide 認證資訊。</span><span class="sxs-lookup"><span data-stu-id="30bed-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="30bed-151">使用下列資訊 tooset hello Operations Manager 執行身分帳戶的 SQL 評估 hello。</span><span class="sxs-lookup"><span data-stu-id="30bed-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="30bed-152">設定 hello 執行身分帳戶的 SQL 評估</span><span class="sxs-lookup"><span data-stu-id="30bed-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="30bed-153">如果您已經在使用 hello SQL Server 管理組件，您應該使用該執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="30bed-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="30bed-154">tooconfigure hello hello Operations 主控台中的 SQL 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="30bed-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="30bed-155">如果您使用 hello OMS 直接代理程式，而不是 hello SCOM 代理程式，hello 管理組件一律會 hello 的 hello 本機系統帳戶的安全性內容中執行。</span><span class="sxs-lookup"><span data-stu-id="30bed-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="30bed-156">略過步驟 1-5，並執行或是 hello T-SQL 或 Powershell 範例中，指定與 hello 使用者名稱的 NT AUTHORITY\SYSTEM。</span><span class="sxs-lookup"><span data-stu-id="30bed-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="30bed-157">在 Operations Manager 中開啟 hello Operations 主控台，然後**管理**。</span><span class="sxs-lookup"><span data-stu-id="30bed-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="30bed-158">在 [執行身分組態] 下方，按一下 [設定檔]，並開啟 [OMS SQL 評估執行身分設定檔]。</span><span class="sxs-lookup"><span data-stu-id="30bed-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="30bed-159">在 hello**執行身分帳戶**頁面上，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="30bed-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="30bed-160">選取包含 SQL Server 所需的 hello 認證的 Windows 執行身分帳戶，或按一下**新增**toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="30bed-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="30bed-161">hello 執行身分帳戶類型必須是 Windows。</span><span class="sxs-lookup"><span data-stu-id="30bed-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="30bed-162">hello 執行身分帳戶也必須是裝載 SQL Server 執行個體的所有 Windows 伺服器上的本機系統管理員群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="30bed-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="30bed-163">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="30bed-163">Click **Save**.</span></span>
6. <span data-ttu-id="30bed-164">修改並執行下列 T-SQL 範例，在每個 SQL Server 執行個體 toogrant 最小權限需要 tooRun 身分帳戶 tooperform SQL 評估 hello。</span><span class="sxs-lookup"><span data-stu-id="30bed-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="30bed-165">不過，您不需要 toodo 這如果執行身分帳戶已是 SQL Server 執行個體上的 hello sysadmin 伺服器角色的一部分。</span><span class="sxs-lookup"><span data-stu-id="30bed-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="30bed-166">tooconfigure hello SQL 執行身分帳戶使用 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="30bed-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="30bed-167">開啟 PowerShell 視窗並執行下列指令碼，在您已更新成您的資訊之後 hello:</span><span class="sxs-lookup"><span data-stu-id="30bed-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="30bed-168">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="30bed-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="30bed-169">每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="30bed-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="30bed-170">只有 hello 十個最重要的建議會出現。</span><span class="sxs-lookup"><span data-stu-id="30bed-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="30bed-171">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="30bed-171">How weights are calculated</span></span>
<span data-ttu-id="30bed-172">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="30bed-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="30bed-173">hello*機率*識別之疑難引發問題。</span><span class="sxs-lookup"><span data-stu-id="30bed-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="30bed-174">較高的機率等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="30bed-175">hello*影響*hello 問題如果確實引發問題對您組織。</span><span class="sxs-lookup"><span data-stu-id="30bed-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="30bed-176">較高的影響等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="30bed-177">hello*投入時間*需要 tooimplement hello 建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="30bed-178">勞力較高 tooa 整體分數較低的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="30bed-179">每個建議的加權 hello hello 總分每個焦點區域的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="30bed-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="30bed-180">例如，如果 hello 安全性和相容性的焦點區域建議的分數為 5%，實作該項建議將會增加您整體安全性和法規遵循分數 5%。</span><span class="sxs-lookup"><span data-stu-id="30bed-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="30bed-181">焦點區域</span><span class="sxs-lookup"><span data-stu-id="30bed-181">Focus areas</span></span>
<span data-ttu-id="30bed-182">**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。</span><span class="sxs-lookup"><span data-stu-id="30bed-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="30bed-183">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="30bed-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="30bed-184">**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。</span><span class="sxs-lookup"><span data-stu-id="30bed-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="30bed-185">**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 SQL Server tooyour 現有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="30bed-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="30bed-186">**作業和監視**-這個焦點區域會顯示建議 toohelp 簡化 IT 作業，實作的預防性維護，並將效能最大化。</span><span class="sxs-lookup"><span data-stu-id="30bed-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="30bed-187">**變更和組態管理**-這個焦點區域會顯示建議 toohelp 保護日常作業，確定變更不產生負面影響您的基礎結構、 建立變更控制程序和 tootrack 稽核系統組態。</span><span class="sxs-lookup"><span data-stu-id="30bed-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="30bed-188">您的目標應該 tooscore 100%中每個焦點區域？</span><span class="sxs-lookup"><span data-stu-id="30bed-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="30bed-189">不一定。</span><span class="sxs-lookup"><span data-stu-id="30bed-189">Not necessarily.</span></span> <span data-ttu-id="30bed-190">hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。</span><span class="sxs-lookup"><span data-stu-id="30bed-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="30bed-191">不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。</span><span class="sxs-lookup"><span data-stu-id="30bed-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="30bed-192">例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="30bed-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="30bed-193">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="30bed-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="30bed-194">重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。</span><span class="sxs-lookup"><span data-stu-id="30bed-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="30bed-195">您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="30bed-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="30bed-196">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="30bed-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="30bed-197">您應該使用此指南 tooevaluate 是否實作 hello 建議適用於您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質。</span><span class="sxs-lookup"><span data-stu-id="30bed-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="30bed-198">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="30bed-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="30bed-199">您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="30bed-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="30bed-200">tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="30bed-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="30bed-201">安裝之後，您可以使用 OMS hello 概觀 頁面上的 hello SQL 評估磚檢視建議 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="30bed-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="30bed-202">檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。</span><span class="sxs-lookup"><span data-stu-id="30bed-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="30bed-203">tooview 焦點區域，並採取修正動作的建議</span><span class="sxs-lookup"><span data-stu-id="30bed-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="30bed-204">在 hello**概觀**頁面上，按一下 hello **SQL 評估**磚。</span><span class="sxs-lookup"><span data-stu-id="30bed-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="30bed-205">在 hello **SQL 評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="30bed-206">在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="30bed-207">按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="30bed-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="30bed-208">![SQL 評定建議圖片](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="30bed-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="30bed-209">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="30bed-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="30bed-210">Hello 項目已獲得解決之後，後續評估會記錄的建議動作並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="30bed-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="30bed-211">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="30bed-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="30bed-212">忽略建議</span><span class="sxs-lookup"><span data-stu-id="30bed-212">Ignore recommendations</span></span>
<span data-ttu-id="30bed-213">如果您有想 tooignore 的建議，您可以建立 OMS 將會使用您的評估結果中出現 tooprevent 建議的文字檔。</span><span class="sxs-lookup"><span data-stu-id="30bed-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="30bed-214">tooidentify，建議您將會忽略</span><span class="sxs-lookup"><span data-stu-id="30bed-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="30bed-215">登入 tooyour 工作區，並開啟 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="30bed-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="30bed-216">使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="30bed-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="30bed-217">以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：![失敗的建議](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="30bed-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="30bed-218">選擇您想 tooignore 的建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="30bed-219">您會在 hello 下一個程序中使用 RecommendationId hello 值。</span><span class="sxs-lookup"><span data-stu-id="30bed-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="30bed-220">toocreate 及使用 IgnoreRecommendations.txt 文字檔</span><span class="sxs-lookup"><span data-stu-id="30bed-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="30bed-221">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="30bed-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="30bed-222">貼上或輸入您要 OMS tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。</span><span class="sxs-lookup"><span data-stu-id="30bed-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="30bed-223">將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="30bed-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="30bed-224">以 hello Microsoft Monitoring Agent （直接或透過 Operations Manager 連線） 的電腦上*SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="30bed-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="30bed-225">Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="30bed-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="30bed-226">tooverify 建議已忽略</span><span class="sxs-lookup"><span data-stu-id="30bed-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="30bed-227">執行下一個排程評估 hello，預設每隔 7 天之後, hello 指定建議會標示忽略，而且不會出現在 hello 評估儀表板上。</span><span class="sxs-lookup"><span data-stu-id="30bed-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="30bed-228">您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="30bed-229">如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。</span><span class="sxs-lookup"><span data-stu-id="30bed-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="30bed-230">SQL 評估方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="30bed-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="30bed-231">*評估的執行頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="30bed-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="30bed-232">hello 評估每 7 天執行。</span><span class="sxs-lookup"><span data-stu-id="30bed-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="30bed-233">*有方法 tooconfigure 頻率 hello 評估執行嗎？*</span><span class="sxs-lookup"><span data-stu-id="30bed-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="30bed-234">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="30bed-234">Not at this time.</span></span>

<span data-ttu-id="30bed-235">*如果在我新增 hello SQL 評估解決方案之後探索到另一部伺服器，它會受到評估嗎？*</span><span class="sxs-lookup"><span data-stu-id="30bed-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="30bed-236">是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。</span><span class="sxs-lookup"><span data-stu-id="30bed-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="30bed-237">*如果伺服器除役，何時將它會移除來自 hello 評估？*</span><span class="sxs-lookup"><span data-stu-id="30bed-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="30bed-238">如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。</span><span class="sxs-lookup"><span data-stu-id="30bed-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="30bed-239">*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="30bed-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="30bed-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="30bed-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="30bed-241">*如何花費時間的資料收集的 toobe？*</span><span class="sxs-lookup"><span data-stu-id="30bed-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="30bed-242">hello hello 伺服器上的實際資料收集需費時約 1 小時。</span><span class="sxs-lookup"><span data-stu-id="30bed-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="30bed-243">對於擁有大量 SQL 執行個體或資料庫的伺服器，資料收集可能需要花費更久的時間。</span><span class="sxs-lookup"><span data-stu-id="30bed-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="30bed-244">*收集的資料類型為何？*</span><span class="sxs-lookup"><span data-stu-id="30bed-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="30bed-245">收集下列類型的資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="30bed-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="30bed-246">WMI</span><span class="sxs-lookup"><span data-stu-id="30bed-246">WMI</span></span>
  * <span data-ttu-id="30bed-247">登錄</span><span class="sxs-lookup"><span data-stu-id="30bed-247">Registry</span></span>
  * <span data-ttu-id="30bed-248">效能計數器</span><span class="sxs-lookup"><span data-stu-id="30bed-248">Performance counters</span></span>
  * <span data-ttu-id="30bed-249">SQL 動態管理檢視 (DMV)。</span><span class="sxs-lookup"><span data-stu-id="30bed-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="30bed-250">*有方法 tooconfigure 時收集資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="30bed-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="30bed-251">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="30bed-251">Not at this time.</span></span>

<span data-ttu-id="30bed-252">*為什麼我必須 tooconfigure 執行身分帳戶？*</span><span class="sxs-lookup"><span data-stu-id="30bed-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="30bed-253">智慧套件會針對 SQL Server 執行少量的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="30bed-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="30bed-254">為了讓它們必須使用 toorun，執行身分帳戶與 VIEW SERVER STATE 權限 tooSQL。</span><span class="sxs-lookup"><span data-stu-id="30bed-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="30bed-255">此外，在訂單 tooquery WMI，就需要本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="30bed-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="30bed-256">*為什麼只顯示 hello 前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="30bed-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="30bed-257">與其提供鉅細靡遺的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。</span><span class="sxs-lookup"><span data-stu-id="30bed-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="30bed-258">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="30bed-259">如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用 hello OMS 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="30bed-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="30bed-260">*是否有方法 tooignore 建議？*</span><span class="sxs-lookup"><span data-stu-id="30bed-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="30bed-261">是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。</span><span class="sxs-lookup"><span data-stu-id="30bed-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30bed-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30bed-262">Next steps</span></span>
* <span data-ttu-id="30bed-263">[搜尋記錄](log-analytics-log-searches.md)tooview 詳細的 SQL 評估資料和建議。</span><span class="sxs-lookup"><span data-stu-id="30bed-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
