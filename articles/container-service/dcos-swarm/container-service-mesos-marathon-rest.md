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
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="ec2fb-104">透過 hello 馬拉松 REST API 的 DC/OS 容器管理</span><span class="sxs-lookup"><span data-stu-id="ec2fb-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="ec2fb-105">DC/OS 會提供一個環境來部署及調整叢集工作負載，同時減少了 hello 基礎硬體。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="ec2fb-106">在 DC/OS 之上有架構會管理排程和執行計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="ec2fb-107">雖然架構可供許多常用的工作負載，這份文件可讓您開始建立及調整容器部署使用 hello 馬拉松 REST API。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ec2fb-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ec2fb-108">Prerequisites</span></span>

<span data-ttu-id="ec2fb-109">在練習這些範例之前，您需要 Azure 容器服務中設定的 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="ec2fb-110">您也需要 toohave 遠端連線 toothis 叢集。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="ec2fb-111">如需有關這些項目詳細資訊，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec2fb-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="ec2fb-112">部署 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="ec2fb-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="ec2fb-113">連接 tooan Azure 容器服務的叢集</span><span class="sxs-lookup"><span data-stu-id="ec2fb-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="ec2fb-114">存取 hello DC/OS 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="ec2fb-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="ec2fb-115">您已連線的 toohello Azure 容器服務的叢集之後，您可以透過 http://localhost:local 連接埠存取 hello DC/OS 和相關的 REST Api。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="ec2fb-116">這份文件中的 hello 範例假設您要設定通道連接埠 80 上。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="ec2fb-117">例如，達到 hello 馬拉松端點，在 Url 開頭`http://localhost/marathon/v2/`。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="ec2fb-118">如需有關 hello 各種 API，請參閱 hello hello Mesosphere 文件[馬拉松 API](https://mesosphere.github.io/marathon/docs/rest-api.html)和[Chronos API](https://mesos.github.io/chronos/docs/api.html)，與 hello Apache 文件集[Mesos 排程器應用程式開發介面](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="ec2fb-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="ec2fb-119">從 DC/OS 和 Marathon 收集資訊</span><span class="sxs-lookup"><span data-stu-id="ec2fb-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="ec2fb-120">部署容器 toohello DC/OS 叢集前，請先收集 hello DC/OS 叢集中，例如 hello 名稱和 hello DC/OS 代理程式狀態的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="ec2fb-121">因此，查詢 toodo 的 hello `master/slaves` hello DC/OS REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="ec2fb-122">如果一切順利，hello 查詢就會傳回每個 DC/OS 代理程式和數個屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="ec2fb-123">現在，使用 hello 馬拉松`/apps`端點 toocheck 目前應用程式部署 toohello DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="ec2fb-124">如果這是新的叢集，您會看到空的應用程式陣列。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="ec2fb-125">部署 Docker 格式化容器</span><span class="sxs-lookup"><span data-stu-id="ec2fb-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="ec2fb-126">您可以使用描述 hello 適合部署在 JSON 檔案，以部署 hello 馬拉松 REST API 透過 Docker 格式化的容器。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="ec2fb-127">hello 下列範例會將部署 Nginx 容器 tooa 私用代理程式在 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

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

<span data-ttu-id="ec2fb-128">toodeploy Docker 格式化容器使用時，會將 hello JSON 檔案儲存在可存取的位置。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="ec2fb-129">下一步 toodeploy hello 的容器，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="ec2fb-130">指定 hello hello JSON 檔案名稱 (`marathon.json`在此範例中)。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="ec2fb-131">hello 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="ec2fb-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="ec2fb-132">現在，如果您的應用程式查詢馬拉松，這個新的應用程式將會出現在 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="ec2fb-133">到達 hello 容器</span><span class="sxs-lookup"><span data-stu-id="ec2fb-133">Reach hello container</span></span>

