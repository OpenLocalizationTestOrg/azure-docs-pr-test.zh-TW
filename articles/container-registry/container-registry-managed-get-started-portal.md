---
title: "aaaCreate 的私用 Docker 登錄-而 Azure 入口網站 |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure 入口網站"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>建立受管理的容器登錄中使用 hello Azure 入口網站

Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。 本指南詳述建立受管理的 Azure 容器登錄中執行個體使用 hello Azure 入口網站。

受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。

## <a name="log-in-tooazure"></a>登入 tooAzure

登入 toohello http://portal.azure.com 在 Azure 入口網站。

## <a name="create-a-container-registry"></a>建立容器登錄庫

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 搜尋 hello marketplace 中的**Azure 容器登錄**並加以選取。

3. 按一下**建立**來開啟 hello ACR 建立刀鋒視窗。

    ![容器登錄庫設定](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. 在 hello **Azure 容器登錄中**刀鋒視窗中，輸入下列資訊的 hello。 完成後按一下 [建立]。

    a. **登錄名稱**：指定登錄的全域唯一最上層網域名稱。 在此範例中，是 hello 登錄名稱*myAzureContainerRegistry1*，但以取代您自己的唯一名稱。 hello 名稱只能包含字母和數字。

    b. **資源群組**： 選取現有[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。

    c. **位置**： 選取 hello 服務所在的 Azure 資料中心位置[可用](https://azure.microsoft.com/regions/services/)，例如**美國中南部**。

    d. **系統管理使用者**： 如果您想，讓系統管理員使用者 tooaccess hello 登錄。 您可以變更此設定建立 hello 登錄之後。

    e. **使用 managed 的登錄**： 選取 [是] toohave ACR 自動管理 hello 登錄存放裝置、 使用 webhook，以及使用 AAD 驗證。

    f. **定價層**：選取定價層，以在這裡查看 ACR 定價的詳細資訊。

## <a name="log-in-tooacr-instance"></a>登入 tooACR 執行個體

然後再推送和提取容器映像，您必須登入 toohello ACR 執行個體。 

toodo 因此，使用 Azure CLI 2.0 hello。 首先，如有需要登入 Azure 使用 hello [az 登入](/cli/azure/#login)命令。 

```azurecli
az login
```

接下來，使用 hello [az acr 登入](/cli/azure/acr#login)命令 toolog toohello Azure 容器登錄中的。

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a>使用 Azure Container Registry

### <a name="list-container-images"></a>列出容器映像

使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。

> [!NOTE]
> 目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。

### <a name="list-repositories"></a>列出儲存機制

hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>列出標籤

hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>後續步驟

在這個快速入門中，您已建立的受管理的 Azure 容器登錄中執行個體使用 hello Azure 入口網站。

> [!div class="nextstepaction"]
> [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
