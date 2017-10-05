---
title: "Azure CLI 指令碼範例 - 在 Batch 中加入應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="11643-103">使用 Azure CLI 將應用程式加入 Azure Batch</span><span class="sxs-lookup"><span data-stu-id="11643-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="11643-104">此指令碼示範如何設定應用程式，以搭配 Azure Batch 集區或作業使用。</span><span class="sxs-lookup"><span data-stu-id="11643-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="11643-105">設定應用程式，將可執行檔及任何相依性封裝到 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="11643-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="11643-106">在此範例中，可執行的 zip 檔案稱為 'my-application-exe.zip'。</span><span class="sxs-lookup"><span data-stu-id="11643-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11643-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="11643-107">Prerequisites</span></span>

- <span data-ttu-id="11643-108">如果您尚未安裝 Azure CLI，請使用 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)中所提供的指示來安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="11643-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="11643-109">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="11643-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="11643-110">如需用以建立帳戶的指令碼範例，請參閱[使用 Azure CLI 建立 Batch 帳戶](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)。</span><span class="sxs-lookup"><span data-stu-id="11643-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="11643-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="11643-111">Sample script</span></span>

<span data-ttu-id="11643-112">[!code-azurecli[主要](../../../cli_scripts/batch/add-application/add-application.sh "加入應用程式")]</span><span class="sxs-lookup"><span data-stu-id="11643-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="11643-113">清除應用程式</span><span class="sxs-lookup"><span data-stu-id="11643-113">Clean up application</span></span>

<span data-ttu-id="11643-114">執行上述範例指令碼之後，請執行下列命令以移除應用程式和其所有已上傳的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="11643-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="11643-115">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="11643-115">Script explanation</span></span>

<span data-ttu-id="11643-116">這個指令碼使用下列命令來建立應用程式和上傳應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="11643-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="11643-117">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="11643-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="11643-118">命令</span><span class="sxs-lookup"><span data-stu-id="11643-118">Command</span></span> | <span data-ttu-id="11643-119">注意事項</span><span class="sxs-lookup"><span data-stu-id="11643-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11643-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="11643-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="11643-121">建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="11643-121">Creates an application.</span></span>  |
| [<span data-ttu-id="11643-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="11643-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="11643-123">更新應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="11643-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="11643-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="11643-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="11643-125">將應用程式封裝加入指定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11643-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="11643-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11643-126">Next steps</span></span>

<span data-ttu-id="11643-127">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="11643-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="11643-128">您可以在 [Azure Batch CLI 文件](../batch-cli-samples.md)中找到其他的 Batch CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="11643-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
