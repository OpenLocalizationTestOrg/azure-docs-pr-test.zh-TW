---
title: "Azure CLI 指令碼範例 - 建立 Batch 帳戶 | Microsoft Docs"
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
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="dd5a8-103">使用 Azure CLI 建立 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="dd5a8-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="dd5a8-104">此指令碼會建立 Azure Batch 帳戶，並顯示各種可以查詢和更新的帳戶屬性。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd5a8-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="dd5a8-105">Prerequisites</span></span>

<span data-ttu-id="dd5a8-106">如果您尚未安裝 Azure CLI，請使用 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)中所提供的指示來安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="dd5a8-107">Batch 帳戶範例指令碼</span><span class="sxs-lookup"><span data-stu-id="dd5a8-107">Batch account sample script</span></span>

<span data-ttu-id="dd5a8-108">當您建立 Batch 帳戶時，根據預設，其計算節點是由 Batch 服務在內部指派。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="dd5a8-109">配置的計算節點將受個別的核心配額限制，帳戶可透過共用金鑰認證或 Azure Active Dirctory 權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="dd5a8-110">[!code-azurecli[主要](../../../cli_scripts/batch/create-account/create-account.sh "建立帳戶")]</span><span class="sxs-lookup"><span data-stu-id="dd5a8-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="dd5a8-111">使用使用者訂閱範例指令碼的 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="dd5a8-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="dd5a8-112">您也可以選擇讓 Batch 在您自己的 Azure 訂用帳戶中建立其計算節點。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="dd5a8-113">將計算節點配置到您的訂用帳戶的帳戶必須透過 Azure Active Directory 權杖驗證，配置的計算節點將計入您的訂用帳戶配額。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="dd5a8-114">若要在此模式建立帳戶，使用者必須在建立帳戶時指定 Key Vault 參考。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="dd5a8-115">[!code-azurecli[主要](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "使用使用者訂用帳戶建立帳戶")]</span><span class="sxs-lookup"><span data-stu-id="dd5a8-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dd5a8-116">清除部署</span><span class="sxs-lookup"><span data-stu-id="dd5a8-116">Clean up deployment</span></span>

<span data-ttu-id="dd5a8-117">執行上述範例指令碼之後，請執行下列命令以移除資源群組和所有相關資源 (包括 Batch 帳戶、Azure 儲存體帳戶和 Azure Key Vault)。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dd5a8-118">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="dd5a8-118">Script explanation</span></span>

<span data-ttu-id="dd5a8-119">此指令碼使用下列命令來建立資源群組、Batch 帳戶和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="dd5a8-120">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="dd5a8-121">命令</span><span class="sxs-lookup"><span data-stu-id="dd5a8-121">Command</span></span> | <span data-ttu-id="dd5a8-122">注意事項</span><span class="sxs-lookup"><span data-stu-id="dd5a8-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dd5a8-123">az group create</span><span class="sxs-lookup"><span data-stu-id="dd5a8-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dd5a8-124">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dd5a8-125">az batch account create</span><span class="sxs-lookup"><span data-stu-id="dd5a8-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="dd5a8-126">建立 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="dd5a8-127">az batch account set</span><span class="sxs-lookup"><span data-stu-id="dd5a8-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="dd5a8-128">更新 Batch 帳戶的屬性。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="dd5a8-129">az batch account show</span><span class="sxs-lookup"><span data-stu-id="dd5a8-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="dd5a8-130">擷取指定的 Batch 帳戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="dd5a8-131">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="dd5a8-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="dd5a8-132">擷取指定的 Batch 帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="dd5a8-133">az batch account login</span><span class="sxs-lookup"><span data-stu-id="dd5a8-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="dd5a8-134">對指定的 Batch 帳戶驗證以進行進一步的 CLI 互動。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="dd5a8-135">az storage account create</span><span class="sxs-lookup"><span data-stu-id="dd5a8-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="dd5a8-136">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="dd5a8-137">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="dd5a8-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="dd5a8-138">建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="dd5a8-139">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="dd5a8-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="dd5a8-140">更新指定的 Key Vault 的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="dd5a8-141">az group delete</span><span class="sxs-lookup"><span data-stu-id="dd5a8-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="dd5a8-142">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dd5a8-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd5a8-143">Next steps</span></span>

<span data-ttu-id="dd5a8-144">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dd5a8-145">您可以在 [Azure Batch CLI 文件](../batch-cli-samples.md)中找到其他的 Batch CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="dd5a8-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
