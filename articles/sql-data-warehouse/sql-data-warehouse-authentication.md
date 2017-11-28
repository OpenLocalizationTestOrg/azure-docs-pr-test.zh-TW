---
title: "適用於 Azure SQL 資料倉儲的驗證 | Microsoft Docs"
description: "適用於 Azure SQL 資料倉儲的 Azure Active Directory (AAD) 與 SQL Server 驗證。"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="59e05-103">適用於 Azure SQL 資料倉儲的驗證</span><span class="sxs-lookup"><span data-stu-id="59e05-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59e05-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="59e05-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="59e05-105">驗證</span><span class="sxs-lookup"><span data-stu-id="59e05-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="59e05-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="59e05-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="59e05-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="59e05-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="59e05-108">若要連線到 SQL 資料倉儲，您必須傳入安全性認證進行驗證用途。</span><span class="sxs-lookup"><span data-stu-id="59e05-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="59e05-109">建立連線時，會設定特定的連線設定，以做為建立查詢工作階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="59e05-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="59e05-110">如需安全性以及如何啟用您資料倉儲連線的詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="59e05-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="59e05-111">SQL 驗證</span><span class="sxs-lookup"><span data-stu-id="59e05-111">SQL authentication</span></span>
<span data-ttu-id="59e05-112">若要連線到 SQL 資料倉儲，您必須提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="59e05-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="59e05-113">完整伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="59e05-113">Fully qualified servername</span></span>
* <span data-ttu-id="59e05-114">指定 SQL 驗證</span><span class="sxs-lookup"><span data-stu-id="59e05-114">Specify SQL authentication</span></span>
* <span data-ttu-id="59e05-115">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="59e05-115">Username</span></span>
* <span data-ttu-id="59e05-116">密碼</span><span class="sxs-lookup"><span data-stu-id="59e05-116">Password</span></span>
* <span data-ttu-id="59e05-117">預設資料庫 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="59e05-117">Default database (optional)</span></span>

