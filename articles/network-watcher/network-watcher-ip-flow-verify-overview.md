---
title: "在 Azure 網路監看員確認 aaaIntroduction tooIP 流程 |Microsoft 文件"
description: "此頁面提供概觀的 hello 網路監看員 IP 流量確認功能"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>簡介 tooIP 流程確認在 Azure 網路監看員

如果允許或拒絕 tooor 5-tuple 資訊為基礎的虛擬機器從封包，IP 流量驗證檢查。 這些資訊包括方向、通訊協定、本機 IP、遠端 IP、本機連接埠和遠端連接埠。 如果安全性群組遭拒絕 hello 封包，會傳回 hello 拒絕 hello 封包的 hello 規則名稱。 這項功能時可以選擇任何來源或目的地 IP，協助系統管理員快速診斷中的連線問題或 toohello 網際網路來回或 toohello 在內部部署環境。

IP 流量驗證是以虛擬機器的網路介面做為目標。 根據設定的 hello 設定 tooor 該網路介面，然後驗證流量。 這項功能可用於確認從虛擬機器的輸入或輸出流量 tooor 時，是否要封鎖網路安全性群組中的規則。

請確認網路監看員需求 toobe 您計劃 toorun IP 流量的所有區域中建立的執行個體。 網路監看員是地區服務，並只對 hello 中的資源已執行相同的區域。 這不會影響的 hello IP 流量的結果，請確認為 hello 與 hello 仍會傳回 NIC 相關聯的路由。

![1][1]

## <a name="next-steps"></a>後續步驟

如果封包允許或拒絕特定虛擬機器透過 hello 入口網站的下列文章 toolearn hello 請瀏覽。 [檢查是否流量允許的 IP 流量驗證 VM 上使用 hello 入口網站](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












