---
title: "Azure Container Service 教學課程 - 監視 Kubernetes | Microsoft Docs"
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
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="8df06-104">使用 Operations Management Suite 監視 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="8df06-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="8df06-105">監視 Kubernetes 叢集和容器很重要，尤其在您使用多個應用程式大規模管理生產叢集時。</span><span class="sxs-lookup"><span data-stu-id="8df06-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="8df06-106">您可以利用來自 Microsoft 或其他提供者的數個 Kubernetes 監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="8df06-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="8df06-107">在本教學課程中，您會使用 [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md) 中的 Containers 解決方案 (Microsoft 的雲端式 IT 管理解決方案) 來監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="8df06-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="8df06-108">(OMS Containers 解決方案處於預覽狀態。)</span><span class="sxs-lookup"><span data-stu-id="8df06-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="8df06-109">本教學課程 (七個章節的第七部分) 涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="8df06-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8df06-110">取得 OMS 工作區設定</span><span class="sxs-lookup"><span data-stu-id="8df06-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="8df06-111">在 Kubernetes 節點上設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="8df06-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="8df06-112">在 OMS 入口網站或 Azure 入口網站中存取監視資訊</span><span class="sxs-lookup"><span data-stu-id="8df06-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8df06-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="8df06-113">Before you begin</span></span>

<span data-ttu-id="8df06-114">在上一個教學課程中，應用程式已封裝成容器映像、這些映像已上傳至 Azure Container Registry，並已建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="8df06-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="8df06-115">如果您尚未完成這些步驟，而想要跟著做，請回到[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="8df06-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="8df06-116">本教學課程至少需要含有 Linux 代理程式節點的 Kubernetes 叢集，以及 Operations Management Suite (OMS) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8df06-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="8df06-117">如有需要，請註冊[免費試用 OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。</span><span class="sxs-lookup"><span data-stu-id="8df06-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="8df06-118">取得工作區設定</span><span class="sxs-lookup"><span data-stu-id="8df06-118">Get Workspace settings</span></span>

<span data-ttu-id="8df06-119">可以存取 [OMS 入口網站](https://mms.microsoft.com)時，請移至 [設定] >  [已連線的服務] >  [Linux 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="8df06-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="8df06-120">您可以在那裡找到「工作區識別碼」和主要或次要「工作區金鑰」。</span><span class="sxs-lookup"><span data-stu-id="8df06-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="8df06-121">請記下這些值，您在叢集上設定 OMS 代理程式時需要用到這些值。</span><span class="sxs-lookup"><span data-stu-id="8df06-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="8df06-122">設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="8df06-122">Set up OMS agents</span></span>

<span data-ttu-id="8df06-123">以下是 YAML 檔案，用來在 Linux 叢集節點上設定 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8df06-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="8df06-124">它會建立 Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)，以在每個叢集節點上執行單一相同的 pod。</span><span class="sxs-lookup"><span data-stu-id="8df06-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="8df06-125">DaemonSet 資源非常適合用於部署監視代理程式。</span><span class="sxs-lookup"><span data-stu-id="8df06-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="8df06-126">將下列文字儲存到名為 `oms-daemonset.yaml` 的檔案，並以您的 OMS 工作區識別碼和金鑰取代 myWorkspaceID 和 myWorkspaceKey 的預留位置值。</span><span class="sxs-lookup"><span data-stu-id="8df06-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="8df06-127">(在生產環境中，您可以將這些值編碼為秘密)。</span><span class="sxs-lookup"><span data-stu-id="8df06-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="8df06-128">使用下列命令建立 DaemonSet：</span><span class="sxs-lookup"><span data-stu-id="8df06-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="8df06-129">若要查看是否已建立 DaemonSet，請執行：</span><span class="sxs-lookup"><span data-stu-id="8df06-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="8df06-130">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="8df06-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="8df06-131">執行代理程式之後，OMS 需要幾分鐘的時間來擷取及處理資料。</span><span class="sxs-lookup"><span data-stu-id="8df06-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="8df06-132">存取監視資料</span><span class="sxs-lookup"><span data-stu-id="8df06-132">Access monitoring data</span></span>

<span data-ttu-id="8df06-133">在 OMS 入口網站或 Azure 入口網站中，使用 [Container 解決方案](../../log-analytics/log-analytics-containers.md)來檢視和分析 OMS 容器監視資料。</span><span class="sxs-lookup"><span data-stu-id="8df06-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="8df06-134">若要使用 [OMS 入口網站](https://mms.microsoft.com)安裝 Container 解決方案，請移至**方案庫**。</span><span class="sxs-lookup"><span data-stu-id="8df06-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="8df06-135">然後新增 [Container 解決方案]。</span><span class="sxs-lookup"><span data-stu-id="8df06-135">Then add **Container Solution**.</span></span> <span data-ttu-id="8df06-136">或者，從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview) 新增 Containers 解決方案。</span><span class="sxs-lookup"><span data-stu-id="8df06-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="8df06-137">在 OMS 入口網站中，尋找 OMS 儀表板上的 [Containers] 摘要圖格。</span><span class="sxs-lookup"><span data-stu-id="8df06-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="8df06-138">按一下此圖格以取得下列詳細資訊：容器事件、錯誤、狀態、映像清查，以及 CPU 和記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="8df06-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="8df06-139">如需更細微的資訊，請按一下任何圖格上的資料列，或執行[記錄搜尋](../../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="8df06-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![OMS 入口網站中的 Containers 儀表板](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="8df06-141">同樣地，在 Azure 入口網站中，移至 [Log Analytics] 並選取您的工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="8df06-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="8df06-142">若要查看 [Containers] 摘要圖格，請按一下 [解決方案] > [Containers]。</span><span class="sxs-lookup"><span data-stu-id="8df06-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="8df06-143">若要查看詳細資料，按一下圖格。</span><span class="sxs-lookup"><span data-stu-id="8df06-143">To see details, click the tile.</span></span>

<span data-ttu-id="8df06-144">請參閱 [Azure Log Analytics 文件](../../log-analytics/index.md)，以取得查詢及分析監視資料的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="8df06-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df06-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8df06-145">Next steps</span></span>

<span data-ttu-id="8df06-146">在本教學課程中，您已使用 OMS 監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="8df06-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="8df06-147">涵蓋的工作包括：</span><span class="sxs-lookup"><span data-stu-id="8df06-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8df06-148">取得 OMS 工作區設定</span><span class="sxs-lookup"><span data-stu-id="8df06-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="8df06-149">在 Kubernetes 節點上設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="8df06-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="8df06-150">在 OMS 入口網站或 Azure 入口網站中存取監視資訊</span><span class="sxs-lookup"><span data-stu-id="8df06-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="8df06-151">用以下連結查看針對 Container Service 預先建立的指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="8df06-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8df06-152">Azure Container Service 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="8df06-152">Azure Container Service script samples</span></span>](cli-samples.md)
