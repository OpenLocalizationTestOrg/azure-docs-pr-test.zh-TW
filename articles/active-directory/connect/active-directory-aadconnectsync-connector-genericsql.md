---
title: "aaaGeneric SQL 連接器 |Microsoft 文件"
description: "本文說明如何 tooconfigure Microsoft 泛型 SQL 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a><span data-ttu-id="d496a-103">一般 SQL 連接器技術參考</span><span class="sxs-lookup"><span data-stu-id="d496a-103">Generic SQL Connector technical reference</span></span>
<span data-ttu-id="d496a-104">本文說明 hello 泛型 SQL 連接器。</span><span class="sxs-lookup"><span data-stu-id="d496a-104">This article describes hello Generic SQL Connector.</span></span> <span data-ttu-id="d496a-105">hello 文章適用 toohello 下列產品：</span><span class="sxs-lookup"><span data-stu-id="d496a-105">hello article applies toohello following products:</span></span>

* <span data-ttu-id="d496a-106">Microsoft Identity Manager 2016 (MIM2016)</span><span class="sxs-lookup"><span data-stu-id="d496a-106">Microsoft Identity Manager 2016 (MIM2016)</span></span>
* <span data-ttu-id="d496a-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span><span class="sxs-lookup"><span data-stu-id="d496a-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span></span>
  * <span data-ttu-id="d496a-108">必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。</span><span class="sxs-lookup"><span data-stu-id="d496a-108">Must use hotfix 4.1.3671.0 or later [KB3092178](https://support.microsoft.com/kb/3092178).</span></span>

<span data-ttu-id="d496a-109">MIM2016 和 FIM2010R2，hello 連接器可做為從 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495)。</span><span class="sxs-lookup"><span data-stu-id="d496a-109">For MIM2016 and FIM2010R2, hello Connector is available as a download from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).</span></span>

