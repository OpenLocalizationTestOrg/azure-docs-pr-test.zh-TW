---
title: "aaaInternet 面對負載平衡器概觀 |Microsoft 文件"
description: "網際網路面向的負載平衡器及其功能的概觀。 負載平衡器如何作用於使用虛擬機器和雲端服務的 Azure。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>網際網路面向的負載平衡器概觀

Azure 負載平衡器對應 hello 公用 IP 位址和連接埠號碼的連入流量 toohello 私用 IP 位址和連接埠號碼的 hello 回應 hello 虛擬機器流量 hello 虛擬機器，反之亦然。 負載平衡規則可讓您 toodistribute 特定類型的多個虛擬機器或服務之間的流量。 例如，您可以 hello 負載分散 web 要求流量的多個 web 伺服器或 web 角色。

雲端服務包含 web 角色或背景工作角色執行個體，您可以在 hello 服務定義 (.csdef) 檔中定義公用端點。

hello *servicedefinition.csdef*檔案包含 hello 端點組態，而且當您有 web 或背景工作角色部署多個角色執行個體，hello 負載平衡器將會為它的安裝程式。 hello 方式 tooadd 執行個體 tooyour 雲端部署正在變更 hello hello 服務組態檔 (.csfg) 上的執行個體計數。

hello 如下圖所示為 hello 公用和私人 TCP 連接埠 80 的三部虛擬機器之間共用的網路流量的負載平衡端點。 這三部虛擬機器均位在負載平衡集合中。

![建立負載平衡器範例](./media/load-balancer-internet-overview/IC727496.png)

圖 1 - Web 流量的負載平衡端點

當網際網路用戶端傳送網頁要求 toohello 公用 IP 位址 hello 雲端服務的 TCP 連接埠 80 時，hello Azure 負載平衡器會將 hello hello 負載平衡集內 hello 三部虛擬機器之間的要求分散。 如需有關負載平衡器演算法的詳細資訊，請參閱 hello[負載平衡器的概觀頁面](load-balancer-overview.md#load-balancer-features)。

根據預設，Azure Load Balancer 會在多個虛擬機器執行個體之間均分網路流量。 您也可以設定工作階段親和性。如需詳細資訊，請參閱[負載平衡器分配模式](load-balancer-distribution-mode.md)。

## <a name="next-steps"></a>後續步驟

深入了解[內部負載平衡器](load-balancer-internal-overview.md)toobetter 了解哪些負載平衡器是否適合您的雲端部署。

您也可以[開始建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)，以及為特定負載平衡器的網路流量行為設定[分配模式](load-balancer-distribution-mode.md)類型。

如果您的應用程式需要 tookeep 連線運作的負載平衡器後方的伺服器，您可以瞭解多[閒置 TCP 逾時設定的負載平衡器](load-balancer-tcp-idle-timeout.md)。 當您使用 Azure 負載平衡器，它會協助 toolearn 有關閒置連線行為。
