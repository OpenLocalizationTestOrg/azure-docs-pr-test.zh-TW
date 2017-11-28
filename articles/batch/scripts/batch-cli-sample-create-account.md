---
title: "CLI 指令碼範例-aaaAzure 建立 Batch 帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Batch 帳戶"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="d90ee-103">以 hello Azure CLI 建立 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="d90ee-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="d90ee-104">此指令碼會建立 Azure Batch 帳戶，並顯示可以查詢及更新的 hello 帳戶方式的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="d90ee-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d90ee-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="d90ee-105">Prerequisites</span></span>

<span data-ttu-id="d90ee-106">安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。</span><span class="sxs-lookup"><span data-stu-id="d90ee-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="d90ee-107">Batch 帳戶範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d90ee-107">Batch account sample script</span></span>

<span data-ttu-id="d90ee-108">當您建立的批次帳戶時，依預設其運算節點會指派內部 hello 批次服務。</span><span class="sxs-lookup"><span data-stu-id="d90ee-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="d90ee-109">配置的運算節點會是主體 tooa 不同的核心配額，可以驗證 hello 帳戶，透過共用金鑰認證或 Azure Active Dirctory 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d90ee-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="d90ee-110">使用使用者訂閱範例指令碼的 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="d90ee-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="d90ee-111">您也可以選擇 toohave 批次在您自己的 Azure 訂用帳戶中建立的計算節點。</span><span class="sxs-lookup"><span data-stu-id="d90ee-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="d90ee-112">帳戶配置的計算節點插入您的訂用帳戶必須透過 Azure Active Directory 權杖驗證配置的 hello 計算節點都會計入您的訂用帳戶配額。</span><span class="sxs-lookup"><span data-stu-id="d90ee-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="d90ee-113">toocreate 在此模式中的帳戶，其中一個金鑰保存庫的參考建立時必須指定 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d90ee-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d90ee-114">清除部署</span><span class="sxs-lookup"><span data-stu-id="d90ee-114">Clean up deployment</span></span>

<span data-ttu-id="d90ee-115">其中一個 hello 上方範例指令碼執行之後，執行下列命令 tooremove hello 的資源群組和所有相關的資源 （包括批次帳戶、 Azure 儲存體帳戶以及 Azure 金鑰保存庫）。</span><span class="sxs-lookup"><span data-stu-id="d90ee-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d90ee-116">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="d90ee-116">Script explanation</span></span>

<span data-ttu-id="d90ee-117">此指令碼會使用下列命令 toocreate 資源群組、 批次帳戶和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="d90ee-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="d90ee-118">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="d90ee-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d90ee-119">命令</span><span class="sxs-lookup"><span data-stu-id="d90ee-119">Command</span></span> | <span data-ttu-id="d90ee-120">注意事項</span><span class="sxs-lookup"><span data-stu-id="d90ee-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d90ee-121">az group create</span><span class="sxs-lookup"><span data-stu-id="d90ee-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d90ee-122">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d90ee-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d90ee-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="d90ee-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="d90ee-124">建立 hello Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d90ee-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="d90ee-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="d90ee-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="d90ee-126">更新 hello 批次帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="d90ee-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="d90ee-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="d90ee-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="d90ee-128">指定批次帳戶的 hello 的擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d90ee-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="d90ee-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="d90ee-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="d90ee-130">擷取 hello 便捷鍵的 hello 指定批次帳戶。</span><span class="sxs-lookup"><span data-stu-id="d90ee-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="d90ee-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d90ee-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="d90ee-132">驗證指定的 hello 批次帳戶進一步 CLI 互動。</span><span class="sxs-lookup"><span data-stu-id="d90ee-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="d90ee-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="d90ee-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d90ee-134">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d90ee-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="d90ee-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="d90ee-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="d90ee-136">建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="d90ee-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="d90ee-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="d90ee-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="d90ee-138">更新 hello 指定的金鑰保存庫的 hello 安全性的原則。</span><span class="sxs-lookup"><span data-stu-id="d90ee-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="d90ee-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="d90ee-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d90ee-140">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="d90ee-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d90ee-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d90ee-141">Next steps</span></span>

<span data-ttu-id="d90ee-142">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d90ee-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d90ee-143">其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d90ee-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
