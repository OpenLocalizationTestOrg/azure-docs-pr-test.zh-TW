---
title: "一般 SQL 連接器 | Microsoft Docs"
description: "本文說明如何設定 Microsoft 的一般 SQL 連接器。"
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
ms.openlocfilehash: a84096ba53a308855beedd76d9dec827c025cd57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-technical-reference"></a><span data-ttu-id="1530e-103">一般 SQL 連接器技術參考</span><span class="sxs-lookup"><span data-stu-id="1530e-103">Generic SQL Connector technical reference</span></span>
<span data-ttu-id="1530e-104">本文說明一般 SQL 連接器。</span><span class="sxs-lookup"><span data-stu-id="1530e-104">This article describes the Generic SQL Connector.</span></span> <span data-ttu-id="1530e-105">本文適用於下列產品：</span><span class="sxs-lookup"><span data-stu-id="1530e-105">The article applies to the following products:</span></span>

* <span data-ttu-id="1530e-106">Microsoft Identity Manager 2016 (MIM2016)</span><span class="sxs-lookup"><span data-stu-id="1530e-106">Microsoft Identity Manager 2016 (MIM2016)</span></span>
* <span data-ttu-id="1530e-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span><span class="sxs-lookup"><span data-stu-id="1530e-107">Forefront Identity Manager 2010 R2 (FIM2010R2)</span></span>
  * <span data-ttu-id="1530e-108">必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。</span><span class="sxs-lookup"><span data-stu-id="1530e-108">Must use hotfix 4.1.3671.0 or later [KB3092178](https://support.microsoft.com/kb/3092178).</span></span>

<span data-ttu-id="1530e-109">對於 MIM2016 和 FIM2010R2，可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=717495)下載此連接器。</span><span class="sxs-lookup"><span data-stu-id="1530e-109">For MIM2016 and FIM2010R2, the Connector is available as a download from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).</span></span>

