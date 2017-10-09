---
title: "aaaManage 馬拉松 UI 叢集 Azure DC/OS |Microsoft 文件"
description: "部署容器 tooan Azure 容器服務的叢集服務使用 hello 馬拉松 web UI。"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="c816d-104">管理透過 hello 馬拉松 web UI Azure 容器服務 DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="c816d-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="c816d-105">DC/OS 會提供一個環境來部署及調整叢集工作負載，同時減少了 hello 基礎硬體。</span><span class="sxs-lookup"><span data-stu-id="c816d-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="c816d-106">在 DC/OS 之上有架構會管理排程和執行計算工作負載。</span><span class="sxs-lookup"><span data-stu-id="c816d-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="c816d-107">架構可供許多常用的工作負載時，本文件說明 tooget 啟動部署具有馬拉松容器的方式。</span><span class="sxs-lookup"><span data-stu-id="c816d-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="c816d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c816d-108">Prerequisites</span></span>
<span data-ttu-id="c816d-109">在練習這些範例之前，您需要 Azure 容器服務中設定的 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="c816d-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="c816d-110">您也需要 toohave 遠端連線 toothis 叢集。</span><span class="sxs-lookup"><span data-stu-id="c816d-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="c816d-111">如需有關這些項目詳細資訊，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="c816d-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="c816d-112">部署 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="c816d-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="c816d-113">Tooan Azure 容器服務叢集連線</span><span class="sxs-lookup"><span data-stu-id="c816d-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="c816d-114">本文假設您透過本機連接埠 80 的通道 toohello DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="c816d-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="c816d-115">瀏覽 hello DC/OS UI</span><span class="sxs-lookup"><span data-stu-id="c816d-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="c816d-116">使用安全殼層 (SSH) 通道[建立](../container-service-connect.md)，瀏覽 toohttp://localhost/。</span><span class="sxs-lookup"><span data-stu-id="c816d-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="c816d-117">這會載入 hello DC/OS web UI，並顯示 hello 叢集中，例如使用的資源、 使用中的代理程式，以及執行中的服務的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c816d-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS UI](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="c816d-119">瀏覽 hello 馬拉松 UI</span><span class="sxs-lookup"><span data-stu-id="c816d-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="c816d-120">toosee hello 馬拉松 UI 中，瀏覽 toohttp://localhost/marathon。</span><span class="sxs-lookup"><span data-stu-id="c816d-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="c816d-121">在這個畫面上，您可以在 hello Azure 容器服務 DC/OS 叢集上啟動新的容器或另一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="c816d-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="c816d-122">您也可以看到有關執行容器和應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="c816d-122">You can also see information about running containers and applications.</span></span>  

![Marathon UI](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="c816d-124">部署 Docker 格式化容器</span><span class="sxs-lookup"><span data-stu-id="c816d-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="c816d-125">按一下新的容器使用馬拉松，toodeploy**建立應用程式**，並輸入下列資訊成 hello 表單索引標籤的 hello:</span><span class="sxs-lookup"><span data-stu-id="c816d-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="c816d-126">欄位</span><span class="sxs-lookup"><span data-stu-id="c816d-126">Field</span></span> | <span data-ttu-id="c816d-127">值</span><span class="sxs-lookup"><span data-stu-id="c816d-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c816d-128">ID</span><span class="sxs-lookup"><span data-stu-id="c816d-128">ID</span></span> |<span data-ttu-id="c816d-129">nginx</span><span class="sxs-lookup"><span data-stu-id="c816d-129">nginx</span></span> |
| <span data-ttu-id="c816d-130">記憶體</span><span class="sxs-lookup"><span data-stu-id="c816d-130">Memory</span></span> | <span data-ttu-id="c816d-131">32</span><span class="sxs-lookup"><span data-stu-id="c816d-131">32</span></span> |
| <span data-ttu-id="c816d-132">映像</span><span class="sxs-lookup"><span data-stu-id="c816d-132">Image</span></span> |<span data-ttu-id="c816d-133">nginx</span><span class="sxs-lookup"><span data-stu-id="c816d-133">nginx</span></span> |
| <span data-ttu-id="c816d-134">網路</span><span class="sxs-lookup"><span data-stu-id="c816d-134">Network</span></span> |<span data-ttu-id="c816d-135">橋接</span><span class="sxs-lookup"><span data-stu-id="c816d-135">Bridged</span></span> |
| <span data-ttu-id="c816d-136">主機連接埠</span><span class="sxs-lookup"><span data-stu-id="c816d-136">Host Port</span></span> |<span data-ttu-id="c816d-137">80</span><span class="sxs-lookup"><span data-stu-id="c816d-137">80</span></span> |
| <span data-ttu-id="c816d-138">通訊協定</span><span class="sxs-lookup"><span data-stu-id="c816d-138">Protocol</span></span> |<span data-ttu-id="c816d-139">TCP</span><span class="sxs-lookup"><span data-stu-id="c816d-139">TCP</span></span> |

![新增應用程式 UI--一般](./media/container-service-mesos-marathon-ui/dcos4.png)

![新增應用程式 UI--Docker 容器](./media/container-service-mesos-marathon-ui/dcos5.png)

![新增應用程式 UI--連接埠和服務探索](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="c816d-143">如果您想 toostatically 對應 hello 容器連接埠 tooa port hello 代理程式上的，您會需要 toouse JSON 模式。</span><span class="sxs-lookup"><span data-stu-id="c816d-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="c816d-144">toodo，切換 hello 新的應用程式精靈太**JSON 模式**使用 hello 切換。</span><span class="sxs-lookup"><span data-stu-id="c816d-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="c816d-145">然後輸入下列設定下 hello hello `portMappings` hello 應用程式定義的區段。</span><span class="sxs-lookup"><span data-stu-id="c816d-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="c816d-146">此範例中會繫結 hello 容器 tooport 80 hello DC/OS 代理程式的連接的埠 80。</span><span class="sxs-lookup"><span data-stu-id="c816d-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="c816d-147">在進行這項變更之後，您可以將此精靈切換離開 JSON 模式。</span><span class="sxs-lookup"><span data-stu-id="c816d-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![新增應用程式 UI--連接埠 80 範例](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="c816d-149">如果您想 tooenable 健康情況檢查，設定路徑上 hello**健康情況檢查** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c816d-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![新的應用程式 UI--健康狀態檢查](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="c816d-151">hello DC/OS 叢集部署的私人和公用的代理程式的設定。</span><span class="sxs-lookup"><span data-stu-id="c816d-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="c816d-152">Hello 叢集 toobe 無法 tooaccess 應用程式從 hello 網際網路，您需要 toodeploy hello 應用程式 tooa 公用代理程式。</span><span class="sxs-lookup"><span data-stu-id="c816d-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="c816d-153">因此，選取 toodo 的 hello**選擇性**hello 新的應用程式精靈 索引標籤並輸入**slave_public** hello**接受資源角色**。</span><span class="sxs-lookup"><span data-stu-id="c816d-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="c816d-154">然後按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c816d-154">Then click **Create Application**.</span></span>

![新增應用程式 UI--公用代理程式設定](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="c816d-156">在 hello 馬拉松主要頁面上，您可以看到 hello hello 容器的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="c816d-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="c816d-157">一開始您看到的狀態為 [部署中]。</span><span class="sxs-lookup"><span data-stu-id="c816d-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="c816d-158">成功部署之後，hello 狀態變更太**執行**。</span><span class="sxs-lookup"><span data-stu-id="c816d-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Marathon 主頁面 UI--容器部署狀態](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="c816d-160">當您切換後 toohello DC/OS web UI (http://localhost/) 時，您會看到 hello DC/OS 叢集上確認正在執行的工作 （在此情況下，Docker 格式化的容器）。</span><span class="sxs-lookup"><span data-stu-id="c816d-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![DC/OS web UI-hello 叢集上執行的工作](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="c816d-162">hello 工作 toosee hello 叢集節點上執行，請按一下 hello**節點** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c816d-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![DC/OS Web UI--工作叢集節點](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="c816d-164">到達 hello 容器</span><span class="sxs-lookup"><span data-stu-id="c816d-164">Reach hello container</span></span>

<span data-ttu-id="c816d-165">在此範例中，hello 應用程式公用的代理程式節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c816d-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="c816d-166">您到達 hello 應用程式從 hello 網際網路瀏覽 toohello 代理程式 hello 叢集的 FQDN: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`，其中：</span><span class="sxs-lookup"><span data-stu-id="c816d-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="c816d-167">**DNSPREFIX**是您部署 hello 叢集時，您所提供的 hello DNS 前置詞。</span><span class="sxs-lookup"><span data-stu-id="c816d-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="c816d-168">**區域**是資源群組所在的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="c816d-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![來自網際網路的 Nginx](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="c816d-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c816d-170">Next steps</span></span>
* [<span data-ttu-id="c816d-171">使用 DC/OS 和 hello 馬拉松應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="c816d-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="c816d-172">深入探討在 hello 與 Mesos Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="c816d-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
