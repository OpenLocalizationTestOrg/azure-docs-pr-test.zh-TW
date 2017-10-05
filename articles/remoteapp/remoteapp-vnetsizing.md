---
title: "Azure RemoteApp 中 VNET 的大小調整資訊 | Microsoft Docs"
description: "深入了解使用 VNET 執行之 Azure RemoteApp 的 IP 位址需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Azure RemoteApp 中 VNET 的大小調整資訊
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

使用 Azure RemoteApp 與虛擬網路 (VNET) 搭配時，RemoteApp 會使用子網路內的 IP 位址。 根據 RemoteApp 服務的規模，您需要確保子網路具有足夠的 IP 位址可用於 RemoteApp 虛擬機器。 雖然此大小調整指導方針未完美地指定 RemoteApp 如何動態旋轉集合內的虛擬機器，但是可協助您估計子網路範圍。 這特別重要，因為在 VNET 中放置 RemoteApp 服務之後，需要移除 RemoteApp，才能增加子網路大小。

針對每個您想要以最大容量執行的 RemoteApp 集合，您應該有 100 個 IP 位址可用。 例如，如果您在標準計畫中有一個 RemoteApp 集合，而且您最多想要有 500 位使用者，則該集合應該有 100 個 IP 位址。 同樣地，在具有 800 位使用者的基本計畫中，RemoteApp 集合需要有 100 個 IP 位址。 如果您想要有較少的使用者 (小於最大值)，則可以減少每個集合所需的 IP 位址。 最少子網路大小需求是 30 個 IP 位址 (/27)。

請查看下列資訊，確認您的 VNET 已設定並正常運作：

* [從個人 VNET 移轉至 Azure VNET](remoteapp-migratevnet.md)
* [驗證要搭配 Azure RemoteApp 使用的 Azure VNET](remoteapp-vnet.md)

