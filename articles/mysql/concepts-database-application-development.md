---
title: "Azure 資料庫的 MySQL aaaDatabase 應用程式開發概觀 |Microsoft 文件"
description: "引進了用於 MySQL 撰寫應用程式程式碼 tooconnect tooAzure 資料庫時，開發人員應該遵循的設計考量"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="82c9a-103">適用於 MySQL 的 Azure 資料庫的應用程式開發概觀</span><span class="sxs-lookup"><span data-stu-id="82c9a-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="82c9a-104">這篇文章討論的 MySQL 撰寫應用程式程式碼 tooconnect tooAzure 資料庫時，開發人員應該遵循的設計考量</span><span class="sxs-lookup"><span data-stu-id="82c9a-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="82c9a-105">教學課程顯示如何 toocreate 伺服器，建立伺服器型防火牆，檢視伺服器屬性、 建立資料庫、 連線，並使用 workbench 和 mysql.exe 查詢，請參閱[設計您的第一個 Azure MySQL 資料庫](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="82c9a-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="82c9a-106">語言和平台</span><span class="sxs-lookup"><span data-stu-id="82c9a-106">Language and platform</span></span>
<span data-ttu-id="82c9a-107">有一些程式碼範例可供各種程式設計語言和平台使用。</span><span class="sxs-lookup"><span data-stu-id="82c9a-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="82c9a-108">您可以找到連結 toohello 程式碼範例：[連接程式庫用於 MySQL 的 tooconnect tooAzure 資料庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="82c9a-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="82c9a-109">工具</span><span class="sxs-lookup"><span data-stu-id="82c9a-109">Tools</span></span>
<span data-ttu-id="82c9a-110">Azure 的 MySQL 資料庫使用 hello MySQL community 版本，與 MySQL 常見的管理工具 Workbench 或 MySQL 公用程式，例如 mysql.exe，例如相容[phpMyAdmin](https://www.phpmyadmin.net/)， [Navicat](https://www.navicat.com/products/navicat-for-mysql)，和其他人。</span><span class="sxs-lookup"><span data-stu-id="82c9a-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="82c9a-111">您也可以使用 hello Azure 入口網站、 Azure CLI 和 REST Api toointeract 與 hello 資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="82c9a-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="82c9a-112">資源限制</span><span class="sxs-lookup"><span data-stu-id="82c9a-112">Resource limitations</span></span>
<span data-ttu-id="82c9a-113">Azure 的 MySQL 資料庫管理 hello 資源可用 tooa 伺服器使用兩個不同的機制：</span><span class="sxs-lookup"><span data-stu-id="82c9a-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="82c9a-114">資源管理</span><span class="sxs-lookup"><span data-stu-id="82c9a-114">Resources Governance</span></span> 
- <span data-ttu-id="82c9a-115">強制執行限制。</span><span class="sxs-lookup"><span data-stu-id="82c9a-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="82c9a-116">安全性</span><span class="sxs-lookup"><span data-stu-id="82c9a-116">Security</span></span>
<span data-ttu-id="82c9a-117">Azure MySQL 資料庫提供資源，以便在 MySQL 資料庫上限制存取、保護資料、設定使用者和角色，以及監視活動。</span><span class="sxs-lookup"><span data-stu-id="82c9a-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="82c9a-118">驗證</span><span class="sxs-lookup"><span data-stu-id="82c9a-118">Authentication</span></span>
<span data-ttu-id="82c9a-119">Azure MySQL 資料庫支援適用於使用者與登入的伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="82c9a-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="82c9a-120">復原功能</span><span class="sxs-lookup"><span data-stu-id="82c9a-120">Resiliency</span></span>
<span data-ttu-id="82c9a-121">當連線 tooMySQL 資料庫時，就會發生暫時性的錯誤時，您的程式碼應該重試 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="82c9a-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="82c9a-122">我們建議您使用 hello 重試邏輯使用邏輯、 功能，讓它不會不會使不勝負荷 hello SQL Database 與多個用戶端重試一次同時。</span><span class="sxs-lookup"><span data-stu-id="82c9a-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="82c9a-123">程式碼範例： 取得程式碼範例將示範中，然後重試邏輯，請參閱您選擇在 hello 語言的範例：[連接程式庫用於 MySQL 的 tooconnect tooAzure 資料庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="82c9a-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="82c9a-124">管理連接</span><span class="sxs-lookup"><span data-stu-id="82c9a-124">Managing Connections</span></span>
<span data-ttu-id="82c9a-125">資料庫連線是有限的資源，因此我們建議您合理使用的連接存取您的 MySQL 資料庫時 tooachieve 更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="82c9a-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="82c9a-126">存取 hello 資料庫使用連接共用或持續連線。</span><span class="sxs-lookup"><span data-stu-id="82c9a-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="82c9a-127">使用簡短的連接生命週期的 access hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="82c9a-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="82c9a-128">Hello hello 連線嘗試、 toocatch 失敗，因為 tooconcurrent 連接點的應用程式中使用重試邏輯已達到允許的 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="82c9a-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="82c9a-129">在 [hello 重試邏輯、 設定短暫的延遲，，然後等待 hello 其他連接嘗試之前的隨機時間點。</span><span class="sxs-lookup"><span data-stu-id="82c9a-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
