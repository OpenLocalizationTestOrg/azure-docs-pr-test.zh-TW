---
title: "aaaAzure CLI 指令碼範例的批次中加入的應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 在 Batch 中加入應用程式"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="0d78e-103">新增應用程式 tooAzure 批次使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0d78e-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="0d78e-104">此指令碼示範如何 tooset 組成應用程式適用於 Azure Batch 集區或工作。</span><span class="sxs-lookup"><span data-stu-id="0d78e-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="0d78e-105">tooset 組成應用程式，封裝可執行檔，以及任何相依性，成.zip 檔。</span><span class="sxs-lookup"><span data-stu-id="0d78e-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="0d78e-106">在此範例中的 hello 可執行 zip 檔稱為 ' 我的應用程式-exe.zip'。</span><span class="sxs-lookup"><span data-stu-id="0d78e-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d78e-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d78e-107">Prerequisites</span></span>

- <span data-ttu-id="0d78e-108">安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。</span><span class="sxs-lookup"><span data-stu-id="0d78e-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="0d78e-109">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="0d78e-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="0d78e-110">請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d78e-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0d78e-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0d78e-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="0d78e-112">清除應用程式</span><span class="sxs-lookup"><span data-stu-id="0d78e-112">Clean up application</span></span>

<span data-ttu-id="0d78e-113">執行 hello 上面的範例指令碼之後，執行下列命令 tooremove hello 應用程式和所有其上傳應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="0d78e-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0d78e-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0d78e-114">Script explanation</span></span>

<span data-ttu-id="0d78e-115">應用程式和上傳應用程式套件，此指令碼會使用下列命令 toocreate hello。</span><span class="sxs-lookup"><span data-stu-id="0d78e-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="0d78e-116">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="0d78e-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="0d78e-117">命令</span><span class="sxs-lookup"><span data-stu-id="0d78e-117">Command</span></span> | <span data-ttu-id="0d78e-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="0d78e-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d78e-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="0d78e-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="0d78e-120">建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d78e-120">Creates an application.</span></span>  |
| [<span data-ttu-id="0d78e-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="0d78e-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="0d78e-122">更新應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="0d78e-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="0d78e-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="0d78e-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="0d78e-124">將指定的應用程式封裝 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d78e-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="0d78e-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d78e-125">Next steps</span></span>

<span data-ttu-id="0d78e-126">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0d78e-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0d78e-127">其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="0d78e-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
