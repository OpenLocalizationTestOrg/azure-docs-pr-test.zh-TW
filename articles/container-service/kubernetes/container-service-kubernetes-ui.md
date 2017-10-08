---
title: "使用 web UI 的 aaaManage Azure Kubernetes 叢集 |Microsoft 文件"
description: "使用 hello Kubernetes web UI 中 Azure 容器服務"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="055c5-103">使用 hello Kubernetes web UI，使用 Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="055c5-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="055c5-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="055c5-104">Prerequisites</span></span>
<span data-ttu-id="055c5-105">本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="055c5-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="055c5-106">它也假設您擁有 hello Azure CLI 2.0 和`kubectl`安裝工具。</span><span class="sxs-lookup"><span data-stu-id="055c5-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="055c5-107">您可以測試是否有 hello`az`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="055c5-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="055c5-108">如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。</span><span class="sxs-lookup"><span data-stu-id="055c5-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="055c5-109">您可以測試是否有 hello`kubectl`安裝執行工具：</span><span class="sxs-lookup"><span data-stu-id="055c5-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="055c5-110">如果您尚未安裝 `kubectl`，可以執行︰</span><span class="sxs-lookup"><span data-stu-id="055c5-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="055c5-111">概觀</span><span class="sxs-lookup"><span data-stu-id="055c5-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="055c5-112">連接 toohello web UI</span><span class="sxs-lookup"><span data-stu-id="055c5-112">Connect toohello web UI</span></span>
<span data-ttu-id="055c5-113">您可以啟動 hello Kubernetes web UI 執行：</span><span class="sxs-lookup"><span data-stu-id="055c5-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="055c5-114">這應該會開啟網頁瀏覽器設定 tootalk tooa 安全 proxy 連接您的本機電腦 toohello Kubernetes web UI。</span><span class="sxs-lookup"><span data-stu-id="055c5-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="055c5-115">建立和公開服務</span><span class="sxs-lookup"><span data-stu-id="055c5-115">Create and expose a service</span></span>
1. <span data-ttu-id="055c5-116">在 hello Kubernetes web UI，按一下 **建立**hello 上方右視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="055c5-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes Create UI](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="055c5-118">隨即會開啟對話方塊，您可以在其中開始建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="055c5-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="055c5-119">提供給它 hello 名稱`hello-nginx`。</span><span class="sxs-lookup"><span data-stu-id="055c5-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="055c5-120">使用 hello [ `nginx` Docker 容器](https://hub.docker.com/_/nginx/)及部署此 web 服務的三個複本。</span><span class="sxs-lookup"><span data-stu-id="055c5-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Kubernetes Pod 建立對話方塊](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="055c5-122">在 [服務] 之下，選取 [外部] 並輸入連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="055c5-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="055c5-123">這項設定負載平衡流量 toohello 三個複本。</span><span class="sxs-lookup"><span data-stu-id="055c5-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Kubernetes 服務建立對話方塊](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="055c5-125">按一下**部署**toodeploy 這些容器和服務。</span><span class="sxs-lookup"><span data-stu-id="055c5-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Kubernetes 部署](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="055c5-127">檢視您的容器</span><span class="sxs-lookup"><span data-stu-id="055c5-127">View your containers</span></span>
<span data-ttu-id="055c5-128">按一下 之後**部署**，hello UI 顯示的檢視，您的服務部署：</span><span class="sxs-lookup"><span data-stu-id="055c5-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Kubernetes 狀態](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="055c5-130">您可以查看左側 hello 的 ui 中，每個 Kubernetes 物件 hello 圓形中有 hello 狀態下**Pod**。</span><span class="sxs-lookup"><span data-stu-id="055c5-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="055c5-131">如果是部分完整圓形，正在仍會部署 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="055c5-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="055c5-132">完整部署物件時，它會顯示綠色的核取記號︰</span><span class="sxs-lookup"><span data-stu-id="055c5-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes 已部署](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="055c5-134">所有項目開始執行之後，按一下您有關執行 web 服務的 hello 的 pod toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="055c5-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Kubernetes Pods](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="055c5-136">在 hello **Pod**檢視中，您可以看到 hello pod，以及這些容器所使用的 hello CPU 和記憶體資源中的 hello 容器的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="055c5-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes 資源](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="055c5-138">如果您沒有看到 hello 資源，您可能需要 toowait 幾分鐘的時間監視資料 toopropagate hello。</span><span class="sxs-lookup"><span data-stu-id="055c5-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="055c5-139">toosee hello 記錄檔以取得您的容器，按一下**檢視記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="055c5-139">toosee hello logs for your container, click **View logs**.</span></span>

![Kubernetes 記錄檔](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="055c5-141">檢視您的服務</span><span class="sxs-lookup"><span data-stu-id="055c5-141">Viewing your service</span></span>
<span data-ttu-id="055c5-142">在加法 toorunning 您容器 hello Kubernetes UI 已經建立外部`Service`的佈建負載平衡器 toobring 流量 toohello 容器在叢集中。</span><span class="sxs-lookup"><span data-stu-id="055c5-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="055c5-143">在 hello 左側瀏覽窗格中，按一下 **服務**tooview （應該只有一個） 的所有服務。</span><span class="sxs-lookup"><span data-stu-id="055c5-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Kubernetes 服務](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="055c5-145">在該檢視中，您應該會看到已配置 tooyour 服務的外部端點 （IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="055c5-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="055c5-146">如果您按一下該 IP 位址，應該會看到在負載平衡器後方執行的 Nginx 容器。</span><span class="sxs-lookup"><span data-stu-id="055c5-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx 檢視](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="055c5-148">調整您的服務大小</span><span class="sxs-lookup"><span data-stu-id="055c5-148">Resizing your service</span></span>
<span data-ttu-id="055c5-149">在加法 tooviewing 物件在 hello UI，您可以編輯並更新 hello Kubernetes 應用程式開發介面的物件。</span><span class="sxs-lookup"><span data-stu-id="055c5-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="055c5-150">首先，請按一下**部署**hello 左導覽窗格 toosee hello 部署您的服務中。</span><span class="sxs-lookup"><span data-stu-id="055c5-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="055c5-151">一旦您是在該檢視中，按一下 hello 複本集，然後按一下**編輯**hello 上方瀏覽列中：</span><span class="sxs-lookup"><span data-stu-id="055c5-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Kubernetes 編輯](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="055c5-153">編輯 hello`spec.replicas`欄位 toobe `2`，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="055c5-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="055c5-154">這樣 hello 數目複本 toodrop tootwo 刪除您 pod 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="055c5-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

