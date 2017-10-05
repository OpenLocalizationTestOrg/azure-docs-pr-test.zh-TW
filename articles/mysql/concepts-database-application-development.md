---
title: "適用於 MySQL 的 Azure 資料庫的資料庫應用程式開發概觀 | Microsoft Docs"
description: "介紹開發人員在撰寫應用程式程式碼以連接到適用於 MySQL 的 Azure 資料庫時所應遵循的設計考量"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="f67b8-103">適用於 MySQL 的 Azure 資料庫的應用程式開發概觀</span><span class="sxs-lookup"><span data-stu-id="f67b8-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="f67b8-104">本文討論開發人員在撰寫應用程式程式碼以連接到適用於 MySQL 的 Azure 資料庫時所應遵循的設計考量</span><span class="sxs-lookup"><span data-stu-id="f67b8-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="f67b8-105">如需示範如何建立伺服器、建立伺服器型防火牆、檢視伺服器屬性、建立資料庫、使用 Workbench 和 mysql.exe 進行連接和查詢的教學課程，請參閱[設計您的第一個 Azure MySQL 資料庫](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f67b8-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="f67b8-106">語言和平台</span><span class="sxs-lookup"><span data-stu-id="f67b8-106">Language and platform</span></span>
<span data-ttu-id="f67b8-107">有一些程式碼範例可供各種程式設計語言和平台使用。</span><span class="sxs-lookup"><span data-stu-id="f67b8-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="f67b8-108">您可以在下列文章中找到程式碼範例的連結：[用來連接到適用於 MySQL 的 Azure 資料庫的連線庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="f67b8-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="f67b8-109">工具</span><span class="sxs-lookup"><span data-stu-id="f67b8-109">Tools</span></span>
<span data-ttu-id="f67b8-110">適用於 MySQL 的 Azure 資料庫會使用 MySQL 社群版本，此版本可與 MySQL 一般管理工具相容，例如 Workbench 或 MySQL 公用程式 (例如 mysql.exe、[phpMyAdmin](https://www.phpmyadmin.net/)、[Navicat](https://www.navicat.com/products/navicat-for-mysql) 等)。</span><span class="sxs-lookup"><span data-stu-id="f67b8-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="f67b8-111">您也可以使用 Azure 入口網站、Azure CLI 和 REST API，來與資料庫服務互動。</span><span class="sxs-lookup"><span data-stu-id="f67b8-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="f67b8-112">資源限制</span><span class="sxs-lookup"><span data-stu-id="f67b8-112">Resource limitations</span></span>
<span data-ttu-id="f67b8-113">Azure MySQL 資料庫會使用兩個種不同機制來管理可供伺服器使用的資源：</span><span class="sxs-lookup"><span data-stu-id="f67b8-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="f67b8-114">資源管理</span><span class="sxs-lookup"><span data-stu-id="f67b8-114">Resources Governance</span></span> 
- <span data-ttu-id="f67b8-115">強制執行限制。</span><span class="sxs-lookup"><span data-stu-id="f67b8-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="f67b8-116">安全性</span><span class="sxs-lookup"><span data-stu-id="f67b8-116">Security</span></span>
<span data-ttu-id="f67b8-117">Azure MySQL 資料庫提供資源，以便在 MySQL 資料庫上限制存取、保護資料、設定使用者和角色，以及監視活動。</span><span class="sxs-lookup"><span data-stu-id="f67b8-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="f67b8-118">驗證</span><span class="sxs-lookup"><span data-stu-id="f67b8-118">Authentication</span></span>
<span data-ttu-id="f67b8-119">Azure MySQL 資料庫支援適用於使用者與登入的伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="f67b8-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="f67b8-120">復原功能</span><span class="sxs-lookup"><span data-stu-id="f67b8-120">Resiliency</span></span>
<span data-ttu-id="f67b8-121">當連接到 MySQL 資料庫發生暫時性錯誤時，您的程式碼應該重試呼叫。</span><span class="sxs-lookup"><span data-stu-id="f67b8-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="f67b8-122">我們建議重試邏輯使用後端停止邏輯，如此它就不會同時重試多個用戶端而讓 SQL Database 超過負荷。</span><span class="sxs-lookup"><span data-stu-id="f67b8-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="f67b8-123">程式碼範例︰如需示範重試邏輯的程式碼範例，請參閱以下文章中您所選擇語言的範例︰[用來連接到適用於 MySQL 的 Azure 資料庫的連線庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="f67b8-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="f67b8-124">管理連接</span><span class="sxs-lookup"><span data-stu-id="f67b8-124">Managing Connections</span></span>
<span data-ttu-id="f67b8-125">資料庫連接是一項有限的資源，因此我們建議在存取您的 MySQL 資料庫時合理地使用連接，以達到更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="f67b8-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="f67b8-126">使用連接共用或持續性連接來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="f67b8-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="f67b8-127">使用簡短的連接存留時間範圍來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="f67b8-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="f67b8-128">在嘗試連接期間，於您的應用程式中使用重試邏輯，會因為並行連接數已達到允許的最大值而導致失敗。</span><span class="sxs-lookup"><span data-stu-id="f67b8-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="f67b8-129">在重試邏輯中，設定短暫的延遲，接著等待一段隨機的時間，然後再嘗試其他連接。</span><span class="sxs-lookup"><span data-stu-id="f67b8-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>