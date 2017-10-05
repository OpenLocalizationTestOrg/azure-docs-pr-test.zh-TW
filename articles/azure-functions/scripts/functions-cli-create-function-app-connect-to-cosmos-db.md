---
title: "建立連線至 Azure Cosmos DB 的 Azure 函式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立連線至 Azure Cosmos DB 的 Azure 函式"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="b7fa4-103">建立連線至 Azure Cosmos DB 的 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="b7fa4-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="b7fa4-104">此範例指令碼建立連線至 Azure Cosmos DB 資料庫的 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b7fa4-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b7fa4-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="b7fa4-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b7fa4-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b7fa4-108">Sample script</span></span>

<span data-ttu-id="b7fa4-109">這個範例會建立 Azure 函數應用程式，並在應用程式設定中新增 Cosmos DB 端點和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="b7fa4-110">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "建立連線至 Azure Cosmos DB 的 Azure 函式")]</span><span class="sxs-lookup"><span data-stu-id="b7fa4-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b7fa4-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="b7fa4-111">Clean up deployment</span></span>

<span data-ttu-id="b7fa4-112">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b7fa4-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b7fa4-113">Script explanation</span></span>

<span data-ttu-id="b7fa4-114">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-114">This script uses the following commands.</span></span> <span data-ttu-id="b7fa4-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b7fa4-116">命令</span><span class="sxs-lookup"><span data-stu-id="b7fa4-116">Command</span></span> | <span data-ttu-id="b7fa4-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="b7fa4-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b7fa4-118">az login</span><span class="sxs-lookup"><span data-stu-id="b7fa4-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="b7fa4-119">登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-119">Login to Azure.</span></span> |
| [<span data-ttu-id="b7fa4-120">az group create</span><span class="sxs-lookup"><span data-stu-id="b7fa4-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b7fa4-121">指定位置建立資源群組</span><span class="sxs-lookup"><span data-stu-id="b7fa4-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="b7fa4-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="b7fa4-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="b7fa4-123">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b7fa4-123">Create a storage account</span></span> |
| [<span data-ttu-id="b7fa4-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="b7fa4-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b7fa4-125">建立新的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="b7fa4-125">Create a new function app</span></span> |
| [<span data-ttu-id="b7fa4-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="b7fa4-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="b7fa4-127">建立 DocumentDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="b7fa4-127">Create documentdb database</span></span> |
| [<span data-ttu-id="b7fa4-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="b7fa4-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b7fa4-129">清除</span><span class="sxs-lookup"><span data-stu-id="b7fa4-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b7fa4-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7fa4-130">Next steps</span></span>

<span data-ttu-id="b7fa4-131">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b7fa4-132">您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b7fa4-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