<span data-ttu-id="d496a-110">toosee 在動作中，此連接器，請參閱 「 hello[泛型 SQL Connector 逐步](active-directory-aadconnectsync-connector-genericsql-step-by-step.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="d496a-110">toosee this Connector in action, see hello [Generic SQL Connector step-by-step](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) article.</span></span>

## <a name="overview-of-hello-generic-sql-connector"></a><span data-ttu-id="d496a-111">Hello 泛型 SQL 連接器的概觀</span><span class="sxs-lookup"><span data-stu-id="d496a-111">Overview of hello Generic SQL Connector</span></span>
<span data-ttu-id="d496a-112">hello 泛型 SQL 連接器可讓您使用 ODBC 連接的資料庫系統 toointegrate hello 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="d496a-112">hello Generic SQL Connector enables you toointegrate hello synchronization service with a database system that offers ODBC connectivity.</span></span>  

<span data-ttu-id="d496a-113">從高階觀點來看，hello hello 連接器目前版本支援下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="d496a-113">From a high-level perspective, hello following features are supported by hello current release of hello connector:</span></span>

| <span data-ttu-id="d496a-114">功能</span><span class="sxs-lookup"><span data-stu-id="d496a-114">Feature</span></span> | <span data-ttu-id="d496a-115">支援</span><span class="sxs-lookup"><span data-stu-id="d496a-115">Support</span></span> |
| --- | --- |
| <span data-ttu-id="d496a-116">連接的資料來源</span><span class="sxs-lookup"><span data-stu-id="d496a-116">Connected data source</span></span> |<span data-ttu-id="d496a-117">hello 連接器僅支援所有的 64 位元 ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="d496a-117">hello Connector is supported with all 64-bit ODBC drivers.</span></span> <span data-ttu-id="d496a-118">經過 hello 下列測試：</span><span class="sxs-lookup"><span data-stu-id="d496a-118">It has been tested with hello following:</span></span> <li><span data-ttu-id="d496a-119">Microsoft SQL Server 與 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d496a-119">Microsoft SQL Server & SQL Azure</span></span></li><li><span data-ttu-id="d496a-120">IBM DB2 10.x</span><span class="sxs-lookup"><span data-stu-id="d496a-120">IBM DB2 10.x</span></span></li><li><span data-ttu-id="d496a-121">IBM DB2 9.x</span><span class="sxs-lookup"><span data-stu-id="d496a-121">IBM DB2 9.x</span></span></li><li><span data-ttu-id="d496a-122">Oracle 10 和 11 g</span><span class="sxs-lookup"><span data-stu-id="d496a-122">Oracle 10 & 11g</span></span></li><li><span data-ttu-id="d496a-123">MySQL 5.x</span><span class="sxs-lookup"><span data-stu-id="d496a-123">MySQL 5.x</span></span></li> |
| <span data-ttu-id="d496a-124">案例</span><span class="sxs-lookup"><span data-stu-id="d496a-124">Scenarios</span></span> |<li><span data-ttu-id="d496a-125">物件生命週期管理</span><span class="sxs-lookup"><span data-stu-id="d496a-125">Object Lifecycle Management</span></span></li><li><span data-ttu-id="d496a-126">密碼管理</span><span class="sxs-lookup"><span data-stu-id="d496a-126">Password Management</span></span></li> |
| <span data-ttu-id="d496a-127">作業</span><span class="sxs-lookup"><span data-stu-id="d496a-127">Operations</span></span> |<li><span data-ttu-id="d496a-128">完整匯入和差異匯入、匯出</span><span class="sxs-lookup"><span data-stu-id="d496a-128">Full Import and Delta Import, Export</span></span></li><li><span data-ttu-id="d496a-129">針對匯出：新增、刪除、更新和取代</span><span class="sxs-lookup"><span data-stu-id="d496a-129">For Export: Add, Delete, Update, and Replace</span></span></li><li><span data-ttu-id="d496a-130">設定密碼、變更密碼</span><span class="sxs-lookup"><span data-stu-id="d496a-130">Set Password, Change Password</span></span></li> |
| <span data-ttu-id="d496a-131">結構描述</span><span class="sxs-lookup"><span data-stu-id="d496a-131">Schema</span></span> |<li><span data-ttu-id="d496a-132">動態探索物件和屬性</span><span class="sxs-lookup"><span data-stu-id="d496a-132">Dynamic discovery of objects and attributes</span></span></li> |

### <a name="prerequisites"></a><span data-ttu-id="d496a-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="d496a-133">Prerequisites</span></span>
<span data-ttu-id="d496a-134">使用 hello 連接器之前，請確定您擁有 hello 同步處理伺服器 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="d496a-134">Before you use hello Connector, make sure you have hello following on hello synchronization server:</span></span>

* <span data-ttu-id="d496a-135">Microsoft .NET 4.5.2 Framework 或更新版本</span><span class="sxs-lookup"><span data-stu-id="d496a-135">Microsoft .NET 4.5.2 Framework or later</span></span>
* <span data-ttu-id="d496a-136">64 位元的 ODBC 用戶端驅動程式</span><span class="sxs-lookup"><span data-stu-id="d496a-136">64-bit ODBC client drivers</span></span>

### <a name="permissions-in-connected-data-source"></a><span data-ttu-id="d496a-137">連接的資料來源權限</span><span class="sxs-lookup"><span data-stu-id="d496a-137">Permissions in connected data source</span></span>
<span data-ttu-id="d496a-138">toocreate 或執行任何支援的 hello 工作一般 SQL 連接器中，您必須具有：</span><span class="sxs-lookup"><span data-stu-id="d496a-138">toocreate or perform any of hello supported tasks in Generic SQL connector, you must have:</span></span>

* <span data-ttu-id="d496a-139">db_datareader</span><span class="sxs-lookup"><span data-stu-id="d496a-139">db_datareader</span></span>
* <span data-ttu-id="d496a-140">db_datawriter</span><span class="sxs-lookup"><span data-stu-id="d496a-140">db_datawriter</span></span>

### <a name="ports-and-protocols"></a><span data-ttu-id="d496a-141">連接埠和通訊協定</span><span class="sxs-lookup"><span data-stu-id="d496a-141">Ports and protocols</span></span>
<span data-ttu-id="d496a-142">Hello hello ODBC 驅動程式 toowork 所需的連接埠，請參閱 hello 資料庫供應商的文件。</span><span class="sxs-lookup"><span data-stu-id="d496a-142">For hello ports required for hello ODBC driver toowork, consult hello database vendor's documentation.</span></span>

## <a name="create-a-new-connector"></a><span data-ttu-id="d496a-143">建立新的連接器</span><span class="sxs-lookup"><span data-stu-id="d496a-143">Create a new Connector</span></span>
<span data-ttu-id="d496a-144">tooCreate 一般 SQL 連接器，請在**同步處理服務**選取**管理代理程式**和**建立**。</span><span class="sxs-lookup"><span data-stu-id="d496a-144">tooCreate a Generic SQL connector, in **Synchronization Service** select **Management Agent** and **Create**.</span></span> <span data-ttu-id="d496a-145">選取 hello**一般 SQL (Microsoft)**連接器。</span><span class="sxs-lookup"><span data-stu-id="d496a-145">Select hello **Generic SQL (Microsoft)** Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a><span data-ttu-id="d496a-147">連線能力</span><span class="sxs-lookup"><span data-stu-id="d496a-147">Connectivity</span></span>
<span data-ttu-id="d496a-148">hello 連接器會使用 ODBC DSN 檔案的連線。</span><span class="sxs-lookup"><span data-stu-id="d496a-148">hello Connector uses an ODBC DSN file for connectivity.</span></span> <span data-ttu-id="d496a-149">建立 hello DSN 檔案使用**ODBC 資料來源**下 hello [開始] 功能表中找到**系統管理工具**。</span><span class="sxs-lookup"><span data-stu-id="d496a-149">Create hello DSN file using **ODBC Data Sources** found in hello start menu under **Administrative Tools**.</span></span> <span data-ttu-id="d496a-150">在 [hello] 系統管理工具，建立**檔案 DSN**讓它可以提供 toohello 連接器。</span><span class="sxs-lookup"><span data-stu-id="d496a-150">In hello administrative tool, create a **File DSN** so it can be provided toohello Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

<span data-ttu-id="d496a-152">hello 連線能力畫面第一次為 hello，當您建立新的一般 SQL 連接器。</span><span class="sxs-lookup"><span data-stu-id="d496a-152">hello Connectivity screen is hello first when you create a new Generic SQL Connector.</span></span> <span data-ttu-id="d496a-153">您必須先 tooprovide hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d496a-153">You first need tooprovide hello following information:</span></span>

* <span data-ttu-id="d496a-154">DSN 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="d496a-154">DSN file path</span></span>
* <span data-ttu-id="d496a-155">驗證</span><span class="sxs-lookup"><span data-stu-id="d496a-155">Authentication</span></span>
  * <span data-ttu-id="d496a-156">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d496a-156">User Name</span></span>
  * <span data-ttu-id="d496a-157">密碼</span><span class="sxs-lookup"><span data-stu-id="d496a-157">Password</span></span>

<span data-ttu-id="d496a-158">hello 資料庫應該支援其中一種驗證方法：</span><span class="sxs-lookup"><span data-stu-id="d496a-158">hello database should support one of these authentication methods:</span></span>

* <span data-ttu-id="d496a-159">**Windows 驗證**: hello 驗證資料庫使用 hello Windows 認證 tooverify hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d496a-159">**Windows authentication**: hello authenticating database uses hello Windows credentials tooverify hello user.</span></span> <span data-ttu-id="d496a-160">hello 使用者名稱/密碼指定為使用的 tooauthenticate 與 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d496a-160">hello user name/password specified is used tooauthenticate with hello database.</span></span> <span data-ttu-id="d496a-161">此帳戶需要權限 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d496a-161">This account needs permissions toohello database.</span></span>
* <span data-ttu-id="d496a-162">**SQL 驗證**： 資料庫使用 hello 使用者名稱/密碼進行驗證的 hello 定義一個 hello 連線能力畫面 tooconnect toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d496a-162">**SQL authentication**: hello authenticating database uses hello user name/password defined one hello Connectivity screen tooconnect toohello database.</span></span> <span data-ttu-id="d496a-163">如果您儲存使用者名稱/密碼 hello hello DSN 檔案中，hello hello 連線能力畫面上所提供的認證具有優先順序。</span><span class="sxs-lookup"><span data-stu-id="d496a-163">If you store hello user name/pasword in hello DSN file, hello credentials provided on hello Connectivity screen have precedence.</span></span>
* <span data-ttu-id="d496a-164">**Azure SQL Database 驗證**： 如需詳細資訊，請參閱[連接 tooSQL 資料庫使用 Azure Active Directory 驗證](../../sql-database/sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="d496a-164">**Azure SQL Database authentication**: For more information, see [Connect tooSQL Database By Using Azure Active Directory Authentication](../../sql-database/sql-database-aad-authentication.md).</span></span>

<span data-ttu-id="d496a-165">**DN 是錨點**: hello DN 如果您選取此選項時，也會當做 hello 錨點屬性使用。</span><span class="sxs-lookup"><span data-stu-id="d496a-165">**DN is Anchor**: If you select this option, hello DN is also used as hello anchor attribute.</span></span> <span data-ttu-id="d496a-166">它可以使用的簡單實作，但也有下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="d496a-166">It can be used for a simple implementation but also has hello following limitation:</span></span>

* <span data-ttu-id="d496a-167">連接器只支援一種物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-167">Connector supports only one object type.</span></span> <span data-ttu-id="d496a-168">因此屬性只能參考的任何參考 hello 相同物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-168">Therefore any reference attributes can only reference hello same object type.</span></span>

<span data-ttu-id="d496a-169">**匯出型別： 物件取代**： 在匯出期間，當只有某些屬性已變更，匯出 hello 整個物件所有屬性，並取代 hello 現有物件。</span><span class="sxs-lookup"><span data-stu-id="d496a-169">**Export Type: Object Replace**: During export, when only some attributes have changed, hello entire object with all attributes is exported and replaces hello existing object.</span></span>

### <a name="schema-1-detect-object-types"></a><span data-ttu-id="d496a-170">結構描述 1 (偵測物件類型)</span><span class="sxs-lookup"><span data-stu-id="d496a-170">Schema 1 (Detect object types)</span></span>
<span data-ttu-id="d496a-171">這個頁面上，您將 tooconfigure hello 連接器的方式進行 toofind hello hello 資料庫中的不同物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-171">On this page, you are going tooconfigure how hello Connector is going toofind hello different object types in hello database.</span></span>

<span data-ttu-id="d496a-172">每個物件類型會顯示為一個資料分割，並且在 [設定資料分割和階層] 上進一步設定。</span><span class="sxs-lookup"><span data-stu-id="d496a-172">Every object type is presented as a partition and configured further on **Configure Partitions and Hierarchies**.</span></span>

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

<span data-ttu-id="d496a-174">**物件類型的偵測方法**: hello 連接器支援這些物件類型的偵測方法。</span><span class="sxs-lookup"><span data-stu-id="d496a-174">**Object Type detection method**: hello Connector supports these object type detection methods.</span></span>

* <span data-ttu-id="d496a-175">**固定值**： 您提供的物件類型的 hello 清單，以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="d496a-175">**Fixed Value**: You provide hello list of object types with a comma-separated list.</span></span> <span data-ttu-id="d496a-176">例如： `User,Group,Department`。</span><span class="sxs-lookup"><span data-stu-id="d496a-176">For example: `User,Group,Department`.</span></span>  
  <span data-ttu-id="d496a-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span></span>
* <span data-ttu-id="d496a-178">**資料表/檢視/預存程序**： 提供 hello hello 資料表/檢視/預存程序名稱，然後 hello 提供 hello 清單的物件類型的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="d496a-178">**Table/View/Stored Procedure**: Provide hello name of hello table/view/stored procedure and then hello column name that provides hello list of object types.</span></span> <span data-ttu-id="d496a-179">如果您使用預存程序，然後也提供參數，格式為 hello **[名稱]: [方向]: [Value]**。</span><span class="sxs-lookup"><span data-stu-id="d496a-179">If you use a stored procedure, then also provide parameters for it in hello format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="d496a-180">提供每個參數，在不同行 （使用 Ctrl + Enter tooget 新行）。</span><span class="sxs-lookup"><span data-stu-id="d496a-180">Provide each parameter on a separate line (use Ctrl+Enter tooget a new line).</span></span>  
  <span data-ttu-id="d496a-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span></span>
* <span data-ttu-id="d496a-182">**SQL 查詢**： 此選項可讓您 tooprovide SQL 查詢，以傳回物件類型的單一資料行，例如`SELECT [Column Name] FROM TABLENAME`。</span><span class="sxs-lookup"><span data-stu-id="d496a-182">**SQL Query**: This option allows you tooprovide a SQL query that returns a single column with object types, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="d496a-183">hello 傳回資料行必須是字串類型 (varchar)。</span><span class="sxs-lookup"><span data-stu-id="d496a-183">hello returned column must be of type string (varchar).</span></span>

### <a name="schema-2-detect-attribute-types"></a><span data-ttu-id="d496a-184">結構描述 2 (偵測屬性類型)</span><span class="sxs-lookup"><span data-stu-id="d496a-184">Schema 2 (Detect attribute types)</span></span>
<span data-ttu-id="d496a-185">這個頁面上，您將如何 tooconfigure hello 的屬性名稱和型別將 toobe 偵測到。</span><span class="sxs-lookup"><span data-stu-id="d496a-185">On this page, you are going tooconfigure how hello attribute names and types are going toobe detected.</span></span> <span data-ttu-id="d496a-186">hello 組態選項會列出每個 hello 前一頁上偵測到的物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-186">hello configuration options are listed for every object type detected on hello previous page.</span></span>

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

<span data-ttu-id="d496a-188">**屬性類型的偵測方法**: hello 連接器支援結構描述 1 畫面中的這些屬性類型偵測方法可搭配每個偵測到的物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-188">**Attribute Type detection method**: hello Connector supports these attribute type detection methods with every detected object type in Schema 1 screen.</span></span>

* <span data-ttu-id="d496a-189">**資料表/檢視/預存程序**： 提供 hello hello 資料表/檢視/預存程序應使用的 toofind hello 屬性名稱的名稱。</span><span class="sxs-lookup"><span data-stu-id="d496a-189">**Table/View/Stored Procedure**: Provide hello name of hello table/view/stored procedure that should be used toofind hello attribute names.</span></span> <span data-ttu-id="d496a-190">如果您使用預存程序，然後也提供參數，格式為 hello **[名稱]: [方向]: [Value]**。</span><span class="sxs-lookup"><span data-stu-id="d496a-190">If you use a stored procedure, then also provide parameters for it in hello format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="d496a-191">提供每個參數，在不同行 （使用 Ctrl + Enter tooget 新行）。</span><span class="sxs-lookup"><span data-stu-id="d496a-191">Provide each parameter on a separate line (use Ctrl+Enter tooget a new line).</span></span> <span data-ttu-id="d496a-192">toodetect hello 屬性名稱中的多重值屬性，提供以逗號分隔清單的資料表或檢視表。</span><span class="sxs-lookup"><span data-stu-id="d496a-192">toodetect hello attribute names in a multi-valued attribute, provide a comma-separated list of Tables or Views.</span></span> <span data-ttu-id="d496a-193">當父和子資料表具有相同的資料行名稱時，則不支援多重值案例。</span><span class="sxs-lookup"><span data-stu-id="d496a-193">Multivalued scenarios are not supported when parent and child table have same column names.</span></span>
* <span data-ttu-id="d496a-194">**SQL 查詢**： 此選項可讓您 tooprovide SQL 查詢，以傳回屬性名稱的單一資料行，例如`SELECT [Column Name] FROM TABLENAME`。</span><span class="sxs-lookup"><span data-stu-id="d496a-194">**SQL query**: This option allows you tooprovide a SQL query that returns a single column with attribute names, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="d496a-195">hello 傳回資料行必須是字串類型 (varchar)。</span><span class="sxs-lookup"><span data-stu-id="d496a-195">hello returned column must be of type string (varchar).</span></span>

### <a name="schema-3-define-anchor-and-dn"></a><span data-ttu-id="d496a-196">結構描述 3 (定義錨點和 DN)</span><span class="sxs-lookup"><span data-stu-id="d496a-196">Schema 3 (Define anchor and DN)</span></span>
<span data-ttu-id="d496a-197">此頁面可讓您 tooconfigure 錨點和 DN 屬性每個偵測到的物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-197">This page allows you tooconfigure anchor and DN attribute for each detected object type.</span></span> <span data-ttu-id="d496a-198">您可以選取多個屬性 toomake hello 錨點唯一。</span><span class="sxs-lookup"><span data-stu-id="d496a-198">You can select multiple attributes toomake hello anchor unique.</span></span>

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* <span data-ttu-id="d496a-200">不會列出多重值和布林值屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-200">Multi-valued and Boolean attributes are not listed.</span></span>
* <span data-ttu-id="d496a-201">相同的屬性無法用於 DN 和 錨點，除非**DN 是錨點**hello 連線能力 頁面上選取。</span><span class="sxs-lookup"><span data-stu-id="d496a-201">Same attribute cannot use for DN and anchor, unless **DN is Anchor** is selected on hello Connectivity page.</span></span>
* <span data-ttu-id="d496a-202">如果**DN 是錨點**選取在 hello 連線能力 頁面上，此頁面需要唯一的 hello DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-202">If **DN is Anchor** is selected on hello Connectivity page, this page requires only hello DN attribute.</span></span> <span data-ttu-id="d496a-203">這個屬性也會用為 hello 錨點屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-203">This attribute would also be used as hello anchor attribute.</span></span>

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a><span data-ttu-id="d496a-205">結構描述 4 (定義屬性類型、參考和方向)</span><span class="sxs-lookup"><span data-stu-id="d496a-205">Schema 4 (Define attribute type, reference, and direction)</span></span>
<span data-ttu-id="d496a-206">此頁面可讓您 tooconfigure hello 屬性類型，例如整數、 二進位或布林值，以及針對每個屬性的方向。</span><span class="sxs-lookup"><span data-stu-id="d496a-206">This page allows you tooconfigure hello attribute type, such as integer, binary, or Boolean, and direction for each attribute.</span></span> <span data-ttu-id="d496a-207">[結構描述 2]  頁面中的所有屬性都會列出，包括多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-207">All attributes from page **schema 2** are listed including multi-valued attributes.</span></span>

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* <span data-ttu-id="d496a-209">**資料型別**: toomap hello 屬性型別 toothose 類型已知 hello 同步處理引擎所使用。</span><span class="sxs-lookup"><span data-stu-id="d496a-209">**DataType**: Used toomap hello attribute type toothose types known by hello sync engine.</span></span> <span data-ttu-id="d496a-210">hello 預設值是相同的型別在 hello SQL 結構描述中，偵測到的 toouse hello 但無法輕易地偵測 DateTime 和參考。</span><span class="sxs-lookup"><span data-stu-id="d496a-210">hello default is toouse hello same type as detected in hello SQL schema, but DateTime and Reference are not easily detectable.</span></span> <span data-ttu-id="d496a-211">對於，您需要 toospecify **DateTime**或**參考**。</span><span class="sxs-lookup"><span data-stu-id="d496a-211">For those, you need toospecify **DateTime** or **Reference**.</span></span>
* <span data-ttu-id="d496a-212">**方向**: hello 屬性方向 tooImport、 匯出或 ImportExport，您可以設定。</span><span class="sxs-lookup"><span data-stu-id="d496a-212">**Direction**: You can set hello attribute direction tooImport, Export, or ImportExport.</span></span> <span data-ttu-id="d496a-213">ImportExport 是預設值。</span><span class="sxs-lookup"><span data-stu-id="d496a-213">ImportExport is default.</span></span>

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

<span data-ttu-id="d496a-215">注意：</span><span class="sxs-lookup"><span data-stu-id="d496a-215">Notes:</span></span>

* <span data-ttu-id="d496a-216">如果屬性型別不是偵測到 hello 連接器，它會使用 hello 字串資料類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-216">If an attribute type is not detectable by hello Connector, it uses hello String data type.</span></span>
* <span data-ttu-id="d496a-217">**巢狀資料表** 視為一個資料行的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="d496a-217">**Nested tables** can be considered one-column database tables.</span></span> <span data-ttu-id="d496a-218">Oracle 會 hello 巢狀資料表資料列儲存不依特定順序。</span><span class="sxs-lookup"><span data-stu-id="d496a-218">Oracle stores hello rows of a nested table in no particular order.</span></span> <span data-ttu-id="d496a-219">不過，當您擷取 hello 巢狀的資料表至 PL/SQL 變數，hello 資料列會提供從 1 開始的連續註標。</span><span class="sxs-lookup"><span data-stu-id="d496a-219">However, when you retrieve hello nested table into a PL/SQL variable, hello rows are given consecutive subscripts starting at 1.</span></span> <span data-ttu-id="d496a-220">提供陣列存取 tooindividual 資料列。</span><span class="sxs-lookup"><span data-stu-id="d496a-220">That gives you array-like access tooindividual rows.</span></span>
* <span data-ttu-id="d496a-221">**VARRYS** hello 連接器中不支援。</span><span class="sxs-lookup"><span data-stu-id="d496a-221">**VARRYS** are not supported in hello connector.</span></span>

### <a name="schema-5-define-partition-for-reference-attributes"></a><span data-ttu-id="d496a-222">結構描述 5 (定義參考屬性的資料分割)</span><span class="sxs-lookup"><span data-stu-id="d496a-222">Schema 5 (Define partition for reference attributes)</span></span>
<span data-ttu-id="d496a-223">在此頁面上，您會為所有參考屬性設定屬性所參考的資料分割 (物件類型)。</span><span class="sxs-lookup"><span data-stu-id="d496a-223">On this page, you configure for all reference attributes which partition (object type) an attribute is referring to.</span></span>

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

<span data-ttu-id="d496a-225">如果您使用**DN 是錨點**，則您必須使用相同的物件型別為其中一個您要從參考 hello 的 hello。</span><span class="sxs-lookup"><span data-stu-id="d496a-225">If you use **DN is anchor**, then you must use hello same object type as hello one you are referring from.</span></span> <span data-ttu-id="d496a-226">您無法參考其他物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-226">You cannot reference another object type.</span></span>

>[!NOTE]
<span data-ttu-id="d496a-227">現在是可選擇的 hello 2017 年 3 月更新中啟動"*"這個選項時所選然後所有可能成員類型將會匯入。</span><span class="sxs-lookup"><span data-stu-id="d496a-227">Starting in hello March 2017 update there is now an option for "*" When this option is chosen then all possible member types will be imported.</span></span>

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 <span data-ttu-id="d496a-229">自 2017 年 hello"*"也稱為**任何選項**已變更 toosupport 匯入和匯出流程。</span><span class="sxs-lookup"><span data-stu-id="d496a-229">As of May 2017 hello “*” aka **any option** has been changed toosupport import and export flow.</span></span> <span data-ttu-id="d496a-230">如果您想要 toouse 這個選項您多重值的資料表/檢視應該包含 hello 物件類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-230">If you want toouse this option your multi-valued table/view should have an attribute that contains hello object type.</span></span>

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> <span data-ttu-id="d496a-231">如果"*"也必須指定 hello hello hello 物件類型資料行名稱，然後選取。</span><span class="sxs-lookup"><span data-stu-id="d496a-231">If "*" is selected then hello name of hello column with hello object type must also be specified.</span></span></br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

<span data-ttu-id="d496a-232">在匯入之後，您會看到類似下面的 toohello 影像：</span><span class="sxs-lookup"><span data-stu-id="d496a-232">After import you will see something similar toohello image below:</span></span>

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a><span data-ttu-id="d496a-234">全域參數</span><span class="sxs-lookup"><span data-stu-id="d496a-234">Global Parameters</span></span>
<span data-ttu-id="d496a-235">hello 全域參數頁面是使用的 tooconfigure 差異匯入，日期/時間格式和密碼方法。</span><span class="sxs-lookup"><span data-stu-id="d496a-235">hello Global Parameters page is used tooconfigure Delta Import, Date/Time format, and Password method.</span></span>

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



<span data-ttu-id="d496a-237">hello 泛型 SQL Connector 支援 hello 差異匯入下列方法：</span><span class="sxs-lookup"><span data-stu-id="d496a-237">hello Generic SQL Connector supports hello following methods for Delta Import:</span></span>

* <span data-ttu-id="d496a-238">**觸發程序**：請參閱 [使用觸發程序產生差異檢視](https://technet.microsoft.com/library/cc708665.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d496a-238">**Trigger**: See [Generating Delta Views Using Triggers](https://technet.microsoft.com/library/cc708665.aspx).</span></span>
* <span data-ttu-id="d496a-239">**浮水印**：可以用於任何資料庫的一般方法。</span><span class="sxs-lookup"><span data-stu-id="d496a-239">**Watermark**: A generic approach that can be used with any database.</span></span> <span data-ttu-id="d496a-240">hello 浮水印查詢是根據 hello 資料庫供應商，預先填入。</span><span class="sxs-lookup"><span data-stu-id="d496a-240">hello watermark query is pre-populated based on hello database vendor.</span></span> <span data-ttu-id="d496a-241">浮水印資料行必須出現在所用的每個資料表/檢視上。</span><span class="sxs-lookup"><span data-stu-id="d496a-241">A watermark column must be present on every table/view used.</span></span> <span data-ttu-id="d496a-242">此資料行必須在插入和更新 toohello 做為資料表和其相依性追蹤 (多重值或子系) 資料表。</span><span class="sxs-lookup"><span data-stu-id="d496a-242">This column must track inserts and updates toohello tables as and its dependent (multi-valued or child) tables.</span></span> <span data-ttu-id="d496a-243">同步處理服務與 hello 資料庫伺服器之間的 hello 時鐘必須同步處理。</span><span class="sxs-lookup"><span data-stu-id="d496a-243">hello clocks between Synchronization Service and hello database server must be synchronized.</span></span> <span data-ttu-id="d496a-244">如果沒有，則可能會省略 hello 差異匯入中的某些項目。</span><span class="sxs-lookup"><span data-stu-id="d496a-244">If not, some entries in hello delta import might be omitted.</span></span>  
  <span data-ttu-id="d496a-245">限制：</span><span class="sxs-lookup"><span data-stu-id="d496a-245">Limitation:</span></span>
  * <span data-ttu-id="d496a-246">浮水印策略不支援已刪除的物件。</span><span class="sxs-lookup"><span data-stu-id="d496a-246">Watermark strategy does not support deleted objects.</span></span>
* <span data-ttu-id="d496a-247">**快照**：(僅適用於 Microsoft SQL Server) [使用快照產生差異檢視](https://technet.microsoft.com/library/cc720640.aspx)</span><span class="sxs-lookup"><span data-stu-id="d496a-247">**Snapshot**: (Works only with Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)</span></span>
* <span data-ttu-id="d496a-248">**變更追蹤**：(僅適用於 Microsoft SQL Server) [About 變更追蹤](https://msdn.microsoft.com/library/bb933875.aspx)</span><span class="sxs-lookup"><span data-stu-id="d496a-248">**Change Tracking**: (Works only with Microsoft SQL Server) [About Change Tracking](https://msdn.microsoft.com/library/bb933875.aspx)</span></span>  
  <span data-ttu-id="d496a-249">限制：</span><span class="sxs-lookup"><span data-stu-id="d496a-249">Limitations:</span></span>
  * <span data-ttu-id="d496a-250">錨點和 DN 屬性必須是 hello hello 資料表中的所選物件的主索引鍵的一部分。</span><span class="sxs-lookup"><span data-stu-id="d496a-250">Anchor & DN attribute must be part of primary key for hello selected object in hello table.</span></span>
  * <span data-ttu-id="d496a-251">在使用變更追蹤的匯入和匯出期間內，不支援 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d496a-251">SQL query is unsupported during Import and Export with Change Tracking.</span></span>

<span data-ttu-id="d496a-252">**其他參數**： 指定 hello 指出您的資料庫伺服器所在的資料庫伺服器時區。</span><span class="sxs-lookup"><span data-stu-id="d496a-252">**Additional Parameters**: Specify hello Database Server Time Zone indicating where your Database server is located.</span></span> <span data-ttu-id="d496a-253">會使用此值 toosupport hello 各種格式的日期和時間屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-253">This value is used toosupport hello various formats of date & time attributes.</span></span>

<span data-ttu-id="d496a-254">hello 連接器一律日期和日期時間以 UTC 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="d496a-254">hello Connector always stores date and date-time in UTC format.</span></span> <span data-ttu-id="d496a-255">toobe 無法 toocorrectly 轉換 hello 日期和時間值，必須指定 hello 時區 hello 資料庫伺服器以及使用 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="d496a-255">toobe able toocorrectly convert hello date and times, hello time zone of hello database server and hello format used must be specified.</span></span> <span data-ttu-id="d496a-256">hello 格式應該是以.Net 格式表示。</span><span class="sxs-lookup"><span data-stu-id="d496a-256">hello format should be expressed in .Net format.</span></span>

<span data-ttu-id="d496a-257">在匯出期間的每個日期時間屬性必須提供 toohello 連接器以 UTC 時間格式。</span><span class="sxs-lookup"><span data-stu-id="d496a-257">During export every date time attribute must be provided toohello Connector in UTC time format.</span></span>

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

<span data-ttu-id="d496a-259">**密碼設定**: hello 連接器提供的密碼同步處理功能和支援設定及變更密碼。</span><span class="sxs-lookup"><span data-stu-id="d496a-259">**Password Configuration**: hello connector provides password synchronization capabilities and supports set and change password.</span></span>

<span data-ttu-id="d496a-260">hello 連接器提供兩種 toosupport 密碼同步處理：</span><span class="sxs-lookup"><span data-stu-id="d496a-260">hello Connector provides two methods toosupport password synchronization:</span></span>

* <span data-ttu-id="d496a-261">**預存程序**： 此方法需要兩個預存程序 toosupport 集與變更密碼。</span><span class="sxs-lookup"><span data-stu-id="d496a-261">**Stored Procedure**: This method requires two stored procedures toosupport Set & Change password.</span></span> <span data-ttu-id="d496a-262">輸入新增的所有參數，並變更中的 hello 密碼作業**設定密碼 SP**和**變更密碼 SP**分別依照下列範例中的參數。</span><span class="sxs-lookup"><span data-stu-id="d496a-262">Type all parameters for add and change hello password operation in **Set Password SP** and **Change Password SP** Parameters respectively as per below example.</span></span>
  <span data-ttu-id="d496a-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span></span>
* <span data-ttu-id="d496a-264">**密碼延伸模組**： 這個方法會要求密碼延伸模組 DLL (您需要 tooprovide hello 其實作 hello 的延伸模組 DLL 名稱[IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx)介面)。</span><span class="sxs-lookup"><span data-stu-id="d496a-264">**Password Extension**: This method requires Password extension DLL (you need tooprovide hello Extension DLL Name that is implementing hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface).</span></span> <span data-ttu-id="d496a-265">密碼延伸模組組件必須放在 擴充功能資料夾中，如此 hello 連接器可以載入 hello DLL 在執行階段。</span><span class="sxs-lookup"><span data-stu-id="d496a-265">Password extension assembly must be placed in extension folder so that hello connector can load hello DLL at runtime.</span></span>
  <span data-ttu-id="d496a-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span></span>

<span data-ttu-id="d496a-267">您也可以在 hello tooenable hello 密碼管理**設定副檔名**頁面。</span><span class="sxs-lookup"><span data-stu-id="d496a-267">You also have tooenable hello Password Management on hello **Configure Extension** page.</span></span>
<span data-ttu-id="d496a-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span></span>

### <a name="configure-partitions-and-hierarchies"></a><span data-ttu-id="d496a-269">設定資料分割和階層</span><span class="sxs-lookup"><span data-stu-id="d496a-269">Configure Partitions and Hierarchies</span></span>
<span data-ttu-id="d496a-270">在 hello 資料分割和階層 頁面上，選取所有物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-270">On hello partitions and hierarchies page, select all object types.</span></span> <span data-ttu-id="d496a-271">每個物件類型都在自己的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="d496a-271">Each object type is its own partition.</span></span>

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

<span data-ttu-id="d496a-273">您也可以覆寫 hello 上定義的 hello 值**連線**或**全域參數**頁面。</span><span class="sxs-lookup"><span data-stu-id="d496a-273">You can also override hello values defined on hello **Connectivity** or **Global Parameters** page.</span></span>

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a><span data-ttu-id="d496a-275">設定錨點</span><span class="sxs-lookup"><span data-stu-id="d496a-275">Configure Anchors</span></span>
<span data-ttu-id="d496a-276">此頁面是唯讀的因為已定義 hello 錨點。</span><span class="sxs-lookup"><span data-stu-id="d496a-276">This page is read-only since hello anchor has already been defined.</span></span> <span data-ttu-id="d496a-277">hello 選錨點屬性一律會附加與 hello 物件型別 tooensure 則仍會保持唯一的各種物件類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-277">hello selected anchor attribute is always appended with hello object type tooensure it remains unique across object types.</span></span>

![錨點](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a><span data-ttu-id="d496a-279">設定執行步驟參數</span><span class="sxs-lookup"><span data-stu-id="d496a-279">Configure Run Step Parameter</span></span>
<span data-ttu-id="d496a-280">Hello hello 連接器上執行設定檔上設定這些步驟。</span><span class="sxs-lookup"><span data-stu-id="d496a-280">These steps are configured on hello run profiles on hello Connector.</span></span> <span data-ttu-id="d496a-281">這些設定進行 hello 匯入及匯出資料的實際工作。</span><span class="sxs-lookup"><span data-stu-id="d496a-281">These configurations do hello actual work of importing and exporting data.</span></span>

### <a name="full-and-delta-import"></a><span data-ttu-id="d496a-282">完整和差異匯入</span><span class="sxs-lookup"><span data-stu-id="d496a-282">Full and Delta Import</span></span>
<span data-ttu-id="d496a-283">一般 SQL 連接器支援使用下列方法的完整和差異匯入：</span><span class="sxs-lookup"><span data-stu-id="d496a-283">Generic SQL Connector support Full and Delta Import using these methods:</span></span>

* <span data-ttu-id="d496a-284">資料表</span><span class="sxs-lookup"><span data-stu-id="d496a-284">Table</span></span>
* <span data-ttu-id="d496a-285">檢視</span><span class="sxs-lookup"><span data-stu-id="d496a-285">View</span></span>
* <span data-ttu-id="d496a-286">預存程序</span><span class="sxs-lookup"><span data-stu-id="d496a-286">Stored Procedure</span></span>
* <span data-ttu-id="d496a-287">SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="d496a-287">SQL Query</span></span>

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

<span data-ttu-id="d496a-289">**資料表/檢視**</span><span class="sxs-lookup"><span data-stu-id="d496a-289">**Table/View**</span></span>  
<span data-ttu-id="d496a-290">tooimport 多重值的屬性物件，您必須有 tooprovide hello 以逗號分隔的資料表/檢視表名稱**名稱的多重值的資料表/檢視**和個別的聯結條件中 hello**聯結條件**與 hello 父資料表。</span><span class="sxs-lookup"><span data-stu-id="d496a-290">tooimport multi-valued attributes for an object, you have tooprovide hello comma-separated table/view name in **Name of Multi-Valued table/views** and respective join conditions in hello **Join condition** with hello parent table.</span></span>

<span data-ttu-id="d496a-291">範例： 您想 tooimport hello Employee 物件和其所有多重值的屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-291">Example: You want tooimport hello Employee object and all its multi-valued attributes.</span></span> <span data-ttu-id="d496a-292">有兩個資料表：[員工] \(主要資料表) 和 [部門] \(多重值)。</span><span class="sxs-lookup"><span data-stu-id="d496a-292">There are two tables, named Employee (main table) and Department (multi-valued).</span></span>
<span data-ttu-id="d496a-293">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="d496a-293">Do hello following:</span></span>

* <span data-ttu-id="d496a-294">在 [資料表/檢視/SP] 中輸入**員工**。</span><span class="sxs-lookup"><span data-stu-id="d496a-294">Type **Employee** in **Table/View/SP**.</span></span>
* <span data-ttu-id="d496a-295">在 [多重資料表/檢視名稱] 中輸入 [部門]。</span><span class="sxs-lookup"><span data-stu-id="d496a-295">Type Department in **Name of Multi-Valued table/views**.</span></span>
* <span data-ttu-id="d496a-296">輸入 hello 員工 （& s） 中的部門之間的聯結條件**聯結條件**，例如`Employee.DEPTID=Department.DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="d496a-296">Type hello join condition between Employee & Department in **Join Condition**, for example `Employee.DEPTID=Department.DepartmentID`.</span></span>
  <span data-ttu-id="d496a-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span></span>

<span data-ttu-id="d496a-298">**預存程序**</span><span class="sxs-lookup"><span data-stu-id="d496a-298">**Stored procedures**</span></span>  
<span data-ttu-id="d496a-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span></span>

* <span data-ttu-id="d496a-300">如果您有太多資料，建議您預存程序與 tooimplement 分頁。</span><span class="sxs-lookup"><span data-stu-id="d496a-300">If you have much data, it is recommended tooimplement pagination with your Stored Procedures.</span></span>
* <span data-ttu-id="d496a-301">您的預存程序 toosupport 分頁，您需要 tooprovide 開始索引 」 和 「 結束索引。</span><span class="sxs-lookup"><span data-stu-id="d496a-301">For your Stored Procedure toosupport pagination, you need tooprovide Start Index and End Index.</span></span> <span data-ttu-id="d496a-302">請參閱： [有效地進行大量資料的分頁](https://msdn.microsoft.com/library/bb445504.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d496a-302">See: [Efficiently Paging Through Large Amounts of Data](https://msdn.microsoft.com/library/bb445504.aspx).</span></span>
* <span data-ttu-id="d496a-303">在執行時，會以在 [設定步驟] 頁面上設定的各自頁面大小值取代 @StartIndex 和 @EndIndex。</span><span class="sxs-lookup"><span data-stu-id="d496a-303">@StartIndex and @EndIndex are replaced at execution time with respective page size value configured on **Configure Step** page.</span></span> <span data-ttu-id="d496a-304">例如，當 hello 連接器擷取第一頁和 hello 頁面大小設定 500，在這種情況下@StartIndex會是 1 和@EndIndex500。</span><span class="sxs-lookup"><span data-stu-id="d496a-304">For example, when hello connector retrieves first page and hello page size is set 500, in such situation @StartIndex would be 1 and @EndIndex 500.</span></span> <span data-ttu-id="d496a-305">連接器擷取的後續頁面時，請增加這些值，並變更 hello @StartIndex &@EndIndex值。</span><span class="sxs-lookup"><span data-stu-id="d496a-305">These values increase when connector retrieves subsequent pages and change hello @StartIndex & @EndIndex value.</span></span>
* <span data-ttu-id="d496a-306">tooexecute 參數化預存程序，提供中的 hello 參數`[Name]:[Direction]:[Value]`格式。</span><span class="sxs-lookup"><span data-stu-id="d496a-306">tooexecute parameterized Stored Procedure, provide hello parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="d496a-307">輸入每個參數 （使用 Ctrl + Enter tooget 新行） 的個別行上。</span><span class="sxs-lookup"><span data-stu-id="d496a-307">Enter each parameter on a separate line (Use Ctrl + Enter tooget a new line).</span></span>
* <span data-ttu-id="d496a-308">一般 SQL 連接器也支援從 Microsoft SQL Server 中連結伺服器的匯入作業。</span><span class="sxs-lookup"><span data-stu-id="d496a-308">Generic SQL connector also supports Import operation from Linked Servers in Microsoft SQL Server.</span></span> <span data-ttu-id="d496a-309">如果應該從連結的伺服器中的資料表中擷取資訊，則資料表應該 hello 格式提供：`[ServerName].[Database].[Schema].[TableName]`</span><span class="sxs-lookup"><span data-stu-id="d496a-309">If information should be retrieved from a Table in Linked server, then Table should be provided in hello format: `[ServerName].[Database].[Schema].[TableName]`</span></span>
* <span data-ttu-id="d496a-310">一般 SQL 連接器僅支援在執行步驟資訊和結構描述偵測之間具有類似結構 (包括別名和資料類型) 的物件。</span><span class="sxs-lookup"><span data-stu-id="d496a-310">Generic SQL Connector supports only those objects that have similar structure (both alias name and data type) between run steps information and schema detection.</span></span> <span data-ttu-id="d496a-311">如果 hello 選取從結構描述並提供在執行步驟的詳細資訊的物件不同，則 SQL Connector 是無法 toosupport 這種案例。</span><span class="sxs-lookup"><span data-stu-id="d496a-311">If hello selected object from schema and provided information at run step is different, then SQL Connector is unable toosupport this type of scenarios.</span></span>

<span data-ttu-id="d496a-312">**SQL 查詢**</span><span class="sxs-lookup"><span data-stu-id="d496a-312">**SQL Query**</span></span>  
<span data-ttu-id="d496a-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span></span>

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* <span data-ttu-id="d496a-315">不支援多個結果集查詢。</span><span class="sxs-lookup"><span data-stu-id="d496a-315">Multiple result sets queries not supported.</span></span>
* <span data-ttu-id="d496a-316">SQL 查詢支援 hello 分頁，並提供開始索引和結束索引做為變數 toosupport 分頁。</span><span class="sxs-lookup"><span data-stu-id="d496a-316">SQL query supports hello pagination and provide start Index and End Index as a variable toosupport pagination.</span></span>

### <a name="delta-import"></a><span data-ttu-id="d496a-317">差異匯入</span><span class="sxs-lookup"><span data-stu-id="d496a-317">Delta Import</span></span>
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

<span data-ttu-id="d496a-319">相較於完整匯入，差異匯入設定需要一些更詳細的設定。</span><span class="sxs-lookup"><span data-stu-id="d496a-319">Delta Import configuration requires some more configuration compared with Full Import.</span></span>

* <span data-ttu-id="d496a-320">如果您選擇 hello 觸發程序或快照集的方法 tootrack 差異變更，然後提供在歷程記錄資料表或快照集資料庫**歷程記錄資料表或快照集資料庫名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="d496a-320">If you choose hello Trigger or Snapshot approach tootrack delta changes, then provide History Table or Snapshot database in **History Table or Snapshot database name** box.</span></span>
* <span data-ttu-id="d496a-321">您也需要 tooprovide 歷程記錄資料表與父資料表之間的聯結條件例如`Employee.ID=History.EmployeeID`</span><span class="sxs-lookup"><span data-stu-id="d496a-321">You also need tooprovide join condition between History table and Parent table, for example `Employee.ID=History.EmployeeID`</span></span>
* <span data-ttu-id="d496a-322">tootrack hello hello 歷程記錄資料表中的 hello 父資料表上的交易，您必須提供包含 hello 作業資訊 （新增/更新/刪除） 的 hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="d496a-322">tootrack hello transaction on hello parent table from hello history table, you must provide hello column name that contains hello operation information (Add/Update/Delete).</span></span>
* <span data-ttu-id="d496a-323">如果您選擇浮水印 tootrack 差異變更，然後提供包含 hello 作業資訊中的 hello 資料行名稱**上限標記資料行名稱**。</span><span class="sxs-lookup"><span data-stu-id="d496a-323">If you choose Watermark tootrack delta changes, then provide hello column name that contains hello operation information in **Water Mark Column Name**.</span></span>
* <span data-ttu-id="d496a-324">hello**變更類型屬性**資料行是 hello 變更類型的必要項。</span><span class="sxs-lookup"><span data-stu-id="d496a-324">hello **change Type attribute** column is required for hello change type.</span></span> <span data-ttu-id="d496a-325">此資料行對應 hello 主資料表中發生的變更或多重值資料表 tooa 變更 hello 差異檢視中的類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-325">This column maps a change that occurs in hello primary table or multi-value table tooa change type in hello delta view.</span></span> <span data-ttu-id="d496a-326">這個資料行可以包含 hello Modify_Attribute 變更類型屬性層級變更或新增、 修改或刪除變更為物件層級變更類型的類型。</span><span class="sxs-lookup"><span data-stu-id="d496a-326">This column can contain hello Modify_Attribute change type for attribute-level change or an Add, Modify, or Delete change type for an object-level change type.</span></span> <span data-ttu-id="d496a-327">如果以外的 hello 預設值新增、 修改或刪除，則您可以定義使用這個選項的值。</span><span class="sxs-lookup"><span data-stu-id="d496a-327">If it is something other than hello default value Add, Modify, or Delete, then you can define those values using this option.</span></span>

### <a name="export"></a><span data-ttu-id="d496a-328">匯出</span><span class="sxs-lookup"><span data-stu-id="d496a-328">Export</span></span>
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

<span data-ttu-id="d496a-330">一般 SQL 連接器支援使用下列四種方法的匯出：</span><span class="sxs-lookup"><span data-stu-id="d496a-330">Generic SQL Connector support Export using four supported methods such as:</span></span>

* <span data-ttu-id="d496a-331">資料表</span><span class="sxs-lookup"><span data-stu-id="d496a-331">Table</span></span>
* <span data-ttu-id="d496a-332">檢視</span><span class="sxs-lookup"><span data-stu-id="d496a-332">View</span></span>
* <span data-ttu-id="d496a-333">預存程序</span><span class="sxs-lookup"><span data-stu-id="d496a-333">Stored Procedure</span></span>
* <span data-ttu-id="d496a-334">SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="d496a-334">SQL Query</span></span>

<span data-ttu-id="d496a-335">**資料表/檢視**</span><span class="sxs-lookup"><span data-stu-id="d496a-335">**Table/View**</span></span>  
<span data-ttu-id="d496a-336">如果您選擇 hello 資料表/檢視表選項，hello 連接器會產生 hello 個別查詢 toodo hello 匯出。</span><span class="sxs-lookup"><span data-stu-id="d496a-336">If you choose hello Table/View option, then hello connector generates hello respective queries toodo hello Export.</span></span>

<span data-ttu-id="d496a-337">**預存程序**</span><span class="sxs-lookup"><span data-stu-id="d496a-337">**Stored procedures**</span></span>  
<span data-ttu-id="d496a-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span></span>

<span data-ttu-id="d496a-339">如果您選擇 hello 預存程序選項，匯出，需要三個不同預存程序 tooperform Insert/Update/Delete 作業。</span><span class="sxs-lookup"><span data-stu-id="d496a-339">If you choose hello Stored Procedure option, Export requires three different Stored procedures tooperform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="d496a-340">**將預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中插入作業會執行此預存程序。</span><span class="sxs-lookup"><span data-stu-id="d496a-340">**Add SP Name**: This SP runs if any object comes tooconnector for insertion in hello respective table.</span></span>
* <span data-ttu-id="d496a-341">**更新預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中的更新，會執行此預存程序。</span><span class="sxs-lookup"><span data-stu-id="d496a-341">**Update SP Name**: This SP runs if any object comes tooconnector for update in hello respective table.</span></span>
* <span data-ttu-id="d496a-342">**刪除預存程序名稱**： 如果任何物件都有 tooconnector hello 個別資料表中要刪除此預存程序來執行。</span><span class="sxs-lookup"><span data-stu-id="d496a-342">**Delete SP Name**: This SP runs if any object comes tooconnector for deletion in hello respective table.</span></span>
* <span data-ttu-id="d496a-343">從 hello 做為參數值 toohello 預存程序的結構描述中所選取的屬性。</span><span class="sxs-lookup"><span data-stu-id="d496a-343">Attribute selected from hello schema used as a parameter value toohello stored procedure.</span></span> <span data-ttu-id="d496a-344">例如， `EmployeeName: INPUT: @EmployeeName` （hello 連接器結構描述中選取員工姓名和 hello 連接器進行匯出時取代 hello 個別值）</span><span class="sxs-lookup"><span data-stu-id="d496a-344">For example, `EmployeeName: INPUT: @EmployeeName` (EmployeeName is selected in hello connector schema and hello connector replaces hello respective value while doing export)</span></span>
* <span data-ttu-id="d496a-345">toorun 參數化預存程序，提供中的參數`[Name]:[Direction]:[Value]`格式。</span><span class="sxs-lookup"><span data-stu-id="d496a-345">toorun parameterized stored procedure, provide parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="d496a-346">輸入每個參數 （使用 Ctrl + Enter tooget 新行） 的個別行上。</span><span class="sxs-lookup"><span data-stu-id="d496a-346">Enter each parameter on a separate line (Use Ctrl + Enter tooget a new line).</span></span>

<span data-ttu-id="d496a-347">**SQL query**</span><span class="sxs-lookup"><span data-stu-id="d496a-347">**SQL query**</span></span>  
<span data-ttu-id="d496a-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span><span class="sxs-lookup"><span data-stu-id="d496a-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span></span>

<span data-ttu-id="d496a-349">如果您選擇 hello SQL 查詢選項，匯出，需要有三個不同查詢 tooperform Insert/Update/Delete 作業。</span><span class="sxs-lookup"><span data-stu-id="d496a-349">If you choose hello SQL query option, Export requires three different queries tooperform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="d496a-350">**插入查詢**： 如果任何物件都有 tooconnector hello 個別資料表中插入作業會執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="d496a-350">**Insert Query**: This query runs if any object comes tooconnector for insertion in hello respective table.</span></span>
* <span data-ttu-id="d496a-351">**更新查詢**： 如果任何物件都有 tooconnector hello 個別資料表中更新執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="d496a-351">**Update Query**: This query runs if any object comes tooconnector for update in hello respective table.</span></span>
* <span data-ttu-id="d496a-352">**刪除查詢**： 如果任何物件都有 tooconnector hello 個別資料表中要刪除此查詢會執行。</span><span class="sxs-lookup"><span data-stu-id="d496a-352">**Delete Query**: This query runs if any object comes tooconnector for deletion in hello respective table.</span></span>
* <span data-ttu-id="d496a-353">從當做參數值 toohello 查詢，例如 hello 結構描述中所選取屬性`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span><span class="sxs-lookup"><span data-stu-id="d496a-353">Attribute selected from hello schema used as a parameter value toohello query, for example `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d496a-354">疑難排解</span><span class="sxs-lookup"><span data-stu-id="d496a-354">Troubleshooting</span></span>
* <span data-ttu-id="d496a-355">如需如何 tooenable 記錄 tootroubleshoot hello 連接器資訊，請參閱 hello[如何 tooEnable ETW 追蹤連接器](http://go.microsoft.com/fwlink/?LinkId=335731)。</span><span class="sxs-lookup"><span data-stu-id="d496a-355">For information on how tooenable logging tootroubleshoot hello connector, see hello [How tooEnable ETW Tracing for Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).</span></span>