<span data-ttu-id="ec2fb-134">您可以確認該 Nginx 其中 hello hello 叢集中的私人代理程式執行的容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="ec2fb-135">toofind hello 主機和連接埠其中 hello 容器執行時，查詢執行工作的 hello 馬拉松：</span><span class="sxs-lookup"><span data-stu-id="ec2fb-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="ec2fb-136">找出 hello 值`host`hello 輸出中 (IP 位址太類似`10.32.0.x`)，以及 hello 值`ports`。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="ec2fb-137">現在可讓 hello 叢集 SSH 終端機連線 （不通道連線） toohello 管理 FQDN。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="ec2fb-138">一旦連接之後，進行下列要求，並以 hello 正確值的替代 hello`host`和`ports`:</span><span class="sxs-lookup"><span data-stu-id="ec2fb-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="ec2fb-139">hello Nginx server 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="ec2fb-139">hello Nginx server output is similar toohello following:</span></span>

![來自容器的 Nginx](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="ec2fb-141">調整容器的大小</span><span class="sxs-lookup"><span data-stu-id="ec2fb-141">Scale your containers</span></span>
<span data-ttu-id="ec2fb-142">在應用程式部署中，您可以使用出 hello 馬拉松 API tooscale 或小數位數。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="ec2fb-143">在 hello 上述範例中，您可以部署一個應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="ec2fb-144">讓我們來調整這個 out toothree 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="ec2fb-145">toodo 因此使用下列 JSON 文字的 hello 建立 JSON 檔案，然後將它儲存在可存取的位置。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="ec2fb-146">從通道的連線，執行下列命令 tooscale 出 hello 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="ec2fb-147">hello URI 是後面接著 hello 識別碼 hello 應用程式 tooscale http://localhost/marathon/v2/apps/。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="ec2fb-148">如果您在此使用 hello Nginx 範例所提供，hello URI 將 http://localhost/marathon/v2/apps/nginx。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="ec2fb-149">最後，查詢的應用程式的 hello 馬拉松端點。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="ec2fb-150">您會看到現在有三個 Nginx 容器。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="ec2fb-151">對等的 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="ec2fb-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="ec2fb-152">您可以在 Windows 系統上使用 PowerShell 命令來執行這些相同的動作。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="ec2fb-153">toogather 資訊 hello DC/OS 叢集中，例如代理程式名稱和代理程式狀態，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec2fb-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="ec2fb-154">您可以使用描述 hello 適合部署在 JSON 檔案，以部署馬拉松透過 Docker 格式化的容器。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="ec2fb-155">hello 下列範例會將部署 hello Nginx 容器，繫結的 hello DC/OS 代理程式 tooport 80 hello 容器的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

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

<span data-ttu-id="ec2fb-156">toodeploy Docker 格式化容器使用時，會將 hello JSON 檔案儲存在可存取的位置。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="ec2fb-157">下一步 toodeploy hello 的容器，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="ec2fb-158">指定 hello 路徑 toohello JSON 檔案 (`marathon.json`在此範例中)。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="ec2fb-159">您也可以使用 hello 馬拉松 API tooscale out 或延展應用程式部署中。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="ec2fb-160">在 hello 上述範例中，您可以部署一個應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="ec2fb-161">讓我們來調整這個 out toothree 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="ec2fb-162">toodo 因此使用下列 JSON 文字的 hello 建立 JSON 檔案，然後將它儲存在可存取的位置。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="ec2fb-163">執行下列命令 tooscale 出 hello 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec2fb-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="ec2fb-164">hello URI 是後面接著 hello 識別碼 hello 應用程式 tooscale http://localhost/marathon/v2/apps/。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="ec2fb-165">如果您使用 hello Nginx 範例提供此處，hello URI 將 http://localhost/marathon/v2/apps/nginx。</span><span class="sxs-lookup"><span data-stu-id="ec2fb-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="ec2fb-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec2fb-166">Next steps</span></span>
* [<span data-ttu-id="ec2fb-167">深入了解 hello Mesos HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="ec2fb-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="ec2fb-168">深入了解 hello 馬拉松 REST API</span><span class="sxs-lookup"><span data-stu-id="ec2fb-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

