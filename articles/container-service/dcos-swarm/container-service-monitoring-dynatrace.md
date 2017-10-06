---
title: "aaaMonitor Azure DC/OS 叢集 Dynatrace |Microsoft 文件"
description: "使用 Dynatrace 監視 Azure Container Service DC/OS 叢集。 部署 hello Dynatrace OneAgent 使用 hello DC/OS 儀表板。"
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "容器，DC/OS，Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>使用 Dynatrace SaaS/Managed 監視 Azure Container Service DC/OS 叢集
在本文中，我們會示範如何 toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor 所有 hello Azure 容器服務叢集中的代理程式節點。 您需要 Dynatrace SaaS/Managed 帳戶以進行這項設定。 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/Managed
Dynatrace 是高動態容器和叢集環境適用的雲端原生監視解決方案。 它可讓您 toobetter 最佳化您的容器部署和配置的記憶體使用即時使用狀況資料。 其藉由提供自動化基準、問題相互關聯和根本原因偵測，就能夠自動查明應用程式和基礎結構問題。

hello 以下圖顯示 hello Dynatrace UI:

![Dynatrace UI](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>必要條件 
[部署](container-service-deployment.md)和[連接](./../container-service-connect.md)tooa Azure 容器服務所設定的叢集。 瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。 跳過[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS 帳戶。  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>使用 Marathon 設定 Dynatrace 部署
這些步驟顯示如何 tooconfigure 和部署與馬拉松 Dynatrace 應用程式 tooyour 叢集。

1. 透過 [http://localhost:80/](http://localhost:80/)存取 DC/OS UI。 一次在 hello DC/OS UI 中，瀏覽 toohello **Universe**索引標籤，然後搜尋**Dynatrace**。

    ![DC/OS Universe 中的 Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. toocomplete hello 組態中，您需要 Dynatrace SaaS 帳戶或免費的試用帳戶。 一旦您登入 hello Dynatrace 儀表板，選取**部署 Dynatrace**。

    ![Dynatrace 設定 PaaS 整合](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. 在 hello 頁面上，選取  **PaaS 整合**。 

    ![Dynatrace API 權杖](./media/container-service-monitoring-dynatrace/api-token.png) 

4. 輸入您的 API 語彙基元 hello Dynatrace OneAgent 組態 hello DC/OS Universe 內。 

    ![在 hello DC/OS Universe Dynatrace OneAgent 組態](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Toohello 數目設定 hello 執行個體的節點中，您想 toorun。 設定較高數字也有效，但是 DC/OS 將會繼續嘗試 toofind 的新執行個體一直該數目的實際。 如果您想要的話，您也可以設定類似 1000000 這個 tooa 值。 在此情況下，每當 toohello 叢集時，會加入新的節點，Dynatrace 自動將部署代理程式 toothat 新節點，hello 價格的 DC/OS 不斷地嘗試 toodeploy 進一步執行個體。

    ![Dynatrace hello DC/OS Universe-執行個體中的組態](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>後續步驟

一旦您已安裝 hello 封裝，請瀏覽後 toohello Dynatrace 儀表板。 您可以在您的叢集探索 hello 容器 hello 不同的使用計量。 
