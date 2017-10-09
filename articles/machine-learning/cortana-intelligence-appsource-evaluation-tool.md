---
title: "aaaCortana 智慧方案評估工具 |Microsoft 文件"
description: "Microsoft 合作夥伴身分，以下是需要您 Cortana 智慧方案 tooAppSource toofollow toopublish 所有 hello 步驟。"
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a><span data-ttu-id="da6c6-103">Cortana Intelligence 解決方案評估工具</span><span class="sxs-lookup"><span data-stu-id="da6c6-103">Cortana Intelligence solution evaluation tool</span></span>
## <a name="overview"></a><span data-ttu-id="da6c6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="da6c6-104">Overview</span></span>
<span data-ttu-id="da6c6-105">您可以用於 hello Cortana 智慧方案評估工具 tooassess 進階的分析解決方案符合 Microsoft 建議的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="da6c6-105">You can use hello Cortana Intelligence solution evaluation tool tooassess your advanced analytics solutions for compliance with Microsoft-recommended best practices.</span></span> <span data-ttu-id="da6c6-106">Microsoft 是高興的 toowork 與我們的協力廠商 (Isv / SIs) 的客戶、 轉售商與實作 tooprovide 高品質解決方案。</span><span class="sxs-lookup"><span data-stu-id="da6c6-106">Microsoft is excited toowork with our partners (ISVs / SIs) tooprovide high-quality solutions for customers, resellers and implementation.</span></span> <span data-ttu-id="da6c6-107">本指南會逐步解說的 hello 解決方案評估工具使用與您的方案 hello 程序，並說明 hello 特定的最佳作法中檢查。</span><span class="sxs-lookup"><span data-stu-id="da6c6-107">This guide will walk through hello process of using hello Solution evaluation tool with your solution and describe hello specific best practices in checks for.</span></span>

