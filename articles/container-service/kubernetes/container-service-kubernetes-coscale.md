---
title: "aaaMonitor Azure Kubernetes 叢集 CoScale |Microsoft 文件"
description: "使用 CoScale 監視 Azure Container Service 中的 Kubernetes 叢集"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>使用 CoScale 監視 Azure Container Service Kubernetes 叢集

在本文中，我們會示範如何 toodeploy hello [CoScale](https://www.coscale.com/)代理程式 toomonitor Azure 容器服務中的所有節點和容器，在您 Kubernetes 都叢集。 您需要 CoScale 帳戶以進行這項設定。 


## <a name="about-coscale"></a>關於 CoScale 

CoScale 是監視平台，收集數個協調流程平台上所有容器的計量和事件。 CoScale 提供 Kubernetes 環境的全方位監視。 它提供視覺效果和分析 hello 堆疊中的所有圖層： hello OS、 Kubernetes、 Docker 和在您的容器內執行的應用程式。 CoScale 提供數個內建監視儀表板，它有內建的異常偵測 tooallow 運算子和快速開發人員 toofind 基礎結構和應用程式問題。

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

本文所示，您可以安裝代理程式上 Kubernetes 叢集 toorun CoScale 做為 SaaS 解決方案。 如果您希望 tookeep 資料公司，CoScale 也是可在內部部署安裝。


## <a name="prerequisites"></a>必要條件

您必須先太[建立 CoScale 帳戶](https://www.coscale.com/free-trial)。

本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。

它也假設您擁有 hello `az` Azure CLI 和`kubectl`安裝工具。

您可以測試是否有 hello`az`安裝執行工具：

```azurecli
az --version
```

如果您沒有 hello`az`工具安裝，指示[這裡](/cli/azure/install-azure-cli)。

您可以測試是否有 hello`kubectl`安裝執行工具：

```bash
kubectl version
```

如果您尚未安裝 `kubectl`，可以執行︰

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>安裝 DaemonSet hello CoScale 代理程式
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)是 Kubernetes toorun 容器的單一執行個體上使用 hello 叢集中各主機。
它們很適合執行例如 hello CoScale 代理程式監視代理程式。

在您登入 tooCoScale 之後，請繼續 toohello[代理程式 頁面](https://app.coscale.com/)tooinstall CoScale 代理程式使用 DaemonSet 在叢集上的。 hello CoScale UI 提供引導式的組態步驟 toocreate 代理程式，並開始監視完整的 Kubernetes 叢集。

![CoScale 代理程式設定](./media/container-service-kubernetes-coscale/installation.png)

hello 在叢集上，執行命令提供的 hello toostart hello 代理程式：

![啟動 hello CoScale 代理程式](./media/container-service-kubernetes-coscale/agent_script.png)

就這麼簡單！ 一旦 hello 代理程式正在執行，您應該在幾分鐘內看到 hello 主控台中的資料。 請瀏覽 hello[代理程式 頁面](https://app.coscale.com/)toosee 叢集的摘要執行其他設定步驟，並查看儀表板例如 hello **Kubernetes 叢集概觀**。

![Kubernetes 叢集概觀](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

hello CoScale 代理程式會自動部署 hello 叢集中的新電腦上。 hello 代理程式更新的新版本時自動釋放。


## <a name="next-steps"></a>後續步驟

請參閱 hello [CoScale 文件](http://docs.coscale.com/)和[部落格](https://www.coscale.com/blog)如需 CoScale 監視解決方案，更詳細資訊。 

