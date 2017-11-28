---
title: "aaaSQL 資料庫應用程式開發概觀 |Microsoft 文件"
description: "了解可用的連接程式庫和連接 tooSQL 資料庫應用程式的最佳作法。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a><span data-ttu-id="ea7b1-103">SQL Database 應用程式開發概觀</span><span class="sxs-lookup"><span data-stu-id="ea7b1-103">SQL Database application development overview</span></span>
<span data-ttu-id="ea7b1-104">本文逐步 hello 開發人員應該注意撰寫程式碼 tooconnect tooAzure SQL Database 時的基本考量。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-104">This article walks through hello basic considerations that a developer should be aware of when writing code tooconnect tooAzure SQL Database.</span></span>

> [!TIP]
> <span data-ttu-id="ea7b1-105">如需教學課程顯示您如何 toocreate 伺服器，建立伺服器型防火牆，檢視伺服器屬性，使用 SQL Server Management Studio，查詢 hello master 資料庫進行連接、 建立範例資料庫和一個空白資料庫、 查詢資料庫內容，連接使用 SQL Server Management Studio，而且查詢 hello 範例資料庫，請參閱[取得教學課程](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, connect using SQL Server Management Studio, query hello master database, create a sample database and a blank database, query database properties, connect using SQL Server Management Studio, and query hello sample database, see [Get Started Tutorial](sql-database-get-started-portal.md).</span></span>
>

## <a name="language-and-platform"></a><span data-ttu-id="ea7b1-106">語言和平台</span><span class="sxs-lookup"><span data-stu-id="ea7b1-106">Language and platform</span></span>
<span data-ttu-id="ea7b1-107">有一些程式碼範例可供各種程式設計語言和平台使用。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="ea7b1-108">您可以找到連結 toohello 程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="ea7b1-108">You can find links toohello code samples at:</span></span> 

* <span data-ttu-id="ea7b1-109">詳細資訊： [SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-109">More Information: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="ea7b1-110">工具</span><span class="sxs-lookup"><span data-stu-id="ea7b1-110">Tools</span></span> 
<span data-ttu-id="ea7b1-111">您可以利用 [cheetah](https://github.com/wunderlist/cheetah)、[sql-cli](https://www.npmjs.com/package/sql-cli)、[VS Code](https://code.visualstudio.com/) 等開放原始碼工具。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-111">You can leverage open source tools like [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli), [VS Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="ea7b1-112">此外，Azure SQL Database 使用 [Visual Studio](https://www.visualstudio.com/downloads/) 和 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) 等 Microsoft 工具。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-112">Additionally, Azure SQL Database works with Microsoft tools like [Visual Studio](https://www.visualstudio.com/downloads/) and  [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>  <span data-ttu-id="ea7b1-113">您也可以使用 hello Azure 管理入口網站、 PowerShell 和 REST Api 可協助您獲得額外的產能。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-113">You can also use hello Azure Management Portal, PowerShell, and REST APIs help you gain additional productivity.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="ea7b1-114">資源限制</span><span class="sxs-lookup"><span data-stu-id="ea7b1-114">Resource limitations</span></span>
<span data-ttu-id="ea7b1-115">Azure SQL Database 管理 hello 資源可用 tooa 資料庫使用兩個不同的機制： 資源控管和強制執行的限制。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-115">Azure SQL Database manages hello resources available tooa database using two different mechanisms: Resources Governance and Enforcement of Limits.</span></span>

* <span data-ttu-id="ea7b1-116">詳細資訊： [Azure SQL Database 資源限制](sql-database-resource-limits.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-116">More Information: [Azure SQL Database resource limits](sql-database-resource-limits.md)</span></span>

## <a name="security"></a><span data-ttu-id="ea7b1-117">安全性</span><span class="sxs-lookup"><span data-stu-id="ea7b1-117">Security</span></span>
<span data-ttu-id="ea7b1-118">Azure SQL Database 提供資源以在 SQL Database 上限制存取、保護資料，以及監視活動。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-118">Azure SQL Database provides resources for limiting access, protecting data, and monitoring activities on a SQL Database.</span></span>

* <span data-ttu-id="ea7b1-119">詳細資訊： [保護您的 SQL Database](sql-database-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-119">More Information: [Securing your SQL Database](sql-database-security-overview.md)</span></span>

## <a name="authentication"></a><span data-ttu-id="ea7b1-120">驗證</span><span class="sxs-lookup"><span data-stu-id="ea7b1-120">Authentication</span></span>
* <span data-ttu-id="ea7b1-121">Azure SQL Database 支援 SQL Server 驗證使用者和登入，以及 [Azure Active Directory 驗證](sql-database-aad-authentication.md) 使用者和登入。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-121">Azure SQL Database supports both SQL Server authentication users and logins, as well as [Azure Active Directory authentication](sql-database-aad-authentication.md) users and logins.</span></span>
* <span data-ttu-id="ea7b1-122">您需要特定的資料庫，而不是正在 toohello toospecify*主要*資料庫。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-122">You need toospecify a particular database, instead of defaulting toohello *master* database.</span></span>
* <span data-ttu-id="ea7b1-123">您無法使用 hello TRANSACT-SQL**使用 myDatabaseName;** SQL Database tooswitch tooanother 資料庫上的陳述式。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-123">You cannot use hello Transact-SQL **USE myDatabaseName;** statement on SQL Database tooswitch tooanother database.</span></span>
* <span data-ttu-id="ea7b1-124">詳細資訊： [SQL Database 安全性：管理資料庫存取與登入安全性](sql-database-manage-logins.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-124">More information: [SQL Database security: Manage database access and login security](sql-database-manage-logins.md)</span></span>

## <a name="resiliency"></a><span data-ttu-id="ea7b1-125">復原功能</span><span class="sxs-lookup"><span data-stu-id="ea7b1-125">Resiliency</span></span>
<span data-ttu-id="ea7b1-126">當連線 tooSQL 資料庫時，就會發生暫時性的錯誤時，您的程式碼應該重試 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-126">When a transient error occurs while connecting tooSQL Database, your code should retry hello call.</span></span>  <span data-ttu-id="ea7b1-127">建議重試邏輯使用輪詢邏輯，使它不會不會淹沒 hello SQL Database 與多個用戶端同時重試。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-127">We recommend that retry logic use backoff logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

* <span data-ttu-id="ea7b1-128">程式碼範例： 取得程式碼範例將示範中，然後重試邏輯，請參閱您選擇在 hello 語言的範例：[連接程式庫，針對 SQL Database 和 SQL Server](sql-database-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-128">Code samples:  For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connection libraries for SQL Database and SQL Server](sql-database-libraries.md)</span></span>
* <span data-ttu-id="ea7b1-129">詳細資訊： [SQL Database 用戶端程式的錯誤訊息](sql-database-develop-error-messages.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-129">More information: [Error messages for SQL Database client programs](sql-database-develop-error-messages.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="ea7b1-130">管理連線</span><span class="sxs-lookup"><span data-stu-id="ea7b1-130">Managing connections</span></span>
* <span data-ttu-id="ea7b1-131">在您用戶端連線的邏輯，覆寫 hello 預設逾時 toobe 30 秒。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-131">In your client connection logic, override hello default timeout toobe 30 seconds.</span></span>  <span data-ttu-id="ea7b1-132">hello 預設值是 15 秒會太短，取決於的連接 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-132">hello default of 15 seconds is too short for connections that depend on hello internet.</span></span>
* <span data-ttu-id="ea7b1-133">如果您使用[連接集區](http://msdn.microsoft.com/library/8xx3tyca.aspx)，是確定 tooclose hello 連接 hello 立即程式未主動使用它，並不準備 tooreuse 它。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-133">If you are using a [connection pool](http://msdn.microsoft.com/library/8xx3tyca.aspx), be sure tooclose hello connection hello instant your program is not actively using it, and is not preparing tooreuse it.</span></span>

## <a name="network-considerations"></a><span data-ttu-id="ea7b1-134">網路考量事項</span><span class="sxs-lookup"><span data-stu-id="ea7b1-134">Network considerations</span></span>
* <span data-ttu-id="ea7b1-135">Hello 電腦上裝載您的用戶端程式，確定 hello 防火牆允許連接埠 1433年上的傳出 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-135">On hello computer that hosts your client program, ensure hello firewall allows outgoing TCP communication on port 1433.</span></span>  <span data-ttu-id="ea7b1-136">詳細資訊： [設定 Azure SQL Database 防火牆](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-136">More information: [Configure an Azure SQL Database firewall](sql-database-configure-firewall-settings.md)</span></span>
* <span data-ttu-id="ea7b1-137">如果您的用戶端會在 Azure 虛擬機器 (VM) 上執行時，用戶端程式會連接 tooSQL 資料庫，您必須開啟 hello VM 上的特定連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-137">If your client program connects tooSQL Database while your client runs on an Azure virtual machine (VM), you must open certain port ranges on hello VM.</span></span> <span data-ttu-id="ea7b1-138">詳細資訊：[針對 ADO.NET 4.5 和 SQL Database 之 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-138">More information: [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)</span></span>
* <span data-ttu-id="ea7b1-139">用戶端連線 tooAzure SQL 資料庫有時會略過 hello proxy，並與 hello 資料庫直接互動。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-139">Client connections tooAzure SQL Database sometimes bypass hello proxy and interact directly with hello database.</span></span> <span data-ttu-id="ea7b1-140">1433 以外的連接埠變得重要。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-140">Ports other than 1433 become important.</span></span> <span data-ttu-id="ea7b1-141">如需詳細資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)和[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)一節。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-141">For more information, [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) and [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

## <a name="data-sharding-with-elastic-scale"></a><span data-ttu-id="ea7b1-142">使用 Elastic Scale 的資料分區化</span><span class="sxs-lookup"><span data-stu-id="ea7b1-142">Data sharding with elastic scale</span></span>
<span data-ttu-id="ea7b1-143">Elastic Scale 簡化 hello 的縮放比例外 （和） 的程序。</span><span class="sxs-lookup"><span data-stu-id="ea7b1-143">Elastic Scale simplifies hello process of scaling out (and in).</span></span> 

* [<span data-ttu-id="ea7b1-144">多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式</span><span class="sxs-lookup"><span data-stu-id="ea7b1-144">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="ea7b1-145">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="ea7b1-145">Data dependent routing</span></span>](sql-database-elastic-scale-data-dependent-routing.md)
* [<span data-ttu-id="ea7b1-146">開始使用 Azure SQL Database Elastic Scale 預覽</span><span class="sxs-lookup"><span data-stu-id="ea7b1-146">Get Started with Azure SQL Database Elastic Scale Preview</span></span>](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a><span data-ttu-id="ea7b1-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea7b1-147">Next steps</span></span>
<span data-ttu-id="ea7b1-148">瀏覽所有 hello [SQL Database 的功能](sql-database-technical-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ea7b1-148">Explore all hello [capabilities of SQL Database](sql-database-technical-overview.md)</span></span>
