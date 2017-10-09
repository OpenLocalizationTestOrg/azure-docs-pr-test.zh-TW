---
title: "aaaAuthentication tooAzure SQL 資料倉儲 |Microsoft 文件"
description: "Azure Active Directory (AAD) 與 SQL Server 驗證 tooAzure SQL 資料倉儲。"
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
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="04d56-103">驗證 tooAzure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="04d56-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04d56-104">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="04d56-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="04d56-105">驗證</span><span class="sxs-lookup"><span data-stu-id="04d56-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="04d56-106">加密 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="04d56-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="04d56-107">加密 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="04d56-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="04d56-108">tooconnect tooSQL 資料倉儲，您必須傳入安全性認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="04d56-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="04d56-109">建立連線時，會設定特定的連線設定，以做為建立查詢工作階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="04d56-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="04d56-110">如需有關安全性和如何 tooenable 連線 tooyour 資料倉儲時，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="04d56-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="04d56-111">SQL 驗證</span><span class="sxs-lookup"><span data-stu-id="04d56-111">SQL authentication</span></span>
<span data-ttu-id="04d56-112">tooconnect tooSQL 資料倉儲，您必須提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="04d56-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="04d56-113">完整伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="04d56-113">Fully qualified servername</span></span>
* <span data-ttu-id="04d56-114">指定 SQL 驗證</span><span class="sxs-lookup"><span data-stu-id="04d56-114">Specify SQL authentication</span></span>
* <span data-ttu-id="04d56-115">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="04d56-115">Username</span></span>
* <span data-ttu-id="04d56-116">密碼</span><span class="sxs-lookup"><span data-stu-id="04d56-116">Password</span></span>
* <span data-ttu-id="04d56-117">預設資料庫 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="04d56-117">Default database (optional)</span></span>

<span data-ttu-id="04d56-118">依預設您的連接會連接 toohello*主要*資料庫而非您的使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="04d56-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="04d56-119">tooconnect tooyour 使用者資料庫中，您可以選擇 toodo 兩種情況之一：</span><span class="sxs-lookup"><span data-stu-id="04d56-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="04d56-120">以 SQL Server 物件總管在 SSDT 中，SSMS 中，或在您的應用程式的連接字串中的 hello 註冊您的伺服器時，請指定 hello 預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="04d56-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="04d56-121">例如，包含 ODBC 連接的 hello InitialCatalog 參數。</span><span class="sxs-lookup"><span data-stu-id="04d56-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="04d56-122">在 SSDT 中建立工作階段之前，反白 hello 使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="04d56-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="04d56-123">hello TRANSACT-SQL 陳述式**使用 MyDatabase;**不支援變更 hello 連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="04d56-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="04d56-124">有了 SSDT 連接 tooSQL 資料倉儲的指引，請參閱 toohello [Visual Studio 中的查詢][ Query with Visual Studio]發行項。</span><span class="sxs-lookup"><span data-stu-id="04d56-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="04d56-125">Azure Active Directory (AAD) 驗證</span><span class="sxs-lookup"><span data-stu-id="04d56-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="04d56-126">[Azure Active Directory] [ What is Azure Active Directory]驗證是一項機制的 Azure Active Directory (Azure AD) 中使用身分識別連接 tooMicrosoft Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="04d56-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="04d56-127">使用 Azure Active Directory 驗證時，您可以集中管理 hello 的資料庫使用者的身分識別和其他 Microsoft 服務在單一中央位置。</span><span class="sxs-lookup"><span data-stu-id="04d56-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="04d56-128">中央識別碼管理 toomanage SQL 資料倉儲使用者提供單一位置，並簡化權限管理。</span><span class="sxs-lookup"><span data-stu-id="04d56-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="04d56-129">優點</span><span class="sxs-lookup"><span data-stu-id="04d56-129">Benefits</span></span>
<span data-ttu-id="04d56-130">Azure Active Directory 的優點包括：</span><span class="sxs-lookup"><span data-stu-id="04d56-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="04d56-131">提供的替代 tooSQL 伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="04d56-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="04d56-132">可協助停止使用者身分識別的 hello 的擴散到資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="04d56-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="04d56-133">允許在單一位置的密碼替換</span><span class="sxs-lookup"><span data-stu-id="04d56-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="04d56-134">使用外部 (AAD) 群組管理資料庫權限。</span><span class="sxs-lookup"><span data-stu-id="04d56-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="04d56-135">藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="04d56-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="04d56-136">使用自主資料庫使用者 tooauthenticate 識別 hello 資料庫層級。</span><span class="sxs-lookup"><span data-stu-id="04d56-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="04d56-137">支援權杖為基礎的驗證連接 tooSQL 資料倉儲的應用程式。</span><span class="sxs-lookup"><span data-stu-id="04d56-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="04d56-138">透過 SQL Server Management Studio 的 Active Directory 通用驗證支援 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="04d56-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="04d56-139">如需 Multi-Factor Authentication 的說明，請參閱 [適用於 Azure AD MFA 與 SQL Database 和 SQL 資料倉儲的 SSMS 支援](../sql-database/sql-database-ssms-mfa-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="04d56-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="04d56-140">Azure Active Directory 相對來說仍較新，且具有一些限制。</span><span class="sxs-lookup"><span data-stu-id="04d56-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="04d56-141">請參閱 Azure Active Directory 是您的環境，適合 tooensure [Azure AD 的功能和限制][Azure AD features and limitations]，具體來說 hello 其他考量。</span><span class="sxs-lookup"><span data-stu-id="04d56-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="04d56-142">組態步驟</span><span class="sxs-lookup"><span data-stu-id="04d56-142">Configuration steps</span></span>
<span data-ttu-id="04d56-143">請遵循這些步驟 tooconfigure Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="04d56-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="04d56-144">建立和填入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04d56-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="04d56-145">選擇性： 建立關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory</span><span class="sxs-lookup"><span data-stu-id="04d56-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="04d56-146">建立 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="04d56-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="04d56-147">設定用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="04d56-147">Configure your client computers</span></span>
5. <span data-ttu-id="04d56-148">在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者</span><span class="sxs-lookup"><span data-stu-id="04d56-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="04d56-149">使用 Azure AD 識別身分，連接 tooyour 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="04d56-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="04d56-150">Azure Active Directory 使用者目前不會顯示在 SSDT 物件總管中。</span><span class="sxs-lookup"><span data-stu-id="04d56-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="04d56-151">因應措施，檢視中的 hello 使用者[sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04d56-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="04d56-152">找出 hello 詳細資料</span><span class="sxs-lookup"><span data-stu-id="04d56-152">Find hello details</span></span>
* <span data-ttu-id="04d56-153">hello 步驟 tooconfigure 和使用 Azure Active Directory 驗證是用於 Azure SQL Database 和 Azure SQL 資料倉儲幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="04d56-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="04d56-154">請遵循 hello 詳細 hello 主題中的步驟[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](../sql-database/sql-database-aad-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="04d56-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="04d56-155">建立自訂資料庫角色，並新增使用者 toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="04d56-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="04d56-156">然後授與的細微權限 toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="04d56-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="04d56-157">如需詳細資訊，請參閱 [資料庫引擎權限使用者入門](https://msdn.microsoft.com/library/mt667986.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04d56-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d56-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04d56-158">Next steps</span></span>
<span data-ttu-id="04d56-159">toostart 查詢您的資料倉儲與 Visual Studio 和其他應用程式，請參閱[Visual Studio 中的查詢][Query with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="04d56-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
