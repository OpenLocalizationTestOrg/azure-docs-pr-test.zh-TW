---
title: "在 Azure 雲端中裝載的 aaaDocker 容器 |Microsoft 文件"
description: "Azure 容器服務提供方式 toosimplify hello 建立、 設定及管理叢集的虛擬機器會預先設定的 toorun 容器化應用程式。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a>裝載 Azure 容器服務方案的簡介 tooDocker 容器 
Azure 容器服務簡化了 toocreate、 設定和管理所預先設定的 toorun 容器化應用程式的虛擬機器的叢集。 它使用受歡迎開放原始碼排程和協調流程工具的最佳化組態。 這可讓您 toouse 您現有的技術，或運用社群專業知識，toodeploy 大量且不斷主體和管理容器應用程式在 Microsoft Azure 上。

![Azure 容器服務在 Azure 上的多個主機上，toomanage 容器化應用程式將提供的方法。](./media/acs-intro/acs-cluster-new.png)

Azure 容器服務會利用您的應用程式容器是完全可攜 hello Docker 容器格式 tooensure。 它也支援您所選擇的馬拉松和 DC/OS、 Docker Swarm，或 Kubernetes，以便您可以調整的容器，這些應用程式 toothousands 或甚至數以萬計。

藉由使用 Azure 容器服務，您可以利用企業級功能的 Azure，同時仍維持應用程式可攜性-包括 hello 協調流程層級的可攜性。

## <a name="using-azure-container-service"></a>使用 Azure 容器服務
我們使用 Azure 容器服務的目標是使用開放原始碼工具和技術，現在都可以在我們的客戶之間的熱門 tooprovide 容器主機環境。 toothis 結束時，就會公開 hello 標準應用程式開發介面端點如您所選擇的 orchestrator （DC/OS，Docker Swarm，或 Kubernetes）。 藉由使用這些端點，您可以利用能夠 toothose 端點進行交談的任何軟體。 例如，在 hello Docker Swarm 端點的 hello 情況下，您可能會選擇 toouse hello Docker 命令列介面 (CLI)。 DC/作業系統，您可能會選擇 hello DCOS CLI。 若為 Kubernetes，您可以選擇 `kubectl`。

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>使用 Azure Container Service 建立 Docker 叢集
toobegin 使用 Azure 容器服務，您部署 Azure 容器服務叢集透過 hello 入口網站 (搜尋 hello Marketplace 的**Azure 容器服務**)，使用 Azure Resource Manager 範本 ([Docker廣域](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)， [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)，或[Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes))，或以 hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)。 hello 提供快速入門範本可以修改的 tooinclude 額外或進階 Azure 組態。 如需詳細資訊，請參閱[部署 Azure Container Service 叢集](container-service-deployment.md)。

## <a name="deploying-an-application"></a>部署應用程式
Azure Container Service 提供協調流程的選擇：Docker Swarm 、DC/OS 或 Kubernetes。 部署應用程式的方式取決於您所選擇的 Orchestrator。

### <a name="using-dcos"></a>使用 DC/OS
DC/OS 是分散式作業系統 hello Apache Mesos 分散式的系統的核心為基礎。 Apache Mesos 就會放在 hello Apache Software Foundation，並列出一些 hello[中的最大名稱 IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/)做為使用者及參與者。

![針對顯示代理程式與主要節點的 DC/OS 設定的 Azure Container Service。](media/acs-intro/dcos.png)

DC/OS 和 Apache Mesos 包含令人印象深刻的功能集︰

* 經實證的延展性
* 使用 Apache ZooKeeper 進行主要和從屬容錯複寫
* 支援 Docker 格式的容器
* 在工作與 Linux 容器之間的原生隔離
* 多資源排程 (記憶體、CPU、磁碟和連接埠)
* 用於開發全新平行應用程式的 Java、Python 和 C++ API
* 用於檢視叢集狀態的 Web UI

根據預設，在 Azure 容器服務上執行的 DC/OS 會包括 hello 馬拉松協調流程平台，用來設定排程的工作負載。 不過，包含以 hello DC/OS 部署 ACS 是 hello Mesosphere Universe 的可以加入 tooyour 服務的服務。 服務在 hello Universe 包括 Spark、 Hadoop、 Cassandra，以及執行更多。

![Azure Container Service 中的 DC/OS Universe](media/dcos/universe.png)

#### <a name="using-marathon"></a>使用 Marathon
馬拉松是整個叢集 init 和服務在 cgroups-，或在 hello 情況下，Azure 容器服務，Docker 格式化容器的控制系統。 Marathon 提供 Web UI，您可以用它來部署您的應用程式。 您可以在 `http://DNS_PREFIX.REGION.cloudapp.azure.com` 這樣的 URL 存取此程式：其中 DNS\_PREFIX 及 REGION 兩者都在部署時定義。 當然，您也可以提供您自己的 DNS 名稱。 如需有關執行的容器使用 hello 馬拉松 web UI 的詳細資訊，請參閱[DC/OS 容器管理透過 hello 馬拉松 web UI](container-service-mesos-marathon-ui.md)。

![Marathon 應用程式清單](media/dcos/marathon-applications-list.png)

您也可以使用 REST Api hello 與馬拉松進行通訊。 有許多可用於每個工具的用戶端程式庫。 這些資料涵蓋多種語言-和當然，您可以使用任何語言的 hello HTTP 通訊協定。 此外，許多受歡迎的 DevOps 工具都提供 Marathon 的支援。 當您使用 Azure Container Service 叢集時，這為作業小組提供了最大的彈性。 如需有關使用 hello 馬拉松 REST API 來執行容器的詳細資訊，請參閱[透過 hello 馬拉松 REST API 的 DC/OS 容器管理](container-service-mesos-marathon-rest.md)。

### <a name="using-docker-swarm"></a>使用 Docker Swarm
Docker Swarm 為 Docker 提供原生叢集。 因為 Docker Swarm 兼具 hello 標準 Docker 的 API，任何已經與 Docker 精靈通訊的工具可以使用 Azure 容器服務群集 tootransparently 標尺 toomultiple 主機。

![Azure 容器服務設定 toouse 群集。](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

管理容器群集叢集上的支援的工具包括但不限於下列 hello:

* Dokku
* Docker CLI 與 Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>使用 Kubernetes
Kubernetes 是常用的開放原始碼生產等級容器 Orchestrator 工具。 Kubernetes 能自動化部署、調整和管理容器化應用程式。 因為它是開放原始碼解決方案，而由 hello 開放原始碼社群所驅動，它會順暢地執行於 Azure 容器服務，而且可以使用的 toodeploy 大規模 Azure 容器服務上的容器。

![Azure 容器服務設定 toouse Kubernetes。](media/acs-intro/kubernetes.png)

它包含一組豐富的功能，包括︰
* 水平調整
* 服務探索和負載平衡
* 密碼和組態管理
* API 型的自動化推出和復原
* 自我修復

## <a name="videos"></a>影片
開始使用 Azure Container Service (101)：  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

建置應用程式使用 hello Azure 容器服務 (組建 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>後續步驟

部署使用 hello 的容器服務叢集[入口網站](container-service-deployment.md)或[Azure CLI 2.0](container-service-create-acs-cluster-cli.md)。
