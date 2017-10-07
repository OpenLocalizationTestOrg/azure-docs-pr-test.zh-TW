---
title: "aaaCreate 連接 tooan Azure 儲存體 Azure 函式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-建立連線 tooan Azure 儲存體 Azure 函式"
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
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="b9559-103">將函式應用程式整合到 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b9559-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="b9559-104">此範例指令碼會建立函數應用程式和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9559-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b9559-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b9559-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b9559-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="b9559-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b9559-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b9559-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b9559-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b9559-108">Sample script</span></span>

<span data-ttu-id="b9559-109">這個範例會建立 Azure 函式應用程式，並將 hello 儲存體連接字串 tooan 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="b9559-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="b9559-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="b9559-110">Clean up deployment</span></span>

<span data-ttu-id="b9559-111">Hello 指令碼範例執行後，使用的 tooremove hello 資源群組，App Service 應用程式，而且所有相關的資源，可以是 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9559-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b9559-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b9559-112">Script explanation</span></span>

<span data-ttu-id="b9559-113">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="b9559-113">This script uses hello following commands.</span></span> <span data-ttu-id="b9559-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b9559-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b9559-115">命令</span><span class="sxs-lookup"><span data-stu-id="b9559-115">Command</span></span> | <span data-ttu-id="b9559-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="b9559-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9559-117">az login</span><span class="sxs-lookup"><span data-stu-id="b9559-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="b9559-118">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b9559-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="b9559-119">az group create</span><span class="sxs-lookup"><span data-stu-id="b9559-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b9559-120">指定位置建立資源群組</span><span class="sxs-lookup"><span data-stu-id="b9559-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="b9559-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="b9559-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="b9559-122">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b9559-122">Create a storage account</span></span> |
| [<span data-ttu-id="b9559-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="b9559-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b9559-124">建立新的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="b9559-124">Create a new function app</span></span> |
| [<span data-ttu-id="b9559-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="b9559-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b9559-126">清除</span><span class="sxs-lookup"><span data-stu-id="b9559-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9559-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9559-127">Next steps</span></span>

<span data-ttu-id="b9559-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b9559-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b9559-129">其他 Azure 函式 CLI 指令碼範例可以在 hello [Azure 函式文件](../functions-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b9559-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
