---
title: "在 Azure RemoteApp VNET aaaSizing 資訊 |Microsoft 文件"
description: "深入了解 Azure RemoteApp VNET 執行 hello IP 位址需求"
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Azure RemoteApp 中 VNET 的大小調整資訊
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

當您使用 Azure RemoteApp 搭配虛擬網路 (VNET) 時，RemoteApp 會使用 hello 子網路內的 IP 位址。 根據您的 RemoteApp 服務的 hello 小數位數，必須 tooensure 子網路有足夠可用的 RemoteApp 虛擬機器的 IP 位址。 雖然此大小調整指導方針未完美地指定 RemoteApp 如何動態旋轉集合內的虛擬機器，但是可協助您估計子網路範圍。 這是因為一旦 RemoteApp 服務放置在 VNET 中，您無法增加 hello 子網路大小，不會移除 RemoteApp 尤其重要。

每個您想要以最大容量 toorun RemoteApp 集合，您應指派 100 可用的 IP 位址。 比方說，如果 hello 標準方案中有一個 RemoteApp 集合，而且您想 toohave hello 上限 500 位使用者，您應該有 100 的 IP 位址，該集合。 同樣地，您需要 100 的 IP 位址的 RemoteApp 集合有 800 使用者 hello 基本計劃中。 如果您計劃 toohave 較少的使用者 （大於或等於最大的 hello），您可以減少每個集合所需的 hello IP 位址。 hello 最小的子網路大小需求是 30 個 IP 位址 （/ 27）。

請參閱下列資訊 toomake 確定您的 VNET 設定且運作卻 hello:

* [從個人的 VNET tooan Azure VNET 移轉](remoteapp-migratevnet.md)
* [驗證與 Azure RemoteApp 一起 hello Azure VNET toouse](remoteapp-vnet.md)

