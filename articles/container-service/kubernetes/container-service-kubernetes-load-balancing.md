---
title: "針對 Azure 中的 Kubernetes 容器進行負載平衡 | Microsoft Docs"
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
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="6ddc4-104">在 Azure Container Service 中針對 Kubernetes 叢集內的容器進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="6ddc4-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="6ddc4-105">本文將介紹在 Azure Container Service 中 Kubernetes 叢集內進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="6ddc4-106">負載平衡提供服務可供外部存取的 IP 位址，並將網路流量分散於代理程式 VM 中執行的 Pod 之間。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="6ddc4-107">您可以設定 Kubernetes 服務使用 [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) 來管理外部網路 (TCP) 流量。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="6ddc4-108">透過其他設定，便可以達成 HTTP 或 HTTPS 流量 (或更進階的案例) 的負載平衡和路由。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ddc4-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6ddc4-109">Prerequisites</span></span>
* <span data-ttu-id="6ddc4-110">在 Azure Container Service 中[部署 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="6ddc4-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="6ddc4-111">[將您的用戶端連接到](../container-service-connect.md)您的叢集</span><span class="sxs-lookup"><span data-stu-id="6ddc4-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="6ddc4-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6ddc4-112">Azure load balancer</span></span>

<span data-ttu-id="6ddc4-113">根據預設，在 Azure Container Service 中部署的 Kubernetes 叢集包含代理程式 VM 的網際網路對應 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="6ddc4-114">(將針對主要 VM 設定個別的負載平衡器資源)。Azure Load Balancer 是第 4 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="6ddc4-115">目前，負載平衡器只支援 Kubernetes 中的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="6ddc4-116">建立 Kubernetes 服務時，您可以自動設定 Azure Load Balancer 允許存取服務。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="6ddc4-117">若要設定負載平衡器，請將服務 `type` 設定為 `LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="6ddc4-118">負載平衡器會建立一個規則，將連入服務流量的公用 IP 位址和連接埠號碼對應到代理程式 VM 中 Pod 的私人 IP 位址和連接埠號碼 (回應流量反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="6ddc4-119">下列兩個範例顯示如何將 Kubernetes 服務 `type` 設定為 `LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="6ddc4-120">(嘗試這些範例之後，如果您不再需要它們，請刪除部署)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="6ddc4-121">範例︰使用 `kubectl expose` 命令</span><span class="sxs-lookup"><span data-stu-id="6ddc4-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="6ddc4-122">[Kubernetes 逐步解說](container-service-kubernetes-walkthrough.md)包含如何使用 `kubectl expose` 命令與其 `--type=LoadBalancer` 旗標公開服務的範例。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="6ddc4-123">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-123">Here are the steps :</span></span>

1. <span data-ttu-id="6ddc4-124">啟動新的容器部署。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-124">Start a new container deployment.</span></span> <span data-ttu-id="6ddc4-125">例如，下列命令會啟動稱為 `mynginx` 的新部署。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="6ddc4-126">部署會包含三個以 Nginx Web 伺服器的 Docker 映像為基礎的容器。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="6ddc4-127">確認容器正在執行。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-127">Verify that the containers are running.</span></span> <span data-ttu-id="6ddc4-128">例如，如果您使用 `kubectl get pods` 查詢容器，您會看到類似下列的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![取得 Nginx 容器](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="6ddc4-130">若要設定負載平衡器以接受部署的外部流量，請搭配 `--type=LoadBalancer` 執行 `kubectl expose`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="6ddc4-131">下列命令會在連接埠 80 上公開 Nginx 伺服器：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="6ddc4-132">輸入 `kubectl get svc` 以查看叢集中服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="6ddc4-133">負載平衡器設定規則時，服務的 `EXTERNAL-IP` 會顯示為 `<pending>`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="6ddc4-134">幾分鐘之後，外部 IP 位址會完成設定：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-134">After a few minutes, the external IP address is configured:</span></span> 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="6ddc4-136">確認您可以在外部 IP 位址存取服務。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="6ddc4-137">例如，開啟網頁瀏覽器並前往顯示的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="6ddc4-138">瀏覽器會顯示 Nginx Web 伺服器正在其中一個容器中執行。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="6ddc4-139">或者，執行 `curl` 或 `wget` 命令。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="6ddc4-140">例如：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="6ddc4-141">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-141">You should see output similar to:</span></span>

    ![使用 curl 存取 Nginx](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="6ddc4-143">若要查看 Azure Load Balancer 的組態，請移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="6ddc4-144">瀏覽您容器服務叢集的資源群組，並選取代理程式 VM 的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="6ddc4-145">其名稱應該與容器服務相同。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="6ddc4-146">(請勿選擇主要節點的負載平衡器。主要節點就是名稱包含 **master-lb** 的節點)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![資源群組中的負載平衡器](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="6ddc4-148">若要查看負載平衡器組態的詳細資訊，請按一下 [負載平衡規則] 和已設定規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![負載平衡器規則](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="6ddc4-150">範例︰在服務組態檔中指定 `type: LoadBalancer`</span><span class="sxs-lookup"><span data-stu-id="6ddc4-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="6ddc4-151">如果您從 YAML 或 JSON [服務組態檔 (英文)](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file)部署 Kubernetes 容器應用程式，請透過將下列一行加入至服務規格中，以指定外部負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="6ddc4-152">下列步驟使用 Kubernetes [訪客留言範例 (英文)](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="6ddc4-153">此範例是以 Redis 和 PHP Docker 映像為基礎的多層式 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="6ddc4-154">您可以在服務組態檔中指定前端 PHP 伺服器使用 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="6ddc4-155">從 [GitHub (英文)](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one) 下載檔案 `guestbook-all-in-one.yaml`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="6ddc4-156">瀏覽 `frontend` 服務的 `spec`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="6ddc4-157">取消註解行 `type: LoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![服務組態中的負載平衡器](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="6ddc4-159">儲存檔案，並執行下列命令以部署應用程式︰</span><span class="sxs-lookup"><span data-stu-id="6ddc4-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="6ddc4-160">輸入 `kubectl get svc` 以查看叢集中服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="6ddc4-161">負載平衡器設定規則時，`frontend` 服務的 `EXTERNAL-IP` 會顯示為 `<pending>`。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="6ddc4-162">幾分鐘之後，外部 IP 位址會完成設定：</span><span class="sxs-lookup"><span data-stu-id="6ddc4-162">After a few minutes, the external IP address is configured:</span></span> 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="6ddc4-164">確認您可以在外部 IP 位址存取服務。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="6ddc4-165">例如，您可以開啟網頁瀏覽器並前往服務的外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![外部存取訪客留言](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="6ddc4-167">您可以加入訪客留言項目。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="6ddc4-168">若要查看 Azure Load Balancer 的組態，請瀏覽 [Azure 入口網站](https://portal.azure.com)中叢集的負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6ddc4-169">請參閱前一個範例中的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="6ddc4-170">考量</span><span class="sxs-lookup"><span data-stu-id="6ddc4-170">Considerations</span></span>

* <span data-ttu-id="6ddc4-171">負載平衡器規則會以非同步的方式建立，且已佈建之平衡器的相關資訊會在服務的 `status.loadBalancer` 欄位中發行。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="6ddc4-172">每個服務都會在負載平衡器中被自動指定屬於自己的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="6ddc4-173">如果您想要透過 DNS 名稱來連絡負載平衡器，請與您的網域服務提供者合作建立規則之 IP 位址的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="6ddc4-174">HTTP 或 HTTPS 流量</span><span class="sxs-lookup"><span data-stu-id="6ddc4-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="6ddc4-175">若要將 HTTP 或 HTTPS 流量負載平衡到容器 Web 應用程式，並管理傳輸層安全性 (TLS) 的憑證，您可以使用 Kubernetes [輸入 (英文)](https://kubernetes.io/docs/user-guide/ingress/) 資源。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="6ddc4-176">輸入是允許傳入連線連絡叢集服務的規則集合。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="6ddc4-177">若要使輸入資源順利運作，Kubernetes 叢集必須具備執行中的[輸入控制器 (英文)](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="6ddc4-178">Azure Container Service 不會自動實作 Kubernetes 輸入控制器。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="6ddc4-179">有數個控制器實作可供使用。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-179">Several controller implementations are available.</span></span> <span data-ttu-id="6ddc4-180">目前，建議您使用 [Nginx 輸入控制器 (英文)](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) 來設定輸入規則，並針對 HTTP 與 HTTPS 流量進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="6ddc4-181">如需詳細資訊，請參閱 [Nginx 輸入控制器文件集 (英文)](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md)。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ddc4-182">在 Azure Container Service 中使用 Nginx 輸入控制器時，您必須使用 `type: LoadBalancer` 將控制器部署公開為服務。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="6ddc4-183">這會設定 Azure Load Balancer 將流量路由傳送到控制器。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="6ddc4-184">如需詳細資訊，請參閱上一節。</span><span class="sxs-lookup"><span data-stu-id="6ddc4-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6ddc4-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ddc4-185">Next steps</span></span>

* <span data-ttu-id="6ddc4-186">請參閱 [Kubernetes LoadBalancer 文件集 (英文)](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="6ddc4-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="6ddc4-187">深入了解 [Kubernetes 輸入和輸入控制器 (英文)](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="6ddc4-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="6ddc4-188">請參閱 [Kubernetes 範例 (英文)](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="6ddc4-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

