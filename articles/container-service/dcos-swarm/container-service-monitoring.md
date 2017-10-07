---
title: "aaaMonitor Azure DC/OS 叢集 Datadog |Microsoft 文件"
description: "使用 Datadog 監視 Azure 容器服務叢集。 使用 hello DC/OS web UI toodeploy hello Datadog 代理程式 tooyour 叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>使用 Datadog 監視 Azure Container Service DC/OS 叢集
本文章中我們將部署 Datadog 代理程式 tooall hello 代理程式節點 Azure 容器服務叢集中。 您將需要 Datadog 帳戶以進行這項設定。 

## <a name="prerequisites"></a>必要條件
[部署](container-service-deployment.md)和[連接](../container-service-connect.md) Azure Container Service 所設定的叢集。 瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。 跳過[http://datadoghq.com](http://datadoghq.com) tooset Datadog 帳戶。 

## <a name="datadog"></a>Datadog
Datadog 是一項監視服務，會從 Azure 容器服務叢集內的容器收集監視資料。 Datadog 有 Docker 整合儀表板，可供您查看容器內的特定度量。 從容器收集到的度量會依 CPU、記憶體、網路和 I/O 來加以整理。 Datadog 會將度量分割成容器和映像。 舉例來說，哪些 hello cpu 使用量低於似乎 UI。

![Datadog UI](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>使用 Marathon 設定 Datadog 部署
這些步驟將示範如何 tooconfigure 和部署與馬拉松 Datadog 應用程式 tooyour 叢集。 

透過 [http://localhost:80/](http://localhost:80/)存取 DC/OS UI。 一次在 hello DC/OS UI 導覽 toohello"Universe"，這位於 hello 下由然後搜尋 「 Datadog"並按一下 [安裝]。

![Hello DC/OS Universe 內 Datadog 封裝](./media/container-service-monitoring/datadog1.png)

現在 toocomplete hello 設定，您需要 Datadog 帳戶或免費的試用帳戶。 一旦您登入 toohello Datadog 網站中看起來 toohello 左邊，並移 tooIntegrations-> 然後[Api](https://app.datadoghq.com/account/settings#api)。 

![Datadog API 金鑰](./media/container-service-monitoring/datadog2.png)

接下來 hello Datadog 組態 hello DC/OS Universe 內輸入您的 API 金鑰。 

![在 hello DC/OS Universe Datadog 組態](./media/container-service-monitoring/datadog3.png) 

Hello 上述組態中執行個體已設定 too10000000，所以每當新的節點加入 toohello 叢集 Datadog 就會自動部署的代理程式 toothat 節點。 這是過渡解決方案。 一旦您已安裝 hello 封裝應該回復 toohello Datadog 網站瀏覽並尋找"[儀表板](https://app.datadoghq.com/dash/list)。 」 從該處，您會看到自訂和整合儀表板。 hello [Docker 儀表板](https://app.datadoghq.com/screen/integration/docker)會有所有的 hello 容器度量，您必須監視您的叢集。 

