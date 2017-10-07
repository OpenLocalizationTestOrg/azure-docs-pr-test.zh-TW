---
title: "aaaAzure 容器服務教學課程-監視器 Kubernetes |Microsoft 文件"
description: "Azure Container Service 教學課程 - 使用 Microsoft Operations Management Suite (OMS) 監視 Kubernetes"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="46654-104">使用 Operations Management Suite 監視 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="46654-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="46654-105">監視 Kubernetes 叢集和容器很重要，尤其在您使用多個應用程式大規模管理生產叢集時。</span><span class="sxs-lookup"><span data-stu-id="46654-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="46654-106">您可以利用來自 Microsoft 或其他提供者的數個 Kubernetes 監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="46654-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="46654-107">在本教學課程中，您必須監視 Kubernetes 叢集使用中的 hello 容器解決方案[Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md)，Microsoft 的雲端 IT 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="46654-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="46654-108">（hello OMS 容器解決方案是在預覽中）。</span><span class="sxs-lookup"><span data-stu-id="46654-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="46654-109">本教學課程部份七 7，涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="46654-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46654-110">取得 OMS 工作區設定</span><span class="sxs-lookup"><span data-stu-id="46654-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="46654-111">Hello Kubernetes 節點上的 OMS 代理程式設定</span><span class="sxs-lookup"><span data-stu-id="46654-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="46654-112">監視 hello OMS 入口網站或 Azure 入口網站中的資訊的存取</span><span class="sxs-lookup"><span data-stu-id="46654-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="46654-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="46654-113">Before you begin</span></span>

<span data-ttu-id="46654-114">在上一個教學課程中，應用程式封裝成容器映像，這些映像上載 tooAzure 容器登錄中，並建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="46654-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="46654-115">如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="46654-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="46654-116">本教學課程至少需要含有 Linux 代理程式節點的 Kubernetes 叢集，以及 Operations Management Suite (OMS) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="46654-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="46654-117">如有需要，請註冊[免費試用 OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。</span><span class="sxs-lookup"><span data-stu-id="46654-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="46654-118">取得工作區設定</span><span class="sxs-lookup"><span data-stu-id="46654-118">Get Workspace settings</span></span>

<span data-ttu-id="46654-119">當您可以存取 hello [OMS 入口網站](https://mms.microsoft.com)，跳過**設定** > **連線來源** > **Linux 伺服器**.</span><span class="sxs-lookup"><span data-stu-id="46654-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="46654-120">您可以在該處找到 hello*工作區識別碼*和主要或次要*工作區金鑰*。</span><span class="sxs-lookup"><span data-stu-id="46654-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="46654-121">請注意，這些值，您需要 tooset 向上 hello 叢集上的 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="46654-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="46654-122">設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="46654-122">Set up OMS agents</span></span>

<span data-ttu-id="46654-123">以下是 YAML 檔案 tooset 向上 hello Linux 叢集節點上的 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="46654-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="46654-124">它會建立 Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)，以在每個叢集節點上執行單一相同的 pod。</span><span class="sxs-lookup"><span data-stu-id="46654-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="46654-125">hello DaemonSet 資源非常適用於部署監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="46654-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="46654-126">儲存下列文字 tooa 檔名為 hello `oms-daemonset.yaml`，並取代為 hello 預留位置值*myWorkspaceID*和*myWorkspaceKey*與您的 OMS 工作區識別碼及金鑰。</span><span class="sxs-lookup"><span data-stu-id="46654-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="46654-127">(在生產環境中，您可以將這些值編碼為秘密)。</span><span class="sxs-lookup"><span data-stu-id="46654-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="46654-128">建立 hello DaemonSet 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="46654-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="46654-129">toosee DaemonSet 建立時，該 hello 執行：</span><span class="sxs-lookup"><span data-stu-id="46654-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="46654-130">輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="46654-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="46654-131">Hello 代理程式執行之後，請花幾分鐘的時間 OMS tooingest 和處理序 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="46654-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="46654-132">存取監視資料</span><span class="sxs-lookup"><span data-stu-id="46654-132">Access monitoring data</span></span>

<span data-ttu-id="46654-133">檢視及分析 hello OMS 容器監視資料與 hello[容器解決方案](../../log-analytics/log-analytics-containers.md)hello OMS 入口網站或 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="46654-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="46654-134">使用 hello tooinstall hello 容器解決方案[OMS 入口網站](https://mms.microsoft.com)，跳過**解決方案資源庫**。</span><span class="sxs-lookup"><span data-stu-id="46654-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="46654-135">然後新增 [Container 解決方案]。</span><span class="sxs-lookup"><span data-stu-id="46654-135">Then add **Container Solution**.</span></span> <span data-ttu-id="46654-136">或者，新增 hello 容器解決方案從 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview)。</span><span class="sxs-lookup"><span data-stu-id="46654-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="46654-137">在 hello OMS 入口網站中，尋找**容器**hello OMS 儀表板上的摘要磚。</span><span class="sxs-lookup"><span data-stu-id="46654-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="46654-138">按一下 hello 磚，如需詳細資訊，包括： 容器事件、 錯誤、 狀態、 映像的清查，以及 CPU 和記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="46654-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="46654-139">如需更細微的資訊，請按一下任何圖格上的資料列，或執行[記錄搜尋](../../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="46654-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![OMS 入口網站中的 Containers 儀表板](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="46654-141">同樣地，在 hello Azure 入口網站，請移過**記錄分析**並選取您的工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="46654-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="46654-142">toosee hello**容器**摘要磚中，按一下 **解決方案** > **容器**。</span><span class="sxs-lookup"><span data-stu-id="46654-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="46654-143">toosee 的詳細資訊，按一下 hello 磚。</span><span class="sxs-lookup"><span data-stu-id="46654-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="46654-144">請參閱 hello [Azure Log Analytics 文件](../../log-analytics/index.md)如查詢及分析監視資料的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="46654-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46654-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46654-145">Next steps</span></span>

<span data-ttu-id="46654-146">在本教學課程中，您已使用 OMS 監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="46654-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="46654-147">涵蓋的工作包括：</span><span class="sxs-lookup"><span data-stu-id="46654-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46654-148">取得 OMS 工作區設定</span><span class="sxs-lookup"><span data-stu-id="46654-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="46654-149">Hello Kubernetes 節點上的 OMS 代理程式設定</span><span class="sxs-lookup"><span data-stu-id="46654-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="46654-150">監視 hello OMS 入口網站或 Azure 入口網站中的資訊的存取</span><span class="sxs-lookup"><span data-stu-id="46654-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="46654-151">請依照此連結 toosee，預先建立的容器服務的指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="46654-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46654-152">Azure Container Service 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="46654-152">Azure Container Service script samples</span></span>](cli-samples.md)
