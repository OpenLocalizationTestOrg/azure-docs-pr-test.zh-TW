---
title: "aaaCreate 私用 Docker 容器登錄中的 Azure CLI |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>建立私用 Docker 容器登錄中使用 Azure CLI 2.0 hello
在 hello 中使用命令[Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate 容器登錄和管理其設定從 Linux、 Mac 或 Windows 電腦。 您也可以建立及管理使用 hello 容器登錄[Azure 入口網站](container-registry-get-started-portal.md)或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)。


* 背景和概念，請參閱[hello 概觀](container-registry-intro.md)
* 如需容器登錄 CLI 命令的說明 (`az acr`命令)，傳遞 hello`-h`參數 tooany 命令。


## <a name="prerequisites"></a>必要條件
* **Azure CLI 2.0**: tooinstall 和開始使用 hello CLI 2.0，請參閱 hello[安裝指示](/cli/azure/install-azure-cli)。 執行登入 Azure 訂用帳戶 tooyour `az login`。 如需詳細資訊，請參閱[hello CLI 2.0 使用者入門](/cli/azure/get-started-with-azure-cli)。
* **資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。 請確定 hello 資源群組是在 hello 容器登錄服務所在的位置[可用](https://azure.microsoft.com/regions/services/)。 使用資源群組的 toocreate hello CLI 2.0，請參閱[hello CLI 2.0 參考](/cli/azure/group)。
* **儲存體帳戶**（選擇性）： 建立標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)tooback hello 容器登錄中 hello 相同的位置。 如果您未指定儲存體帳戶時建立登錄中的以`az acr create`，hello 命令為您建立一個。 儲存體帳戶使用 toocreate hello CLI 2.0，請參閱[hello CLI 2.0 參考](/cli/azure/storage/account)。 目前不支援進階儲存體。
* **服務主體**（選擇性）： 當您建立登錄以 hello CLI 時，依預設它會無法存取權限設定。 根據您的需求，您可以指定現有的 Azure Active Directory 服務主體 tooa 登錄 （或建立並指派新的），或啟用 hello 登錄系統管理使用者帳戶。 請參閱本文稍後的 hello 章節。 如需登錄存取權的詳細資訊，請參閱[與 hello 容器登錄中的 Authenticate](container-registry-authentication.md)。

## <a name="create-a-container-registry"></a>建立容器登錄庫
執行 hello`az acr create`命令 toocreate 容器登錄中。

> [!TIP]
> 當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。 hello 範例中的 hello 登錄名稱`myRegistry1`，但以取代您自己的唯一名稱。
>
>

下列命令會使用 hello 最少參數 toocreate 容器登錄中的 hello `myRegistry1` hello 資源群組中`myResourceGroup`，並使用 hello*基本*sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` 為選擇性。 如果未指定，儲存體帳戶建立 hello 登錄名稱所組成的名稱，並 hello 的時間戳記指定資源群組。

建立 hello 登錄時，hello 輸出會是類似 toohello 下列：

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


請特別注意︰

* `id`Hello 登錄您的訂閱，如果您想要 tooassign 服務主體，則需要在識別項。
* `loginServer`-您指定過 hello 完整限定的名稱[登入 toohello 登錄](container-registry-authentication.md)。 在此範例中，hello 名稱是`myregistry1.exp.azurecr.io`（全部小寫）。

## <a name="assign-a-service-principal"></a>指派服務主體
使用 CLI 2.0 命令 tooassign Azure Active Directory 服務主體 tooa 登錄。 hello 這些範例中的服務主體指派 hello 擁有者角色，但您可以指派[其他角色](../active-directory/role-based-access-control-configure.md)如果您想要。

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>建立服務主體，並指派存取 toohello 登錄
Hello 下列命令，在新的服務主體指派擁有者角色存取 toohello 登錄識別碼傳遞以 hello`--scopes`參數。 指定強式密碼以 hello`--password`參數。

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>指派現有的服務主體
如果您已經有服務主體，而且想 tooassign 它擁有者角色存取 toohello 登錄中，執行下列範例命令類似 toohello。 您將使用 hello hello 服務主體的應用程式識別碼傳遞`--assignee`參數：

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>管理管理員認證
系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。 下列範例會顯示的 hello `az acr` CLI 命令的容器登錄 toomanage hello 系統管理員認證。

### <a name="obtain-admin-user-credentials"></a>取得管理員使用者認證
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>啟用現有登錄庫的管理員使用者
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>停用現有登錄庫的管理員使用者
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>列出映像和標籤
使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。

> [!NOTE]
> 目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。


### <a name="list-repositories"></a>列出儲存機制
hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>列出標籤
hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>後續步驟
* [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
