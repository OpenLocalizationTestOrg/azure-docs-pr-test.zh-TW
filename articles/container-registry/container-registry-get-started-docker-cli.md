---
title: "aaaPush Docker 映像 tooprivate Azure 登錄 |Microsoft 文件"
description: "發送和提取 Docker 映像 tooa 私用容器登錄在 Azure 中使用 hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>推入第一個影像 tooa 私用 Docker 容器登錄使用 hello Docker CLI
Azure 容器登錄中儲存和管理私人[Docker](http://hub.docker.com)容器映像、 類似 toohello 方式[Docker Hub](https://hub.docker.com/)存放公用 Docker 映像檔。 使用 hello [Docker 命令列介面](https://docs.docker.com/engine/reference/commandline/cli/)(Docker CLI) 的[登入](https://docs.docker.com/engine/reference/commandline/login/)，[發送](https://docs.docker.com/engine/reference/commandline/push/)，[提取](https://docs.docker.com/engine/reference/commandline/pull/)，和您的容器上的其他操作登錄中。

如需背景和概念，請參閱[hello 概觀](container-registry-intro.md)



## <a name="prerequisites"></a>必要條件
* **Azure 容器登錄庫** - 在 Azure 訂用帳戶中建立容器登錄庫。 例如，使用 hello [Azure 入口網站](container-registry-get-started-portal.md)或 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)。
* **Docker CLI** -tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上的安裝[Docker 引擎](https://docs.docker.com/engine/installation/)。

## <a name="log-in-tooa-registry"></a>登入 tooa 登錄
執行`docker login`toolog tooyour 容器登錄中以在您[登錄認證](container-registry-authentication.md)。

hello 下列範例會傳遞 hello ID 和 Azure Active Directory 密碼[服務主體](../active-directory/active-directory-application-objects.md)。 例如，您可能已指派服務主體 tooyour 登錄所需自動化案例。

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> 請確定 toospecify hello 完整的登錄名稱 （全部小寫）。 在此範例中為 `myregistry.azurecr.io`。

## <a name="steps-toopull-and-push-an-image"></a>步驟 toopull 並推送映像
hello，請遵循下載 hello Nginx 映像從公用 Docker Hub 登錄 hello，標記為私用 Azure 容器登錄中，將其發送 tooyour 登錄中，則會將其再次的範例。

**1.如 Nginx 提取 hello Docker 官方映像**

第一次提取 hello 公用 Nginx 映像 tooyour 本機電腦。

```
docker pull nginx
```
**2.啟動 hello Nginx 容器**

hello 下列命令會啟動本機 Nginx 容器 hello 以互動方式在連接埠 8080，可讓您從 Nginx toosee 輸出。 它會移除 hello 執行一次停止容器。

```
docker run -it --rm -p 8080:80 nginx
```

瀏覽過[http://localhost:8080/<](http://localhost:8080) tooview hello 執行容器。 您會看到下列其中一個螢幕類似 toohello。

![本機電腦上的 Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

toostop hello 執行的容器，請按 [CTRL] + [C]。

**3.在登錄中建立 hello 映像的別名**

hello 下列命令會建立別名 hello 影像的完整的路徑 tooyour 登錄。 這個範例會指定 hello `samples` hello hello 登錄根目錄中的命名空間 tooavoid 雜亂。

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4.推入 hello 映像 tooyour 登錄**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5.從登錄中提取 hello 映像**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6.從登錄啟動 hello Nginx 容器**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

瀏覽過[http://localhost:8080/<](http://localhost:8080) tooview hello 執行容器。

toostop hello 執行的容器，請按 [CTRL] + [C]。

**7.（選擇性）移除 hello 映像**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>並行限制
在某些情況下，同時執行呼叫可能會導致錯誤。 下表中的 hello 包含 hello 限制的並行呼叫上 Azure 容器登錄中的 「 發送 」 和 「 提取 」 作業：

| 作業  | 限制                                  |
| ---------- | -------------------------------------- |
| PULL       | 向上 too10 並行提取每個登錄 |
| PUSH       | 並行 too5 向上推播通知登錄每 |

## <a name="next-steps"></a>後續步驟
知道 hello 基本概念之後，您已經準備好使用您的登錄的 toostart ！ 例如，啟動 部署容器映像 tooan [Azure 容器服務](https://azure.microsoft.com/documentation/services/container-service/)叢集。
