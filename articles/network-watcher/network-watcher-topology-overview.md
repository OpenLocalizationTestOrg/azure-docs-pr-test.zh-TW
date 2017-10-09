---
title: "在 Azure 網路監看員 aaaIntroduction tootopology |Microsoft 文件"
description: "此頁面提供 hello 網路監看員拓撲的功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>在 Azure 網路監看員的簡介 tootopology

拓撲會傳回虛擬網路中的網路資源之圖形。 hello 圖描繪 hello 資源 toorepresent hello 結束 tooend 網路連線之間的 hello 互連。

![拓撲概觀][1]

Hello 入口網站中，在拓撲會傳回 hello 資源物件上每個虛擬網路。 即使在 hello 資源群組將不會顯示，但會由 hello 網路監看員區域以外的 hello 資源的資源間的線條顯示 hello 關聯性。 傳回在 hello 入口網站檢視中的 hello 資源是 hello 網路元件是圖形化的子集。 您可以使用網路資源的 toosee hello 完整清單[PowerShell](network-watcher-topology-powershell.md)或[REST](network-watcher-topology-rest.md)

> [!NOTE]
> 您想 toorun 拓撲每個區域中需要的網路監看員執行個體。

資源會傳回它們之間的 hello 連接是在兩個關聯性建立模型。

- **內含項目** - 範例︰虛擬網路包含其中含有 NIC 的子網路
- **相關聯** - 範例︰NIC 與 VM 相關聯

### <a name="next-steps"></a>後續步驟

了解如何 toouse PowerShell tooretrieve hello 拓撲檢視造訪[網路監看員拓撲使用 PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