<span data-ttu-id="1530e-110">若要查看這個作用中的連接器，請參閱 [Generic SQL Connector step-by-step (一般 SQL 連接器的逐步解說)](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="1530e-110">To see this Connector in action, see the [Generic SQL Connector step-by-step](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) article.</span></span>

## <a name="overview-of-the-generic-sql-connector"></a><span data-ttu-id="1530e-111">一般 SQL 連接器概觀</span><span class="sxs-lookup"><span data-stu-id="1530e-111">Overview of the Generic SQL Connector</span></span>
<span data-ttu-id="1530e-112">一般 SQL 連接器可讓您整合同步處理服務與提供 ODBC 連線的資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="1530e-112">The Generic SQL Connector enables you to integrate the synchronization service with a database system that offers ODBC connectivity.</span></span>  

<span data-ttu-id="1530e-113">目前的連接器版本大致支援下列功能：</span><span class="sxs-lookup"><span data-stu-id="1530e-113">From a high-level perspective, the following features are supported by the current release of the connector:</span></span>

| <span data-ttu-id="1530e-114">功能</span><span class="sxs-lookup"><span data-stu-id="1530e-114">Feature</span></span> | <span data-ttu-id="1530e-115">支援</span><span class="sxs-lookup"><span data-stu-id="1530e-115">Support</span></span> |
| --- | --- |
| <span data-ttu-id="1530e-116">連接的資料來源</span><span class="sxs-lookup"><span data-stu-id="1530e-116">Connected data source</span></span> |<span data-ttu-id="1530e-117">此連接器支援所有 64 位元的 ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="1530e-117">The Connector is supported with all 64-bit ODBC drivers.</span></span> <span data-ttu-id="1530e-118">此連接器已進行下列各項的測試：</span><span class="sxs-lookup"><span data-stu-id="1530e-118">It has been tested with the following:</span></span> <li><span data-ttu-id="1530e-119">Microsoft SQL Server 與 SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1530e-119">Microsoft SQL Server & SQL Azure</span></span></li><li><span data-ttu-id="1530e-120">IBM DB2 10.x</span><span class="sxs-lookup"><span data-stu-id="1530e-120">IBM DB2 10.x</span></span></li><li><span data-ttu-id="1530e-121">IBM DB2 9.x</span><span class="sxs-lookup"><span data-stu-id="1530e-121">IBM DB2 9.x</span></span></li><li><span data-ttu-id="1530e-122">Oracle 10 和 11 g</span><span class="sxs-lookup"><span data-stu-id="1530e-122">Oracle 10 & 11g</span></span></li><li><span data-ttu-id="1530e-123">MySQL 5.x</span><span class="sxs-lookup"><span data-stu-id="1530e-123">MySQL 5.x</span></span></li> |
| <span data-ttu-id="1530e-124">案例</span><span class="sxs-lookup"><span data-stu-id="1530e-124">Scenarios</span></span> |<li><span data-ttu-id="1530e-125">物件生命週期管理</span><span class="sxs-lookup"><span data-stu-id="1530e-125">Object Lifecycle Management</span></span></li><li><span data-ttu-id="1530e-126">密碼管理</span><span class="sxs-lookup"><span data-stu-id="1530e-126">Password Management</span></span></li> |
| <span data-ttu-id="1530e-127">作業</span><span class="sxs-lookup"><span data-stu-id="1530e-127">Operations</span></span> |<li><span data-ttu-id="1530e-128">完整匯入和差異匯入、匯出</span><span class="sxs-lookup"><span data-stu-id="1530e-128">Full Import and Delta Import, Export</span></span></li><li><span data-ttu-id="1530e-129">針對匯出：新增、刪除、更新和取代</span><span class="sxs-lookup"><span data-stu-id="1530e-129">For Export: Add, Delete, Update, and Replace</span></span></li><li><span data-ttu-id="1530e-130">設定密碼、變更密碼</span><span class="sxs-lookup"><span data-stu-id="1530e-130">Set Password, Change Password</span></span></li> |
| <span data-ttu-id="1530e-131">結構描述</span><span class="sxs-lookup"><span data-stu-id="1530e-131">Schema</span></span> |<li><span data-ttu-id="1530e-132">動態探索物件和屬性</span><span class="sxs-lookup"><span data-stu-id="1530e-132">Dynamic discovery of objects and attributes</span></span></li> |

### <a name="prerequisites"></a><span data-ttu-id="1530e-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="1530e-133">Prerequisites</span></span>
<span data-ttu-id="1530e-134">在您使用連接器之前，請確定同步處理伺服器上有下列項目：</span><span class="sxs-lookup"><span data-stu-id="1530e-134">Before you use the Connector, make sure you have the following on the synchronization server:</span></span>

* <span data-ttu-id="1530e-135">Microsoft .NET 4.5.2 Framework 或更新版本</span><span class="sxs-lookup"><span data-stu-id="1530e-135">Microsoft .NET 4.5.2 Framework or later</span></span>
* <span data-ttu-id="1530e-136">64 位元的 ODBC 用戶端驅動程式</span><span class="sxs-lookup"><span data-stu-id="1530e-136">64-bit ODBC client drivers</span></span>

### <a name="permissions-in-connected-data-source"></a><span data-ttu-id="1530e-137">連接的資料來源權限</span><span class="sxs-lookup"><span data-stu-id="1530e-137">Permissions in connected data source</span></span>
<span data-ttu-id="1530e-138">若要在一般 SQL 連接器中建立或執行任何支援的工作，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="1530e-138">To create or perform any of the supported tasks in Generic SQL connector, you must have:</span></span>

* <span data-ttu-id="1530e-139">db_datareader</span><span class="sxs-lookup"><span data-stu-id="1530e-139">db_datareader</span></span>
* <span data-ttu-id="1530e-140">db_datawriter</span><span class="sxs-lookup"><span data-stu-id="1530e-140">db_datawriter</span></span>

### <a name="ports-and-protocols"></a><span data-ttu-id="1530e-141">連接埠和通訊協定</span><span class="sxs-lookup"><span data-stu-id="1530e-141">Ports and protocols</span></span>
<span data-ttu-id="1530e-142">如需 ODBC 驅動程式運作所需的連接埠，請參閱資料庫廠商的說明文件。</span><span class="sxs-lookup"><span data-stu-id="1530e-142">For the ports required for the ODBC driver to work, consult the database vendor's documentation.</span></span>

## <a name="create-a-new-connector"></a><span data-ttu-id="1530e-143">建立新的連接器</span><span class="sxs-lookup"><span data-stu-id="1530e-143">Create a new Connector</span></span>
<span data-ttu-id="1530e-144">若要建立一般 SQL 連接器，請在 [同步處理服務] 中選取 [管理代理程式] 和 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1530e-144">To Create a Generic SQL connector, in **Synchronization Service** select **Management Agent** and **Create**.</span></span> <span data-ttu-id="1530e-145">選取 [一般 SQL (Microsoft)] 連接器。</span><span class="sxs-lookup"><span data-stu-id="1530e-145">Select the **Generic SQL (Microsoft)** Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a><span data-ttu-id="1530e-147">連線能力</span><span class="sxs-lookup"><span data-stu-id="1530e-147">Connectivity</span></span>
<span data-ttu-id="1530e-148">連接器會使用 ODBC DSN 檔案進行連線。</span><span class="sxs-lookup"><span data-stu-id="1530e-148">The Connector uses an ODBC DSN file for connectivity.</span></span> <span data-ttu-id="1530e-149">使用在 [系統管理工具] 下的開始功能表中找到的 [ODBC 資料來源]，建立 DSN 檔案。</span><span class="sxs-lookup"><span data-stu-id="1530e-149">Create the DSN file using **ODBC Data Sources** found in the start menu under **Administrative Tools**.</span></span> <span data-ttu-id="1530e-150">在系統管理工具中，建立 [檔案 DSN]  ，以便提供給連接器。</span><span class="sxs-lookup"><span data-stu-id="1530e-150">In the administrative tool, create a **File DSN** so it can be provided to the Connector.</span></span>

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

<span data-ttu-id="1530e-152">當您建立新的一般 SQL 連接器時，[連線能力] 是第一個畫面。</span><span class="sxs-lookup"><span data-stu-id="1530e-152">The Connectivity screen is the first when you create a new Generic SQL Connector.</span></span> <span data-ttu-id="1530e-153">您必須先提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1530e-153">You first need to provide the following information:</span></span>

* <span data-ttu-id="1530e-154">DSN 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="1530e-154">DSN file path</span></span>
* <span data-ttu-id="1530e-155">驗證</span><span class="sxs-lookup"><span data-stu-id="1530e-155">Authentication</span></span>
  * <span data-ttu-id="1530e-156">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="1530e-156">User Name</span></span>
  * <span data-ttu-id="1530e-157">密碼</span><span class="sxs-lookup"><span data-stu-id="1530e-157">Password</span></span>

<span data-ttu-id="1530e-158">資料庫應該支援下列其中一種驗證方法：</span><span class="sxs-lookup"><span data-stu-id="1530e-158">The database should support one of these authentication methods:</span></span>

* <span data-ttu-id="1530e-159">**Windows 驗證**：驗證資料庫會使用 Windows 認證來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="1530e-159">**Windows authentication**: The authenticating database uses the Windows credentials to verify the user.</span></span> <span data-ttu-id="1530e-160">指定的使用者名稱/密碼用來向資料庫進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1530e-160">The user name/password specified is used to authenticate with the database.</span></span> <span data-ttu-id="1530e-161">此帳戶需要資料庫的權限。</span><span class="sxs-lookup"><span data-stu-id="1530e-161">This account needs permissions to the database.</span></span>
* <span data-ttu-id="1530e-162">**SQL 驗證**：驗證資料庫會使用 [連線能力] 畫面上定義的使用者名稱/密碼連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="1530e-162">**SQL authentication**: The authenticating database uses the user name/password defined one the Connectivity screen to connect to the database.</span></span> <span data-ttu-id="1530e-163">如果您在 DSN 檔案中儲存使用者名稱/密碼，則優先使用在 [連線能力] 畫面上提供的認證。</span><span class="sxs-lookup"><span data-stu-id="1530e-163">If you store the user name/pasword in the DSN file, the credentials provided on the Connectivity screen have precedence.</span></span>
* <span data-ttu-id="1530e-164">**Azure SQL Database 驗證**：如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連接到 SQL Database](../../sql-database/sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="1530e-164">**Azure SQL Database authentication**: For more information, see [Connect to SQL Database By Using Azure Active Directory Authentication](../../sql-database/sql-database-aad-authentication.md).</span></span>

<span data-ttu-id="1530e-165">**DN 是錨點**：如果您選取此選項，DN 也會做為錨點屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-165">**DN is Anchor**: If you select this option, the DN is also used as the anchor attribute.</span></span> <span data-ttu-id="1530e-166">它可用於簡單實作，但也有下列限制：</span><span class="sxs-lookup"><span data-stu-id="1530e-166">It can be used for a simple implementation but also has the following limitation:</span></span>

* <span data-ttu-id="1530e-167">連接器只支援一種物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-167">Connector supports only one object type.</span></span> <span data-ttu-id="1530e-168">因此，所有參考屬性只能參考相同的物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-168">Therefore any reference attributes can only reference the same object type.</span></span>

<span data-ttu-id="1530e-169">**匯出類型：物件取代**：在匯出期間，只有一些屬性已變更時，包含所有屬性的整個物件則會匯出並取代現有的物件。</span><span class="sxs-lookup"><span data-stu-id="1530e-169">**Export Type: Object Replace**: During export, when only some attributes have changed, the entire object with all attributes is exported and replaces the existing object.</span></span>

### <a name="schema-1-detect-object-types"></a><span data-ttu-id="1530e-170">結構描述 1 (偵測物件類型)</span><span class="sxs-lookup"><span data-stu-id="1530e-170">Schema 1 (Detect object types)</span></span>
<span data-ttu-id="1530e-171">此頁面上，您將設定連接器要如何在資料庫中尋找不同的物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-171">On this page, you are going to configure how the Connector is going to find the different object types in the database.</span></span>

<span data-ttu-id="1530e-172">每個物件類型會顯示為一個資料分割，並且在 [設定資料分割和階層] 上進一步設定。</span><span class="sxs-lookup"><span data-stu-id="1530e-172">Every object type is presented as a partition and configured further on **Configure Partitions and Hierarchies**.</span></span>

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

<span data-ttu-id="1530e-174">**物件類型偵測方法**：連接器支援下列物件類型偵測方法。</span><span class="sxs-lookup"><span data-stu-id="1530e-174">**Object Type detection method**: The Connector supports these object type detection methods.</span></span>

* <span data-ttu-id="1530e-175">**固定值**：您以逗號分隔的清單來提供物件類型清單。</span><span class="sxs-lookup"><span data-stu-id="1530e-175">**Fixed Value**: You provide the list of object types with a comma-separated list.</span></span> <span data-ttu-id="1530e-176">例如， `User,Group,Department`。</span><span class="sxs-lookup"><span data-stu-id="1530e-176">For example: `User,Group,Department`.</span></span>  
  <span data-ttu-id="1530e-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-177">![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)</span></span>
* <span data-ttu-id="1530e-178">**資料表/檢視/預存程序**：提供資料表/檢視/預存程序的名稱，然後提供資料行名稱以提供物件類型的清單。</span><span class="sxs-lookup"><span data-stu-id="1530e-178">**Table/View/Stored Procedure**: Provide the name of the table/view/stored procedure and then the column name that provides the list of object types.</span></span> <span data-ttu-id="1530e-179">如果您使用預存程序，也需以下列格式提供其參數： **[名稱]:[方向]:[值]**。</span><span class="sxs-lookup"><span data-stu-id="1530e-179">If you use a stored procedure, then also provide parameters for it in the format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="1530e-180">在個別一行上提供每個參數 (使用 Ctrl+Enter 來換行)。</span><span class="sxs-lookup"><span data-stu-id="1530e-180">Provide each parameter on a separate line (use Ctrl+Enter to get a new line).</span></span>  
  <span data-ttu-id="1530e-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-181">![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)</span></span>
* <span data-ttu-id="1530e-182">**SQL 查詢**：此選項可讓您提供 SQL 查詢，以傳回包含物件類型的單一資料行，例如 `SELECT [Column Name] FROM TABLENAME`。</span><span class="sxs-lookup"><span data-stu-id="1530e-182">**SQL Query**: This option allows you to provide a SQL query that returns a single column with object types, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="1530e-183">傳回的資料行必須是字串類型 (varchar)。</span><span class="sxs-lookup"><span data-stu-id="1530e-183">The returned column must be of type string (varchar).</span></span>

### <a name="schema-2-detect-attribute-types"></a><span data-ttu-id="1530e-184">結構描述 2 (偵測屬性類型)</span><span class="sxs-lookup"><span data-stu-id="1530e-184">Schema 2 (Detect attribute types)</span></span>
<span data-ttu-id="1530e-185">在此頁面上，您將設定要如何偵測屬性名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-185">On this page, you are going to configure how the attribute names and types are going to be detected.</span></span> <span data-ttu-id="1530e-186">系統會針對在前一頁偵測到的每個物件類型，列出設定選項。</span><span class="sxs-lookup"><span data-stu-id="1530e-186">The configuration options are listed for every object type detected on the previous page.</span></span>

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

<span data-ttu-id="1530e-188">**屬性類型偵測方法**：連接器會以 [結構描述 1] 畫面中每個偵測到的物件類型，支援下列屬性類型偵測方法。</span><span class="sxs-lookup"><span data-stu-id="1530e-188">**Attribute Type detection method**: The Connector supports these attribute type detection methods with every detected object type in Schema 1 screen.</span></span>

* <span data-ttu-id="1530e-189">**資料表/檢視/預存程序**：提供資料表/檢視/預存程序的名稱，以便用來尋找屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1530e-189">**Table/View/Stored Procedure**: Provide the name of the table/view/stored procedure that should be used to find the attribute names.</span></span> <span data-ttu-id="1530e-190">如果您使用預存程序，也需以下列格式提供其參數： **[名稱]:[方向]:[值]**。</span><span class="sxs-lookup"><span data-stu-id="1530e-190">If you use a stored procedure, then also provide parameters for it in the format **[Name]:[Direction]:[Value]**.</span></span> <span data-ttu-id="1530e-191">在個別一行上提供每個參數 (使用 Ctrl+Enter 來換行)。</span><span class="sxs-lookup"><span data-stu-id="1530e-191">Provide each parameter on a separate line (use Ctrl+Enter to get a new line).</span></span> <span data-ttu-id="1530e-192">若要偵測多重值屬性中的屬性名稱，請提供以逗號分隔的資料表或檢視清單。</span><span class="sxs-lookup"><span data-stu-id="1530e-192">To detect the attribute names in a multi-valued attribute, provide a comma-separated list of Tables or Views.</span></span> <span data-ttu-id="1530e-193">當父和子資料表具有相同的資料行名稱時，則不支援多重值案例。</span><span class="sxs-lookup"><span data-stu-id="1530e-193">Multivalued scenarios are not supported when parent and child table have same column names.</span></span>
* <span data-ttu-id="1530e-194">**SQL 查詢**：此選項可讓您提供 SQL 查詢，以傳回包含屬性名稱的單一資料行，例如 `SELECT [Column Name] FROM TABLENAME`。</span><span class="sxs-lookup"><span data-stu-id="1530e-194">**SQL query**: This option allows you to provide a SQL query that returns a single column with attribute names, for example `SELECT [Column Name] FROM TABLENAME`.</span></span> <span data-ttu-id="1530e-195">傳回的資料行必須是字串類型 (varchar)。</span><span class="sxs-lookup"><span data-stu-id="1530e-195">The returned column must be of type string (varchar).</span></span>

### <a name="schema-3-define-anchor-and-dn"></a><span data-ttu-id="1530e-196">結構描述 3 (定義錨點和 DN)</span><span class="sxs-lookup"><span data-stu-id="1530e-196">Schema 3 (Define anchor and DN)</span></span>
<span data-ttu-id="1530e-197">此頁面可讓您為每個偵測到的物件類型設定錨點和 DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-197">This page allows you to configure anchor and DN attribute for each detected object type.</span></span> <span data-ttu-id="1530e-198">您可以選取多個屬性，讓錨點變成唯一的。</span><span class="sxs-lookup"><span data-stu-id="1530e-198">You can select multiple attributes to make the anchor unique.</span></span>

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* <span data-ttu-id="1530e-200">不會列出多重值和布林值屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-200">Multi-valued and Boolean attributes are not listed.</span></span>
* <span data-ttu-id="1530e-201">DN 和錨點無法使用相同的屬性，除非已在 [連線能力] 頁面上選取 [DN 是錨點]  。</span><span class="sxs-lookup"><span data-stu-id="1530e-201">Same attribute cannot use for DN and anchor, unless **DN is Anchor** is selected on the Connectivity page.</span></span>
* <span data-ttu-id="1530e-202">如果已在 [連線能力] 頁面上選取 [DN 是錨點]  ，此頁面只需要 DN 屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-202">If **DN is Anchor** is selected on the Connectivity page, this page requires only the DN attribute.</span></span> <span data-ttu-id="1530e-203">這個屬性也會做為錨點屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-203">This attribute would also be used as the anchor attribute.</span></span>

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a><span data-ttu-id="1530e-205">結構描述 4 (定義屬性類型、參考和方向)</span><span class="sxs-lookup"><span data-stu-id="1530e-205">Schema 4 (Define attribute type, reference, and direction)</span></span>
<span data-ttu-id="1530e-206">此頁面可讓您設定每個屬性的屬性類型，如整數、二進位或布林值和方向。</span><span class="sxs-lookup"><span data-stu-id="1530e-206">This page allows you to configure the attribute type, such as integer, binary, or Boolean, and direction for each attribute.</span></span> <span data-ttu-id="1530e-207">[結構描述 2]  頁面中的所有屬性都會列出，包括多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-207">All attributes from page **schema 2** are listed including multi-valued attributes.</span></span>

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* <span data-ttu-id="1530e-209">**DataType**：用來將屬性類型對應至同步處理引擎所知的屬性類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-209">**DataType**: Used to map the attribute type to those types known by the sync engine.</span></span> <span data-ttu-id="1530e-210">預設會使用在 SQL 結構描述中偵測到的相同類型，但 DateTime 和 Reference 不容易偵測。</span><span class="sxs-lookup"><span data-stu-id="1530e-210">The default is to use the same type as detected in the SQL schema, but DateTime and Reference are not easily detectable.</span></span> <span data-ttu-id="1530e-211">因此，您必須指定 **DateTime** 或 **Reference**。</span><span class="sxs-lookup"><span data-stu-id="1530e-211">For those, you need to specify **DateTime** or **Reference**.</span></span>
* <span data-ttu-id="1530e-212">**方向**：您可以設定 Import、Export 或 ImportExport 的屬性方向。</span><span class="sxs-lookup"><span data-stu-id="1530e-212">**Direction**: You can set the attribute direction to Import, Export, or ImportExport.</span></span> <span data-ttu-id="1530e-213">ImportExport 是預設值。</span><span class="sxs-lookup"><span data-stu-id="1530e-213">ImportExport is default.</span></span>

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

<span data-ttu-id="1530e-215">注意：</span><span class="sxs-lookup"><span data-stu-id="1530e-215">Notes:</span></span>

* <span data-ttu-id="1530e-216">如果連接器無法偵測屬性類型，則會使用字串資料類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-216">If an attribute type is not detectable by the Connector, it uses the String data type.</span></span>
* <span data-ttu-id="1530e-217">**巢狀資料表** 視為一個資料行的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="1530e-217">**Nested tables** can be considered one-column database tables.</span></span> <span data-ttu-id="1530e-218">Oracle 不會以任何特定順序儲存巢狀資料表的資料列。</span><span class="sxs-lookup"><span data-stu-id="1530e-218">Oracle stores the rows of a nested table in no particular order.</span></span> <span data-ttu-id="1530e-219">不過，當您將巢狀資料表擷取至 PL/SQL 變數時，資料列便會有從 1 開始的連續下標。</span><span class="sxs-lookup"><span data-stu-id="1530e-219">However, when you retrieve the nested table into a PL/SQL variable, the rows are given consecutive subscripts starting at 1.</span></span> <span data-ttu-id="1530e-220">這可讓您取得個別資料列的類似陣列存取。</span><span class="sxs-lookup"><span data-stu-id="1530e-220">That gives you array-like access to individual rows.</span></span>
* <span data-ttu-id="1530e-221">**VARRYS** 。</span><span class="sxs-lookup"><span data-stu-id="1530e-221">**VARRYS** are not supported in the connector.</span></span>

### <a name="schema-5-define-partition-for-reference-attributes"></a><span data-ttu-id="1530e-222">結構描述 5 (定義參考屬性的資料分割)</span><span class="sxs-lookup"><span data-stu-id="1530e-222">Schema 5 (Define partition for reference attributes)</span></span>
<span data-ttu-id="1530e-223">在此頁面上，您會為所有參考屬性設定屬性所參考的資料分割 (物件類型)。</span><span class="sxs-lookup"><span data-stu-id="1530e-223">On this page, you configure for all reference attributes which partition (object type) an attribute is referring to.</span></span>

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

<span data-ttu-id="1530e-225">如果您使用 [DN 是錨點] ，則必須使用相同的物件類型做為您參考的來源物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-225">If you use **DN is anchor**, then you must use the same object type as the one you are referring from.</span></span> <span data-ttu-id="1530e-226">您無法參考其他物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-226">You cannot reference another object type.</span></span>

>[!NOTE]
<span data-ttu-id="1530e-227">從 2017 年 3 月的更新開始，現在已有 "*" 的選項。在選擇了此選項時，系統便會匯入所有可能的成員類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-227">Starting in the March 2017 update there is now an option for "*" When this option is chosen then all possible member types will be imported.</span></span>

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 <span data-ttu-id="1530e-229">自 2017 年 5 月起，“*” (也稱為「任何選項」) 已變更，以支援匯入與匯出流程。</span><span class="sxs-lookup"><span data-stu-id="1530e-229">As of May 2017 the “*” aka **any option** has been changed to support import and export flow.</span></span> <span data-ttu-id="1530e-230">如果您想要使用此選項，您的多重值資料表/檢視應該有包含物件類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-230">If you want to use this option your multi-valued table/view should have an attribute that contains the object type.</span></span>

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> <span data-ttu-id="1530e-231">如果 "*" 已選取，則也必須指定含有物件類型的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="1530e-231">If "*" is selected then the name of the column with the object type must also be specified.</span></span></br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

<span data-ttu-id="1530e-232">在匯入後，您會看到類似下圖的情形︰</span><span class="sxs-lookup"><span data-stu-id="1530e-232">After import you will see something similar to the image below:</span></span>

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a><span data-ttu-id="1530e-234">全域參數</span><span class="sxs-lookup"><span data-stu-id="1530e-234">Global Parameters</span></span>
<span data-ttu-id="1530e-235">[全域參數] 頁面用來設定差異匯入、日期/時間格式，以及密碼方法。</span><span class="sxs-lookup"><span data-stu-id="1530e-235">The Global Parameters page is used to configure Delta Import, Date/Time format, and Password method.</span></span>

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



<span data-ttu-id="1530e-237">一般 SQL 連接器支援使用下列差異匯入方法：</span><span class="sxs-lookup"><span data-stu-id="1530e-237">The Generic SQL Connector supports the following methods for Delta Import:</span></span>

* <span data-ttu-id="1530e-238">**觸發程序**：請參閱 [使用觸發程序產生差異檢視](https://technet.microsoft.com/library/cc708665.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1530e-238">**Trigger**: See [Generating Delta Views Using Triggers](https://technet.microsoft.com/library/cc708665.aspx).</span></span>
* <span data-ttu-id="1530e-239">**浮水印**：可以用於任何資料庫的一般方法。</span><span class="sxs-lookup"><span data-stu-id="1530e-239">**Watermark**: A generic approach that can be used with any database.</span></span> <span data-ttu-id="1530e-240">浮水印查詢會根據資料庫供應商預先填入。</span><span class="sxs-lookup"><span data-stu-id="1530e-240">The watermark query is pre-populated based on the database vendor.</span></span> <span data-ttu-id="1530e-241">浮水印資料行必須出現在所用的每個資料表/檢視上。</span><span class="sxs-lookup"><span data-stu-id="1530e-241">A watermark column must be present on every table/view used.</span></span> <span data-ttu-id="1530e-242">此資料行必須追蹤資料表的插入和更新，以及其相依 (多重值或子系) 資料表。</span><span class="sxs-lookup"><span data-stu-id="1530e-242">This column must track inserts and updates to the tables as and its dependent (multi-valued or child) tables.</span></span> <span data-ttu-id="1530e-243">同步處理服務與資料庫伺服器之間的時鐘必須同步。</span><span class="sxs-lookup"><span data-stu-id="1530e-243">The clocks between Synchronization Service and the database server must be synchronized.</span></span> <span data-ttu-id="1530e-244">如果沒有同步，則可能會省略差異匯入中的某些項目。</span><span class="sxs-lookup"><span data-stu-id="1530e-244">If not, some entries in the delta import might be omitted.</span></span>  
  <span data-ttu-id="1530e-245">限制：</span><span class="sxs-lookup"><span data-stu-id="1530e-245">Limitation:</span></span>
  * <span data-ttu-id="1530e-246">浮水印策略不支援已刪除的物件。</span><span class="sxs-lookup"><span data-stu-id="1530e-246">Watermark strategy does not support deleted objects.</span></span>
* <span data-ttu-id="1530e-247">**快照**：(僅適用於 Microsoft SQL Server) [使用快照產生差異檢視](https://technet.microsoft.com/library/cc720640.aspx)</span><span class="sxs-lookup"><span data-stu-id="1530e-247">**Snapshot**: (Works only with Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)</span></span>
* <span data-ttu-id="1530e-248">**變更追蹤**：(僅適用於 Microsoft SQL Server) [About 變更追蹤](https://msdn.microsoft.com/library/bb933875.aspx)</span><span class="sxs-lookup"><span data-stu-id="1530e-248">**Change Tracking**: (Works only with Microsoft SQL Server) [About Change Tracking](https://msdn.microsoft.com/library/bb933875.aspx)</span></span>  
  <span data-ttu-id="1530e-249">限制：</span><span class="sxs-lookup"><span data-stu-id="1530e-249">Limitations:</span></span>
  * <span data-ttu-id="1530e-250">錨點和 DN 屬性必須屬於資料表中所選物件的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1530e-250">Anchor & DN attribute must be part of primary key for the selected object in the table.</span></span>
  * <span data-ttu-id="1530e-251">在使用變更追蹤的匯入和匯出期間內，不支援 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="1530e-251">SQL query is unsupported during Import and Export with Change Tracking.</span></span>

<span data-ttu-id="1530e-252">**其他參數**：指定 [資料庫伺服器時區]，以指出您的資料庫伺服器所在的位置。</span><span class="sxs-lookup"><span data-stu-id="1530e-252">**Additional Parameters**: Specify the Database Server Time Zone indicating where your Database server is located.</span></span> <span data-ttu-id="1530e-253">這個值用來支援各種格式的日期和時間屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-253">This value is used to support the various formats of date & time attributes.</span></span>

<span data-ttu-id="1530e-254">連接器一律會以 UTC 格式儲存日期和日期時間。</span><span class="sxs-lookup"><span data-stu-id="1530e-254">The Connector always stores date and date-time in UTC format.</span></span> <span data-ttu-id="1530e-255">若要能夠正確地轉換日期和時間，必須指定資料庫伺服器的時區以及所用的格式。</span><span class="sxs-lookup"><span data-stu-id="1530e-255">To be able to correctly convert the date and times, the time zone of the database server and the format used must be specified.</span></span> <span data-ttu-id="1530e-256">格式應該是以 .Net 格式表示。</span><span class="sxs-lookup"><span data-stu-id="1530e-256">The format should be expressed in .Net format.</span></span>

<span data-ttu-id="1530e-257">在匯出期間，必須器以 UTC 時間格式將每個日期時間屬性提供給連接器。</span><span class="sxs-lookup"><span data-stu-id="1530e-257">During export every date time attribute must be provided to the Connector in UTC time format.</span></span>

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

<span data-ttu-id="1530e-259">**密碼設定**：連接器會提供密碼同步處理功能並支援設定和變更密碼。</span><span class="sxs-lookup"><span data-stu-id="1530e-259">**Password Configuration**: The connector provides password synchronization capabilities and supports set and change password.</span></span>

<span data-ttu-id="1530e-260">連接器提供兩種方法來支援密碼同步處理：</span><span class="sxs-lookup"><span data-stu-id="1530e-260">The Connector provides two methods to support password synchronization:</span></span>

* <span data-ttu-id="1530e-261">**預存程序**：此方法需要兩個預存程序，以支援設定和變更密碼。</span><span class="sxs-lookup"><span data-stu-id="1530e-261">**Stored Procedure**: This method requires two stored procedures to support Set & Change password.</span></span> <span data-ttu-id="1530e-262">按照以下範例，分別在 [設定密碼 SP] 和 [變更密碼 SP] 參數中輸入新增和變更密碼作業的所有參數。</span><span class="sxs-lookup"><span data-stu-id="1530e-262">Type all parameters for add and change the password operation in **Set Password SP** and **Change Password SP** Parameters respectively as per below example.</span></span>
  <span data-ttu-id="1530e-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-263">![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)</span></span>
* <span data-ttu-id="1530e-264">**密碼延伸模組**：此方法需要密碼延伸模組 DLL (您必須提供實作 [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) 介面的延伸模組 DLL 名稱)。</span><span class="sxs-lookup"><span data-stu-id="1530e-264">**Password Extension**: This method requires Password extension DLL (you need to provide the Extension DLL Name that is implementing the [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface).</span></span> <span data-ttu-id="1530e-265">密碼延伸模組組件必須放在延伸模組資料夾中，連接器才可以在執行階段載入 DLL。</span><span class="sxs-lookup"><span data-stu-id="1530e-265">Password extension assembly must be placed in extension folder so that the connector can load the DLL at runtime.</span></span>
  <span data-ttu-id="1530e-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-266">![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)</span></span>

<span data-ttu-id="1530e-267">您也必須在 [設定延伸模組]  頁面上啟用密碼管理。</span><span class="sxs-lookup"><span data-stu-id="1530e-267">You also have to enable the Password Management on the **Configure Extension** page.</span></span>
<span data-ttu-id="1530e-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-268">![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)</span></span>

### <a name="configure-partitions-and-hierarchies"></a><span data-ttu-id="1530e-269">設定資料分割和階層</span><span class="sxs-lookup"><span data-stu-id="1530e-269">Configure Partitions and Hierarchies</span></span>
<span data-ttu-id="1530e-270">在資料分割和階層頁面上，選取所有物件類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-270">On the partitions and hierarchies page, select all object types.</span></span> <span data-ttu-id="1530e-271">每個物件類型都在自己的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="1530e-271">Each object type is its own partition.</span></span>

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

<span data-ttu-id="1530e-273">您也可以覆寫在 [連線能力] 或 [全域參數] 頁面上定義的值。</span><span class="sxs-lookup"><span data-stu-id="1530e-273">You can also override the values defined on the **Connectivity** or **Global Parameters** page.</span></span>

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a><span data-ttu-id="1530e-275">設定錨點</span><span class="sxs-lookup"><span data-stu-id="1530e-275">Configure Anchors</span></span>
<span data-ttu-id="1530e-276">此頁面是唯讀頁面，因為已經定義錨點。</span><span class="sxs-lookup"><span data-stu-id="1530e-276">This page is read-only since the anchor has already been defined.</span></span> <span data-ttu-id="1530e-277">選取的錨點屬性一律會附加物件類型，以確保它在所有物件類型中保持獨一無二。</span><span class="sxs-lookup"><span data-stu-id="1530e-277">The selected anchor attribute is always appended with the object type to ensure it remains unique across object types.</span></span>

![錨點](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a><span data-ttu-id="1530e-279">設定執行步驟參數</span><span class="sxs-lookup"><span data-stu-id="1530e-279">Configure Run Step Parameter</span></span>
<span data-ttu-id="1530e-280">這些步驟設定於連接器的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="1530e-280">These steps are configured on the run profiles on the Connector.</span></span> <span data-ttu-id="1530e-281">這些設定會進行匯入和匯出資料的實際工作。</span><span class="sxs-lookup"><span data-stu-id="1530e-281">These configurations do the actual work of importing and exporting data.</span></span>

### <a name="full-and-delta-import"></a><span data-ttu-id="1530e-282">完整和差異匯入</span><span class="sxs-lookup"><span data-stu-id="1530e-282">Full and Delta Import</span></span>
<span data-ttu-id="1530e-283">一般 SQL 連接器支援使用下列方法的完整和差異匯入：</span><span class="sxs-lookup"><span data-stu-id="1530e-283">Generic SQL Connector support Full and Delta Import using these methods:</span></span>

* <span data-ttu-id="1530e-284">資料表</span><span class="sxs-lookup"><span data-stu-id="1530e-284">Table</span></span>
* <span data-ttu-id="1530e-285">檢視</span><span class="sxs-lookup"><span data-stu-id="1530e-285">View</span></span>
* <span data-ttu-id="1530e-286">預存程序</span><span class="sxs-lookup"><span data-stu-id="1530e-286">Stored Procedure</span></span>
* <span data-ttu-id="1530e-287">SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="1530e-287">SQL Query</span></span>

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

<span data-ttu-id="1530e-289">**資料表/檢視**</span><span class="sxs-lookup"><span data-stu-id="1530e-289">**Table/View**</span></span>  
<span data-ttu-id="1530e-290">若要匯入物件的多重值屬性，您必須在 [多重資料表/檢視名稱] 中提供以逗號分隔的資料表/檢視名稱，以及在父資料表的 [聯結條件] 中提供各自的聯結條件。</span><span class="sxs-lookup"><span data-stu-id="1530e-290">To import multi-valued attributes for an object, you have to provide the comma-separated table/view name in **Name of Multi-Valued table/views** and respective join conditions in the **Join condition** with the parent table.</span></span>

<span data-ttu-id="1530e-291">範例：您想要匯入 [員工] 物件與其所有的多重值屬性。</span><span class="sxs-lookup"><span data-stu-id="1530e-291">Example: You want to import the Employee object and all its multi-valued attributes.</span></span> <span data-ttu-id="1530e-292">有兩個資料表：[員工] \(主要資料表) 和 [部門] \(多重值)。</span><span class="sxs-lookup"><span data-stu-id="1530e-292">There are two tables, named Employee (main table) and Department (multi-valued).</span></span>
<span data-ttu-id="1530e-293">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="1530e-293">Do the following:</span></span>

* <span data-ttu-id="1530e-294">在 [資料表/檢視/SP] 中輸入**員工**。</span><span class="sxs-lookup"><span data-stu-id="1530e-294">Type **Employee** in **Table/View/SP**.</span></span>
* <span data-ttu-id="1530e-295">在 [多重資料表/檢視名稱] 中輸入 [部門]。</span><span class="sxs-lookup"><span data-stu-id="1530e-295">Type Department in **Name of Multi-Valued table/views**.</span></span>
* <span data-ttu-id="1530e-296">在 [聯結條件] 中輸入 [員工] 和 [部門] 之間的聯結條件，例如 `Employee.DEPTID=Department.DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="1530e-296">Type the join condition between Employee & Department in **Join Condition**, for example `Employee.DEPTID=Department.DepartmentID`.</span></span>
  <span data-ttu-id="1530e-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-297">![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)</span></span>

<span data-ttu-id="1530e-298">**預存程序**</span><span class="sxs-lookup"><span data-stu-id="1530e-298">**Stored procedures**</span></span>  
<span data-ttu-id="1530e-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-299">![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)</span></span>

* <span data-ttu-id="1530e-300">如果您有大量資料，建議實作預存程序的分頁。</span><span class="sxs-lookup"><span data-stu-id="1530e-300">If you have much data, it is recommended to implement pagination with your Stored Procedures.</span></span>
* <span data-ttu-id="1530e-301">若要讓預存程序支援分頁，您必須提供開始索引和結束索引。</span><span class="sxs-lookup"><span data-stu-id="1530e-301">For your Stored Procedure to support pagination, you need to provide Start Index and End Index.</span></span> <span data-ttu-id="1530e-302">請參閱： [有效地進行大量資料的分頁](https://msdn.microsoft.com/library/bb445504.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1530e-302">See: [Efficiently Paging Through Large Amounts of Data](https://msdn.microsoft.com/library/bb445504.aspx).</span></span>
* <span data-ttu-id="1530e-303">在執行時，會以在 [設定步驟] 頁面上設定的各自頁面大小值取代 @StartIndex 和 @EndIndex。</span><span class="sxs-lookup"><span data-stu-id="1530e-303">@StartIndex and @EndIndex are replaced at execution time with respective page size value configured on **Configure Step** page.</span></span> <span data-ttu-id="1530e-304">例如，當連接器擷取第一頁且頁面大小設為 500 時，在這種情況下 @StartIndex 會是 1 而 @EndIndex 會是 500。</span><span class="sxs-lookup"><span data-stu-id="1530e-304">For example, when the connector retrieves first page and the page size is set 500, in such situation @StartIndex would be 1 and @EndIndex 500.</span></span> <span data-ttu-id="1530e-305">當連接器擷取後續頁面並變更 @StartIndex 和 @EndIndex 值時，這些值增加。</span><span class="sxs-lookup"><span data-stu-id="1530e-305">These values increase when connector retrieves subsequent pages and change the @StartIndex & @EndIndex value.</span></span>
* <span data-ttu-id="1530e-306">若要執行參數化預存程序，請以 `[Name]:[Direction]:[Value]` 格式提供參數。</span><span class="sxs-lookup"><span data-stu-id="1530e-306">To execute parameterized Stored Procedure, provide the parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="1530e-307">在個別一行上輸入每個參數 (使用 Ctrl + Enter 來換行)。</span><span class="sxs-lookup"><span data-stu-id="1530e-307">Enter each parameter on a separate line (Use Ctrl + Enter to get a new line).</span></span>
* <span data-ttu-id="1530e-308">一般 SQL 連接器也支援從 Microsoft SQL Server 中連結伺服器的匯入作業。</span><span class="sxs-lookup"><span data-stu-id="1530e-308">Generic SQL connector also supports Import operation from Linked Servers in Microsoft SQL Server.</span></span> <span data-ttu-id="1530e-309">如果應該從連結的伺服器中的資料表擷取資訊，則應該以下列格式提供資料表： `[ServerName].[Database].[Schema].[TableName]`</span><span class="sxs-lookup"><span data-stu-id="1530e-309">If information should be retrieved from a Table in Linked server, then Table should be provided in the format: `[ServerName].[Database].[Schema].[TableName]`</span></span>
* <span data-ttu-id="1530e-310">一般 SQL 連接器僅支援在執行步驟資訊和結構描述偵測之間具有類似結構 (包括別名和資料類型) 的物件。</span><span class="sxs-lookup"><span data-stu-id="1530e-310">Generic SQL Connector supports only those objects that have similar structure (both alias name and data type) between run steps information and schema detection.</span></span> <span data-ttu-id="1530e-311">如果結構描述中選取的物件與在執行步驟提供的資訊不同，則 SQL 連接器無法支援這類案例。</span><span class="sxs-lookup"><span data-stu-id="1530e-311">If the selected object from schema and provided information at run step is different, then SQL Connector is unable to support this type of scenarios.</span></span>

<span data-ttu-id="1530e-312">**SQL 查詢**</span><span class="sxs-lookup"><span data-stu-id="1530e-312">**SQL Query**</span></span>  
<span data-ttu-id="1530e-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-313">![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)</span></span>

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* <span data-ttu-id="1530e-315">不支援多個結果集查詢。</span><span class="sxs-lookup"><span data-stu-id="1530e-315">Multiple result sets queries not supported.</span></span>
* <span data-ttu-id="1530e-316">SQL 查詢支援分頁並提供開始索引和結束索引做為變數，以支援分頁。</span><span class="sxs-lookup"><span data-stu-id="1530e-316">SQL query supports the pagination and provide start Index and End Index as a variable to support pagination.</span></span>

### <a name="delta-import"></a><span data-ttu-id="1530e-317">差異匯入</span><span class="sxs-lookup"><span data-stu-id="1530e-317">Delta Import</span></span>
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

<span data-ttu-id="1530e-319">相較於完整匯入，差異匯入設定需要一些更詳細的設定。</span><span class="sxs-lookup"><span data-stu-id="1530e-319">Delta Import configuration requires some more configuration compared with Full Import.</span></span>

* <span data-ttu-id="1530e-320">如果您選擇 [觸發程序] 或 [快照] 方法來追蹤差異變更，則在 [歷程記錄資料表或快照資料庫名稱]  方塊中提供歷程記錄資料表或快照資料庫。</span><span class="sxs-lookup"><span data-stu-id="1530e-320">If you choose the Trigger or Snapshot approach to track delta changes, then provide History Table or Snapshot database in **History Table or Snapshot database name** box.</span></span>
* <span data-ttu-id="1530e-321">您也必須提供歷程記錄資枓表與父資料表之間的聯結條件，例如 `Employee.ID=History.EmployeeID`</span><span class="sxs-lookup"><span data-stu-id="1530e-321">You also need to provide join condition between History table and Parent table, for example `Employee.ID=History.EmployeeID`</span></span>
* <span data-ttu-id="1530e-322">若要從歷程記錄資料表追蹤父資料表上的交易，您必須提供包含作業資訊 (新增/更新/刪除) 的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="1530e-322">To track the transaction on the parent table from the history table, you must provide the column name that contains the operation information (Add/Update/Delete).</span></span>
* <span data-ttu-id="1530e-323">如果您者選擇 [浮水印] 來追蹤差異變更，則在 [浮水印資料行名稱] 中提供包含作業資訊的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="1530e-323">If you choose Watermark to track delta changes, then provide the column name that contains the operation information in **Water Mark Column Name**.</span></span>
* <span data-ttu-id="1530e-324">變更類型需要 [變更型別屬性]  資料行。</span><span class="sxs-lookup"><span data-stu-id="1530e-324">The **change Type attribute** column is required for the change type.</span></span> <span data-ttu-id="1530e-325">此資料行會將主要資料表或多重值資料表中發生的變更，對應至差異檢視中的變更類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-325">This column maps a change that occurs in the primary table or multi-value table to a change type in the delta view.</span></span> <span data-ttu-id="1530e-326">此資料行可以包含適用於屬性層級變更的 Modify_Attribute 變更類型，或適用於物件層級變更的 [新增]、[修改] 或 [刪除] 變更類型。</span><span class="sxs-lookup"><span data-stu-id="1530e-326">This column can contain the Modify_Attribute change type for attribute-level change or an Add, Modify, or Delete change type for an object-level change type.</span></span> <span data-ttu-id="1530e-327">如果除了預設值 [新增]、[修改] 或 [刪除] 以外，您可以使用此選項來定義這些值。</span><span class="sxs-lookup"><span data-stu-id="1530e-327">If it is something other than the default value Add, Modify, or Delete, then you can define those values using this option.</span></span>

### <a name="export"></a><span data-ttu-id="1530e-328">匯出</span><span class="sxs-lookup"><span data-stu-id="1530e-328">Export</span></span>
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

<span data-ttu-id="1530e-330">一般 SQL 連接器支援使用下列四種方法的匯出：</span><span class="sxs-lookup"><span data-stu-id="1530e-330">Generic SQL Connector support Export using four supported methods such as:</span></span>

* <span data-ttu-id="1530e-331">資料表</span><span class="sxs-lookup"><span data-stu-id="1530e-331">Table</span></span>
* <span data-ttu-id="1530e-332">檢視</span><span class="sxs-lookup"><span data-stu-id="1530e-332">View</span></span>
* <span data-ttu-id="1530e-333">預存程序</span><span class="sxs-lookup"><span data-stu-id="1530e-333">Stored Procedure</span></span>
* <span data-ttu-id="1530e-334">SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="1530e-334">SQL Query</span></span>

<span data-ttu-id="1530e-335">**資料表/檢視**</span><span class="sxs-lookup"><span data-stu-id="1530e-335">**Table/View**</span></span>  
<span data-ttu-id="1530e-336">如果您選擇 [資料表/檢視] 選項，則連接器會產生各自的查詢來進行匯出。</span><span class="sxs-lookup"><span data-stu-id="1530e-336">If you choose the Table/View option, then the connector generates the respective queries to do the Export.</span></span>

<span data-ttu-id="1530e-337">**預存程序**</span><span class="sxs-lookup"><span data-stu-id="1530e-337">**Stored procedures**</span></span>  
<span data-ttu-id="1530e-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-338">![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)</span></span>

<span data-ttu-id="1530e-339">如果您選擇預存程序選項，則匯出需要 3 個不同的預存程序才能執行插入/更新/刪除作業。</span><span class="sxs-lookup"><span data-stu-id="1530e-339">If you choose the Stored Procedure option, Export requires three different Stored procedures to perform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="1530e-340">**新增 SP 名稱**：如有任何物件來到連接器以便在各自的資料表中插入，就會執行此 SP。</span><span class="sxs-lookup"><span data-stu-id="1530e-340">**Add SP Name**: This SP runs if any object comes to connector for insertion in the respective table.</span></span>
* <span data-ttu-id="1530e-341">**更新 SP 名稱**：如有任何物件來到連接器以便在各自的資料表中更新，就會執行此 SP。</span><span class="sxs-lookup"><span data-stu-id="1530e-341">**Update SP Name**: This SP runs if any object comes to connector for update in the respective table.</span></span>
* <span data-ttu-id="1530e-342">**刪除 SP 名稱**：如有任何物件來到連接器以便在各自的資料表中刪除，就會執行此 SP。</span><span class="sxs-lookup"><span data-stu-id="1530e-342">**Delete SP Name**: This SP runs if any object comes to connector for deletion in the respective table.</span></span>
* <span data-ttu-id="1530e-343">從結構描述選取的屬性會做為預存程序的參數值。</span><span class="sxs-lookup"><span data-stu-id="1530e-343">Attribute selected from the schema used as a parameter value to the stored procedure.</span></span> <span data-ttu-id="1530e-344">範例： `EmployeeName: INPUT: @EmployeeName` (EmployeeName 已在連接器結構描述中選取，而連接器會在進行匯出時取代各自的值)</span><span class="sxs-lookup"><span data-stu-id="1530e-344">For example, `EmployeeName: INPUT: @EmployeeName` (EmployeeName is selected in the connector schema and the connector replaces the respective value while doing export)</span></span>
* <span data-ttu-id="1530e-345">若要執行參數化預存程序，請以 `[Name]:[Direction]:[Value]` 格式提供參數。</span><span class="sxs-lookup"><span data-stu-id="1530e-345">To run parameterized stored procedure, provide parameters in `[Name]:[Direction]:[Value]` format.</span></span> <span data-ttu-id="1530e-346">在個別一行上輸入每個參數 (使用 Ctrl + Enter 來換行)。</span><span class="sxs-lookup"><span data-stu-id="1530e-346">Enter each parameter on a separate line (Use Ctrl + Enter to get a new line).</span></span>

<span data-ttu-id="1530e-347">**SQL query**</span><span class="sxs-lookup"><span data-stu-id="1530e-347">**SQL query**</span></span>  
<span data-ttu-id="1530e-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span><span class="sxs-lookup"><span data-stu-id="1530e-348">![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)</span></span>

<span data-ttu-id="1530e-349">如果您選擇 SQL 查詢選項，則匯出需要 3 個不同的查詢來執行插入/更新/刪除作業。</span><span class="sxs-lookup"><span data-stu-id="1530e-349">If you choose the SQL query option, Export requires three different queries to perform Insert/Update/Delete operations.</span></span>

* <span data-ttu-id="1530e-350">**插入查詢**：如有任何物件來到連接器以便在各自的資料表中插入，就會執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="1530e-350">**Insert Query**: This query runs if any object comes to connector for insertion in the respective table.</span></span>
* <span data-ttu-id="1530e-351">**更新查詢**：如有任何物件來到連接器以便在各自的資料表中更新，就會執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="1530e-351">**Update Query**: This query runs if any object comes to connector for update in the respective table.</span></span>
* <span data-ttu-id="1530e-352">**刪除查詢**：如有任何物件來到連接器以便在各自的資料表中刪除，就會執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="1530e-352">**Delete Query**: This query runs if any object comes to connector for deletion in the respective table.</span></span>
* <span data-ttu-id="1530e-353">從結構描述選取的屬性會做為查詢的參數值，例如 `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span><span class="sxs-lookup"><span data-stu-id="1530e-353">Attribute selected from the schema used as a parameter value to the query, for example `Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1530e-354">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1530e-354">Troubleshooting</span></span>
* <span data-ttu-id="1530e-355">如需如何啟用記錄來疑難排解連接器的資訊，請參閱 [如何啟用連接器的 ETW 追蹤](http://go.microsoft.com/fwlink/?LinkId=335731)。</span><span class="sxs-lookup"><span data-stu-id="1530e-355">For information on how to enable logging to troubleshoot the connector, see the [How to Enable ETW Tracing for Connectors](http://go.microsoft.com/fwlink/?LinkId=335731).</span></span>
