---
title: "Azure 容器服務 aaaDC/OS 代理程式集區 |Microsoft 文件"
description: "Hello 公用和私用的代理程式集區與 Azure 容器服務 DC/OS 叢集的運作方式"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Azure Container Service 的 DC/OS 代理程式集區
Azure Container Service 中的 DC/OS 叢集包含兩個集區中的代理程式節點，即公用集區和私用集區。 應用程式可以部署 tooeither 集區，會影響您的容器服務在電腦之間的存取範圍。 hello 機器可以是公開的 toohello 網際網路 （公用） 或保留內部 （私用）。 本文簡短概述為什麼會有公用集區和私用集區。


* **私用代理程式**：私用代理程式節點會透過非可路由網路來執行。 從 hello 管理區域，或透過 hello 公用區域邊緣路由器，才可存取此網路。 根據預設，DC/OS 會在私用代理程式節點上啟動應用程式。 

* **公用代理程式**：公用代理程式節點會透過可公開存取的網路執行 DC/OS 應用程式和服務。 

如需 DC/OS 網路安全性的詳細資訊，請參閱 hello [DC/OS 文件](https://dcos.io/docs/1.7/administration/securing-your-cluster/)。

## <a name="deploy-agent-pools"></a>部署代理程式集區

hello DC/OS 代理程式集區中的 Azure 容器服務會建立，如下所示：

* hello**私用的集區**包含 hello 號碼的代理程式節點可以指定何時您[部署 hello DC/OS 叢集](container-service-deployment.md)。 

* hello**公用集區**一開始包含預先定義的代理程式節點數。 Hello DC/OS 叢集已佈建時，會自動加入此集區。

hello 私用，而 hello 公用集區是 Azure 虛擬機器規模集。 您可以在部署後調整這些集區的大小。

## <a name="use-agent-pools"></a>使用代理程式集區
根據預設，**馬拉松**部署任何新的應用程式 toohello*私人*代理程式節點。 您必須部署 hello 應用程式 toohello tooexplicitly*公用*hello hello 應用程式建立期間的節點。 選取 hello**選擇性**索引標籤並輸入**slave_public** hello**接受資源角色**值。 此程序會說明[這裡](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container)在 hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/)文件。

## <a name="next-steps"></a>後續步驟
* 深入了解如何[管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。

* 了解如何太[開啟 hello 防火牆](container-service-enable-public-access.md)Azure tooallow 公用存取 tooyour DC/OS 容器所提供。

