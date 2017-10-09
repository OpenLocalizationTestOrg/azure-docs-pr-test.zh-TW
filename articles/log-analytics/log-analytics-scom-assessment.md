---
title: "aaaOptimize System Center Operations Manager 環境與 Azure Log Analytics |Microsoft 文件"
description: "您可以使用 hello 系統 Center Operations Manager 評估解決方案 tooassess hello 定期的風險和伺服器環境的健全狀況。"
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
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="478ff-103">利用 hello System Center Operations Manager 評估 （預覽） 解決方案最佳化環境</span><span class="sxs-lookup"><span data-stu-id="478ff-103">Optimize your environment with hello System Center Operations Manager Assessment (Preview) solution</span></span>

![System Center Operations Manager 評定符號](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

<span data-ttu-id="478ff-105">您可以使用 hello 系統 Center Operations Manager 評估解決方案 tooassess hello 風險和 System Center Operations Manager 伺服器環境的健全狀況規則的間隔。</span><span class="sxs-lookup"><span data-stu-id="478ff-105">You can use hello System Center Operations Manager Assessment solution tooassess hello risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="478ff-106">這篇文章可協助您安裝、 設定和使用 hello 解決方案，讓您可以採取修正動作，可能的問題。</span><span class="sxs-lookup"><span data-stu-id="478ff-106">This article helps you install, configure, and use hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="478ff-107">此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。</span><span class="sxs-lookup"><span data-stu-id="478ff-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="478ff-108">hello 建議是跨四個焦點區域，幫助您快速了解 hello 風險並採取更正措施分類。</span><span class="sxs-lookup"><span data-stu-id="478ff-108">hello recommendations are categorized across four focus areas, which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="478ff-109">hello 所提供的建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。</span><span class="sxs-lookup"><span data-stu-id="478ff-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="478ff-110">每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。</span><span class="sxs-lookup"><span data-stu-id="478ff-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="478ff-111">您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。</span><span class="sxs-lookup"><span data-stu-id="478ff-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="478ff-112">焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **System Center Operations Manager 評估**儀表板為您的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="478ff-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="478ff-113">hello 下列各節說明如何 toouse hello 有關 hello **System Center Operations Manager 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 SCOM 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="478ff-113">hello following sections describe how toouse hello information on hello **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager 解決方案圖格](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 評估儀表板](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="478ff-116">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="478ff-116">Installing and configuring hello solution</span></span>

<span data-ttu-id="478ff-117">hello 解決方案適用於 Microsoft System Operations Manager 2012 R2 和 2012 SP1。</span><span class="sxs-lookup"><span data-stu-id="478ff-117">hello solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="478ff-118">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="478ff-118">Use hello following information tooinstall and configure hello solution.</span></span>

 - <span data-ttu-id="478ff-119">您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="478ff-119">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="478ff-120">安裝從 hello 解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview)或依照中的 hello 指示[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="478ff-120">Install hello solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following hello instructions in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="478ff-121">加入工作區中的方案 toohello hello 之後, hello hello 儀表板上的 System Center Operations Manager 評估磚會顯示 hello 額外的設定必要的訊息。</span><span class="sxs-lookup"><span data-stu-id="478ff-121">After adding hello solution toohello workspace, hello System Center Operations Manager Assessment tile on hello dashboard displays hello additional configuration required message.</span></span> <span data-ttu-id="478ff-122">Hello 磚上按一下，然後遵循 hello 頁面中所述的 hello 設定步驟</span><span class="sxs-lookup"><span data-stu-id="478ff-122">Click on hello tile and follow hello configuration steps mentioned in hello page</span></span>

 ![System Center Operations Manager 儀表板圖格](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 <span data-ttu-id="478ff-124">Hello System Center Operations Manager 的設定可以透過 hello 指令碼，依照 hello hello 的 hello 在 OMS 中的方案組態 頁面中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="478ff-124">Configuration of hello System Center Operations Manager can be done through hello script by following hello steps mentioned in hello configuration page of hello solution in OMS.</span></span>

 <span data-ttu-id="478ff-125">相反地，透過 SCOM 主控台中，依照以下的 hello tooconfigure hello 評估中的步驟 hello 相同順序</span><span class="sxs-lookup"><span data-stu-id="478ff-125">Instead, tooconfigure hello assessment through SCOM Console, follow hello below steps in hello same order</span></span>
1. [<span data-ttu-id="478ff-126">設定 System Center Operations Manager 評估 hello 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="478ff-126">Set hello Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="478ff-127">設定 hello System Center Operations Manager 評估規則</span><span class="sxs-lookup"><span data-stu-id="478ff-127">Configure hello System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="478ff-128">收集 System Center Operations Manager 評定資料的詳細資料</span><span class="sxs-lookup"><span data-stu-id="478ff-128">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="478ff-129">System Center Operations Manager 評估 hello 收集 WMI 資料、 登錄資料、 事件記錄檔資料，透過 Windows PowerShell、 SQL 查詢、 使用您已啟用的 hello 伺服器的檔案資訊收集器的 Operations Manager 資料。</span><span class="sxs-lookup"><span data-stu-id="478ff-129">hello System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using hello server that you have enabled.</span></span>

<span data-ttu-id="478ff-130">hello 下表顯示資料收集方法的 System Center Operations Manager 評估及頻率收集資料的代理程式。</span><span class="sxs-lookup"><span data-stu-id="478ff-130">hello following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="478ff-131">平台</span><span class="sxs-lookup"><span data-stu-id="478ff-131">platform</span></span> | <span data-ttu-id="478ff-132">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="478ff-132">Direct Agent</span></span> | <span data-ttu-id="478ff-133">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="478ff-133">SCOM agent</span></span> | <span data-ttu-id="478ff-134">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="478ff-134">Azure Storage</span></span> | <span data-ttu-id="478ff-135">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="478ff-135">SCOM required?</span></span> | <span data-ttu-id="478ff-136">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="478ff-136">SCOM agent data sent via management group</span></span> | <span data-ttu-id="478ff-137">收集頻率</span><span class="sxs-lookup"><span data-stu-id="478ff-137">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="478ff-138">Windows</span><span class="sxs-lookup"><span data-stu-id="478ff-138">Windows</span></span> | | | | <span data-ttu-id="478ff-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="478ff-139">&#8226;</span></span> | | <span data-ttu-id="478ff-140">7 天</span><span class="sxs-lookup"><span data-stu-id="478ff-140">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="478ff-141">OMS 的 Operations Manager 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="478ff-141">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="478ff-142">OMS 會建立工作負載 tooprovide 的管理組件具有附加價值的服務。</span><span class="sxs-lookup"><span data-stu-id="478ff-142">OMS builds on management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="478ff-143">每個工作負載需要在不同的安全性內容中，例如網域帳戶的工作負載特定權限 toorun 管理組件。</span><span class="sxs-lookup"><span data-stu-id="478ff-143">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="478ff-144">設定 Operations Manager 執行身分帳戶 tooprovide 認證資訊。</span><span class="sxs-lookup"><span data-stu-id="478ff-144">Configure an Operations Manager Run As account tooprovide credential information.</span></span>

<span data-ttu-id="478ff-145">使用下列資訊 tooset hello Operations Manager 執行身分帳戶的 System Center Operations Manager 評估 hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-145">Use hello following information tooset hello Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-hello-run-as-account"></a><span data-ttu-id="478ff-146">設定 hello 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="478ff-146">Set hello Run As account</span></span>

1. <span data-ttu-id="478ff-147">在 [hello Operations Manager 主控台，移 toohello**管理**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="478ff-147">In hello Operations Manager Console, go toohello **Administration** tab.</span></span>
2. <span data-ttu-id="478ff-148">在 hello**執行身分設定**，按一下 **帳戶**。</span><span class="sxs-lookup"><span data-stu-id="478ff-148">Under hello **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="478ff-149">建立執行身分帳戶，遵循精靈中，建立 Windows 帳戶 hello hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-149">Create hello Run As Account, following through hello Wizard, creating a Windows account.</span></span> <span data-ttu-id="478ff-150">hello 帳戶 toouse 是其中一個識別 hello 和具有下列所有 hello 必要條件：</span><span class="sxs-lookup"><span data-stu-id="478ff-150">hello account toouse is hello one identified and having all hello prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="478ff-151">hello 執行身分帳戶必須符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="478ff-151">hello Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="478ff-152">Hello 環境 （所有 Operations Manager 角色的管理伺服器、 OpsMgr 資料庫、 資料倉儲、 報表、 Web 主控台、 閘道） 中的所有伺服器 hello 本機 Administrators 群組的網域帳戶成員</span><span class="sxs-lookup"><span data-stu-id="478ff-152">A domain account member of hello local Administrators group on all servers in hello environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="478ff-153">要評估的 hello 管理群組的作業管理員 」 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="478ff-153">Operation Manager Administrator Role for hello management group being assessed</span></span>
    - <span data-ttu-id="478ff-154">執行 hello[指令碼](#sql-script-to-grant-granular-permissions-to-the-run-as-account)toogrant 細微的權限 toohello 帳戶，Operations Manager 所使用的 SQL 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="478ff-154">Execute hello [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant granular permissions toohello account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="478ff-155">注意： 如果此帳戶已經有 sysadmin 權限，請略過 hello 指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="478ff-155">Note: If this account has sysadmin rights already, then skip hello script execution.</span></span>

4. <span data-ttu-id="478ff-156">在 [散發安全性] 下，選取 [較安全]。</span><span class="sxs-lookup"><span data-stu-id="478ff-156">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="478ff-157">指定 hello 管理伺服器 hello 帳戶發佈的位置。</span><span class="sxs-lookup"><span data-stu-id="478ff-157">Specify hello management server where hello account is distributed.</span></span>
3. <span data-ttu-id="478ff-158">請返回 toohello 執行設定，並按一下**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="478ff-158">Go back toohello Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="478ff-159">搜尋 hello *SCOM 評估設定檔*。</span><span class="sxs-lookup"><span data-stu-id="478ff-159">Search for hello *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="478ff-160">hello 設定檔名稱應該是： *Microsoft System Center Advisor SCOM 評估執行身分設定檔*。</span><span class="sxs-lookup"><span data-stu-id="478ff-160">hello profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="478ff-161">以滑鼠右鍵按一下並更新其屬性，新增 hello 最近建立執行身分帳戶為您在步驟 3 中建立。</span><span class="sxs-lookup"><span data-stu-id="478ff-161">Right-click and update its properties and add hello recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a><span data-ttu-id="478ff-162">SQL 指令碼 toogrant 細微的權限 toohello 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="478ff-162">SQL script toogrant granular permissions toohello Run As account</span></span>

<span data-ttu-id="478ff-163">執行下列 SQL 指令碼 toogrant 所需的權限 toohello 執行身分帳戶 hello Operations Manager 所使用的 SQL 執行個體上的 hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-163">Execute hello following SQL script toogrant required permissions toohello Run As account on hello SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a><span data-ttu-id="478ff-164">設定 hello 評估規則</span><span class="sxs-lookup"><span data-stu-id="478ff-164">Configure hello assessment rule</span></span>

<span data-ttu-id="478ff-165">hello 系統 Center Operations Manager 評估解決方案的管理組件包含名為的規則*Microsoft System Center Advisor SCOM 評估執行評估規則*。</span><span class="sxs-lookup"><span data-stu-id="478ff-165">hello System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="478ff-166">此規則會負責執行 hello 評估。</span><span class="sxs-lookup"><span data-stu-id="478ff-166">This rule is responsible for running hello assessment.</span></span> <span data-ttu-id="478ff-167">tooenable hello 規則，並設定 hello 頻率，以下的使用 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="478ff-167">tooenable hello rule and configure hello frequency, use hello procedures below.</span></span>

<span data-ttu-id="478ff-168">根據預設，會停用 hello Microsoft System Center Advisor SCOM 評估執行評估規則。</span><span class="sxs-lookup"><span data-stu-id="478ff-168">By default, hello Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="478ff-169">toorun hello 評估，您必須啟用管理伺服器上的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="478ff-169">toorun hello assessment, you must enable hello rule on a management server.</span></span> <span data-ttu-id="478ff-170">使用下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-170">Use hello following steps.</span></span>

#### <a name="enable-hello-rule-for-a-specific-management-server"></a><span data-ttu-id="478ff-171">啟用特定管理伺服器的 hello 規則</span><span class="sxs-lookup"><span data-stu-id="478ff-171">Enable hello rule for a specific management server</span></span>

1. <span data-ttu-id="478ff-172">在 hello**製作**工作區中的 hello Operations Manager 主控台中，搜尋 hello 規則*Microsoft System Center Advisor SCOM 評估執行評估規則*hello 中**規則**窗格。</span><span class="sxs-lookup"><span data-stu-id="478ff-172">In hello **Authoring** workspace of hello Operations Manager console, search for hello rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in hello **Rules** pane.</span></span>
2. <span data-ttu-id="478ff-173">在 hello 搜尋結果中，選取 hello 包含 hello 文字*類型： 管理伺服器*。</span><span class="sxs-lookup"><span data-stu-id="478ff-173">In hello search results, select hello one that includes hello text *Type: Management Server*.</span></span>
3. <span data-ttu-id="478ff-174">Hello 規則上按一下滑鼠右鍵，然後按一下**會覆寫** > **類別的特定物件： 管理伺服器**。</span><span class="sxs-lookup"><span data-stu-id="478ff-174">Right-click hello rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="478ff-175">在 hello 可用的管理伺服器清單中，選取應在何處執行 hello 規則 hello 管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="478ff-175">In hello available management servers list, select hello management server where hello rule should run.</span></span>
5.  <span data-ttu-id="478ff-176">請確定您也變更覆寫值**True** hello**啟用**參數值。</span><span class="sxs-lookup"><span data-stu-id="478ff-176">Ensure that you change override value too**True** for hello **Enabled** parameter value.</span></span>  
    <span data-ttu-id="478ff-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="478ff-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="478ff-178">雖然仍在這個視窗中，設定 hello 頻率的 hello 使用 hello 下一個程序執行。</span><span class="sxs-lookup"><span data-stu-id="478ff-178">While still in this window, configure hello frequency of hello run using hello next procedure.</span></span>

#### <a name="configure-hello-run-frequency"></a><span data-ttu-id="478ff-179">設定執行 hello 頻率</span><span class="sxs-lookup"><span data-stu-id="478ff-179">Configure hello run frequency</span></span>

<span data-ttu-id="478ff-180">hello 評估是每個 10,080 分鐘 （或七天），設定的 toorun hello 預設間隔。</span><span class="sxs-lookup"><span data-stu-id="478ff-180">hello assessment is configured toorun every 10,080 minutes (or seven days), hello default interval.</span></span> <span data-ttu-id="478ff-181">您可以覆寫 hello 值 tooa 最小值為 1440 分鐘 （或一天）。</span><span class="sxs-lookup"><span data-stu-id="478ff-181">You can override hello value tooa minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="478ff-182">hello 值代表執行後續評估之間所需的 hello 最小時間間隔。</span><span class="sxs-lookup"><span data-stu-id="478ff-182">hello value represents hello minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="478ff-183">使用下列的 hello 步驟 toooverride hello 間隔。</span><span class="sxs-lookup"><span data-stu-id="478ff-183">toooverride hello interval, use hello steps below.</span></span>

1. <span data-ttu-id="478ff-184">在 hello**製作**工作區中的 hello Operations Manager 主控台中，搜尋 hello 規則*Microsoft System Center Advisor SCOM 評估執行評估規則*hello 中**規則**窗格。</span><span class="sxs-lookup"><span data-stu-id="478ff-184">In hello **Authoring** workspace of hello Operations Manager console, search for hello rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in hello **Rules** pane.</span></span>
2. <span data-ttu-id="478ff-185">在 hello 搜尋結果中，選取 hello 包含 hello 文字*類型： 管理伺服器*。</span><span class="sxs-lookup"><span data-stu-id="478ff-185">In hello search results, select hello one that includes hello text *Type: Management Server*.</span></span>
3. <span data-ttu-id="478ff-186">Hello 規則上按一下滑鼠右鍵，然後按一下**覆寫 hello 規則** > **類別的所有物件： 管理伺服器**。</span><span class="sxs-lookup"><span data-stu-id="478ff-186">Right-click hello rule and then click **Override hello Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="478ff-187">變更 hello**間隔**參數值 tooyour 所需的時間間隔值。</span><span class="sxs-lookup"><span data-stu-id="478ff-187">Change hello **Interval** parameter value tooyour desired interval value.</span></span> <span data-ttu-id="478ff-188">在 hello 下列範例中，hello 值設定 too1440 分鐘 （1 天）。</span><span class="sxs-lookup"><span data-stu-id="478ff-188">In hello example below, hello value is set too1440 minutes (one day).</span></span>  
    <span data-ttu-id="478ff-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="478ff-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="478ff-190">如果設定 hello 值 tooless 1440 分鐘以上，hello 規則就會執行一天的間隔。</span><span class="sxs-lookup"><span data-stu-id="478ff-190">If hello value is set tooless than 1440 minutes, then hello rule runs at a one day interval.</span></span> <span data-ttu-id="478ff-191">在此範例中，hello 規則會忽略 hello 間隔值，並執行一天的頻率。</span><span class="sxs-lookup"><span data-stu-id="478ff-191">In this example, hello rule ignores hello interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="478ff-192">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="478ff-192">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="478ff-193">每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="478ff-193">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="478ff-194">只有 hello 10 最重要的建議會出現。</span><span class="sxs-lookup"><span data-stu-id="478ff-194">Only hello 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="478ff-195">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="478ff-195">How weights are calculated</span></span>

<span data-ttu-id="478ff-196">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="478ff-196">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="478ff-197">hello*機率*識別之疑難引發問題。</span><span class="sxs-lookup"><span data-stu-id="478ff-197">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="478ff-198">較高的機率等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-198">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
- <span data-ttu-id="478ff-199">hello*影響*hello 問題如果確實引發問題對您組織。</span><span class="sxs-lookup"><span data-stu-id="478ff-199">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="478ff-200">較高的影響等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-200">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
- <span data-ttu-id="478ff-201">hello*投入時間*需要 tooimplement hello 建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-201">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="478ff-202">勞力較高 tooa 整體分數較低的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-202">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="478ff-203">每個建議的加權 hello hello 總分每個焦點區域的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="478ff-203">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="478ff-204">例如，如果 hello 可用性和業務持續性的焦點區域建議的分數為 5%，實作該項建議會增加您整體的可用性和業務持續性分數 5%。</span><span class="sxs-lookup"><span data-stu-id="478ff-204">For example, if a recommendation in hello Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="478ff-205">焦點區域</span><span class="sxs-lookup"><span data-stu-id="478ff-205">Focus areas</span></span>

<span data-ttu-id="478ff-206">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="478ff-206">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="478ff-207">**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。</span><span class="sxs-lookup"><span data-stu-id="478ff-207">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="478ff-208">**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 SQL Server tooyour 現有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="478ff-208">**Upgrade, Migration, and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="478ff-209">**作業和監視**-這個焦點區域會顯示建議 toohelp 簡化 IT 作業，實作的預防性維護，並將效能最大化。</span><span class="sxs-lookup"><span data-stu-id="478ff-209">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="478ff-210">您的目標應該 tooscore 100%中每個焦點區域？</span><span class="sxs-lookup"><span data-stu-id="478ff-210">Should you aim tooscore 100% in every focus area?</span></span>

<span data-ttu-id="478ff-211">不一定。</span><span class="sxs-lookup"><span data-stu-id="478ff-211">Not necessarily.</span></span> <span data-ttu-id="478ff-212">hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。</span><span class="sxs-lookup"><span data-stu-id="478ff-212">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="478ff-213">不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。</span><span class="sxs-lookup"><span data-stu-id="478ff-213">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="478ff-214">例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="478ff-214">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="478ff-215">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="478ff-215">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="478ff-216">重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。</span><span class="sxs-lookup"><span data-stu-id="478ff-216">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="478ff-217">您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="478ff-217">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="478ff-218">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="478ff-218">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="478ff-219">當實作 hello 建議是適合您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質，請使用本指引 tooevaluate。</span><span class="sxs-lookup"><span data-stu-id="478ff-219">Use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="478ff-220">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="478ff-220">Use assessment focus area recommendations</span></span>

<span data-ttu-id="478ff-221">您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="478ff-221">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="478ff-222">tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="478ff-222">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="478ff-223">安裝之後，您可以使用 OMS hello 概觀 頁面上的 hello System Center Operations Manager 評估磚檢視建議 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="478ff-223">After it is installed, you can view hello summary of recommendations by using hello System Center Operations Manager Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="478ff-224">檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。</span><span class="sxs-lookup"><span data-stu-id="478ff-224">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="478ff-225">tooview 焦點區域，並採取修正動作的建議</span><span class="sxs-lookup"><span data-stu-id="478ff-225">tooview recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="478ff-226">在 hello**概觀**頁面上，按一下 hello **System Center Operations Manager 評估**磚。</span><span class="sxs-lookup"><span data-stu-id="478ff-226">On hello **Overview** page, click hello **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="478ff-227">在 hello **System Center Operations Manager 評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-227">On hello **System Center Operations Manager Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="478ff-228">在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-228">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="478ff-229">按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="478ff-229">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="478ff-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="478ff-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="478ff-231">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="478ff-231">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="478ff-232">Hello 項目已獲得解決之後，後續評估會記錄的建議動作並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="478ff-232">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="478ff-233">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="478ff-233">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="478ff-234">忽略建議</span><span class="sxs-lookup"><span data-stu-id="478ff-234">Ignore recommendations</span></span>

<span data-ttu-id="478ff-235">如果您有想 tooignore 的建議，您可以建立 OMS 使用您的評估結果中出現 tooprevent 建議的文字檔。</span><span class="sxs-lookup"><span data-stu-id="478ff-235">If you have recommendations that you want tooignore, you can create a text file that OMS uses tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a><span data-ttu-id="478ff-236">您想 tooignore tooidentify 建議</span><span class="sxs-lookup"><span data-stu-id="478ff-236">tooidentify recommendations that you want tooignore</span></span>

1. <span data-ttu-id="478ff-237">登入 tooyour 工作區，並開啟 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="478ff-237">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="478ff-238">使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-238">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="478ff-239">以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：</span><span class="sxs-lookup"><span data-stu-id="478ff-239">Here's a screen shot showing hello Log Search query:</span></span>  
    ![log search](./media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="478ff-241">選擇您想 tooignore 的建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-241">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="478ff-242">您會在 hello 下一個程序中使用 RecommendationId hello 值。</span><span class="sxs-lookup"><span data-stu-id="478ff-242">You'll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="478ff-243">toocreate 及使用 IgnoreRecommendations.txt 文字檔</span><span class="sxs-lookup"><span data-stu-id="478ff-243">toocreate and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="478ff-244">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="478ff-244">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="478ff-245">貼上或輸入您要 OMS tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。</span><span class="sxs-lookup"><span data-stu-id="478ff-245">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="478ff-246">將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="478ff-246">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
4. <span data-ttu-id="478ff-247">Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server。</span><span class="sxs-lookup"><span data-stu-id="478ff-247">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="478ff-248">tooverify 建議已忽略</span><span class="sxs-lookup"><span data-stu-id="478ff-248">tooverify that recommendations are ignored</span></span>

1. <span data-ttu-id="478ff-249">執行下一個排程評估 hello，預設每隔七天之後, hello 指定建議會標示忽略，而且不會出現在 hello 評估儀表板上。</span><span class="sxs-lookup"><span data-stu-id="478ff-249">After hello next scheduled assessment runs, by default every seven days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="478ff-250">您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-250">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="478ff-251">如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。</span><span class="sxs-lookup"><span data-stu-id="478ff-251">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="478ff-252">System Center Operations Manager 評定解決方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="478ff-252">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="478ff-253">*我加入 hello 評估解決方案 toomy OMS 工作區。但我沒看到 hello 建議。為什麼？*</span><span class="sxs-lookup"><span data-stu-id="478ff-253">*I added hello assessment solution toomy OMS workspace. But I don’t see hello recommendations. Why not?*</span></span> <span data-ttu-id="478ff-254">加入之後 hello 方案，請使用下列步驟檢視 hello 建議 hello OMS 儀表板上的 hello。</span><span class="sxs-lookup"><span data-stu-id="478ff-254">After adding hello solution, use hello following steps view hello recommendations on hello OMS dashboard.</span></span>  

- [<span data-ttu-id="478ff-255">設定 System Center Operations Manager 評估 hello 執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="478ff-255">Set hello Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="478ff-256">設定 hello System Center Operations Manager 評估規則</span><span class="sxs-lookup"><span data-stu-id="478ff-256">Configure hello System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="478ff-257">*有方法 tooconfigure 頻率 hello 評估執行嗎？*</span><span class="sxs-lookup"><span data-stu-id="478ff-257">*Is there a way tooconfigure how often hello assessment runs?*</span></span> <span data-ttu-id="478ff-258">是。</span><span class="sxs-lookup"><span data-stu-id="478ff-258">Yes.</span></span> <span data-ttu-id="478ff-259">請參閱[執行頻率設定 hello](#configure-the-run-frequency)。</span><span class="sxs-lookup"><span data-stu-id="478ff-259">See [Configure hello run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="478ff-260">*如果在我新增 hello System Center Operations Manager 評估解決方案之後探索到另一部伺服器，它會受到評估嗎？*</span><span class="sxs-lookup"><span data-stu-id="478ff-260">*If another server is discovered after I’ve added hello System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="478ff-261">是，在探索之後，從那時起也會評估它 -- 預設是每隔 7 天。</span><span class="sxs-lookup"><span data-stu-id="478ff-261">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="478ff-262">*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="478ff-262">*What is hello name of hello process that does hello data collection?*</span></span> <span data-ttu-id="478ff-263">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="478ff-263">AdvisorAssessment.exe</span></span>

<span data-ttu-id="478ff-264">*Hello AdvisorAssessment.exe 程序執行的位置為何？*</span><span class="sxs-lookup"><span data-stu-id="478ff-264">*Where does hello AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="478ff-265">AdvisorAssessment.exe 執行 hello hello management server 的 HealthService hello 評估規則啟用的位置。</span><span class="sxs-lookup"><span data-stu-id="478ff-265">AdvisorAssessment.exe runs under hello HealthService of hello management server where hello assessment rule is enabled.</span></span> <span data-ttu-id="478ff-266">使用這個程序時，將會透過遠端資料收集來探索您的整個環境。</span><span class="sxs-lookup"><span data-stu-id="478ff-266">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="478ff-267">收集資料需要花費多少時間？</span><span class="sxs-lookup"><span data-stu-id="478ff-267">*How long does it take for data collection?*</span></span> <span data-ttu-id="478ff-268">Hello 伺服器上的資料收集需費時約一小時。</span><span class="sxs-lookup"><span data-stu-id="478ff-268">Data collection on hello server takes about one hour.</span></span> <span data-ttu-id="478ff-269">在有許多 Operations Manager 執行個體或資料庫的環境中可能更久。</span><span class="sxs-lookup"><span data-stu-id="478ff-269">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="478ff-270">*設定 hello hello 評估 tooless 1440 分鐘以上的時間間隔該怎麼辦？* hello 評估是在每日一次最多的預先設定的 toorun。</span><span class="sxs-lookup"><span data-stu-id="478ff-270">*What if I set hello interval of hello assessment tooless than 1440 minutes?* hello assessment is pre-configured toorun at a maximum of once per day.</span></span> <span data-ttu-id="478ff-271">如果您覆寫 hello 間隔值 tooa 值小於 1440 分鐘，然後 hello 評估使用 1440 分鐘做為 hello 間隔值。</span><span class="sxs-lookup"><span data-stu-id="478ff-271">If you override hello interval value tooa value less than 1440 minutes, then hello assessment uses 1440 minutes as hello interval value.</span></span>

<span data-ttu-id="478ff-272">*如何 tooknow 如果先決條件失敗？*</span><span class="sxs-lookup"><span data-stu-id="478ff-272">*How tooknow if there are pre-requisite failures?*</span></span> <span data-ttu-id="478ff-273">如果 hello 評估執行，而您沒有看到結果，則可能部分之 hello 評估 hello 先決條件失敗。</span><span class="sxs-lookup"><span data-stu-id="478ff-273">If hello assessment ran and you don't see results, then it is likely that some of hello pre-requisites for hello assessment failed.</span></span> <span data-ttu-id="478ff-274">您可以執行查詢：`Type=Operation Solution=SCOMAssessment`和`Type=SCOMAssessmentRecommendation FocusArea=Prerequisites`記錄搜尋 toosee hello 中失敗的必要元件。</span><span class="sxs-lookup"><span data-stu-id="478ff-274">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search toosee hello failed pre-requisites.</span></span>

<span data-ttu-id="478ff-275">*必要條件未通過中出現 `Failed tooconnect toohello SQL Instance (….).` 訊息。什麼是 hello 問題？*</span><span class="sxs-lookup"><span data-stu-id="478ff-275">*There is a `Failed tooconnect toohello SQL Instance (….).` message in pre-requisite failures. What is hello issue?*</span></span> <span data-ttu-id="478ff-276">AdvisorAssessment.exe，hello 處理程序收集資料，會執行 hello hello management server 的 HealthService。</span><span class="sxs-lookup"><span data-stu-id="478ff-276">AdvisorAssessment.exe, hello process that collects data, runs under hello HealthService of hello management server.</span></span> <span data-ttu-id="478ff-277">Hello 評估的一部分，hello 處理序嘗試 tooconnect toohello 存在 hello Operations Manager 資料庫所在的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="478ff-277">As part of hello assessment, hello process attempts tooconnect toohello SQL Server where hello Operations Manager database is present.</span></span> <span data-ttu-id="478ff-278">當防火牆規則封鎖 hello 連接 toohello SQL Server 執行個體時，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="478ff-278">This error can occur when firewall rules block hello connection toohello SQL Server instance.</span></span>

<span data-ttu-id="478ff-279">*收集的資料類型為何？* hello 下列類型的資料收集： WMI 資料登錄資料-事件記錄檔資料-Operations Manager 資料透過 Windows PowerShell，SQL 查詢檔案資訊的收集器。</span><span class="sxs-lookup"><span data-stu-id="478ff-279">*What type of data is collected?* hello following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="478ff-280">*為什麼我必須 tooconfigure 執行身分帳戶？*</span><span class="sxs-lookup"><span data-stu-id="478ff-280">*Why do I have tooconfigure a Run As Account?*</span></span> <span data-ttu-id="478ff-281">Operations Manager 伺服器上會執行各種 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="478ff-281">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="478ff-282">為了讓它們 toorun，您必須使用執行身分帳戶具有必要的權限。</span><span class="sxs-lookup"><span data-stu-id="478ff-282">In order for them toorun, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="478ff-283">此外，本機系統管理員認證是必要的 tooquery WMI。</span><span class="sxs-lookup"><span data-stu-id="478ff-283">In addition, local administrator credentials are required tooquery WMI.</span></span>

<span data-ttu-id="478ff-284">*為什麼只顯示 hello 前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="478ff-284">*Why display only hello top 10 recommendations?*</span></span> <span data-ttu-id="478ff-285">與其提供詳盡、 非常龐大的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。</span><span class="sxs-lookup"><span data-stu-id="478ff-285">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="478ff-286">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-286">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="478ff-287">如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="478ff-287">If you prefer toosee hello detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="478ff-288">*是否有方法 tooignore 建議？*</span><span class="sxs-lookup"><span data-stu-id="478ff-288">*Is there a way tooignore a recommendation?*</span></span> <span data-ttu-id="478ff-289">是，請參閱 hello[忽略建議](#Ignore-recommendations)。</span><span class="sxs-lookup"><span data-stu-id="478ff-289">Yes, see hello [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="478ff-290">後續步驟</span><span class="sxs-lookup"><span data-stu-id="478ff-290">Next steps</span></span>

- <span data-ttu-id="478ff-291">[搜尋記錄](log-analytics-log-searches.md)tooview 詳細的 System Center Operations Manager 評估資料和建議。</span><span class="sxs-lookup"><span data-stu-id="478ff-291">[Search logs](log-analytics-log-searches.md) tooview detailed System Center Operations Manager Assessment data and recommendations.</span></span>
