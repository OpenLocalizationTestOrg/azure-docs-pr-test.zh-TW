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
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>使用 Operations Management Suite 監視 Kubernetes 叢集

監視 Kubernetes 叢集和容器很重要，尤其在您使用多個應用程式大規模管理生產叢集時。 

您可以利用來自 Microsoft 或其他提供者的數個 Kubernetes 監視解決方案。 在本教學課程中，您必須監視 Kubernetes 叢集使用中的 hello 容器解決方案[Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md)，Microsoft 的雲端 IT 管理解決方案。 （hello OMS 容器解決方案是在預覽中）。

本教學課程部份七 7，涵蓋下列工作的 hello:

> [!div class="checklist"]
> * 取得 OMS 工作區設定
> * Hello Kubernetes 節點上的 OMS 代理程式設定
> * 監視 hello OMS 入口網站或 Azure 入口網站中的資訊的存取

## <a name="before-you-begin"></a>開始之前

在上一個教學課程中，應用程式封裝成容器映像，這些映像上載 tooAzure 容器登錄中，並建立 Kubernetes 叢集。 如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。 

本教學課程至少需要含有 Linux 代理程式節點的 Kubernetes 叢集，以及 Operations Management Suite (OMS) 帳戶。 如有需要，請註冊[免費試用 OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。

## <a name="get-workspace-settings"></a>取得工作區設定

當您可以存取 hello [OMS 入口網站](https://mms.microsoft.com)，跳過**設定** > **連線來源** > **Linux 伺服器**. 您可以在該處找到 hello*工作區識別碼*和主要或次要*工作區金鑰*。 請注意，這些值，您需要 tooset 向上 hello 叢集上的 OMS 代理程式。

## <a name="set-up-oms-agents"></a>設定 OMS 代理程式

以下是 YAML 檔案 tooset 向上 hello Linux 叢集節點上的 OMS 代理程式。 它會建立 Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)，以在每個叢集節點上執行單一相同的 pod。 hello DaemonSet 資源非常適用於部署監視代理程式。 

儲存下列文字 tooa 檔名為 hello `oms-daemonset.yaml`，並取代為 hello 預留位置值*myWorkspaceID*和*myWorkspaceKey*與您的 OMS 工作區識別碼及金鑰。 (在生產環境中，您可以將這些值編碼為秘密)。

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

建立 hello DaemonSet 以 hello 下列命令：

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee DaemonSet 建立時，該 hello 執行：

```azurecli-interactive
kubectl get daemonset
```

輸出是類似 toohello 下列：

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Hello 代理程式執行之後，請花幾分鐘的時間 OMS tooingest 和處理序 hello 資料。

## <a name="access-monitoring-data"></a>存取監視資料

檢視及分析 hello OMS 容器監視資料與 hello[容器解決方案](../../log-analytics/log-analytics-containers.md)hello OMS 入口網站或 hello Azure 入口網站中。 

使用 hello tooinstall hello 容器解決方案[OMS 入口網站](https://mms.microsoft.com)，跳過**解決方案資源庫**。 然後新增 [Container 解決方案]。 或者，新增 hello 容器解決方案從 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview)。

在 hello OMS 入口網站中，尋找**容器**hello OMS 儀表板上的摘要磚。 按一下 hello 磚，如需詳細資訊，包括： 容器事件、 錯誤、 狀態、 映像的清查，以及 CPU 和記憶體使用量。 如需更細微的資訊，請按一下任何圖格上的資料列，或執行[記錄搜尋](../../log-analytics/log-analytics-log-searches.md)。

![OMS 入口網站中的 Containers 儀表板](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

同樣地，在 hello Azure 入口網站，請移過**記錄分析**並選取您的工作區名稱。 toosee hello**容器**摘要磚中，按一下 **解決方案** > **容器**。 toosee 的詳細資訊，按一下 hello 磚。

請參閱 hello [Azure Log Analytics 文件](../../log-analytics/index.md)如查詢及分析監視資料的詳細指引。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用 OMS 監視 Kubernetes 叢集。 涵蓋的工作包括：

> [!div class="checklist"]
> * 取得 OMS 工作區設定
> * Hello Kubernetes 節點上的 OMS 代理程式設定
> * 監視 hello OMS 入口網站或 Azure 入口網站中的資訊的存取


請依照此連結 toosee，預先建立的容器服務的指令碼範例。

> [!div class="nextstepaction"]
> [Azure Container Service 指令碼範例](cli-samples.md)
