---
title: "在 Azure 網路監看員 aaaIntroduction toonext 躍點 |Microsoft 文件"
description: "此頁面提供概觀 hello 網路監看員的下一個躍點的功能"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>在 Azure 網路監看員簡介 toonext 躍點

從 VM 的流量會傳送 tooa 根據 hello 與 NIC 相關聯的有效路由的目的地 下一個躍點取得下一個躍點類型 hello 和封包的 IP 位址從特定虛擬機器與 nic。 這可協助 toodetermine 如果 hello 封包會被導向的 toohello 目的地，或為正在黑色 hello 流量書背。 不適當的路由 hello 使用者流量導向的 tooan 在內部部署位置或所在虛擬應用裝置，設定可能會導致 tooconnectivity 問題。 下一個躍點也會傳回 hello 與 hello 下一個躍點相關聯的路由表。 如果 hello 路由定義為使用者定義的路由，請查詢下一個躍點，將會傳回該路由。 否則，下一個躍點會傳回「系統路由」。

![下一個躍點概觀][1]

hello 以下是 hello 下一個躍點類型可以在下一個躍點的查詢時傳回的清單。

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>後續步驟

了解網路連線與下一個躍點 toofind toouse 問題造訪如何[核取 hello 下一個躍點 VM 上](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













