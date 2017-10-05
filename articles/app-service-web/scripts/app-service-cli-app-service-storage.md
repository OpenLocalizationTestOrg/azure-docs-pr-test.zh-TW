---
title: "Azure CLI 指令碼範例 - 將 Web 應用程式連接至儲存體帳戶 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將 Web 應用程式連接至儲存體帳戶"
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
ms.openlocfilehash: 2520eecf54b77b88d6aa1ba2e538d05e3407f3d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="648ec-103">將 Web 應用程式連接至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="648ec-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="648ec-104">在此案例中，您會學習如何建立 Azure 儲存體帳戶和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="648ec-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="648ec-105">然後，您會使用應用程式設定將儲存體帳戶連結到 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="648ec-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="648ec-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="648ec-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="648ec-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="648ec-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="648ec-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="648ec-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="648ec-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="648ec-109">Sample script</span></span>

<span data-ttu-id="648ec-110">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure 儲存體")]</span><span class="sxs-lookup"><span data-stu-id="648ec-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="648ec-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="648ec-111">Script explanation</span></span>

<span data-ttu-id="648ec-112">此指令碼使用下列命令來建立資源群組、Web 應用程式、儲存體帳戶和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="648ec-112">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="648ec-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="648ec-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="648ec-114">命令</span><span class="sxs-lookup"><span data-stu-id="648ec-114">Command</span></span> | <span data-ttu-id="648ec-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="648ec-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="648ec-116">az group create</span><span class="sxs-lookup"><span data-stu-id="648ec-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="648ec-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="648ec-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="648ec-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="648ec-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="648ec-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="648ec-119">Creates an App Service plan.</span></span> <span data-ttu-id="648ec-120">這就像是 Azure Web 應用程式的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="648ec-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="648ec-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="648ec-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="648ec-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="648ec-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="648ec-123">az storage account create</span><span class="sxs-lookup"><span data-stu-id="648ec-123">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="648ec-124">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="648ec-124">Creates a storage account.</span></span> <span data-ttu-id="648ec-125">這是靜態資產的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="648ec-125">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="648ec-126">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="648ec-126">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="648ec-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="648ec-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="648ec-128">建立或更新 Azure Web 應用程式的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="648ec-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="648ec-129">應用程式設定會顯示為應用程式的環境變數。</span><span class="sxs-lookup"><span data-stu-id="648ec-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="648ec-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="648ec-130">Next steps</span></span>

<span data-ttu-id="648ec-131">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="648ec-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="648ec-132">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="648ec-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
