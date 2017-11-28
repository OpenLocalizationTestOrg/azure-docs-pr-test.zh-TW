---
title: "Azure DC/OS 叢集中的 aaaLoad 平衡容器 |Microsoft 文件"
description: "Azure Container Service DC/OS 叢集中多個容器的負載平衡。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, 微服務, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="8f3b6-104">Azure Container Service DC/OS 叢集中容器的負載平衡</span><span class="sxs-lookup"><span data-stu-id="8f3b6-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="8f3b6-105">在本文中，我們會探討 toocreate DC/OS 中使用內部負載平衡器管理使用馬拉松 LB Azure 容器服務的方式。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="8f3b6-106">此設定可讓您 tooscale 應用程式以水平方式。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="8f3b6-107">它也可讓您利用 tootake hello 公用和私用的代理程式的叢集將您的負載平衡器放置在 hello 公用叢集和您的應用程式容器 hello 私用的叢集上。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="8f3b6-108">在本教學課程中，您：</span><span class="sxs-lookup"><span data-stu-id="8f3b6-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f3b6-109">設定 Marathon 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="8f3b6-110">部署應用程式使用 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="8f3b6-111">設定 Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="8f3b6-112">您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="8f3b6-113">如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="8f3b6-114">本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8f3b6-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8f3b6-116">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="8f3b6-117">負載平衡概觀</span><span class="sxs-lookup"><span data-stu-id="8f3b6-117">Load balancing overview</span></span>

<span data-ttu-id="8f3b6-118">在 Azure Container Service DC/OS 叢集中有兩個負載平衡層：</span><span class="sxs-lookup"><span data-stu-id="8f3b6-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="8f3b6-119">**Azure 負載平衡器**提供公用進入點 (是該使用者存取的 hello)。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="8f3b6-120">Azure LB Azure 容器服務會自動提供，而是，預設為設定的 tooexpose 連接埠 80、 443 和 8080。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="8f3b6-121">**hello 馬拉松負載平衡器 (lb 馬拉松)**路由輸入這些要求提供服務的要求 toocontainer 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="8f3b6-122">因為我們縮放 hello 容器提供 web 服務，hello 馬拉松 lb 動態調整。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="8f3b6-123">預設會在您的容器服務未提供此負載平衡器，但它是簡單 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="8f3b6-124">設定 Marathon 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="8f3b6-125">馬拉松負載平衡器以動態方式重新設定根據您已部署的 hello 容器本身。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="8f3b6-126">它也是彈性 toohello 遺失的容器或代理程式-如果發生這種情況，會重新啟動的其他地方 hello 容器 Apache Mesos 馬拉松 lb 會調整。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="8f3b6-127">執行下列命令 tooinstall hello 馬拉松負載平衡器 hello 公用代理程式的叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="8f3b6-128">部署負載平衡應用程式</span><span class="sxs-lookup"><span data-stu-id="8f3b6-128">Deploy load balanced application</span></span>

<span data-ttu-id="8f3b6-129">現在，我們已經 hello 馬拉松 lb 封裝時，我們可以部署，我們希望 tooload 平衡的應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="8f3b6-130">首先，取得 hello hello 公開屬性，代理程式的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="8f3b6-131">接下來，建立名為*hello web.json*和 hello 中的複製下列內容。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="8f3b6-132">hello`HAPROXY_0_VHOST`標籤需要 toobe hello FQDN hello DC/OS 代理程式的更新。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="8f3b6-133">使用 hello DC/OS CLI toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="8f3b6-134">根據預設馬拉松部署 hello hello 應用程式 toohello 私人叢集。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="8f3b6-135">這表示在上面部署 hello 才可存取您的負載平衡器，透過這通常是 hello 預期的行為。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="8f3b6-136">一旦部署的 hello 應用程式，瀏覽 toohello hello 代理程式叢集 tooview 負載平衡應用程式的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![負載平衡應用程式的影像](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="8f3b6-138">設定 Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="8f3b6-139">根據預設，Azure Load Balancer 會公開連接埠 80、8080 和 443。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="8f3b6-140">如果您使用這三個的其中一個連接埠 （像是我們在上述範例中的 hello），則沒有需要 toodo 的項目。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="8f3b6-141">您應該能夠 toohit 代理程式負載平衡器的 FQDN，以及每次您重新整理，您將會叫用其中三個 web 伺服器以循環配置資源方式。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="8f3b6-142">如果您使用不同的通訊埠，您需要 tooadd 循環配置資源的規則，並在 hello 負載平衡器探查的 hello 所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="8f3b6-143">您可以從 hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md)，與 hello 命令`azure network lb rule create`和`azure network lb probe create`。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f3b6-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f3b6-144">Next steps</span></span>

<span data-ttu-id="8f3b6-145">在本教學課程中，您已了解有關負載平衡 acs hello 馬拉松和 Azure 負載平衡器包括 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="8f3b6-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f3b6-146">設定 Marathon 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="8f3b6-147">部署應用程式使用 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="8f3b6-148">設定 Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="8f3b6-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="8f3b6-149">前進 toohello 下一個教學課程的 toolearn 需將 Azure 儲存體與 Azure 中的 DC/OS 的整合。</span><span class="sxs-lookup"><span data-stu-id="8f3b6-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f3b6-150">在 DC/OS 叢集中裝載 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="8f3b6-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)