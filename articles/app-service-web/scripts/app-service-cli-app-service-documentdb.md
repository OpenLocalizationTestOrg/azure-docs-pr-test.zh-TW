---
title: "CLI 指令碼範例-aaaAzure 連接 web 應用程式 tooCosmos DB |Microsoft 文件"
description: "Azure CLI 指令碼範例-連接 web 應用程式 tooCosmos DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="88ef4-103">連接 web 應用程式 tooCosmos DB</span><span class="sxs-lookup"><span data-stu-id="88ef4-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="88ef4-104">在此案例中，您將學習如何 toocreate Azure Cosmos DB 帳戶和 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88ef4-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="88ef4-105">然後，您將連結 hello Cosmos DB toohello web 應用程式使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="88ef4-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="88ef4-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="88ef4-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="88ef4-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="88ef4-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="88ef4-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="88ef4-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="88ef4-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="88ef4-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="88ef4-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="88ef4-110">Script explanation</span></span>

<span data-ttu-id="88ef4-111">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 Cosmos 資料庫和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="88ef4-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="88ef4-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="88ef4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="88ef4-113">命令</span><span class="sxs-lookup"><span data-stu-id="88ef4-113">Command</span></span> | <span data-ttu-id="88ef4-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="88ef4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88ef4-115">az group create</span><span class="sxs-lookup"><span data-stu-id="88ef4-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="88ef4-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="88ef4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88ef4-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="88ef4-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="88ef4-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="88ef4-118">Creates an App Service plan.</span></span> <span data-ttu-id="88ef4-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="88ef4-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="88ef4-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="88ef4-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="88ef4-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88ef4-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="88ef4-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="88ef4-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="88ef4-123">建立 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="88ef4-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="88ef4-124">這是 hello 資料儲存的位置。</span><span class="sxs-lookup"><span data-stu-id="88ef4-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="88ef4-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="88ef4-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="88ef4-126">Hello 清單 hello 存取金鑰指定的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="88ef4-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="88ef4-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="88ef4-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="88ef4-128">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="88ef4-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="88ef4-129">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="88ef4-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="88ef4-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88ef4-130">Next steps</span></span>

<span data-ttu-id="88ef4-131">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="88ef4-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="88ef4-132">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="88ef4-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
