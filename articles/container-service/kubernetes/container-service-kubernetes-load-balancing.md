---
title: "aaaLoad 平衡在 Azure 中的 Kubernetes 容器 |Microsoft 文件"
description: "在 Azure Container Service 中由外部連接並針對 Kubernetes 叢集內的多個容器進行負載平衡。"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, 微服務, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="1cfda-104">在 Azure Container Service 中針對 Kubernetes 叢集內的容器進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="1cfda-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="1cfda-105">本文將介紹在 Azure Container Service 中 Kubernetes 叢集內進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="1cfda-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="1cfda-106">負載平衡 hello 服務提供外部存取的 IP 位址，並將散發代理程式 Vm 中執行的 hello pod 之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="1cfda-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="1cfda-107">您可以設定 Kubernetes 服務 toouse [Azure 負載平衡器](../../load-balancer/load-balancer-overview.md)toomanage 外部網路 (TCP) 流量。</span><span class="sxs-lookup"><span data-stu-id="1cfda-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="1cfda-108">透過其他設定，便可以達成 HTTP 或 HTTPS 流量 (或更進階的案例) 的負載平衡和路由。</span><span class="sxs-lookup"><span data-stu-id="1cfda-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cfda-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1cfda-109">Prerequisites</span></span>
* <span data-ttu-id="1cfda-110">在 Azure Container Service 中[部署 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="1cfda-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="1cfda-111">[將用戶端連線](../container-service-connect.md)tooyour 叢集</span><span class="sxs-lookup"><span data-stu-id="1cfda-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="1cfda-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="1cfda-112">Azure load balancer</span></span>

<span data-ttu-id="1cfda-113">根據預設，Kubernetes 叢集部署在 Azure 容器服務包括 Vm hello 代理程式 」 的網際網路對向 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="1cfda-114">（個別負載平衡器資源 hello 主要 Vm 的設定）。Azure Load Balancer 是第 4 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="1cfda-115">目前，hello 負載平衡器只會支援 TCP 流量 Kubernetes 中。</span><span class="sxs-lookup"><span data-stu-id="1cfda-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="1cfda-116">建立 Kubernetes 服務時，您可以自動設定 hello Azure 負載平衡器 tooallow 存取 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="1cfda-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="1cfda-117">tooconfigure hello 負載平衡器集 hello 服務`type`太`LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="1cfda-118">hello 負載平衡器會建立規則 toomap 公用 IP 位址和連接埠號碼的連入服務流量 toohello 私人 IP 位址和連接埠號碼 hello pod 的代理程式 Vm 中 （反之亦然回應流量）。</span><span class="sxs-lookup"><span data-stu-id="1cfda-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="1cfda-119">下列兩個範例顯示如何 tooset hello Kubernetes 服務`type`太`LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="1cfda-120">（之後嘗試 hello 範例中，刪除 hello 部署如果不再需要）。</span><span class="sxs-lookup"><span data-stu-id="1cfda-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="1cfda-121">範例： 使用 hello`kubectl expose`命令</span><span class="sxs-lookup"><span data-stu-id="1cfda-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="1cfda-122">hello [Kubernetes 逐步解說](container-service-kubernetes-walkthrough.md)包含的範例 tooexpose 服務以 hello`kubectl expose`命令及其`--type=LoadBalancer`旗標。</span><span class="sxs-lookup"><span data-stu-id="1cfda-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="1cfda-123">Hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="1cfda-123">Here are hello steps :</span></span>

1. <span data-ttu-id="1cfda-124">啟動新的容器部署。</span><span class="sxs-lookup"><span data-stu-id="1cfda-124">Start a new container deployment.</span></span> <span data-ttu-id="1cfda-125">例如，hello 下列命令啟動新的部署呼叫`mynginx`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="1cfda-126">hello 部署包含三個容器，根據 hello Nginx 網頁伺服器 hello Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="1cfda-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="1cfda-127">請確認正在 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-127">Verify that hello containers are running.</span></span> <span data-ttu-id="1cfda-128">例如，如果您查詢的 hello 容器`kubectl get pods`，您會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="1cfda-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![取得 Nginx 容器](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="1cfda-130">tooconfigure hello 負載平衡器 tooaccept 外部流量 toohello 部署，執行`kubectl expose`與`--type=LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="1cfda-131">hello 下列命令會公開連接埠 80 上的 hello Nginx 伺服器：</span><span class="sxs-lookup"><span data-stu-id="1cfda-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="1cfda-132">型別`kubectl get svc`toosee hello hello 叢集中的 hello 服務狀態。</span><span class="sxs-lookup"><span data-stu-id="1cfda-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="1cfda-133">雖然 hello 負載平衡器設定 hello 規則 hello `EXTERNAL-IP` hello 的服務，會顯示為`<pending>`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="1cfda-134">請稍候幾分鐘設定 hello 外部 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="1cfda-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="1cfda-136">請確認您可以存取位於 hello 外部 IP 位址的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="1cfda-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="1cfda-137">例如，開啟所顯示的網頁瀏覽器 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1cfda-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="1cfda-138">hello 瀏覽器會顯示執行其中 hello 容器中的 hello Nginx 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="1cfda-139">或者，執行的 hello`curl`或`wget`命令。</span><span class="sxs-lookup"><span data-stu-id="1cfda-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="1cfda-140">例如：</span><span class="sxs-lookup"><span data-stu-id="1cfda-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="1cfda-141">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="1cfda-141">You should see output similar to:</span></span>

    ![使用 curl 存取 Nginx](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="1cfda-143">hello Azure 負載平衡器，請移 toohello toosee hello 組態[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1cfda-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="1cfda-144">瀏覽的容器服務叢集中的 hello 資源群組，然後選取 hello hello 代理程式 Vm 的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="1cfda-145">其名稱應該 hello 與 hello 容器服務相同。</span><span class="sxs-lookup"><span data-stu-id="1cfda-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="1cfda-146">(不選擇 hello hello 主要節點的負載平衡器，其名稱包含一個 hello **master lb**。)</span><span class="sxs-lookup"><span data-stu-id="1cfda-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![資源群組中的負載平衡器](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="1cfda-148">toosee hello 詳細資料的 hello 負載平衡器組態，按一下**負載平衡規則**和 hello hello 規則的設定名稱。</span><span class="sxs-lookup"><span data-stu-id="1cfda-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![負載平衡器規則](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="1cfda-150">範例： 指定`type: LoadBalancer`hello 服務組態檔中</span><span class="sxs-lookup"><span data-stu-id="1cfda-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="1cfda-151">如果您部署 Kubernetes 容器應用程式從 YAML 或 JSON[服務組態檔](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file)，加入下列行 toohello 服務規格的 hello 來指定外部負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="1cfda-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="1cfda-152">hello 下列步驟使用 hello Kubernetes[訪客簿範例](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook)。</span><span class="sxs-lookup"><span data-stu-id="1cfda-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="1cfda-153">此範例是以 Redis 和 PHP Docker 映像為基礎的多層式 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1cfda-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="1cfda-154">您可以在 hello 服務組態檔中指定該 hello 前端 PHP 伺服器使用 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="1cfda-155">下載 hello 檔案`guestbook-all-in-one.yaml`從[GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one)。</span><span class="sxs-lookup"><span data-stu-id="1cfda-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="1cfda-156">瀏覽 hello `spec` hello`frontend`服務。</span><span class="sxs-lookup"><span data-stu-id="1cfda-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="1cfda-157">Hello 行取消註解`type: LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![服務組態中的負載平衡器](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="1cfda-159">儲存 hello 檔案，並部署 hello 應用程式藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1cfda-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="1cfda-160">型別`kubectl get svc`toosee hello hello 叢集中的 hello 服務狀態。</span><span class="sxs-lookup"><span data-stu-id="1cfda-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="1cfda-161">雖然 hello 負載平衡器設定 hello 規則 hello`EXTERNAL-IP`的 hello`frontend`服務會顯示為`<pending>`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="1cfda-162">請稍候幾分鐘設定 hello 外部 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="1cfda-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="1cfda-164">請確認您可以存取位於 hello 外部 IP 位址的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="1cfda-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="1cfda-165">例如，您可以開啟網頁瀏覽器 toohello 外部 IP 位址的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="1cfda-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![外部存取訪客留言](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="1cfda-167">您可以加入訪客留言項目。</span><span class="sxs-lookup"><span data-stu-id="1cfda-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="1cfda-168">hello Azure 負載平衡器，瀏覽 hello 中的 hello 叢集 hello 負載平衡器資源 toosee hello 組態[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1cfda-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1cfda-169">請參閱 hello hello 前一個範例中的步驟。</span><span class="sxs-lookup"><span data-stu-id="1cfda-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="1cfda-170">考量</span><span class="sxs-lookup"><span data-stu-id="1cfda-170">Considerations</span></span>

* <span data-ttu-id="1cfda-171">Hello 負載平衡器規則的建立會以非同步方式時發生，並且在 hello 服務會發行有關佈建的 hello 平衡器資訊`status.loadBalancer`欄位。</span><span class="sxs-lookup"><span data-stu-id="1cfda-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="1cfda-172">每個服務會自動指派自己 hello 負載平衡器中的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1cfda-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="1cfda-173">如果您想 tooreach hello 負載平衡器 DNS 名稱時，使用您的網域服務提供者 toocreate hello 規則的 IP 位址的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1cfda-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="1cfda-174">HTTP 或 HTTPS 流量</span><span class="sxs-lookup"><span data-stu-id="1cfda-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="1cfda-175">tooload 平衡 HTTP 或 HTTPS 流量 toocontainer web 應用程式和管理的傳輸層安全性 (TLS) 憑證，您可以使用 hello Kubernetes[輸入](https://kubernetes.io/docs/user-guide/ingress/)資源。</span><span class="sxs-lookup"><span data-stu-id="1cfda-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="1cfda-176">輸入是規則以允許傳入的連接 tooreach hello 叢集服務的集合。</span><span class="sxs-lookup"><span data-stu-id="1cfda-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="1cfda-177">輸入資源 toowork，hello Kubernetes 叢集必須有[輸入控制器](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers)執行。</span><span class="sxs-lookup"><span data-stu-id="1cfda-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="1cfda-178">Azure Container Service 不會自動實作 Kubernetes 輸入控制器。</span><span class="sxs-lookup"><span data-stu-id="1cfda-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="1cfda-179">有數個控制器實作可供使用。</span><span class="sxs-lookup"><span data-stu-id="1cfda-179">Several controller implementations are available.</span></span> <span data-ttu-id="1cfda-180">目前，hello [Nginx 輸入控制器](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx)建議 tooconfigure 輸入規則和負載平衡 HTTP 及 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="1cfda-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="1cfda-181">如需詳細資訊，請參閱 hello [Nginx 輸入控制器文件集](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md)。</span><span class="sxs-lookup"><span data-stu-id="1cfda-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cfda-182">當 Azure 容器服務中使用 hello Nginx 輸入控制站，您必須公開 hello 控制站部署成與服務`type: LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="1cfda-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="1cfda-183">這會設定 hello Azure 負載平衡器 tooroute 流量 toohello 控制站。</span><span class="sxs-lookup"><span data-stu-id="1cfda-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="1cfda-184">如需詳細資訊，請參閱 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="1cfda-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1cfda-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1cfda-185">Next steps</span></span>

* <span data-ttu-id="1cfda-186">請參閱 hello [Kubernetes 負載平衡器文件](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="1cfda-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="1cfda-187">深入了解 [Kubernetes 輸入和輸入控制器 (英文)](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="1cfda-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="1cfda-188">請參閱 [Kubernetes 範例 (英文)](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="1cfda-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

