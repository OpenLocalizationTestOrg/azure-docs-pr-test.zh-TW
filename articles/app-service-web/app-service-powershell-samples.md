---
title: "Azure PowerShell 範例 - App Service | Microsoft Docs"
description: "Azure PowerShell 範例 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="a7350-103">Azure PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="a7350-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="a7350-104">下表包含使用 Azure PowerShell 所建置的 Bash 指令碼連結。</span><span class="sxs-lookup"><span data-stu-id="a7350-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="a7350-105">**建立應用程式**</span><span class="sxs-lookup"><span data-stu-id="a7350-105">**Create app**</span></span>||
| [<span data-ttu-id="a7350-106">建立可從 GitHub 部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-107">建立會從 GitHub 提取程式碼的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7350-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="a7350-108">建立可從 GitHub 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-109">建立可從 GitHub 連續部署程式碼的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7350-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="a7350-110">建立 Web 應用程式並使用 FTP 部署程式碼</span><span class="sxs-lookup"><span data-stu-id="a7350-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-111">建立 Azure Web 應用程式，並使用 FTP 從本機目錄上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="a7350-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="a7350-112">建立 Web 應用程式並從本機 Git 存放庫部署程式碼</span><span class="sxs-lookup"><span data-stu-id="a7350-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-113">建立 Azure Web 應用程式並設定從本機 Git 存放庫推送程式碼的作業。</span><span class="sxs-lookup"><span data-stu-id="a7350-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="a7350-114">建立 Web 應用程式並將程式碼部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="a7350-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-115">建立具有部署位置以供放置預備程式碼變更的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7350-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="a7350-116">**設定應用程式**</span><span class="sxs-lookup"><span data-stu-id="a7350-116">**Configure app**</span></span>||
| [<span data-ttu-id="a7350-117">將自訂網域對應至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-118">建立 Azure Web 應用程式，並向它對應自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a7350-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="a7350-119">將自訂 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-120">建立 Azure Web 應用程式，並將自訂網域名稱的 SSL 憑證加以繫結。</span><span class="sxs-lookup"><span data-stu-id="a7350-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="a7350-121">**調整應用程式**</span><span class="sxs-lookup"><span data-stu-id="a7350-121">**Scale app**</span></span>||
| [<span data-ttu-id="a7350-122">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-123">建立 Azure Web 應用程式，並將它調整到 2 個執行個體中。</span><span class="sxs-lookup"><span data-stu-id="a7350-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="a7350-124">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="a7350-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-125">在兩個不同的地理區域中建立兩個 Azure Web 應用程式，並使用 Azure 流量管理員讓它們可透過單一端點來使用。</span><span class="sxs-lookup"><span data-stu-id="a7350-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="a7350-126">**將應用程式連線至資源**</span><span class="sxs-lookup"><span data-stu-id="a7350-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="a7350-127">將 Web 應用程式連線至 SQL Database</span><span class="sxs-lookup"><span data-stu-id="a7350-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-128">建立 Azure Web 應用程式和 SQL Database，然後將資料庫連接字串新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a7350-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="a7350-129">將 Web 應用程式連線至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a7350-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a7350-130">建立 Azure Web 應用程式和儲存體帳戶，然後將儲存體連接字串新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a7350-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="a7350-131">**監視應用程式**</span><span class="sxs-lookup"><span data-stu-id="a7350-131">**Monitor app**</span></span>||
| [<span data-ttu-id="a7350-132">使用 Web 伺服器記錄監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7350-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a7350-133">建立 Azure Web 應用程式、為其啟用記錄，並將記錄下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="a7350-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
