---
title: "使用 Azure Event Grid 以自動調整上傳映像的大小 | Microsoft Docs"
description: "Azure Event Grid 可在 Azure 儲存體的 Blob 上傳項目上觸發。 您可以使用此將上傳至 Azure 儲存體的映像檔案傳送至其他服務 (例如 Azure Functions)，以調整大小和其他改善功能。"
services: event-grid
author: ggailey777
manager: cfowler
editor: 
ms.service: event-grid
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 10/20/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 22eafca56eb5677c63a833d298799b725c50f768
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="automate-resizing-uploaded-images-using-event-grid"></a>使用 Event Grid 自動調整已上傳映像的大小

[Azure Event Grid](overview.md) 是一項雲端事件服務。 Event Grid 可讓您建立由 Azure 服務或協力廠商資源引發之事件的訂閱。  

本教學課程是一系列儲存體教學課程的第二部分。 它延伸了[上一個儲存體教學課程][previous-tutorial]，以使用 Azure Event Grid 與 Azure Functions 新增無伺服器自動縮圖產生。 Event Grid 可讓 [Azure Functions](..\azure-functions\functions-overview.md) 回應 [Azure Blob 儲存體](..\storage\blobs\storage-blobs-introduction.md)事件，並產生上傳映像的縮圖。 針對 Blob 儲存體建立事件建立事件訂閱。 當 blob 加入特定的 Blob 儲存體容器時，會呼叫函式端點。 從 Event Grid 傳遞至函式繫結的資料用於存取 Blob 並產生縮圖映像。 

您可以使用 Azure CLI 與 Azure 入口網站，將調整大小功能加入現有的映像上傳應用程式。

