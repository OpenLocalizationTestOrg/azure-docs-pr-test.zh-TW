---
title: "aaaCreate 連接 tooan Azure Cosmos DB Azure 函式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-建立連線 tooan Azure Cosmos DB Azure 函式"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="889f5-103">建立連接 tooan Azure Cosmos DB Azure 函式</span><span class="sxs-lookup"><span data-stu-id="889f5-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="889f5-104">這個範例指令碼會建立 Azure 函式應用程式，並連接 tooan Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="889f5-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="889f5-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="889f5-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="889f5-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="889f5-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="889f5-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="889f5-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="889f5-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="889f5-108">Sample script</span></span>

<span data-ttu-id="889f5-109">這個範例會建立 Azure 函式應用程式，並將 Cosmos DB 端點和存取金鑰 tooapp 設定。</span><span class="sxs-lookup"><span data-stu-id="889f5-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="889f5-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="889f5-110">Clean up deployment</span></span>

<span data-ttu-id="889f5-111">Hello 指令碼範例執行後，hello 後續命令可以是使用的 tooremove hello 資源群組和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="889f5-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="889f5-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="889f5-112">Script explanation</span></span>

<span data-ttu-id="889f5-113">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="889f5-113">This script uses hello following commands.</span></span> <span data-ttu-id="889f5-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="889f5-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="889f5-115">命令</span><span class="sxs-lookup"><span data-stu-id="889f5-115">Command</span></span> | <span data-ttu-id="889f5-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="889f5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="889f5-117">az login</span><span class="sxs-lookup"><span data-stu-id="889f5-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="889f5-118">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="889f5-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="889f5-119">az group create</span><span class="sxs-lookup"><span data-stu-id="889f5-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="889f5-120">指定位置建立資源群組</span><span class="sxs-lookup"><span data-stu-id="889f5-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="889f5-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="889f5-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="889f5-122">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="889f5-122">Create a storage account</span></span> |
| [<span data-ttu-id="889f5-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="889f5-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="889f5-124">建立新的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="889f5-124">Create a new function app</span></span> |
| [<span data-ttu-id="889f5-125">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="889f5-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="889f5-126">建立 DocumentDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="889f5-126">Create documentdb database</span></span> |
| [<span data-ttu-id="889f5-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="889f5-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="889f5-128">清除</span><span class="sxs-lookup"><span data-stu-id="889f5-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="889f5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="889f5-129">Next steps</span></span>

<span data-ttu-id="889f5-130">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="889f5-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="889f5-131">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="889f5-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




