---
title: "aaaAzure 容器服務教學課程-小數位數的應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 調整應用程式"
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>調整 Kubernetes Pod 和 Kubernetes 基礎結構

如果您已依照已 hello 教學課程，Azure 容器服務中有可運作的 Kubernetes 叢集，而且您已部署的 hello Azure 投票應用程式。 

在本教學課程一部分五 7，您可以擴充 hello 應用程式中的 hello pod，然後再次嘗試 pod 自動調整。 您也了解 Azure VM 代理程式節點 toochange tooscale hello 數目 hello 叢集的容量，以裝載工作負載的方式。 完成的工作包括：

> [!div class="checklist"]
> * 手動調整 Kubernetes Pod
> * 設定自動調整規模 pod 執行 hello 應用程式前端
> * 調整 hello Kubernetes Azure 代理程式節點

在後續教學課程中，hello Azure 投票應用程式會更新，而且 Operations Management Suite 設定 toomonitor hello Kubernetes 叢集。

## <a name="before-you-begin"></a>開始之前

在上一個教學課程中，應用程式封裝成容器映像，此映像上載 tooAzure 容器登錄中，並建立 Kubernetes 叢集。 hello 應用程式然後 hello Kubernetes 叢集上執行。 如果您有未完成這些步驟，並希望沿著 toofollow，傳回 toohello[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。 

本教學課程至少需要一個含有執行中應用程式的 Kubernetes 叢集。

## <a name="manually-scale-pods"></a>手動調整 Pod

到目前為止，hello Azure 投票前端和 Redis 執行個體已部署，每個都有單一複本。 tooverify，執行 hello [kubectl 取得](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。

```azurecli-interactive
kubectl get pods
```

輸出：

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

手動變更 hello 數目在 hello pod`azure-vote-front`部署使用 hello [kubectl 標尺](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale)命令。 這個範例會增加 hello 數字 too5。

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

執行[kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes 建立 hello pod。 約一分鐘之後, 執行的其他 pod 的 hello:

```azurecli-interactive
kubectl get pods
```

輸出：

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>自動調整 Pod

Kubernetes 支援[水平的 pod 自動調整](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)tooadjust hello 數目 pod 根據 CPU 使用率或其他部署中選取的度量。 

toouse hello autoscaler，CPU 要求與定義的限制，必須具有您 pod。 在 hello`azure-vote-front`部署 hello 前端容器要求 0.25 CPU，且長度限制為 0.5 的 CPU。 hello 設定如下：

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

hello 下列範例會使用 hello [kubectl 自動調整規模](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale)命令 tooautoscale hello 數目在 hello pod`azure-vote-front`部署。 在這裡，如果 CPU 使用率超過 50%，hello autoscaler 會增加 hello pod tooa 最多 10 個。


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

hello autoscaler，執行下列命令的 hello toosee hello 狀態：

```azurecli-interactive
kubectl get hpa
```

輸出：

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

請稍候幾分鐘，且最負載 hello Azure 投票應用程式，hello pod 複本的數目會自動減少 too3。

## <a name="scale-hello-agents"></a>標尺 hello 代理程式

如果您建立使用 hello 上一個教學課程中的預設指令 Kubernetes 叢集時，它會有三個代理程式節點。 如果您計劃您的叢集更多或較少的容器工作負載，您可以手動調整 hello 代理程式數目。 使用 hello [az acs 調整](/cli/azure/acs#scale)命令，然後指定代理程式的 hello 數目以 hello`--new-agent-count`參數。

hello 下列範例會增加 hello 數目名為 hello Kubernetes 叢集中的代理程式節點 too4 *myK8sCluster*。 hello 命令會使用幾個分鐘 toocomplete。

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

hello 命令輸出會顯示代理程式的 hello 號碼節點中的 hello 值`agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已在 Kubernetes 叢集中使用不同的調整功能。 涵蓋的工作包括：

> [!div class="checklist"]
> * 手動調整 Kubernetes Pod
> * 設定自動調整規模 pod 執行 hello 應用程式前端
> * 調整 hello Kubernetes Azure 代理程式節點

前進 toohello 下一個教學課程的 toolearn 有關更新中 Kubernetes 應用程式。

> [!div class="nextstepaction"]
> [更新 Kubernetes 中的應用程式](./container-service-tutorial-kubernetes-app-update.md)

