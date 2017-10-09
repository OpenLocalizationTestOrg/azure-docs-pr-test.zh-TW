---
title: "aaaMonitor Azure DC/OS 叢集-ELK 堆疊 |Microsoft 文件"
description: "使用 ELK (Elasticsearch、Logstash 與 Kibana) 監視 Azure Container Service 中的 DC/OS 叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Containers, DC/OS, Azure, monitoring, elk, 容器, 監視"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>使用 ELK 監視 Azure Container Service 叢集
在本文中，我們將示範如何 toodeploy hello ELK (Elasticsearch，Logstash，Kibana) 堆疊 Azure 容器服務中的 DC/OS 叢集上。 

## <a name="prerequisites"></a>必要條件
[部署](container-service-deployment.md)並[連接](../container-service-connect.md) Azure Container Service 所設定的 DC/OS 叢集。 瀏覽 hello DC/OS 儀表板和馬拉松服務[這裡](container-service-mesos-marathon-ui.md)。 也會安裝 hello[馬拉松負載平衡器](container-service-load-balancing.md)。


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch、Logstash、Kibana)
ELK 堆疊是 Elasticsearch，Logstash，組合 Kibana，提供結束 tooend 堆疊，可以和使用的 toomonitor 分析您的叢集中的記錄檔。

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>DC/OS 叢集上設定 hello ELK 堆疊
存取您的 DC/OS UI 透過[http://localhost:80 /](http://localhost:80/)一次在 hello DC/OS UI 導覽太**Universe**。 搜尋並安裝 Elasticsearch、 Logstash 和 Kibana 從 hello DC/OS Universe 和的特定順序。 您可以進一步了解組態如果您 toohello**進階安裝**連結。

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

一次 hello ELK 容器和啟動並執行的是，您需要存取透過馬拉松 LB tooenable Kibana toobe。 瀏覽過**服務** > **kibana**，然後按一下**編輯**如下所示。

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


切換太**JSON 模式**和捲動 toohello 標籤 > 一節。
您需要 tooadd`"HAPROXY_GROUP": "external"`項目所示下方。
按一下 [Deploy changes (部署變更)] 之後，容器會重新啟動。

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


如果您想要 tooverify 該 Kibana 註冊為 hello haproxy 等儀表板中的服務，haproxy 等連接埠 9090 上執行時，需要 tooopen 連接埠 9090 hello 代理程式的叢集上。
根據預設，我們開啟連接埠 80、 8080，並在 443 hello DC/OS 代理程式的叢集。
指示 tooopen 連接埠，並提供公用存取會提供[這裡](container-service-enable-public-access.md)。

tooaccess hello haproxy 等儀表板，在開啟 hello 馬拉松 LB 管理介面： `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`。
一旦您瀏覽 toohello URL，如下所示，您應該看到 hello haproxy 等儀表板，您應該看到 Kibana 服務項目。

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


tooaccess hello Kibana 儀表板，將連接埠 5601 部署時，您需要 tooopen 連接埠 5601。 遵循[這裡](container-service-enable-public-access.md)的指示。 然後開啟 在 hello Kibana 儀表板： `http://localhost:5601`。

## <a name="next-steps"></a>後續步驟

* 如需系統和應用程式記錄檔轉送與設定的相關資訊，請參閱 [DC/OS 中使用 ELK 的記錄檔管理 (英文)](https://docs.mesosphere.com/1.8/administration/logging/elk/)。

* toofilter 記錄，請參閱 < [ELK 篩選記錄檔](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/)。 

 

