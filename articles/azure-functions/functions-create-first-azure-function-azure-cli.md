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
# <a name="create-your-first-function-using-hello-azure-cli"></a>建立您使用 Azure CLI hello 的第一個函式

本快速入門教學課程將逐步引導 toouse Azure 函式 toocreate 您的第一個函式。 您使用 hello Azure CLI toocreate 函式應用程式，也就是裝載您的函式的 hello 無伺服器基礎結構。 從 GitHub 範例儲存機制部署 hello 函式程式碼本身。    

您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。 

## <a name="prerequisites"></a>必要條件 

執行此範例之前，您必須擁有 hello 下列：

+ 作用中的 [GitHub](https://github.com) 帳戶。 
+ 有效的 Azure 訂用帳戶。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 


## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)。 Azure 資源群組是在其中部署與管理 Azure 資源 (如函式應用程式、資料庫和儲存體帳戶) 的邏輯容器。

hello 下列範例會建立名為的資源群組`myResourceGroup`。  
如果您未使用 Cloud Shell，您必須先使用 `az login` 登入。

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶

函式會使用 Azure 儲存體帳戶 toomaintain 狀態和您的函式的其他資訊。 在您建立使用 hello hello 資源群組中建立儲存體帳戶[az 儲存體帳戶建立](/cli/azure/storage/account#create)命令。

在 hello 下列命令，以取代您自己了解 hello 的全域唯一的儲存體帳戶名稱`<storage_name>`預留位置。 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

建立 hello 儲存體帳戶之後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

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

## <a name="create-a-function-app"></a>建立函數應用程式

您必須擁有您的函式的函式應用程式 toohost hello 執行。 hello 函式應用程式提供無伺服器程式碼執行的函式的環境。 它可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。 建立函式的應用程式使用 hello [az functionapp 建立](/cli/azure/functionapp#create)命令。 

Hello 中下列命令，將替換成您自己唯一函式應用程式名稱看 hello`<app_name>`預留位置和 hello 儲存體帳戶名稱`<storage_name>`。 hello `<app_name>` hello 預設 DNS 網域 hello 函式應用程式，並因此 hello 名稱需要 toobe 唯一跨所有應用程式在 Azure 中作為。 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
根據預設，函式應用程式會建立與 hello 耗用量主控方案，這表示動態所需的函式加入資源，而且您只需要執行函式時。 如需詳細資訊，請參閱[選擇 hello 正確主控方案](functions-scale.md)。 

建立 hello 函式應用程式之後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

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

有函式應用程式之後，您可以部署 hello GitHub 範例儲存機制中的 hello 實際函式程式碼。

## <a name="deploy-your-function-code"></a>部署函式程式碼  

有數種方式 toocreate 函式的程式碼在應用程式的新函式中。 本主題會連接 tooa GitHub 中的範例儲存機制。 如往常一般，在 hello 下列程式碼取代 hello `<app_name>` hello 您所建立的 hello 函式應用程式名稱的預留位置。 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Hello 部署來源設定之後，Azure CLI 顯示下列範例 （針對可讀性移除 null 值） 的資訊類似 toohello hello:

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

## <a name="test-hello-function"></a>測試 hello 函式

在 Mac 或 Linux 電腦或 Windows 上使用 Bash 使用 cURL tootest 部署的 hello 函式。 執行下列 cURL 命令，取代 hello hello `<app_name>` hello 函式應用程式名稱的預留位置。 附加 hello 查詢字串`&name=<yourname>`toohello URL。

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

如果您沒有 cURL 可用命令列中，輸入 hello hello 位址在網頁瀏覽器中相同的 URL。 同樣地，取代 hello`<app_name>`預留位置 hello 應用程式名稱函式，並附加 hello 查詢字串`&name=<yourname>`toohello URL，然後執行 hello 要求。 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![瀏覽器顯示的函式回應。](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>清除資源

此集合中的其他快速入門會以本快速入門為基礎。 如果您計劃 toocontinue toowork 與後續的快速入門或 hello 教學課程，請執行不會清除建立本快速入門的 hello 資源。 如果您不打算 toocontinue，使用下列命令 toodelete hello 本快速入門所建立的所有資源：

```azurecli-interactive
az group delete --name myResourceGroup
```
在出現提示時輸入 `y`。

## <a name="next-steps"></a>後續步驟

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
