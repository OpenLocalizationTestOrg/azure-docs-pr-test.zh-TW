---
title: "aaaManage 馬拉松 REST API 與 Azure DC/OS 叢集 |Microsoft 文件"
description: "使用 hello 馬拉松 REST API，以部署容器 tooan Azure 容器服務 DC/OS 叢集。"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>透過 hello 馬拉松 REST API 的 DC/OS 容器管理
DC/OS 會提供一個環境來部署及調整叢集工作負載，同時減少了 hello 基礎硬體。 在 DC/OS 之上有架構會管理排程和執行計算工作負載。 雖然架構可供許多常用的工作負載，這份文件可讓您開始建立及調整容器部署使用 hello 馬拉松 REST API。 

## <a name="prerequisites"></a>必要條件

在練習這些範例之前，您需要 Azure 容器服務中設定的 DC/OS 叢集。 您也需要 toohave 遠端連線 toothis 叢集。 如需有關這些項目詳細資訊，請參閱下列文章的 hello:

* [部署 Azure 容器服務叢集](container-service-deployment.md)
* [連接 tooan Azure 容器服務的叢集](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>存取 hello DC/OS 應用程式開發介面
您已連線的 toohello Azure 容器服務的叢集之後，您可以透過 http://localhost:local 連接埠存取 hello DC/OS 和相關的 REST Api。 這份文件中的 hello 範例假設您要設定通道連接埠 80 上。 例如，達到 hello 馬拉松端點，在 Url 開頭`http://localhost/marathon/v2/`。 

如需有關 hello 各種 API，請參閱 hello hello Mesosphere 文件[馬拉松 API](https://mesosphere.github.io/marathon/docs/rest-api.html)和[Chronos API](https://mesos.github.io/chronos/docs/api.html)，與 hello Apache 文件集[Mesos 排程器應用程式開發介面](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>從 DC/OS 和 Marathon 收集資訊
部署容器 toohello DC/OS 叢集前，請先收集 hello DC/OS 叢集中，例如 hello 名稱和 hello DC/OS 代理程式狀態的一些資訊。 因此，查詢 toodo 的 hello `master/slaves` hello DC/OS REST API 端點。 如果一切順利，hello 查詢就會傳回每個 DC/OS 代理程式和數個屬性的清單。

```bash
curl http://localhost/mesos/master/slaves
```

現在，使用 hello 馬拉松`/apps`端點 toocheck 目前應用程式部署 toohello DC/OS 叢集。 如果這是新的叢集，您會看到空的應用程式陣列。

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>部署 Docker 格式化容器
您可以使用描述 hello 適合部署在 JSON 檔案，以部署 hello 馬拉松 REST API 透過 Docker 格式化的容器。 hello 下列範例會將部署 Nginx 容器 tooa 私用代理程式在 hello 叢集中。 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy Docker 格式化容器使用時，會將 hello JSON 檔案儲存在可存取的位置。 下一步 toodeploy hello 的容器，執行下列命令的 hello。 指定 hello hello JSON 檔案名稱 (`marathon.json`在此範例中)。

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

hello 輸出是類似 toohello 下列：

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

現在，如果您的應用程式查詢馬拉松，這個新的應用程式將會出現在 hello 輸出中。

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>到達 hello 容器

您可以確認該 Nginx 其中 hello hello 叢集中的私人代理程式執行的容器中的 hello。 toofind hello 主機和連接埠其中 hello 容器執行時，查詢執行工作的 hello 馬拉松： 

```bash
curl localhost/marathon/v2/tasks
```

找出 hello 值`host`hello 輸出中 (IP 位址太類似`10.32.0.x`)，以及 hello 值`ports`。


現在可讓 hello 叢集 SSH 終端機連線 （不通道連線） toohello 管理 FQDN。 一旦連接之後，進行下列要求，並以 hello 正確值的替代 hello`host`和`ports`:

```bash
curl http://host:ports
```

hello Nginx server 輸出是類似 toohello 下列：

![來自容器的 Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>調整容器的大小
在應用程式部署中，您可以使用出 hello 馬拉松 API tooscale 或小數位數。 在 hello 上述範例中，您可以部署一個應用程式的執行個體。 讓我們來調整這個 out toothree 應用程式執行個體。 toodo 因此使用下列 JSON 文字的 hello 建立 JSON 檔案，然後將它儲存在可存取的位置。

```json
{ "instances": 3 }
```

從通道的連線，執行下列命令 tooscale 出 hello 應用程式的 hello。

> [!NOTE]
> hello URI 是後面接著 hello 識別碼 hello 應用程式 tooscale http://localhost/marathon/v2/apps/。 如果您在此使用 hello Nginx 範例所提供，hello URI 將 http://localhost/marathon/v2/apps/nginx。
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

最後，查詢的應用程式的 hello 馬拉松端點。 您會看到現在有三個 Nginx 容器。

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>對等的 PowerShell 命令
您可以在 Windows 系統上使用 PowerShell 命令來執行這些相同的動作。

toogather 資訊 hello DC/OS 叢集中，例如代理程式名稱和代理程式狀態，執行下列命令的 hello:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

您可以使用描述 hello 適合部署在 JSON 檔案，以部署馬拉松透過 Docker 格式化的容器。 hello 下列範例會將部署 hello Nginx 容器，繫結的 hello DC/OS 代理程式 tooport 80 hello 容器的連接埠 80。

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy Docker 格式化容器使用時，會將 hello JSON 檔案儲存在可存取的位置。 下一步 toodeploy hello 的容器，執行下列命令的 hello。 指定 hello 路徑 toohello JSON 檔案 (`marathon.json`在此範例中)。

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

您也可以使用 hello 馬拉松 API tooscale out 或延展應用程式部署中。 在 hello 上述範例中，您可以部署一個應用程式的執行個體。 讓我們來調整這個 out toothree 應用程式執行個體。 toodo 因此使用下列 JSON 文字的 hello 建立 JSON 檔案，然後將它儲存在可存取的位置。

```json
{ "instances": 3 }
```

執行下列命令 tooscale 出 hello 應用程式的 hello:

> [!NOTE]
> hello URI 是後面接著 hello 識別碼 hello 應用程式 tooscale http://localhost/marathon/v2/apps/。 如果您使用 hello Nginx 範例提供此處，hello URI 將 http://localhost/marathon/v2/apps/nginx。
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>後續步驟
* [深入了解 hello Mesos HTTP 端點](http://mesos.apache.org/documentation/latest/endpoints/)
* [深入了解 hello 馬拉松 REST API](https://mesosphere.github.io/marathon/docs/rest-api.html)

