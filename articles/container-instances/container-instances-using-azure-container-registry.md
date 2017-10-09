---
title: "從 Azure 容器登錄中的 hello aaaDeploy tooAzure 容器執行個體 |Azure 文件"
description: "部署 tooAzure 從 hello Azure 容器登錄中的容器執行個體"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>部署 tooAzure 從 hello Azure 容器登錄中的容器執行個體

hello Azure 容器登錄中是以 Azure 為基礎的私人登錄中，為 Docker 容器映像。 本文件涵蓋如何 toodeploy 容器映像儲存在容器登錄中 Azure hello tooAzure 容器執行個體。

## <a name="using-hello-azure-cli"></a>使用 Azure CLI hello

hello Azure CLI 包含可用來建立和管理 Azure 容器執行個體中的容器命令。 如果您指定的私人映像中 hello`create`命令時，您也可以指定 hello 映像登錄所需密碼 tooauthenticate 與 hello 容器登錄中。

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

hello`create`命令也支援指定 hello`registry-login-server`和`registry-username`。 不過，hello Azure 容器登錄中的 hello 登入伺服器會一律*registryname*。 azurecr.io 和 hello 預設使用者名稱是*registryname*，因此，如果這些值會推斷從 hello 映像名稱未明確提供。

## <a name="using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本

您也可以包括 hello Azure Resource Manager 範本中指定的 Azure 容器登錄 hello 屬性`imageRegistryCredentials`hello 容器群組定義中的屬性：

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid 儲存容器登錄密碼直接在 hello 範本中，我們建議您將其儲存為中的秘密[Azure 金鑰保存庫](../key-vault/key-vault-manage-with-cli2.md)使用 hello hello 範本中參考它[之間的原生整合hello Azure 資源管理員與金鑰保存庫](../azure-resource-manager/resource-manager-keyvault-parameter.md)。

## <a name="using-hello-azure-portal"></a>使用 hello Azure 入口網站

如果您維護 hello Azure 容器登錄中的容器映像，您就可以在 Azure 容器執行個體使用 hello Azure 入口網站，輕鬆建立容器。

1. 在 hello Azure 入口網站，瀏覽 tooyour 容器登錄中。

2. 選擇存放庫。

    ![hello Azure 入口網站中的 hello Azure 容器登錄中功能表][acr-menu]

3. 選擇您想從 toodeploy hello 儲存機制。

4. 以滑鼠右鍵按一下 hello 標記您想 toodeploy hello 容器映像。

    ![可供使用 Azure Container Instances 來啟動容器的快顯功能表][acr-runinstance-contextmenu]

5. 輸入 hello 容器的名稱和 hello 資源群組的名稱。 如果您想要也可以變更 hello 預設值。

    ![建立 Azure Container Instances 的功能表][acr-create-deeplink]

6. Hello 部署完成之後，您可以巡覽 hello 通知窗格 toofind toohello 容器群組，其 IP 位址和其他屬性。

    ![Azure Container Instances 容器群組的詳細資料檢視][aci-detailsview]

## <a name="next-steps"></a>後續步驟

了解 toobuild 容器，將其推送 tooa 私用容器登錄中，並將其部署 tooAzure 容器的執行個體所[完成 hello 教學課程](container-instances-tutorial-prepare-app.md)。

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
