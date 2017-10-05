---
title: "建立連線至 Azure 儲存體的 Azure 函式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立連線至 Azure 儲存體的 Azure 函式"
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
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="f7fe8-103">將函式應用程式整合到 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f7fe8-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="f7fe8-104">此範例指令碼會建立函數應用程式和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f7fe8-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f7fe8-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f7fe8-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f7fe8-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f7fe8-108">Sample script</span></span>

<span data-ttu-id="f7fe8-109">此範例會建立 Azure 函數應用程式，然後將儲存體連接字串新增至應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="f7fe8-110">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "將函式應用程式整合到 Azure 儲存體帳戶")]</span><span class="sxs-lookup"><span data-stu-id="f7fe8-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="f7fe8-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="f7fe8-111">Clean up deployment</span></span>

<span data-ttu-id="f7fe8-112">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、App Service 應用程式和所有相關資源：</span><span class="sxs-lookup"><span data-stu-id="f7fe8-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f7fe8-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f7fe8-113">Script explanation</span></span>

<span data-ttu-id="f7fe8-114">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-114">This script uses the following commands.</span></span> <span data-ttu-id="f7fe8-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f7fe8-116">命令</span><span class="sxs-lookup"><span data-stu-id="f7fe8-116">Command</span></span> | <span data-ttu-id="f7fe8-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="f7fe8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7fe8-118">az login</span><span class="sxs-lookup"><span data-stu-id="f7fe8-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="f7fe8-119">登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-119">Login to Azure.</span></span> |
| [<span data-ttu-id="f7fe8-120">az group create</span><span class="sxs-lookup"><span data-stu-id="f7fe8-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f7fe8-121">指定位置建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f7fe8-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="f7fe8-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f7fe8-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="f7fe8-123">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f7fe8-123">Create a storage account</span></span> |
| [<span data-ttu-id="f7fe8-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f7fe8-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="f7fe8-125">建立新的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="f7fe8-125">Create a new function app</span></span> |
| [<span data-ttu-id="f7fe8-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="f7fe8-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f7fe8-127">清除</span><span class="sxs-lookup"><span data-stu-id="f7fe8-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f7fe8-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7fe8-128">Next steps</span></span>

<span data-ttu-id="f7fe8-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f7fe8-130">您可以在 [Azure Functions 文件](../functions-cli-samples.md)中找到其他 Azure Functions CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="f7fe8-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
