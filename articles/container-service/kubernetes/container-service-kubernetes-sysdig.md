---
title: "aaaMonitor Azure Kubernetes 叢集 Sysdig |Microsoft 文件"
description: "使用 Sysdig 監視 Azure Container Service 中的 Kubernetes 叢集"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>使用 Sysdig 監視 Azure Container Service Kubernetes 叢集

## <a name="prerequisites"></a>必要條件
本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。

它也假設您已安裝的 hello azure cli 和 kubectl 工具。

您可以測試是否有 hello`az`安裝執行工具：

```console
$ az --version
```

如果您沒有 hello`az`工具安裝，指示[這裡](https://github.com/azure/azure-cli#installation)。

您可以測試是否有 hello`kubectl`安裝執行工具：

```console
$ kubectl version
```

如果您尚未安裝 `kubectl`，可以執行︰

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a>Sysdig
Sysdig 是一家外部監視即服務公司，可監視您在 Azure 中執行的 Kubernetes 叢集中的容器。 使用 Sysdig 需要有效的 Sysdig 帳戶。
您可以在他們的[網站](https://app.sysdigcloud.com)上註冊帳戶。

一旦您登入 toohello Sysdig 雲端網站，按一下您的使用者名稱，然後在 hello 頁面上您應該會看到您的 「 存取金鑰 」。 

![Sysdig API 金鑰](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>安裝 hello Sysdig 代理程式 tooKubernetes
您的容器 Sysdig 上執行的處理序每個機器使用 Kubernetes toomonitor `DaemonSet`。
DaemonSets 是每部機器執行單一容器執行個體的 Kubernetes API 物件。
變更就非常適合用以安裝工具 hello Sysdig 的監視代理程式。

tooinstall hello Sysdig daemonset，您應該先下載[hello 範本](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml)從 sysdig。 將該檔案儲存為 `sysdig-daemonset.yaml`。

在 Linux 與 OS X 上，您可以執行︰

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

在 PowerShell 中：

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

接下來編輯該檔案 tooinsert 您的存取金鑰，您從 Sysdig 帳戶取得。

最後，建立 hello DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>檢視您的監視
一旦安裝並正在執行，hello 代理程式應該提取資料回復 tooSysdig。  返回 toothe [sysdig 儀表板](https://app.sysdigcloud.com)，您應該看到的資訊關於您的容器。

您也可以透過[新的儀表板精靈](https://app.sysdigcloud.com/#/dashboards/new)來安裝 Kubernetes 專用儀表板。
