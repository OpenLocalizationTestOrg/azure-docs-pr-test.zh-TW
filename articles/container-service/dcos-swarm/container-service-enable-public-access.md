---
title: "aaaEnable access tooAzure DC/OS 容器應用程式 |Microsoft 文件"
description: "如何 tooenable 公用存取 tooDC/OS Azure 容器服務中的容器。"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>啟用公用存取 tooan Azure 容器服務應用程式
Hello ACS 在任何 DC/OS 容器[公用代理程式集區](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container)會自動公開的 toohello 網際網路。 根據預設，連接埠 **80**、**443**、**8080** 已開啟，在這些連接埠上接聽的任何 (公用) 容器皆可供存取。 本文章將示範如何 tooopen 多連接埠 Azure 容器服務中的應用程式。

## <a name="open-a-port-portal"></a>開啟連接埠 (入口網站)
首先，我們需要我們想要的 tooopen hello 連接埠。

1. 登入 toohello 入口網站。
2. 尋找您所部署的 hello 資源群組 hello Azure 容器服務。
3. 選取 hello 代理程式負載平衡器 (這名為類似太**XXXX 代理程式-lb XXXX**)。
   
    ![Azure Container Service 的負載平衡器](./media/container-service-enable-public-access/agent-load-balancer.png)
4. 依序按一下 [探查] 和 [新增]。
   
    ![Azure Container Service 的負載平衡器探查](./media/container-service-enable-public-access/add-probe.png)
5. 填寫 hello 探查表單，然後按一下**確定**。
   
   | 欄位 | 說明 |
   | --- | --- |
   | 名稱 |Hello 探查的描述性名稱。 |
   | Port |hello 容器 tootest hello 連接埠。 |
   | Path |（在 HTTP 模式時） hello 相對的網站路徑 tooprobe。 不支援 HTTPS。 |
   | 間隔 |嘗試 hello 探查之間的時間量以秒為單位。 |
   | 狀況不良臨界值 |考慮 hello 容器狀況不良之前，先在此連續探查次數。 |
6. 在 hello 代理程式負載平衡器的 hello 內容中，按一下 **負載平衡規則**然後**新增**。
   
    ![Azure Container Service 的負載平衡器規則](./media/container-service-enable-public-access/add-balancer-rule.png)
7. 填寫 hello 負載平衡器表單，然後按一下**確定**。
   
   | 欄位 | 說明 |
   | --- | --- |
   | 名稱 |Hello 負載平衡器的描述性名稱。 |
   | Port |hello 公用的連入通訊埠。 |
   | 後端連接埠 |hello 內部公用連接埠的 hello 容器 tooroute 流量。 |
   | 後端集區 |此集區中的 hello 容器將是此負載平衡器的 hello 目標。 |
   | 探查 |如果目標中 hello hello 探查使用 toodetermine**後端集區**狀況良好。 |
   | 工作階段持續性 |決定應如何從用戶端的流量處理 hello hello 工作階段期間。<br><br>**無**： 來自相同用戶端可以由任何容器的 hello 的後續要求。<br>**用戶端 IP**: hello 相同的用戶端 IP 由處理後續要求 hello 相同的容器。<br>**用戶端 IP 和通訊協定**： 來自相同用戶端 IP 和通訊協定組合都由的 hello 的後續要求 hello 相同的容器。 |
   | 閒置逾時 |(只有 TCP)以分鐘為單位 hello TCP/HTTP 用戶端不需依賴所開啟的時間 tookeep*保持*訊息。 |

## <a name="add-a-security-rule-portal"></a>新增安全性規則 (入口網站)
接下來，我們需要 tooadd 從我們已開啟的連接埠通過 hello 防火牆會路由傳送流量的安全性規則。

1. 登入 toohello 入口網站。
2. 尋找您所部署的 hello 資源群組 hello Azure 容器服務。
3. 選取 hello**公用**代理程式的網路安全性群組 (這名為類似太**XXXX-代理程式-公用-nsg-XXXX**)。
   
    ![Azure Container Service 網路安全性群組](./media/container-service-enable-public-access/agent-nsg.png)
4. 依序選取 [輸入安全性規則] 和 [新增]。
   
    ![Azure Container Service 網路安全性群組規則](./media/container-service-enable-public-access/add-firewall-rule.png)
5. 填寫 hello 防火牆規則 tooallow 公用連接埠，然後按一下**確定**。
   
   | 欄位 | 說明 |
   | --- | --- |
   | 名稱 |Hello 防火牆規則的描述性名稱。 |
   | 優先順序 |Hello 規則的優先順序等級。 hello hello 數字 hello 高 hello 優先順序。 |
   | 來源 |限制 hello 連入 IP 位址範圍 toobe 允許或拒絕此規則。 使用**任何**toonot 指定限制。 |
   | 服務 |選取一組適用此安全性規則的預先定義服務。 否則使用**自訂**toocreate 自己。 |
   | 通訊協定 |根據 **TCP** 或 **UDP** 限制流量。 使用**任何**toonot 指定限制。 |
   | 連接埠範圍 |當**服務**是**自訂**，指定此規則影響的連接埠範圍，hello。 您可以使用單一連接埠 (例如 **80**) 或 **1024-1500** 之類的範圍。 |
   | 動作 |允許或拒絕符合 hello 準則的流量。 |

## <a name="next-steps"></a>後續步驟
深入了解 hello 差異[公用和私用 DC/OS 代理程式](container-service-dcos-agents.md)。

深入了解 [管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。

