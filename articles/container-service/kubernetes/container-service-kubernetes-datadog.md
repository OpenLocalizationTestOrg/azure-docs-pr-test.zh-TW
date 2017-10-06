---
title: "aaaMonitor Datadog 叢集 Azure Kubernetes |Microsoft 文件"
description: "使用 Datadog 監視 Azure Container Service 中的 Kubernetes 叢集"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>使用 DataDog 監視 Azure Container Service 叢集

## <a name="prerequisites"></a>必要條件
本逐步解說假設您已[使用 Azure Container Service 建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)。

它也假設您擁有 hello `az` Azure cli 和`kubectl`安裝工具。

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

## <a name="datadog"></a>DataDog
Datadog 是一項監視服務，會從 Azure 容器服務叢集內的容器收集監視資料。 Datadog 有 Docker 整合儀表板，可供您查看容器內的特定度量。 從容器收集到的度量會依 CPU、記憶體、網路和 I/O 來加以整理。 Datadog 會將度量分割成容器和映像。

您必須先太[建立帳戶](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>安裝 DaemonSet hello Datadog 代理程式
DaemonSets 所使用的 Kubernetes toorun hello 叢集中各主機上的容器的單一執行個體。
它們非常適合用來執行監視代理程式。

一旦您登入 Datadog，您可以依照 hello [Datadog 指示](https://app.datadoghq.com/account/settings#agent/kubernetes)tooinstall Datadog 代理程式使用 DaemonSet 在叢集上的。

## <a name="conclusion"></a>結論
就這麼簡單！ 一旦 hello 代理程式已啟動並執行您應該會看到 hello 主控台中的資料在幾分鐘的時間。 您可以瀏覽 hello 整合[kubernetes 儀表板](https://app.datadoghq.com/screen/integration/kubernetes)toosee 叢集的摘要。