<span data-ttu-id="59e05-118">根據預設，您的連線會連線至「主要」  資料庫，而非您的使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="59e05-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="59e05-119">若要連線到您的使用者資料庫，您可以選擇執行下列兩個動作之一：</span><span class="sxs-lookup"><span data-stu-id="59e05-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="59e05-120">使用伺服器註冊 SSDT、SSMS 或應用程式連接字串中的 SQL Server 物件總管時，請指定預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="59e05-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="59e05-121">例如，包含 ODBC 連線的 InitialCatalog 參數。</span><span class="sxs-lookup"><span data-stu-id="59e05-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="59e05-122">在 SSDT 中建立工作階段之前，先反白顯示使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="59e05-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="59e05-123">變更連線的資料庫時，Transact-SQL 陳述式 **USE MyDatabase;** 不受支援。</span><span class="sxs-lookup"><span data-stu-id="59e05-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="59e05-124">如需使用 SSDT 連線到 SQL 資料倉儲的指引，請參閱[使用 Visual Studio 查詢][Query with Visual Studio]文章。</span><span class="sxs-lookup"><span data-stu-id="59e05-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="59e05-125">Azure Active Directory (AAD) 驗證</span><span class="sxs-lookup"><span data-stu-id="59e05-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="59e05-126">[Azure Active Directory][What is Azure Active Directory] 驗證是 Azure Active Directory (Azure AD) 中使用身分識別連接到 Microsoft Azure SQL 資料倉儲的機制。</span><span class="sxs-lookup"><span data-stu-id="59e05-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="59e05-127">您可以使用 Azure Active Directory 驗證，在單一中央位置集中管理資料庫使用者和其他 Microsoft 服務的身分識別。</span><span class="sxs-lookup"><span data-stu-id="59e05-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="59e05-128">中央識別碼管理提供單一位置以管理 SQL 資料倉儲使用者並簡化權限管理。</span><span class="sxs-lookup"><span data-stu-id="59e05-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="59e05-129">優點</span><span class="sxs-lookup"><span data-stu-id="59e05-129">Benefits</span></span>
<span data-ttu-id="59e05-130">Azure Active Directory 的優點包括：</span><span class="sxs-lookup"><span data-stu-id="59e05-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="59e05-131">提供 SQL Server 驗證的替代方案。</span><span class="sxs-lookup"><span data-stu-id="59e05-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="59e05-132">協助停止跨資料庫伺服器使用過多的使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="59e05-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="59e05-133">允許在單一位置的密碼替換</span><span class="sxs-lookup"><span data-stu-id="59e05-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="59e05-134">使用外部 (AAD) 群組管理資料庫權限。</span><span class="sxs-lookup"><span data-stu-id="59e05-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="59e05-135">藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="59e05-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="59e05-136">使用自主資料庫使用者，在資料庫層級驗證身分。</span><span class="sxs-lookup"><span data-stu-id="59e05-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="59e05-137">針對連線到 SQL 資料倉儲的應用程式支援權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="59e05-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="59e05-138">透過 SQL Server Management Studio 的 Active Directory 通用驗證支援 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="59e05-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="59e05-139">如需 Multi-Factor Authentication 的說明，請參閱 [適用於 Azure AD MFA 與 SQL Database 和 SQL 資料倉儲的 SSMS 支援](../sql-database/sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="59e05-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="59e05-140">Azure Active Directory 相對來說仍較新，且具有一些限制。</span><span class="sxs-lookup"><span data-stu-id="59e05-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="59e05-141">若要確定 Azure Active Directory 適合您的環境，請參閱 [Azure AD 功能和限制][Azure AD features and limitations]，特別是＜其他考量＞。</span><span class="sxs-lookup"><span data-stu-id="59e05-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="59e05-142">組態步驟</span><span class="sxs-lookup"><span data-stu-id="59e05-142">Configuration steps</span></span>
<span data-ttu-id="59e05-143">請遵循下列步驟來設定 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="59e05-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="59e05-144">建立和填入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59e05-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="59e05-145">選用：和目前與您的 Azure 訂用帳戶相關聯的 active directory 產生關聯並加以變更</span><span class="sxs-lookup"><span data-stu-id="59e05-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="59e05-146">建立 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="59e05-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="59e05-147">設定用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="59e05-147">Configure your client computers</span></span>
5. <span data-ttu-id="59e05-148">在對應至 Azure AD 身分識別的資料庫中建立自主資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="59e05-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="59e05-149">使用 Azure AD 身分識別連接到您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="59e05-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="59e05-150">Azure Active Directory 使用者目前不會顯示在 SSDT 物件總管中。</span><span class="sxs-lookup"><span data-stu-id="59e05-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="59e05-151">解決方法是在 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx) 中檢視使用者。</span><span class="sxs-lookup"><span data-stu-id="59e05-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="59e05-152">尋找詳細資料</span><span class="sxs-lookup"><span data-stu-id="59e05-152">Find the details</span></span>
* <span data-ttu-id="59e05-153">針對 Azure SQL Database 及針對 Azure SQL 資料倉儲設定並使用 Azure Active Directory 驗證的步驟幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="59e05-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="59e05-154">請依照 [使用 Azure Active Directory 驗證連線到 SQL Database 或 SQL 資料倉儲](../sql-database/sql-database-aad-authentication.md)主題中的詳細步驟操作。</span><span class="sxs-lookup"><span data-stu-id="59e05-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="59e05-155">建立自訂資料庫角色，並加入使用者至角色。</span><span class="sxs-lookup"><span data-stu-id="59e05-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="59e05-156">然後授與角色細微的權限。</span><span class="sxs-lookup"><span data-stu-id="59e05-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="59e05-157">如需詳細資訊，請參閱 [資料庫引擎權限使用者入門](https://msdn.microsoft.com/library/mt667986.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59e05-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59e05-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59e05-158">Next steps</span></span>
<span data-ttu-id="59e05-159">若要透過 Visual Studio 和其他應用程式開始查詢您的資料倉儲，請參閱[使用 Visual Studio 查詢][Query with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="59e05-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
