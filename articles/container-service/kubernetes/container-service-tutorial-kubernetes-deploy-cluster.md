---
title: "aaaAzure 容器服務教學課程-部署叢集 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 部署叢集"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>在 Azure Container Service 中部署 Kubernetes 叢集

Kubernetes 會提供容器化應用程式的分散式平台。 透過 Azure Container Service，可簡單又快速地佈建生產環境就緒 Kubernetes 叢集。 在本教學課程的第 3 和第 7 部分中，已部署一個 Azure Container Service Kubernetes 叢集。 完成的步驟包括：

> [!div class="checklist"]
> * 部署 Kubernetes ACS 叢集
> * Hello Kubernetes CLI (kubectl) 的安裝
> * 設定 kubectl

在後續教學課程中，hello Azure 投票應用程式是部署 toohello 叢集中，縮放，更新，且 Operations Management Suite 設定的 toomonitor hello Kubernetes 叢集。

## <a name="before-you-begin"></a>開始之前

在上一個教學課程中，容器映像建立和上傳 tooan Azure 容器登錄中的執行個體。 如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。

## <a name="create-kubernetes-cluster"></a>建立 Kubernetes 叢集

在 hello[上一個教學課程](./container-service-tutorial-kubernetes-prepare-acr.md)，資源群組名稱*myResourceGroup*所建立。 如果您尚未這樣做，請立即建立此資源群組。

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

在 Azure 容器服務中建立 Kubernetes 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。 

hello 下列範例會建立名為叢集*myK8sCluster*一個 Linux 的主要節點和三個 Linux 代理程式節點。

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

幾分鐘之後，hello 命令完成，並傳回 json 格式化的 hello ACS 部署的相關資訊。

## <a name="install-hello-kubectl-cli"></a>安裝 hello kubectl CLI

從用戶端電腦，使用叢集的 tooconnect toohello Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)，hello Kubernetes 命令列用戶端。 

如果您是使用 Azure CloudShell，就已安裝 `kubectl`。 如果您想 tooinstall 它在本機，使用 hello [az acs kubernetes 安裝 cli](/cli/azure/acs/kubernetes#install-cli)命令。

如果執行 Linux 或 macOS 中，您可能需要具有 sudo toorun。 在 Windows 上，請確定您的殼層已經是以系統管理員身分執行。

```azurecli-interactive 
az acs kubernetes install-cli 
```

在 Windows 中，是預設安裝中 hello *c:\program files (x86)\kubectl.exe*。 您可能需要 tooadd 此檔案 toohello Windows 路徑。 

## <a name="connect-with-kubectl"></a>使用 kubectl 連線

tooconfigure `kubectl` tooconnect tooyour Kubernetes 叢集，請執行 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello 連接 tooyour 叢集，請執行 hello [kubectl 取得節點](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。

```azurecli-interactive
kubectl get nodes
```

輸出：

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

完成教學課程時，您的 ACS Kubernetes 叢集便已可供工作負載使用。 在後續教學課程中，多重容器應用程式是部署的 toothis 叢集時，向外延展、 更新和監視。

## <a name="next-steps"></a>後續步驟

在本教學課程中，已部署一個 Azure Container Service Kubernetes 叢集。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 已部署 Kubernetes ACS 叢集
> * 已安裝的 hello Kubernetes CLI (kubectl)
> * 已設定 kubectl

前進 toohello 下一個教學課程的 toolearn 有關 hello 叢集上執行應用程式。

> [!div class="nextstepaction"]
> [在 Kubernetes 中部署應用程式](./container-service-tutorial-kubernetes-deploy-application.md)
