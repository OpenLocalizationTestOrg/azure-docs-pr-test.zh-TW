---
title: "CLI 指令碼範例-aaaAzure 連接 web 應用程式 tooa SQL 資料庫 |Microsoft 文件"
description: "Azure CLI 指令碼範例-連接 web 應用程式 tooa SQL 資料庫"
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
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="83d7c-103">連接 web 應用程式 tooa SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="83d7c-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="83d7c-104">在此案例中，您將學習如何 toocreate Azure SQL database 和 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="83d7c-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="83d7c-105">然後，您將連結 hello SQL 資料庫 toohello web 應用程式使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="83d7c-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="83d7c-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="83d7c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="83d7c-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="83d7c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="83d7c-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="83d7c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="83d7c-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="83d7c-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="83d7c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="83d7c-110">Script explanation</span></span>

<span data-ttu-id="83d7c-111">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 SQL 資料庫和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="83d7c-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="83d7c-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="83d7c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="83d7c-113">命令</span><span class="sxs-lookup"><span data-stu-id="83d7c-113">Command</span></span> | <span data-ttu-id="83d7c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="83d7c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="83d7c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="83d7c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="83d7c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="83d7c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="83d7c-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="83d7c-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="83d7c-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="83d7c-118">Creates an App Service plan.</span></span> <span data-ttu-id="83d7c-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="83d7c-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="83d7c-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="83d7c-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="83d7c-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="83d7c-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="83d7c-122">az sql server create</span><span class="sxs-lookup"><span data-stu-id="83d7c-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="83d7c-123">建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="83d7c-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="83d7c-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="83d7c-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="83d7c-125">以 hello SQL 資料庫伺服器建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="83d7c-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="83d7c-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="83d7c-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="83d7c-127">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="83d7c-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="83d7c-128">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="83d7c-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="83d7c-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83d7c-129">Next steps</span></span>

<span data-ttu-id="83d7c-130">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="83d7c-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="83d7c-131">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="83d7c-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