![Edge 瀏覽器中已發佈的 Web 應用程式](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立一般的 Azure 儲存體帳戶
> * 使用 Azure Functions 部署無伺服器程式碼
> * 在 Event Grid 中建立 Blob 儲存體事件訂閱

## <a name="prerequisites"></a>必要條件

若要完成本教學課程：

+ 您必須先完成上一個 Blob 儲存體教學課程：[使用 Azure 儲存體上傳雲端中的映像資料][previous-tutorial]。 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0.14 版或更新版本。 執行 `az --version` 以尋找版本。 如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

如果您未使用 Cloud Shell，您必須先使用 `az login` 登入。

## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶

Azure Functions 需要一般的儲存體帳戶。 使用 [az storage account create](/cli/azure/storage/account#create) 命令，在資源群組中建立單獨的一般儲存體帳戶。

儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。 

在下列命令中，使用您自己的一般儲存體帳戶全域唯一名稱來替代您看見 `<general_storage_account>` 預留位置的地方。 

```azurecli-interactive
az storage account create --name <general_storage_account> \
--location westcentralus --resource-group myResourceGroup \
--sku Standard_LRS --kind storage
```

## <a name="create-a-function-app"></a>建立函數應用程式  

您必須擁有函式應用程式以便主控函式的執行。 函式應用程式會提供環境來讓您的函式程式碼進行無伺服器執行。 使用 [az functionapp create](/cli/azure/functionapp#create) 命令來建立函式應用程式。 

在下列命令中，使用您自己唯一的函式應用程式名稱來替代您看見 `<function_app>` 預留位置的地方。 `<function_app>` 會作為函式應用程式的預設 DNS 網域，所以此名稱在 Azure 的所有應用程式中都必須是唯一的名稱。 在此情況下，`<general_storage_account>` 是您所建立之一般儲存體帳戶的名稱。  

```azurecli-interactive
az functionapp create --name <function_app> --storage-account  <general_storage_account>  \
--resource-group myResourceGroup --consumption-plan-location westcentralus
```

現在，您必須設定函式應用程式以連接到 Blob 儲存體。 

## <a name="configure-the-function-app"></a>設定函式應用程式

此函式需要連接字串以連接到 Blob 儲存體帳戶。 在此情況下，`<blob_storage_account>` 是您在上一個教學課程中建立之 Blob 儲存體帳戶的名稱。 使用 [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string) 命令取得連接字串。 縮圖映像容器名稱也必須設定為 `thumbs`。 使用 [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set) 命令，在函式應用程式中新增這些應用程式設定。

```azurecli-interactive
storageConnectionString=$(az storage account show-connection-string \
--resource-group myResourceGroup --name <blob_storage_account> \
--query connectionString --output tsv)

az functionapp config appsettings set --name <function_app> \
--resource-group myResourceGroup \
--settings myblobstorage_STORAGE=$storageConnectionString \
myContainerName=thumbs
```

您現在可以將函式程式碼專案部署到此函式應用程式。

## <a name="deploy-the-function-code"></a>部署函式程式碼 

此 [GitHub 存放庫](https://github.com/Azure-Samples/function-image-upload-resize)範例中提供執行映像調整大小的 C# 函式。 使用 [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#config) 命令，將此函式程式碼專案部署至函式應用程式。 

在下列命令中，`<function_app>` 是您在先前指令碼中建立的相同函式應用程式。

```azurecli-interactive
az functionapp deployment source config --name <function_app> \
--resource-group myResourceGroup --branch master --manual-integration \
--repo-url https://github.com/Azure-Samples/function-image-upload-resize
```

映像調整大小函式是由 Blob 建立事件的事件訂閱所觸發。 傳遞給觸發程序的資料包括 Blob 的 URL，接著會傳遞至輸入繫結，以從 Blob 儲存體獲取上傳的映像。 此函式會產生縮圖映像，並將產生的串流寫入 Blob 儲存體中的個別容器。 若要深入了解此函式，請參閱[範例存放庫中的讀我檔案](https://github.com/Azure-Samples/function-image-upload-resize/blob/master/README.md)。
 
函式專案程式碼會直接從公用範例存放庫部署。 若要深入了解 Azure Functions 的部署選項，請參閱[Azure Functions 的持續部署](../azure-functions/functions-continuous-deployment.md)。

## <a name="create-your-event-subscription"></a>建立您的事件訂閱

事件訂閱表示您想要傳送至特定端點之提供者產生的事件。 在此情況下，端點會由函式公開。 使用下列步驟以在 Azure 入口網站中，從您的函式建立事件訂閱： 

1. 在 [Azure 入口網站](https://portal.azure.com)中，按一下左下方的箭號以展開所有服務，在 [篩選] 欄位中輸入 `functions`，然後選擇 [函式應用程式]。 

    ![瀏覽至 Azure 入口網站中的函式應用程式](./media/resize-images-on-storage-blob-upload-event/portal-find-functions.png)

2. 展開函式應用程式，選擇 **imageresizerfunc** 函式，然後選取 [新增 Event Grid 訂用帳戶]。

    ![瀏覽至 Azure 入口網站中的函式應用程式](./media/resize-images-on-storage-blob-upload-event/add-event-subscription.png)

3. 使用表格中指定的事件訂閱設定。

    ![從 Azure 入口網站中的函式建立事件訂閱](./media/resize-images-on-storage-blob-upload-event/event-subscription-create-flow.png)

    | 設定      | 建議的值  | 說明                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **名稱** | imageresizersub | 用以識別新事件訂閱的名稱。 | 
    | **主題類型** |  儲存體帳戶 | 選擇儲存體帳戶事件提供者。 | 
    | **訂用帳戶** | 您的訂用帳戶 | 根據預設，您應該選取目前的訂用帳戶。   |
    | **資源群組** | myResourceGroup | 選取 [使用現有]，並選擇您在本主題中一直使用的資源群組。  |
    | **執行個體** |  `<blob_storage_account>` |  選擇您建立的 Blob 儲存體帳戶。 |
    | **事件類型** | 已建立 Blob | 取消勾選 [已建立 Blob] 以外的所有類型。 只有 `Microsoft.Storage.BlobCreated` 的事件類型會傳遞至函式。| 
    | **訂閱者端點** | 自動產生 | 使用為您產生的端點 URL。 | 
    | **前置詞篩選** | /blobServices/default/containers/images/blobs/ | 將儲存體事件篩選為只有**映像**容器上的事件。| 

4. 按一下 [建立] 以新增事件訂閱。 當 Blob 新增至**映像**容器時，這會建立觸發 **imageresizerfunc** 的事件訂閱。 調整大小的映像已新增至 **thumbs** 容器。

既然已設定了後端服務，您可以在範例 Web 應用程式中測試映像調整大小功能。 

## <a name="test-the-sample-app"></a>測試範例應用程式

若要在 Web 應用程式中測試映像調整大小，請瀏覽至已發佈應用程式的 URL。 Web 應用程式的預設 URL 是 `https://<web_app>.azurewebsites.net`。

按一下 [上傳相片] 區域，以選取並上傳檔案。 您也可以將相片拖曳到此區域。 

請注意，上傳的映像消失之後，上傳映像的複本會顯示在 [產生縮圖] 浮動切換中。 此映像已由函式調整大小、新增至 thumbs 容器，並由 Web 用戶端下載。 

![Edge 瀏覽器中已發佈的 Web 應用程式](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png) 

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立一般的 Azure 儲存體帳戶
> * 使用 Azure Functions 部署無伺服器程式碼
> * 在 Event Grid 中建立 Blob 儲存體事件訂閱

進入儲存體教學課程系列的第三部分，了解如何保護儲存體帳戶的存取權。

> [!div class="nextstepaction"]
> [保護雲端中應用程式資料的存取權](../storage/blobs/storage-secure-access-application.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)


+ 如需深入了解 Event Grid，請參閱 [Event Grid 的簡介](overview.md)。 
+ 若要嘗試另一個隨附 Azure Functions 的教學課程，請參閱[建立與 Azure Logic Apps 整合的函式](..\azure-functions\functions-twitter-email.md)。 

[previous-tutorial]: ../storage/blobs/storage-upload-process-images.md