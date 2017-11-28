---
title: "CLI 指令碼範例-aaaAzure 連接 web 應用程式 tooa 儲存體帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例-連接 web 應用程式 tooa 儲存體帳戶"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="bb519-103">連接 web 應用程式 tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bb519-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="bb519-104">在此案例中，您將學習如何 toocreate Azure 儲存體帳戶和 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb519-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="bb519-105">然後，您將連結 hello 儲存體帳戶 toohello web 應用程式使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="bb519-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb519-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bb519-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb519-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="bb519-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bb519-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="bb519-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="bb519-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bb519-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bb519-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bb519-110">Script explanation</span></span>

<span data-ttu-id="bb519-111">此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 儲存體帳戶和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="bb519-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="bb519-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="bb519-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bb519-113">命令</span><span class="sxs-lookup"><span data-stu-id="bb519-113">Command</span></span> | <span data-ttu-id="bb519-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="bb519-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb519-115">az group create</span><span class="sxs-lookup"><span data-stu-id="bb519-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bb519-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bb519-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bb519-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="bb519-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bb519-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="bb519-118">Creates an App Service plan.</span></span> <span data-ttu-id="bb519-119">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="bb519-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="bb519-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="bb519-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bb519-121">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb519-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bb519-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="bb519-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="bb519-123">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb519-123">Creates a storage account.</span></span> <span data-ttu-id="bb519-124">這是要儲存 hello 靜態資產。</span><span class="sxs-lookup"><span data-stu-id="bb519-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="bb519-125">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="bb519-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="bb519-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="bb519-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="bb519-127">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="bb519-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="bb519-128">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="bb519-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb519-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb519-129">Next steps</span></span>

<span data-ttu-id="bb519-130">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bb519-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bb519-131">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="bb519-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
