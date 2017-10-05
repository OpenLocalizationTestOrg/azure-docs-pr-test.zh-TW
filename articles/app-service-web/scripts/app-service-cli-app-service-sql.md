---
title: "Azure CLI 指令碼範例 - 將 Web 應用程式連接至 SQL Database | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將 Web 應用程式連接至 SQL Database"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="8b6ce-103">將 Web 應用程式連接至 SQL Database</span><span class="sxs-lookup"><span data-stu-id="8b6ce-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="8b6ce-104">在此案例中，您會學習如何建立 Azure SQL Database 和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="8b6ce-105">然後，您會使用應用程式設定將 SQL Database 連結到 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b6ce-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8b6ce-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="8b6ce-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8b6ce-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8b6ce-109">Sample script</span></span>

<span data-ttu-id="8b6ce-110">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="8b6ce-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8b6ce-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8b6ce-111">Script explanation</span></span>

<span data-ttu-id="8b6ce-112">此指令碼使用下列命令來建立資源群組、Web 應用程式、SQL Database 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="8b6ce-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8b6ce-114">命令</span><span class="sxs-lookup"><span data-stu-id="8b6ce-114">Command</span></span> | <span data-ttu-id="8b6ce-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b6ce-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8b6ce-116">az group create</span><span class="sxs-lookup"><span data-stu-id="8b6ce-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8b6ce-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8b6ce-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8b6ce-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8b6ce-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-119">Creates an App Service plan.</span></span> <span data-ttu-id="8b6ce-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8b6ce-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="8b6ce-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8b6ce-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8b6ce-123">az sql server create</span><span class="sxs-lookup"><span data-stu-id="8b6ce-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="8b6ce-124">建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="8b6ce-125">az sql db create</span><span class="sxs-lookup"><span data-stu-id="8b6ce-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="8b6ce-126">對 SQL Database 伺服器建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="8b6ce-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="8b6ce-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="8b6ce-128">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="8b6ce-129">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8b6ce-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b6ce-130">Next steps</span></span>

<span data-ttu-id="8b6ce-131">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8b6ce-132">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="8b6ce-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