## <a name="getting-started"></a><span data-ttu-id="da6c6-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="da6c6-108">Getting started</span></span>
<span data-ttu-id="da6c6-109">請[下載](https://aka.ms/aa-evaluation-tool-download)並安裝 hello Cortana 智慧方案評估工具。</span><span class="sxs-lookup"><span data-stu-id="da6c6-109">Please [download](https://aka.ms/aa-evaluation-tool-download) and install hello Cortana Intelligence solution evaluation tool.</span></span>

<span data-ttu-id="da6c6-110">必要條件：</span><span class="sxs-lookup"><span data-stu-id="da6c6-110">Prerequisites:</span></span>
- <span data-ttu-id="da6c6-111">Windows 10：[Windows 10 的官方網站](https://www.microsoft.com/en-us/windows)</span><span class="sxs-lookup"><span data-stu-id="da6c6-111">Windows 10: [Official site for Windows 10](https://www.microsoft.com/en-us/windows)</span></span>
- <span data-ttu-id="da6c6-112">Azure PowerShell：[安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-112">Azure Powershell: [Install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>

## <a name="identifying-your-app"></a><span data-ttu-id="da6c6-113">識別您的應用程式</span><span class="sxs-lookup"><span data-stu-id="da6c6-113">Identifying your app</span></span>
<span data-ttu-id="da6c6-114">安裝完成後，開啟 hello 工具，並開始您第一次評估。</span><span class="sxs-lookup"><span data-stu-id="da6c6-114">After installation completes, open hello tool and begin your first evaluation.</span></span>

![開啟評估工具](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

<span data-ttu-id="da6c6-116">提供關於您解決方案的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="da6c6-116">Provide identifying information about your solution.</span></span>

![連接 Azure 訂用帳戶](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

<span data-ttu-id="da6c6-118">連接 tooyour Azure 訂用帳戶，並提供 hello 包含您的應用程式的資源群組。</span><span class="sxs-lookup"><span data-stu-id="da6c6-118">Connect tooyour Azure subscription and provide hello Resource Group containing your app.</span></span>

![選取資源](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

<span data-ttu-id="da6c6-120">一旦載入 hello 資源群組之後，請選取包含在您的方案中，找出 hello 協助工具，可能是任何資料資源的 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="da6c6-120">Once hello resource group has been loaded, please select hello resources that are included in your solution and identify hello accessibility of any data resources as either:</span></span>
- <span data-ttu-id="da6c6-121">擷取</span><span class="sxs-lookup"><span data-stu-id="da6c6-121">Ingestion</span></span>
- <span data-ttu-id="da6c6-122">使用</span><span class="sxs-lookup"><span data-stu-id="da6c6-122">Consumption</span></span>
- <span data-ttu-id="da6c6-123">內部</span><span class="sxs-lookup"><span data-stu-id="da6c6-123">Internal</span></span>

<span data-ttu-id="da6c6-124">我們會使用這項資訊 toobetter 了解如何您的方案利用各種元件和 tooensure 使用者互動元件都符合最佳做法。</span><span class="sxs-lookup"><span data-stu-id="da6c6-124">We use this information toobetter understand how your solution is utilizing various components and tooensure user-facing components are consistent with best practices.</span></span>

### <a name="ingestion"></a><span data-ttu-id="da6c6-125">擷取</span><span class="sxs-lookup"><span data-stu-id="da6c6-125">Ingestion</span></span>
<span data-ttu-id="da6c6-126">擷取在此情況下表示資料從外部 hello 方案中的使用的 toopull 或 hello 方案之外的任何服務，使用到它 toopush 資料的任何資料來源。</span><span class="sxs-lookup"><span data-stu-id="da6c6-126">Ingestion in this case means any data sources that are used toopull in data from outside hello solution or that any services outside hello solution use toopush data into it.</span></span>

### <a name="consumption"></a><span data-ttu-id="da6c6-127">耗用量</span><span class="sxs-lookup"><span data-stu-id="da6c6-127">Consumption</span></span>
<span data-ttu-id="da6c6-128">耗用量在此情況下表示會使用的 toopush 資料 tooend 使用者，不論是直接或間接的任何資料集。</span><span class="sxs-lookup"><span data-stu-id="da6c6-128">Consumption in this case means any datasets that are used toopush data tooend users, either directly or indirectly.</span></span> <span data-ttu-id="da6c6-129">例如：</span><span class="sxs-lookup"><span data-stu-id="da6c6-129">For example:</span></span>
- <span data-ttu-id="da6c6-130">從 PowerBI 中用於直接查詢的資料集。</span><span class="sxs-lookup"><span data-stu-id="da6c6-130">Datasets used in direct query from PowerBI.</span></span>
- <span data-ttu-id="da6c6-131">在 WebApp 中查詢的資料集。</span><span class="sxs-lookup"><span data-stu-id="da6c6-131">Datasets queried in a WebApp.</span></span>

>[!NOTE]
<span data-ttu-id="da6c6-132">如果特定的資源同時用於擷取和使用，請選擇 [使用]。</span><span class="sxs-lookup"><span data-stu-id="da6c6-132">If a specific resource is used for both ingestion and consumption, please choose **Consumption**.</span></span>

### <a name="internal"></a><span data-ttu-id="da6c6-133">內部</span><span class="sxs-lookup"><span data-stu-id="da6c6-133">Internal</span></span>
<span data-ttu-id="da6c6-134">針對僅用於內部應用程式處理的任何資料資源，請使用「內部」。</span><span class="sxs-lookup"><span data-stu-id="da6c6-134">Use internal for any data resources that are used only in internal application processing.</span></span>

<span data-ttu-id="da6c6-135">接下來，您將會提示的 tooprovide 有效 hello 先前步驟中指定任何資料庫的認證：</span><span class="sxs-lookup"><span data-stu-id="da6c6-135">Next, you will be prompted tooprovide valid credentials for any databases specified in hello prior step:</span></span>

![設定測試必要條件](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a><span data-ttu-id="da6c6-137">解決方案測試案例</span><span class="sxs-lookup"><span data-stu-id="da6c6-137">Solution test cases</span></span>
<span data-ttu-id="da6c6-138">hello 解決方案工具將會執行自動化測試的集合，在您的方案。</span><span class="sxs-lookup"><span data-stu-id="da6c6-138">hello solution tool will perform a collection of automated tests on your solution.</span></span>

![設定測試執行](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

<span data-ttu-id="da6c6-140">Hello 測試完成後，您就可以要求 tooprovide 說明或理由為何您的方案不符合 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="da6c6-140">After hello tests complete, you will be asked tooprovide an explanation or justification for why your solution does not comply with hello requirement.</span></span>

![提供業務理由](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

<span data-ttu-id="da6c6-142">例如，如果您的方案發佈 tooAzure SQL DW，測試需要您 tooalso hello 評估發行 tooAzure Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="da6c6-142">For example, if your solution publishes tooAzure SQL DW, hello evaluation tests require you tooalso publish tooAzure Analysis Services.</span></span> 

<span data-ttu-id="da6c6-143">您的解決方案可能會使用執行 SQL Server Analysis Services (而非 Azure Analysis Services) 的 IaaS 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="da6c6-143">Your solution may use IaaS virtual machines running Sql Server Analysis Services instead of Azure Analysis Services.</span></span> <span data-ttu-id="da6c6-144">這是可接受的 hello 測試的失敗原因。</span><span class="sxs-lookup"><span data-stu-id="da6c6-144">This would be an acceptable reason for failure of hello test.</span></span>
## <a name="packaging-your-evaluation-results"></a><span data-ttu-id="da6c6-145">封裝您的評估結果</span><span class="sxs-lookup"><span data-stu-id="da6c6-145">Packaging your evaluation results</span></span>
<span data-ttu-id="da6c6-146">完成之後 hello 測試案例，評估封裝將會匯出的 tooa zip 檔案，將會要求您的意見反應 tooprovide hello 評估工具。</span><span class="sxs-lookup"><span data-stu-id="da6c6-146">After completing hello test cases, your evaluation package will be exported tooa zip file and you will be asked tooprovide feedback on hello evaluation tool.</span></span> 

<span data-ttu-id="da6c6-147">您需要這項測試結果的評估再取得核准 toobe 加入您的方案 toobe 與 Microsoft 的 zip 檔案的 tooshare tooAppSource</span><span class="sxs-lookup"><span data-stu-id="da6c6-147">You need tooshare this test results zip file with Microsoft for your solution toobe evaluated before getting approval toobe added tooAppSource</span></span>

![為評估工具評分](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

<span data-ttu-id="da6c6-149">這個區段上方文章涵蓋 hello 工具的各種功能，現在讓我們檢閱此工具會評估的最佳作法的類型。</span><span class="sxs-lookup"><span data-stu-id="da6c6-149">Above section of this article covers various features of hello tool, now let us review types of best practices that this tool evaluates.</span></span>

## <a name="security-evaluation-considerations"></a><span data-ttu-id="da6c6-150">安全性評估考量</span><span class="sxs-lookup"><span data-stu-id="da6c6-150">Security evaluation considerations</span></span>
### <a name="databases-should-use-azure-active-directory-authentication"></a><span data-ttu-id="da6c6-151">資料庫應使用 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="da6c6-151">Databases should use Azure Active Directory authentication</span></span>
<span data-ttu-id="da6c6-152">任何 Azure SQL Azure SQL DW 中的或資源 hello sloution 應該啟用 Azure Active Directory (AAD) 驗證。</span><span class="sxs-lookup"><span data-stu-id="da6c6-152">Any Azure SQL or Azure SQL DW resources in hello sloution should be enabled with Azure Active Directory (AAD) authentication.</span></span> <span data-ttu-id="da6c6-153">AAD 提供單一位置 toomanage 所有您的身分識別和角色。</span><span class="sxs-lookup"><span data-stu-id="da6c6-153">AAD provides a single place toomanage all of your identities and roles.</span></span>

| <span data-ttu-id="da6c6-154">如需下列項目的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="da6c6-154">For more information about</span></span> | <span data-ttu-id="da6c6-155">請參閱此文章</span><span class="sxs-lookup"><span data-stu-id="da6c6-155">See this article</span></span> |
| --- | --- |
| <span data-ttu-id="da6c6-156">AAD 搭配 SQL Database 和 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="da6c6-156">AAD with SQL Database and SQL Data Warehouse</span></span> | [<span data-ttu-id="da6c6-157">利用 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證來驗證</span><span class="sxs-lookup"><span data-stu-id="da6c6-157">Use Azure Active Directory Authentication for authentication with SQL Database or SQL Data Warehouse</span></span>](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| <span data-ttu-id="da6c6-158">設定和管理 AAD</span><span class="sxs-lookup"><span data-stu-id="da6c6-158">Configure and manage AAD</span></span> | [<span data-ttu-id="da6c6-159">使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="da6c6-159">Configure and manage Azure Active Directory authentication with SQL Database or SQL Data Warehouse</span></span>](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| <span data-ttu-id="da6c6-160">Azure WebApps 驗證</span><span class="sxs-lookup"><span data-stu-id="da6c6-160">Azure WebApps authentication</span></span> | [<span data-ttu-id="da6c6-161">Azure App Service 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="da6c6-161">Authentication and authorization in Azure App Service</span></span>](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| <span data-ttu-id="da6c6-162">設定 WebApps 以搭配 AAD</span><span class="sxs-lookup"><span data-stu-id="da6c6-162">Configure WebApps with AAD</span></span> | [<span data-ttu-id="da6c6-163">如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入</span><span class="sxs-lookup"><span data-stu-id="da6c6-163">How tooconfigure your App Service application toouse Azure Active Directory login</span></span>](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a><span data-ttu-id="da6c6-164">資料集可存取 tooend 使用者應支援角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="da6c6-164">Datasets accessible tooend-users should support role-based access control</span></span>
<span data-ttu-id="da6c6-165">執行時 hello 評估工具，將會詢問 toospecify 任何報告或發行的資源。</span><span class="sxs-lookup"><span data-stu-id="da6c6-165">While executing hello evaluation tool, you will be asked toospecify any reporting or publishing resources.</span></span> <span data-ttu-id="da6c6-166">系統會假設這些資源是提供給使用者存取，而非開發人員。</span><span class="sxs-lookup"><span data-stu-id="da6c6-166">It is assumed that these resources are intended for access by end-users, not developers.</span></span> <span data-ttu-id="da6c6-167">這些資源應該能提供角色型存取控制 (RBAC) 順序 tooensure 中僅能 tooaccess 授權資料是使用者。</span><span class="sxs-lookup"><span data-stu-id="da6c6-167">These resources should be provide role-based access control (RBAC) in order tooensure that end users are only able tooaccess authorized data.</span></span>

<span data-ttu-id="da6c6-168">具體而言，任何下列 Azure 資源的 hello 可以設定為使用 RBAC，並會被視為可接受：</span><span class="sxs-lookup"><span data-stu-id="da6c6-168">Specifically, any of hello following Azure resources can be configured with RBAC and are considered acceptable:</span></span>
- <span data-ttu-id="da6c6-169">HDInsight 的安全，請參閱[簡介 tooHadoop 使用安全性已加入網域的 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)</span><span class="sxs-lookup"><span data-stu-id="da6c6-169">Secure HDInsight, see [An introduction tooHadoop security with domain-joined HDInsight clusters](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)</span></span>
- <span data-ttu-id="da6c6-170">Azure SQL，請參閱 [AAD 驗證搭配 Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)</span><span class="sxs-lookup"><span data-stu-id="da6c6-170">Azure SQL, see [AAD authentication with Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)</span></span>
- <span data-ttu-id="da6c6-171">Azure Analysis Services，請參閱[針對 Azure Analysis Services 管理資料庫角色和使用者](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="da6c6-171">Azure Analysis Services, see [Manage database roles and users for Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users)</span></span>
- <span data-ttu-id="da6c6-172">Azure SQL 資料倉儲 (請注意，因為 SQL DW 可支援 RBAC，因此不建議用於直接使用者存取)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-172">Azure SQL Data Warehouse (Be aware that because SQL DW does support RBAC, it is not recommended for direct end-user access.)</span></span>

<span data-ttu-id="da6c6-173">如果您使用可支援 RBAC 的不同資源類型，請指定的 hello 測試案例的理由。</span><span class="sxs-lookup"><span data-stu-id="da6c6-173">If you are using a different resource type that supports RBAC, please specify that in hello test case justification.</span></span>

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a><span data-ttu-id="da6c6-174">Azure Data Lake Store 應使用靜態加密</span><span class="sxs-lookup"><span data-stu-id="da6c6-174">Azure Data Lake Store should use at-rest encryption</span></span>
<span data-ttu-id="da6c6-175">Azure Data Lake Store (ADLS) 支援預設使用 ADLS 受管理加密金鑰的靜態加密。</span><span class="sxs-lookup"><span data-stu-id="da6c6-175">Azure Data Lake Store (ADLS) supports at-rest encryption by default using ADLS-managed encryption keys.</span></span> <span data-ttu-id="da6c6-176">您也可以使用 Azure Key Vault 設定加密。</span><span class="sxs-lookup"><span data-stu-id="da6c6-176">You may also configure encryption using Azure Key Vault.</span></span>

<span data-ttu-id="da6c6-177">如需指定 ADLS 加密設定的相關資訊，請參閱[建立 Azure Data Lake Store 帳戶](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-177">For information about specifying ADLS encryption settings, [Create an Azure Data Lake Store account](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).</span></span>

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a><span data-ttu-id="da6c6-178">Azure SQL 和 Azure SQL 資料倉儲應使用加密</span><span class="sxs-lookup"><span data-stu-id="da6c6-178">Azure SQL and Azure SQL Data Warehouse should use encryption</span></span>
<span data-ttu-id="da6c6-179">Azure SQL 和 Azure SQL DW 都支援透明資料加密 (TDE)，這項功能可提供資料與記錄檔的即時加密和解密。</span><span class="sxs-lookup"><span data-stu-id="da6c6-179">Azure SQL and Azure SQL DW both support Transparent Data Encryption (TDE), which provides real-time encryption and decryption of both data and log files.</span></span>

| <span data-ttu-id="da6c6-180">如需下列項目的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="da6c6-180">For more information about</span></span> | <span data-ttu-id="da6c6-181">請參閱此文章</span><span class="sxs-lookup"><span data-stu-id="da6c6-181">See this article</span></span> |
| --- | --- |
| <span data-ttu-id="da6c6-182">透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="da6c6-182">Transparent Data Encryption (TDE)</span></span> | [<span data-ttu-id="da6c6-183">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="da6c6-183">Transparent Data Encryption</span></span>](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| <span data-ttu-id="da6c6-184">Azure SQL 資料倉儲搭配 TDE</span><span class="sxs-lookup"><span data-stu-id="da6c6-184">Azure SQL Data Warehouse with TDE</span></span> | [<span data-ttu-id="da6c6-185">SQL 資料倉儲加密 TDE TSQL</span><span class="sxs-lookup"><span data-stu-id="da6c6-185">SQL Data Warehouse Encrption TDE TSQL</span></span>](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| <span data-ttu-id="da6c6-186">設定 Azure SQL 以搭配 TDE</span><span class="sxs-lookup"><span data-stu-id="da6c6-186">Configure Azure SQL with TDE</span></span> | [<span data-ttu-id="da6c6-187">Azure SQL Database 的透明資料加密</span><span class="sxs-lookup"><span data-stu-id="da6c6-187">Transparent Data Encryption with Azure SQL Database</span></span>](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| <span data-ttu-id="da6c6-188">設定 Azure SQL 以搭配 Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="da6c6-188">Configure Azure SQL with Always Encrypted</span></span> | [<span data-ttu-id="da6c6-189">SQL Database Always Encrypted Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="da6c6-189">SQL Database Always Encrypted Azure Key Vault</span></span>](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

<span data-ttu-id="da6c6-190">此外 tooTDE，Azure SQL 也支援永遠加密，確保資料會經過加密的新資料加密技術不只在 rest 和在移動資料時用戶端與伺服器之間，也會處於 hello 伺服器上執行命令時使用。</span><span class="sxs-lookup"><span data-stu-id="da6c6-190">In addition tooTDE, Azure SQL also supports Always Encrypted, a new data encryption technology that ensures data is encrypted not only at-rest and during movement between client and server, but also while data is in use while executing commands on hello server.</span></span>

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a><span data-ttu-id="da6c6-191">任何虛擬機器必須部署的 hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="da6c6-191">Any Virtual Machines must be deployed from hello Azure Marketplace</span></span>
<span data-ttu-id="da6c6-192">在順序 tooprovide 安全性 AppSource 之間的一致性層級，我們需要經過認證 Cortana 智慧方案的一部分部署任何虛擬機器，並在 hello Azure Marketplace 上發行。</span><span class="sxs-lookup"><span data-stu-id="da6c6-192">In order tooprovide a consistent level of security across AppSource, we require that any virtual machines deployed as part of a Cortana Intelligence solution be certified and published on hello Azure Marketplace.</span></span>

<span data-ttu-id="da6c6-193">toosearch hello 目前 Azure Marketplace 映像的清單，請參閱[Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-193">toosearch hello current list of Azure Marketplace images, see [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).</span></span>

<span data-ttu-id="da6c6-194">如需如何 toopublish 虛擬機器的映像 Azure Marketplace 資訊，請參閱[指南 toocreate hello Azure Marketplace 的虛擬機器映像](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-194">For information on how toopublish a virtual machine image for Azure Marketplace, see [Guide toocreate a virtual machine image for hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).</span></span>

## <a name="scalability-evaluation-considerations"></a><span data-ttu-id="da6c6-195">延展性評估考量</span><span class="sxs-lookup"><span data-stu-id="da6c6-195">Scalability evaluation considerations</span></span>
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a><span data-ttu-id="da6c6-196">Cortana Intelligence 解決方案應包含一個可調整的巨量資料平台</span><span class="sxs-lookup"><span data-stu-id="da6c6-196">Cortana Intelligence solutions should include a scalable big data platform</span></span>
<span data-ttu-id="da6c6-197">Cortana 智慧方案應該會調整 toovery 大型的資料大小。</span><span class="sxs-lookup"><span data-stu-id="da6c6-197">Cortana Intelligence solutions should scale toovery large data sizes.</span></span> <span data-ttu-id="da6c6-198">在 Azure 中，這表示它們應該包含其中一個 hello 兩個小數位數 Pb 的資料平台：</span><span class="sxs-lookup"><span data-stu-id="da6c6-198">In Azure, this means they should include one of hello two Petabyte-scale data platforms:</span></span>
- <span data-ttu-id="da6c6-199">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da6c6-199">Azure Data Lake Store</span></span>
- <span data-ttu-id="da6c6-200">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="da6c6-200">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="da6c6-201">如果您的方案不需要支援的這些資料大小，或如果您使用替代的資料平台，請加以解釋 hello 測試案例的理由。</span><span class="sxs-lookup"><span data-stu-id="da6c6-201">If your solution does not require support for these data sizes or if you are using an alternative data platform, please explain this in hello test case justification.</span></span>
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a><span data-ttu-id="da6c6-202">Cortana Intelligence 解決方案應包含專用的擷取資料環境</span><span class="sxs-lookup"><span data-stu-id="da6c6-202">Cortana Intelligence solutions should include dedicated ingestion data environments</span></span>
<span data-ttu-id="da6c6-203">Cortana Intelligence 解決方案通常應避免將資料直接插入到關聯式資料來源。</span><span class="sxs-lookup"><span data-stu-id="da6c6-203">Cortana Intelligence solutions should generally avoid directly inserting data into relational data sources.</span></span> <span data-ttu-id="da6c6-204">未經處理資料應改為儲存在非結構化環境中，並使用 Azure Data Factory 針對任何關聯式存放區進行等冪插入/更新。</span><span class="sxs-lookup"><span data-stu-id="da6c6-204">Instead, raw data should be stored in an unstructured environment, with idempotent inserts/updates into any relational stores using Azure Data Factory.</span></span>

<span data-ttu-id="da6c6-205">如需使用 Azure Data Factory 複製資料的詳細資訊，請參閱[教學課程：使用 Visual Studio 建立具有複製活動的管線](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-205">For more information on copying data with Azure Data Factory, [Tutorial: Create a pipeline with Copy Activity using Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).</span></span>

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a><span data-ttu-id="da6c6-206">Azure SQL 資料倉儲應使用 PolyBase 進行資料擷取</span><span class="sxs-lookup"><span data-stu-id="da6c6-206">Azure SQL Data Warehouse should use PolyBase for data ingestion</span></span>
<span data-ttu-id="da6c6-207">Azure SQL DW 支援 PolyBase 以進行可高度擴充、平行的資料擷取。</span><span class="sxs-lookup"><span data-stu-id="da6c6-207">Azure SQL DW supports PolyBase for highly scalable, parallel data ingestion.</span></span> <span data-ttu-id="da6c6-208">PolyBase 可讓您針對外部資料集儲存在 Azure Blob 儲存體或 Azure Data Lake Store toouse Azure SQL DW tooissue 查詢。</span><span class="sxs-lookup"><span data-stu-id="da6c6-208">PolyBase allows you toouse Azure SQL DW tooissue queries against external datasets stored in either Azure Blob Storage or Azure Data Lake Store.</span></span> <span data-ttu-id="da6c6-209">這提供更優異的效能的大量更新 tooalternative 方法。</span><span class="sxs-lookup"><span data-stu-id="da6c6-209">This provides superior performance tooalternative methods of bulk updates.</span></span>

<span data-ttu-id="da6c6-210">如需開始使用 PolyBase 和 Azure SQL DW 的指示，請參閱[在 SQL 資料倉儲中使用 PolyBase 載入資料](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-210">For instructions on getting started with PolyBase and Azure SQL DW, see [Load data with PolyBase in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).</span></span>

<span data-ttu-id="da6c6-211">如需使用 PolyBase 和 Azure SQL DW 的最佳做法詳細資訊，請參閱[在 SQL 資料倉儲中使用 PolyBase 的指南](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-211">For more information about best practices with PolyBase and Azure SQL DW, see [Guide for using PolyBase in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).</span></span>

## <a name="availability-evaluation-considerations"></a><span data-ttu-id="da6c6-212">可用性評估考量</span><span class="sxs-lookup"><span data-stu-id="da6c6-212">Availability evaluation considerations</span></span>

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a><span data-ttu-id="da6c6-213">資料集可存取 tooend 使用者應支援大量的並行使用者</span><span class="sxs-lookup"><span data-stu-id="da6c6-213">Datasets accessible tooend users should support a large volume of concurrent users</span></span>
<span data-ttu-id="da6c6-214">執行時 hello 評估工具，將會詢問 toospecify 任何報告或發行的資源。</span><span class="sxs-lookup"><span data-stu-id="da6c6-214">While executing hello evaluation tool, you will be asked toospecify any reporting or publishing resources.</span></span> <span data-ttu-id="da6c6-215">系統會假設這些資源是提供給使用者存取，而非開發人員。</span><span class="sxs-lookup"><span data-stu-id="da6c6-215">It is assumed that these resources are intended for access by end-users, not developers.</span></span> <span data-ttu-id="da6c6-216">這些資源應支援中等/大型數量的並行使用者。</span><span class="sxs-lookup"><span data-stu-id="da6c6-216">These resources should support medium-large numbers of concurrent users.</span></span>

<span data-ttu-id="da6c6-217">具體而言，Azure SQL 資料倉儲不應該 hello 唯一的資料來源可用 tooend 使用者。</span><span class="sxs-lookup"><span data-stu-id="da6c6-217">Specifically, Azure SQL Data Warehouse should NOT be hello sole data source available tooend users.</span></span> <span data-ttu-id="da6c6-218">如果 Azure SQL DW Power Users 提供做為資源，Azure Analysis Services 應該成為可用 tootypical 使用者。</span><span class="sxs-lookup"><span data-stu-id="da6c6-218">If Azure SQL DW is provided as a resource for Power Users, Azure Analysis Services should be made available tootypical users.</span></span>

<span data-ttu-id="da6c6-219">如需關於 Azure SQL DW 並行限制的詳細資訊，請參閱 [SQL 資料倉儲中的並行存取和工作負載管理](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-219">For more information about Azure SQL DW concurrency limits, see [Concurrency and workload management in SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).</span></span>

<span data-ttu-id="da6c6-220">如需 Azure Analysis Services 的詳細資訊，請參閱 [Analysis Services 概觀](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-220">For more information about Azure Analysis Services, see [Analysis Services Overview](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).</span></span>

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a><span data-ttu-id="da6c6-221">Azure SQL 資源應該有唯讀複本以供容錯移轉</span><span class="sxs-lookup"><span data-stu-id="da6c6-221">Azure SQL resources should have a read-only replica for failover</span></span>
<span data-ttu-id="da6c6-222">Azure SQL database 支援異地複寫 tooa 次要執行個體。</span><span class="sxs-lookup"><span data-stu-id="da6c6-222">Azure SQL databases support geo-replication tooa secondary instance.</span></span> <span data-ttu-id="da6c6-223">這個執行個體可用做為容錯移轉執行個體 tooprovide 高可用性應用程式。</span><span class="sxs-lookup"><span data-stu-id="da6c6-223">This instance can then be used as a failover instance tooprovide high availability applications.</span></span>

<span data-ttu-id="da6c6-224">如需 Azure SQL 資料庫異地複寫的詳細資訊，請參閱 [SQL Database 異地複寫概觀](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-224">For more information about geo-replication for Azure SQL databases, see [SQL Database GEO Replication overview](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).</span></span>

<span data-ttu-id="da6c6-225">如需有關指示 tooconfigure 異地複寫適用於 Azure SQL，請參閱[設定使用 Transact SQL Azure SQL Database 的作用中地理複寫](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-225">For instructions on how tooconfigure geo-replication for Azure SQL, see [Configure active geo-replication for Azure SQL Database with Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).</span></span>

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a><span data-ttu-id="da6c6-226">Azure SQL 資料倉儲應已啟用異地備援備份</span><span class="sxs-lookup"><span data-stu-id="da6c6-226">Azure SQL Data Warehouse should have geo-redundant backups enabled</span></span>
<span data-ttu-id="da6c6-227">Azure SQL DW 支援每日備份 toogeo 備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="da6c6-227">Azure SQL DW supports daily backups toogeo-redundant storage.</span></span> <span data-ttu-id="da6c6-228">此地理複寫可確保您能夠還原 hello 資料倉儲，即使在情況下，您無法存取儲存在主要區域中的快照集。</span><span class="sxs-lookup"><span data-stu-id="da6c6-228">This geo-replication ensures you can restore hello data warehouse even in situations where you cannot access snapshots stored in your primary region.</span></span> <span data-ttu-id="da6c6-229">此功能針對 Cortana Intelligence 解決方案預設為開啟，且不應該停用。</span><span class="sxs-lookup"><span data-stu-id="da6c6-229">This feature is on by default and should not be disable for Cortana Intelligence solutions.</span></span>

<span data-ttu-id="da6c6-230">如需 Azure SQL DW 備份和還原的詳細資訊，請參閱 [SQL 資料倉儲備份](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-230">For more information about Azure SQL DW backups and restoration, see here [SQL Data Warehouse Backups](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).</span></span>

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a><span data-ttu-id="da6c6-231">虛擬機器應使用可用性設定組進行設定</span><span class="sxs-lookup"><span data-stu-id="da6c6-231">Virtual machines should be configured with availability sets</span></span>
<span data-ttu-id="da6c6-232">應該設定 azure 虛擬機器的計劃性與非計劃性的維護事件順序 toominimize hello 影響的可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="da6c6-232">Azure virtual machines should be configured in availability sets in order toominimize hello impact of planned and unplanned maintenance events.</span></span>

<span data-ttu-id="da6c6-233">如需有關 Azure 虛擬機器可用性的詳細資訊，請參閱[管理的 Windows Azure 虛擬機器中的 hello 可用性](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-233">For more information about Azure virtual machine availability, see [Manage hello availability of Windows virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).</span></span>

## <a name="other-evaluation-considerations"></a><span data-ttu-id="da6c6-234">其他評估考量</span><span class="sxs-lookup"><span data-stu-id="da6c6-234">Other evaluation considerations</span></span>
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a><span data-ttu-id="da6c6-235">Cortana Intelligence 應用程式針對資料協調流程應使用集中式工具</span><span class="sxs-lookup"><span data-stu-id="da6c6-235">Cortana Intelligence apps should use a centralized tool for data orchestration</span></span>
<span data-ttu-id="da6c6-236">使用單一工具來對資料移動及轉換進行管理和排程，能確保關鍵任務資料的一致性。</span><span class="sxs-lookup"><span data-stu-id="da6c6-236">Using a single tool for managing and scheduling data movement and transformation ensures consistency around mission-critical data.</span></span> <span data-ttu-id="da6c6-237">它可提供關於重試邏輯、相依性管理，警示/記錄等項目的清楚邏輯。我們建議使用 hello [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction)資料在 Azure 中的協調流程。</span><span class="sxs-lookup"><span data-stu-id="da6c6-237">It provides a clear logic around retry logic, dependency management, alert/logging, etc. We recommend hello use of [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) for data orchestration in Azure.</span></span>

<span data-ttu-id="da6c6-238">如果您針對資料協調流程使用 Azure Data Factory 以外的工具，請說明您使用的是哪些工具。</span><span class="sxs-lookup"><span data-stu-id="da6c6-238">If you are using a tool other than Azure Data Factory for data orchestration, please describe which tool or tools you are using.</span></span>
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a><span data-ttu-id="da6c6-239">Azure Machine Learning 模型應使用 Azure Data Factory 重新訓練</span><span class="sxs-lookup"><span data-stu-id="da6c6-239">Azure Machine Learning models should be retrained using Azure Data Factory</span></span>
<span data-ttu-id="da6c6-240">Azure 機器學習 (AzureML) 提供簡單 toouse 工具 hello 建立及部署的預測模型和機器學習管線。</span><span class="sxs-lookup"><span data-stu-id="da6c6-240">Azure Machine Learning (AzureML) provides easy toouse tools for hello creation and deployment of predictive modeling and machine learning pipelines.</span></span> <span data-ttu-id="da6c6-241">不過，請務必生產部署這些 AzureML 模型不以單一固定資料集為基礎，但改為適應 toohello 移位 dynamics 的真實世界的現象。</span><span class="sxs-lookup"><span data-stu-id="da6c6-241">However, it is important that production deployments of these AzureML models is not based on a single fixed dataset, but instead adapts toohello shifting dynamics of real-world phenomena.</span></span>

<span data-ttu-id="da6c6-242">如需在 AzureML 中建立重新訓練 Web 服務的詳細資訊，請參閱[以程式設計方式重新訓練機器學習服務模型](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-242">For more information on creating retraining web services in AzureML, see [Retrain Machine Learning models programmatically](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).</span></span>

<span data-ttu-id="da6c6-243">如需有關如何自動化使用 Azure Data Factory 的 hello 模型定型程序的詳細資訊，請參閱[更新 Azure 機器學習模型使用的更新資源活動](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity)。</span><span class="sxs-lookup"><span data-stu-id="da6c6-243">For more information about automating hello model training process using Azure Data Factory, see [Updating Azure Machine Learning models using Update Resource Activity](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).</span></span>

## <a name="existing-documentation"></a><span data-ttu-id="da6c6-244">現有文件</span><span class="sxs-lookup"><span data-stu-id="da6c6-244">Existing documentation</span></span>
[<span data-ttu-id="da6c6-245">Microsoft Azure 認證 toogrow 業務 cloud</span><span class="sxs-lookup"><span data-stu-id="da6c6-245">Microsoft Azure Certified toogrow your cloud business</span></span>](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[<span data-ttu-id="da6c6-246">Microsoft Azure Cortana Intellignece 認證</span><span class="sxs-lookup"><span data-stu-id="da6c6-246">Microsoft Azure Certified for Cortana Intellignece</span></span>](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

