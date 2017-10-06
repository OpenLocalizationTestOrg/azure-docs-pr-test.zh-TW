---
title: "aaaAzure RemoteApp 網路頻寬的一般指導方針 |Microsoft 文件"
description: "了解 Azure RemoteApp 集合和應用程式的一些基本網路頻寬指導方針。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指導方針 (如果您無法自行測試))
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

如果您沒有 hello 時間或功能 toorun hello[網路頻寬測試](remoteapp-bandwidthtests.md)的 Azure RemoteApp，以下是一些相當普遍的指導方針可協助您估計每個使用者的網路頻寬。

如果您有混合的這些案例，我們不建議的任何項目 （或等於） 小於 10 MB/s 為 hello 現代化的網際網路連線應用程式，在遠端環境中的最小網路頻寬。 (但是，如所述，這不保證會優於一般使用者體驗)。

## <a name="complex-powerpoint-simple-powerpoint"></a>複雜 PowerPoint, 簡單 PowerPoint
Azure RemoteApp 在 100 MB LAN 上運作地最好。 在 hello 10 MB/s 網路設定檔，上述 120 ms 抖動超過 5%時，hello 使用者會看到平均的體驗。 在 1 MB/s hello 不同 glaring-例如，以投影片放映，hello 使用者可能不會看到動畫的轉換完全因為框架會略過。

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, 混合 PDF, PDF, 文字
10 MB/s 的網路設定檔是關閉 tooLAN 在大部分的層面。 1 MB/s 會提供 [確定] 的經驗，雖然可能會有一些抖動使用者捲動時囉 」 畫面上沒有映像時。

## <a name="flash-video-youtube"></a>Flash 視訊 (YouTube)
100 MB/s LAN 提供 hello 獲得最佳經驗，而 10 MB/s 為可接受 （表示我們跟上 hello 畫面播放速率，但抖動增加）。 在 1 MB/s，抖動狀況極高，而且明顯。

## <a name="word-typing-word-remote-input"></a>Word 輸入 (Word 遠端輸入)
這是低頻寬使用案例。 在 256 KB/s，我們提供與 LAN 一樣好的體驗。

## <a name="learn-more"></a>詳細資訊
* [Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)](remoteapp-bandwidth.md)
* [Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量)](remoteapp-bandwidthtests.md)

