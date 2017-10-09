---
title: "Azure RemoteApp 的網路頻寬使用量 aaaEstimate |Microsoft 文件"
description: "深入了解 hello 網路頻寬需求您的 Azure RemoteApp 集合和應用程式。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 使用 hello 遠端桌面通訊協定 (RDP) toocommunicate hello Azure 雲端和使用者在執行的應用程式。 本文提供一些基本的指導方針您可以使用 tooestimate 網路使用量，而且可能會評估每個使用者的 Azure RemoteApp 的網路頻寬使用量。

估計每位使用者的頻寬使用量十分複雜，而且需要在多工作業案例中同時執行多個應用程式，而在此案例中，根據網路頻寬需求，應用程式可能會影響彼此的效能。 即使 hello 類型 （例如 HTML5 用戶端與 Mac 用戶端） 的遠端桌面用戶端可能會導致 toodifferent 頻寬結果。 toohelp 逐步進行這些複雜性，我們會將 hello 使用案例分成幾個 hello 通用類別目錄 tooreplicate 真實世界案例。 （如果 hello 真實世界的實例，混合的類別，不同的使用者。）

請注意，我們假設 RDP 提供良好的 tooexcellent 體驗大部分使用案例的網路上下方 120 ms 和頻寬延遲超過 5 mb/s-這根據 RDP 的能力 toodynamically-在進一步討論前調整使用 hello 可用的網路頻寬和 hello 估計應用程式的頻寬需求。 這篇文章會之外，在 hello 邊緣，其中案例一開始會 toounwind 和使用者經驗開始 toodegrade"大部分使用案例 」 toolook。

立即簽出 hello 下列文章中的 hello 詳細資料，包括因素 tooconsider、 基準建議項目未包含我們的估計值。

* [How do network bandwidth and quality of experience work together? (如何兼顧網路頻寬和體驗品質？)](remoteapp-bandwidthexperience.md)
* [Testing your network bandwidth usage with some common scenarios (利用一些常見案例測試您的網路頻寬使用量)](remoteapp-bandwidthtests.md)
* [如果您沒有 hello 時間或能力 tootest 快速的指導方針](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>未包含的內容
當您檢閱 hello 建議測試和我們整體 （和不可否認一般） 的建議時，請留意有數個因素是不是由我們認為。 例如，hello hello 非對稱性質上傳和下載頻寬所提供的使用者經驗複雜。 hello 非對稱性質大部分的 Wi-fi 網路時，此外會影響 hello 效能和 hello 使用者體驗的感覺。 互動式案例 hello 下游流量優先順序低於 hello 上游，這可能會遺失的視訊或音訊框架的 hello 數目增加，並且因此影響 hello 使用者感覺的 hello 串流處理體驗。 您可以執行您自己實驗 toosee 什麼是適合您特定的使用案例和網路。

雖然我們討論裝置重新導向，但我們並未考慮到 hello 引起的網路流量所附加的裝置，例如儲存體、 印表機、 掃描器、 網路攝影機和其他 USB 裝置考量 hello 頻寬的影響。 這些裝置 hello 效果通常暫時升高 hello 頻寬需求，會隨即消失，hello 工作完成時。 但是，如果經常這樣做，則頻寬需求可能會相當可觀。

我們也不討論如何一位使用者可能會影響其他使用者所 hello 相同的網路。 例如，使用 100 MB/s 網路 4k 視訊的一位使用者可能會大幅影響其他使用者嘗試 toodo 該相同網路上的 hello 相同的工作。 不幸的是取得愈來愈困難 toodetermine hello 影響同時使用 toogive 通用或全能 hello 系統在彙總的執行方式的相關建議。 我們只能說是 hello 基礎通訊協定的技術將善用 hello hello 可用的網路頻寬，但它仍有其限制。

