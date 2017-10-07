---
title: "您的第一個函式從 hello Azure CLI aaaCreate |Microsoft 文件"
description: "深入了解如何使用無伺服器執行的函式的第一個 Azure toocreate hello Azure CLI。"
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
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="df10a-103">建立您使用 Azure CLI hello 的第一個函式</span><span class="sxs-lookup"><span data-stu-id="df10a-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="df10a-104">本快速入門教學課程將逐步引導 toouse Azure 函式 toocreate 您的第一個函式。</span><span class="sxs-lookup"><span data-stu-id="df10a-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="df10a-105">您使用 hello Azure CLI toocreate 函式應用程式，也就是裝載您的函式的 hello 無伺服器基礎結構。</span><span class="sxs-lookup"><span data-stu-id="df10a-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="df10a-106">從 GitHub 範例儲存機制部署 hello 函式程式碼本身。</span><span class="sxs-lookup"><span data-stu-id="df10a-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="df10a-107">您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="df10a-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="df10a-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="df10a-108">Prerequisites</span></span> 

<span data-ttu-id="df10a-109">執行此範例之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="df10a-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="df10a-110">作用中的 [GitHub](https://github.com) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="df10a-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="df10a-111">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="df10a-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="df10a-112">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="df10a-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="df10a-113">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="df10a-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="df10a-114">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="df10a-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="df10a-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="df10a-115">Create a resource group</span></span>

<span data-ttu-id="df10a-116">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="df10a-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="df10a-117">Azure 資源群組是在其中部署與管理 Azure 資源 (如函式應用程式、資料庫和儲存體帳戶) 的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="df10a-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="df10a-118">hello 下列範例會建立名為的資源群組`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="df10a-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="df10a-119">如果您未使用 Cloud Shell，您必須先使用 `az login` 登入。</span><span class="sxs-lookup"><span data-stu-id="df10a-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="df10a-120">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="df10a-120">Create an Azure Storage account</span></span>

<span data-ttu-id="df10a-121">函式會使用 Azure 儲存體帳戶 toomaintain 狀態和您的函式的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="df10a-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="df10a-122">在您建立使用 hello hello 資源群組中建立儲存體帳戶[az 儲存體帳戶建立](/cli/azure/storage/account#create)命令。</span><span class="sxs-lookup"><span data-stu-id="df10a-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="df10a-123">在 hello 下列命令，以取代您自己了解 hello 的全域唯一的儲存體帳戶名稱`<storage_name>`預留位置。</span><span class="sxs-lookup"><span data-stu-id="df10a-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="df10a-124">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="df10a-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="df10a-125">建立 hello 儲存體帳戶之後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="df10a-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="df10a-126">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="df10a-126">Create a function app</span></span>

<span data-ttu-id="df10a-127">您必須擁有您的函式的函式應用程式 toohost hello 執行。</span><span class="sxs-lookup"><span data-stu-id="df10a-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="df10a-128">hello 函式應用程式提供無伺服器程式碼執行的函式的環境。</span><span class="sxs-lookup"><span data-stu-id="df10a-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="df10a-129">它可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。</span><span class="sxs-lookup"><span data-stu-id="df10a-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="df10a-130">建立函式的應用程式使用 hello [az functionapp 建立](/cli/azure/functionapp#create)命令。</span><span class="sxs-lookup"><span data-stu-id="df10a-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="df10a-131">Hello 中下列命令，將替換成您自己唯一函式應用程式名稱看 hello`<app_name>`預留位置和 hello 儲存體帳戶名稱`<storage_name>`。</span><span class="sxs-lookup"><span data-stu-id="df10a-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="df10a-132">hello `<app_name>` hello 預設 DNS 網域 hello 函式應用程式，並因此 hello 名稱需要 toobe 唯一跨所有應用程式在 Azure 中作為。</span><span class="sxs-lookup"><span data-stu-id="df10a-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="df10a-133">根據預設，函式應用程式會建立與 hello 耗用量主控方案，這表示動態所需的函式加入資源，而且您只需要執行函式時。</span><span class="sxs-lookup"><span data-stu-id="df10a-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="df10a-134">如需詳細資訊，請參閱[選擇 hello 正確主控方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="df10a-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="df10a-135">建立 hello 函式應用程式之後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="df10a-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="df10a-136">有函式應用程式之後，您可以部署 hello GitHub 範例儲存機制中的 hello 實際函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="df10a-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="df10a-137">部署函式程式碼</span><span class="sxs-lookup"><span data-stu-id="df10a-137">Deploy your function code</span></span>  

<span data-ttu-id="df10a-138">有數種方式 toocreate 函式的程式碼在應用程式的新函式中。</span><span class="sxs-lookup"><span data-stu-id="df10a-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="df10a-139">本主題會連接 tooa GitHub 中的範例儲存機制。</span><span class="sxs-lookup"><span data-stu-id="df10a-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="df10a-140">如往常一般，在 hello 下列程式碼取代 hello `<app_name>` hello 您所建立的 hello 函式應用程式名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="df10a-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="df10a-141">Hello 部署來源設定之後，Azure CLI 顯示下列範例 （針對可讀性移除 null 值） 的資訊類似 toohello hello:</span><span class="sxs-lookup"><span data-stu-id="df10a-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="df10a-142">測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="df10a-142">Test hello function</span></span>

<span data-ttu-id="df10a-143">在 Mac 或 Linux 電腦或 Windows 上使用 Bash 使用 cURL tootest 部署的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="df10a-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="df10a-144">執行下列 cURL 命令，取代 hello hello `<app_name>` hello 函式應用程式名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="df10a-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="df10a-145">附加 hello 查詢字串`&name=<yourname>`toohello URL。</span><span class="sxs-lookup"><span data-stu-id="df10a-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="df10a-147">如果您沒有 cURL 可用命令列中，輸入 hello hello 位址在網頁瀏覽器中相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="df10a-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="df10a-148">同樣地，取代 hello`<app_name>`預留位置 hello 應用程式名稱函式，並附加 hello 查詢字串`&name=<yourname>`toohello URL，然後執行 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="df10a-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="df10a-150">清除資源</span><span class="sxs-lookup"><span data-stu-id="df10a-150">Clean up resources</span></span>

<span data-ttu-id="df10a-151">此集合中的其他快速入門會以本快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="df10a-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="df10a-152">如果您計劃 toocontinue toowork 與後續的快速入門或 hello 教學課程，請執行不會清除建立本快速入門的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="df10a-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="df10a-153">如果您不打算 toocontinue，使用下列命令 toodelete hello 本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="df10a-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="df10a-154">在出現提示時輸入 `y`。</span><span class="sxs-lookup"><span data-stu-id="df10a-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df10a-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df10a-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
