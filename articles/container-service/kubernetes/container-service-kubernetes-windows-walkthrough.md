---
title: "aaaQuickstart-適用於 Windows Azure Kubernetes 叢集 |Microsoft 文件"
description: "快速了解 toocreate Kubernetes 叢集以 hello Azure CLI Azure 容器服務中的 Windows 容器。"
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>部署適用於 Windows 容器的 Kubernetes 叢集

hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。 本指南詳細說明使用 hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/)叢集[Azure 容器服務](../container-service-intro.md)。 Hello 叢集部署之後，您與 hello Kubernetes 連接 tooit`kubectl`命令列工具，而且您部署您的第一個 Windows 容器。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

> [!NOTE]
> 支援 Windows 容器在 Azure Container Service 上的 Kubernetes 處於預覽階段。 
>

## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>建立 Kubernetes 叢集
在 Azure 容器服務中建立 Kubernetes 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。 

hello 下列範例會建立名為叢集*myK8sCluster*一個 Linux 的主要節點和兩個 Windows 代理程式節點。 這個範例會建立 SSH 金鑰需要的 tooconnect toohello Linux 主要。 這個範例會使用*azureuser*系統管理使用者名稱和*myPassword12* hello hello Windows 節點上的密碼。 更新這些值 toosomething 適當 tooyour 環境。 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

幾分鐘之後，hello 命令會完成，並顯示您部署的相關資訊。

## <a name="install-kubectl"></a>安裝 kubectl

從用戶端電腦，使用叢集的 tooconnect toohello Kubernetes [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/)，hello Kubernetes 命令列用戶端。 

如果您是使用 Azure CloudShell，就已安裝 `kubectl`。 如果您想 tooinstall 它在本機，您可以使用 hello [az acs kubernetes 安裝 cli](/cli/azure/acs/kubernetes#install-cli)命令。

hello 下列 Azure CLI 範例安裝`kubectl`tooyour 系統。 在 Windows 上，以系統管理員身分執行此命令。

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>使用 kubectl 連線

tooconfigure `kubectl` tooconnect tooyour Kubernetes 叢集，請執行 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。 hello 下列範例會下載 hello Kubernetes 叢集的叢集設定。

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello 連接 tooyour 叢集從您的電腦，再試一次執行：

```azurecli-interactive
kubectl get nodes
```

`kubectl`列出 hello master 和代理程式節點。

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>部署 Windows IIS 容器

您可以在 Kubernetes Pod 內執行 Docker 容器，其中包含一個或多個容器。 

這個基本範例會使用 JSON 檔案 toospecify Microsoft Internet Information Server (IIS) 容器，並接著會建立使用 hello hello pod`kubctl apply`命令。 

建立名為本機檔案`iis.json`和複製 hello 文字之後。 這個檔案會告知 Kubernetes toorun IIS Windows Server 2016 Nano Server 上，使用從公用容器映像[Docker Hub](https://hub.docker.com/r/nanoserver/iis/)。 hello 容器會使用連接埠 80，但一開始只有 hello 叢集網路中存取。

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello pod，類型：
  
```azurecli-interactive
kubectl apply -f iis.json
```  

型別 tootrack hello 部署：
  
```azurecli-interactive
kubectl get pods
```

正在部署的 hello pod，hello 狀態即`ContainerCreating`。 可能需要幾分鐘，讓 hello 容器 tooenter hello`Running`狀態。

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>檢視 hello IIS [歡迎使用] 頁面

tooexpose hello pod toohello 世界公用 IP 位址，下列命令的型別 hello:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Kubernetes 會利用這個命令，建立服務和[Azure 負載平衡器規則](container-service-kubernetes-load-balancing.md)與 hello 服務的公用 IP 位址。 

執行下列命令 toosee hello 狀態 hello 服務的 hello。

```azurecli-interactive
kubectl get svc
```

一開始 hello IP 位址會顯示為`pending`。 請稍候幾分鐘 hello 外部 IP 位址的 hello `iis` pod 設定：
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

您可以使用網頁瀏覽器選擇 toosee hello 預設 IIS 歡迎使用頁面的外部 IP 位址為 hello:

![瀏覽 tooIIS 的映像](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>刪除叢集
當不再需要 hello 叢集時，您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 容器服務，以及所有相關的資源。

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>後續步驟

在本快速入門中，您部署了 Kubernetes 叢集、與 `kubectl` 連線，並使用 IIS 容器部署了 Pod。 進一步了解 Azure 容器服務，toolearn 繼續 toohello Kubernetes 教學課程。

> [!div class="nextstepaction"]
> [管理 ACS Kubernetes 叢集](container-service-tutorial-kubernetes-prepare-app.md)
