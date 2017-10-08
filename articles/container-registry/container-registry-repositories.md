---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure 容器登錄存放庫

Azure 容器登錄中，可讓您在儲存機制中 toostore 容器映像。 透過將映像儲存在存放庫中，您可以在隔離的環境中擁有映像 (或映像的版本) 的群組。 推送映像 tooyour 登錄時，您可以指定這些儲存機制。


## <a name="prerequisites"></a>必要條件
* **Azure 容器登錄庫** - 在 Azure 訂用帳戶中建立容器登錄庫。 例如，使用 hello [Azure 入口網站](container-registry-get-started-portal.md)或 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)。
* **Docker CLI** -tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上的安裝[Docker 引擎](https://docs.docker.com/engine/installation/)。
* **提取映像**-從 hello 公用 Docker Hub 登錄提取映像、 標記，並將它推送 tooyour 登錄。 如需如何指引發送和提取映像，請參閱[推入 Docker 映像 tooAzure 私人登錄](container-registry-get-started-docker-cli.md)。


## <a name="viewing-repositories-in-hello-portal"></a>在 hello 入口網站中檢視儲存機制

一旦您已推入映像 tooyour 容器登錄中，您可以看到 hello 儲存機制裝載在 hello Azure 入口網站中的 hello 映像的清單。

如果您遵循 hello 中的 hello 步驟[推入 Docker 映像 tooAzure 私人登錄](container-registry-get-started-docker-cli.md)發行項，您現在應該有 Nginx 映像，在容器登錄中。 Hello 指示的一部分，您應該指定 hello 映像的命名空間。 Hello 以下範例中的 hello 命令將推送 hello NGinx 映像 toohello"samples"儲存機制：

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure 容器登錄庫支援多層級的儲存機制命名空間。 這項功能可讓您 toogroup 集合的映像相關的 tooa 特定應用程式或應用程式 toospecific 開發或操作團隊的集合。 tooread 有關容器登錄中的儲存機制的詳細資訊請參閱[在 Azure 中的私用 Docker 容器登錄](container-registry-intro.md)。

tooview hello 容器登錄儲存機制：

1. 登入 toohello Azure 入口網站
2. 在 hello **Azure 容器登錄中**刀鋒視窗中，您想 tooinspect 選取 hello 登錄
3. 在 hello 登錄刀鋒視窗中，按一下 **儲存機制**toosee 所有 hello 儲存機制和其映像的清單
4. （選擇性）選取特定的映像 toosee 標記

![Hello 入口網站中的儲存機制](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>後續步驟
知道 hello 基本概念之後，您已經準備好使用您的登錄的 toostart ！ 例如，啟動 部署容器映像 tooan [Azure 容器服務](https://azure.microsoft.com/documentation/services/container-service/)叢集。
