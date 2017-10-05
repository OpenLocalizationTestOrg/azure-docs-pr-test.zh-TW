---
title: "從 Azure CLI 建立您的第一個函式 | Microsoft Docs"
description: "了解如何使用 Azure CLI 來建立您的第一個 Azure 函式以進行無伺服器執行。"
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 8bd3e4bb7423db44c48b04f25edcf1074e6ea0bd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="7ba7d-103">在 Azure CLI 建立您的第一個函式</span><span class="sxs-lookup"><span data-stu-id="7ba7d-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="7ba7d-104">本快速入門教學課程會逐步解說如何使用 Azure Functions 來建立您的第一個函式。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-104">This quickstart tutorial walks through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="7ba7d-105">您會使用 Azure CLI 來建立函式應用程式，此應用程式是主控函式的無伺服器基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-105">You use the Azure CLI to create a function app, which is the serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="7ba7d-106">函式程式碼本身是從 GitHub 的範例存放庫部署而來的。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="7ba7d-107">您可以使用 Mac、Windows 或 Linux 電腦，依照下面步驟操作。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7ba7d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ba7d-108">Prerequisites</span></span> 

<span data-ttu-id="7ba7d-109">在執行此範例之前，您必須具備下列項目︰</span><span class="sxs-lookup"><span data-stu-id="7ba7d-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="7ba7d-110">作用中的 [GitHub](https://github.com) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="7ba7d-111">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7ba7d-112">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-112">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7ba7d-113">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="7ba7d-114">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="7ba7d-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="7ba7d-115">Create a resource group</span></span>

<span data-ttu-id="7ba7d-116">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-116">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7ba7d-117">Azure 資源群組是在其中部署與管理 Azure 資源 (如函式應用程式、資料庫和儲存體帳戶) 的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="7ba7d-118">下列範例會建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-118">The following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="7ba7d-119">如果您未使用 Cloud Shell，您必須先使用 `az login` 登入。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="7ba7d-120">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7ba7d-120">Create an Azure Storage account</span></span>

<span data-ttu-id="7ba7d-121">函式會使用 Azure 儲存體帳戶來維護函式的狀態和其他資訊。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-121">Functions uses an Azure Storage account to maintain state and other information about your functions.</span></span> <span data-ttu-id="7ba7d-122">在使用 [az storage account create](/cli/azure/storage/account#create) 命令所建立的資源群組中建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-122">Create a storage account in the resource group you created by using the [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="7ba7d-123">在下列命令中，使用您自己的全域唯一儲存體帳戶名稱來替代您看見 `<storage_name>` 預留位置的地方。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-123">In the following command, substitute your own globally unique storage account name where you see the `<storage_name>` placeholder.</span></span> <span data-ttu-id="7ba7d-124">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="7ba7d-125">建立儲存體帳戶後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="7ba7d-125">After the storage account has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="7ba7d-126">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="7ba7d-126">Create a function app</span></span>

<span data-ttu-id="7ba7d-127">您必須擁有函式應用程式以便主控函式的執行。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-127">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="7ba7d-128">函式應用程式會提供環境來讓您的函式程式碼進行無伺服器執行。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-128">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="7ba7d-129">它可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="7ba7d-130">使用 [az functionapp create](/cli/azure/functionapp#create) 命令來建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-130">Create a function app by using the [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="7ba7d-131">在下列命令中，使用您自己的唯一函式應用程式名稱來替代您看見 `<app_name>` 預留位置的地方，並使用儲存體帳戶名稱來替代 `<storage_name>`。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-131">In the following command, substitute your own unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="7ba7d-132">`<app_name>` 會作為函式應用程式的預設 DNS 網域，所以此名稱在 Azure 的所有應用程式中都必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-132">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="7ba7d-133">根據預設，所建立的函式應用程式會使用「取用」主控方案，也就是說，您的函式會根據需要來動態新增資源，並且只有在函式執行時才會產生費用。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-133">By default, a function app is created with the Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="7ba7d-134">如需詳細資訊，請參閱[選擇正確的主控方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-134">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="7ba7d-135">建立函式應用程式後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="7ba7d-135">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="7ba7d-136">您已經擁有函式應用程式，接下來您可以從 GitHub 的範例存放庫來部署實際的函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-136">Now that you have a function app, you can deploy the actual function code from the GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="7ba7d-137">部署函式程式碼</span><span class="sxs-lookup"><span data-stu-id="7ba7d-137">Deploy your function code</span></span>  

<span data-ttu-id="7ba7d-138">有多種方式可以在新的函式應用程式中建立函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-138">There are several ways to create your function code in your new function app.</span></span> <span data-ttu-id="7ba7d-139">本主題連結到 GitHub 中的範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-139">This topic connects to a sample repository in GitHub.</span></span> <span data-ttu-id="7ba7d-140">和先前一樣，請在下列程式碼中將 `<app_name>` 預留位置改為您所建立之函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-140">As before, in the following code replace the `<app_name>` placeholder with the name of the function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="7ba7d-141">設定部署來源後，Azure CLI 會顯示類似下列範例的資訊 (已移除 Null 值以方便閱讀)︰</span><span class="sxs-lookup"><span data-stu-id="7ba7d-141">After the deployment source been set, the Azure CLI shows information similar to the following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-the-function"></a><span data-ttu-id="7ba7d-142">測試函式</span><span class="sxs-lookup"><span data-stu-id="7ba7d-142">Test the function</span></span>

<span data-ttu-id="7ba7d-143">在 Mac 或 Linux 電腦上使用 cURL 來測試已部署的函式，在 Windows 上則請使用 Bash。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-143">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="7ba7d-144">執行下列 cURL 命令時，但請將其中的 `<app_name>` 預留位置改為函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-144">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="7ba7d-145">將查詢字串 `&name=<yourname>` 附加至 URL。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-145">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="7ba7d-147">如果您的命令列無法使用 cURL，在網頁瀏覽器的位址中輸入相同 URL 即可。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-147">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="7ba7d-148">同樣地，請將 `<app_name>` 預留位置改為函式應用程式的名稱，然後對 URL 附加查詢字串 `&name=<yourname>` 並執行要求。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-148">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="7ba7d-150">清除資源</span><span class="sxs-lookup"><span data-stu-id="7ba7d-150">Clean up resources</span></span>

<span data-ttu-id="7ba7d-151">此集合中的其他快速入門會以本快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="7ba7d-152">如果您打算繼續進行後續的快速入門或教學課程，請勿清除在此快速入門中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-152">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="7ba7d-153">如果您不打算繼續，請使用下列命令來刪除本快速入門建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="7ba7d-153">If you do not plan to continue, use the following command to delete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="7ba7d-154">在出現提示時輸入 `y`。</span><span class="sxs-lookup"><span data-stu-id="7ba7d-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba7d-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ba7d-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
