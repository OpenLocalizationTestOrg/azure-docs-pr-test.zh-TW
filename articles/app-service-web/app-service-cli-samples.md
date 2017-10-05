---
title: "Azure CLI 範例 - App Service | Microsoft Docs"
description: "Azure CLI 範例 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 6718694af487929d193dae54ecb2d85ece64887a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cli-samples"></a><span data-ttu-id="ff7e0-103">Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="ff7e0-103">Azure CLI Samples</span></span>

<span data-ttu-id="ff7e0-104">下表包含使用 Azure CLI 所建置之 Bash 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="ff7e0-105">**建立應用程式**</span><span class="sxs-lookup"><span data-stu-id="ff7e0-105">**Create app**</span></span>||
| [<span data-ttu-id="ff7e0-106">建立 Web 應用程式並從 從 GitHub 部署程式碼</span><span class="sxs-lookup"><span data-stu-id="ff7e0-106">Create a web app and deploy code from GitHub</span></span>](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-107">建立 Azure Web 應用程式和從公用 GitHub 存放庫部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-107">Creates an Azure web app and deploys code from a public GitHub repository.</span></span> |
| [<span data-ttu-id="ff7e0-108">建立可從 GitHub 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-109">建立可從您擁有的 GitHub 存放庫連續發佈的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-109">Creates an Azure web app with continuous publishing from a GitHub repository you own.</span></span> |
| [<span data-ttu-id="ff7e0-110">建立 Web 應用程式並從本機 Git 存放庫部署程式碼</span><span class="sxs-lookup"><span data-stu-id="ff7e0-110">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-111">建立 Azure Web 應用程式並設定從本機 Git 存放庫推送程式碼的作業。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-111">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="ff7e0-112">建立 Web 應用程式並將程式碼部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="ff7e0-112">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-113">建立具有部署位置以供放置預備程式碼變更的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-113">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
| [<span data-ttu-id="ff7e0-114">在 Docker 容器中建立 ASP.NET 核心 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-114">Create an ASP.NET Core web app in a Docker container</span></span>](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-115">在 Linux 上建立 Azure Web 應用程式，並從 Docker Hub 載入 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-115">Creates an Azure web app on Linux and loads a Docker image from Docker Hub.</span></span> |
|<span data-ttu-id="ff7e0-116">**設定應用程式**</span><span class="sxs-lookup"><span data-stu-id="ff7e0-116">**Configure app**</span></span>||
| [<span data-ttu-id="ff7e0-117">將自訂網域對應至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-117">Map a custom domain to a web app</span></span>](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-118">建立 Azure Web 應用程式，並向它對應自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="ff7e0-119">將自訂 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-120">建立 Azure Web 應用程式，並將自訂網域名稱的 SSL 憑證加以繫結。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="ff7e0-121">**調整應用程式**</span><span class="sxs-lookup"><span data-stu-id="ff7e0-121">**Scale app**</span></span>||
| [<span data-ttu-id="ff7e0-122">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-122">Scale a web app manually</span></span>](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-123">建立 Azure Web 應用程式，並將它調整到 2 個執行個體中。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="ff7e0-124">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="ff7e0-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-125">在兩個不同的地理區域中建立兩個 Azure Web 應用程式，並使用 Azure 流量管理員讓它們可透過單一端點來使用。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="ff7e0-126">**將應用程式連線至資源**</span><span class="sxs-lookup"><span data-stu-id="ff7e0-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="ff7e0-127">將 Web 應用程式連線至 SQL Database</span><span class="sxs-lookup"><span data-stu-id="ff7e0-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-128">建立 Azure Web 應用程式和 SQL Database，然後將資料庫連接字串新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="ff7e0-129">將 Web 應用程式連線至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ff7e0-129">Connect a web app to a storage account</span></span>](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="ff7e0-130">建立 Azure Web 應用程式和儲存體帳戶，然後將儲存體連接字串新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
| [<span data-ttu-id="ff7e0-131">將 Web 應用程式連線至 redis 快取</span><span class="sxs-lookup"><span data-stu-id="ff7e0-131">Connect a web app to a redis cache</span></span>](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-132">建立 Azure Web 應用程式和 redis 快取，然後將 redis 連線詳細資料新增至應用程式設定。)</span><span class="sxs-lookup"><span data-stu-id="ff7e0-132">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.)</span></span> |
| [<span data-ttu-id="ff7e0-133">將 Web 應用程式連線至 Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ff7e0-133">Connect a web app to Cosmos DB</span></span>](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-134">建立 Azure Web 應用程式和 Cosmos DB，然後將 Cosmos DB 連線詳細資料新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-134">Creates an Azure web app and a Cosmos DB, then adds the Cosmos DB connection details to the app settings.</span></span> |
|<span data-ttu-id="ff7e0-135">**監視應用程式**</span><span class="sxs-lookup"><span data-stu-id="ff7e0-135">**Monitor app**</span></span>||
| [<span data-ttu-id="ff7e0-136">使用 Web 伺服器記錄監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff7e0-136">Monitor a web app with web server logs</span></span>](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="ff7e0-137">建立 Azure Web 應用程式、為其啟用記錄，並將記錄下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="ff7e0-137">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |