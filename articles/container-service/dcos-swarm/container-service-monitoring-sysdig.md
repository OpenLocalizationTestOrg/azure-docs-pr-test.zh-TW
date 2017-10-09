---
title: "aaaMonitor Azure 容器服務叢集 Sysdig |Microsoft 文件"
description: "使用 Sysdig 監視 Azure 容器服務叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器，DC/OS，Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>使用 Sysdig 監視 Azure 容器服務叢集
在本文中，我們將部署 Sysdig 代理程式 tooall hello 代理程式節點 Azure 容器服務叢集中。 您需要 Sysdig 帳戶以進行這項設定。 

## <a name="prerequisites"></a>必要條件
[部署](container-service-deployment.md)和[連接](../container-service-connect.md) Azure Container Service 所設定的叢集。 瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。 跳過[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig 雲端帳戶。 

## <a name="sysdig"></a>Sysdig
Sysdig 是監視服務，可讓您 toomonitor 您在叢集內的容器。 Sysdig 已知 toohelp 進行疑難排解，但是它也有基本的監視度量的 CPU、 網路、 記憶體和 I/O。 使得的容器使用的簡單 toosee Sysdig hello hardest 或基本上使用 hello 大部分的記憶體和 CPU。 此檢視位於 hello beta 中的 < 概觀 > 一節。 

![Sysdig UI](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>使用 Marathon 設定 Sysdig 部署
這些步驟將示範如何 tooconfigure 和部署與馬拉松 Sysdig 應用程式 tooyour 叢集。 

存取您的 DC/OS UI 透過[http://localhost:80 /](http://localhost:80/)一次在 hello DC/OS UI 瀏覽的 toohello"Universe"，這位於 hello 下，然後搜尋 「 Sysdig。 」

![DC/OS Universe 中的 Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

現在 toocomplete hello 組態需要 Sysdig 雲端帳戶或免費的試用帳戶。 一旦您登入 toohello Sysdig 雲端網站，按一下您的使用者名稱，然後在 hello 頁面上您應該會看到您的 「 存取金鑰 」。 

![Sysdig API 金鑰](./media/container-service-monitoring-sysdig/sysdig2.png) 

接下來 hello Sysdig 組態 hello DC/OS Universe 內輸入您的存取金鑰。 

![在 hello DC/OS Universe Sysdig 組態](./media/container-service-monitoring-sysdig/sysdig3.png)

現在設定 hello 執行個體 too10000000 toohello 叢集 Sysdig 加入新的節點時就會自動部署代理程式以便 toothat 新節點。 這是過渡期解決方案 toomake 確定 Sysdig 將部署 tooall hello 叢集內的新代理程式。 

![Sysdig hello DC/OS Universe-執行個體中的組態](./media/container-service-monitoring-sysdig/sysdig4.png)

一旦您已安裝 hello 封裝瀏覽後 toohello Sysdig UI，然後您會在您的叢集內 hello 容器可以 tooexplore hello 不同的使用情況標準。 

您也可以透過[新的儀表板精靈](https://app.sysdigcloud.com/#/dashboards/new)來安裝 Mesos 和 Marathon 專用儀表板。
