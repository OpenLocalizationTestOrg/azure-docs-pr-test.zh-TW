---
title: "Azure RemoteApp network bandwidth - general guidelines (Azure RemoteApp 網路頻寬 - 一般指導方針) | Microsoft Docs"
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指導方針 (如果您無法自行測試))
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

如果您沒有時間或無法執行 Azure RemoteApp 的 [網路頻寬測試](remoteapp-bandwidthtests.md) ，以下是一些相當常用的指導方針，可協助您估計每位使用者的網路頻寬。

如果您混合使用這些案例，則不建議將小於 (或等於) 10 MB/s 的任何項目用作遠端環境中現代網際網路連線之應用程式的最小網路頻寬。 (但是，如所述，這不保證會優於一般使用者體驗)。

## <a name="complex-powerpoint-simple-powerpoint"></a>複雜 PowerPoint, 簡單 PowerPoint
Azure RemoteApp 在 100 MB LAN 上運作地最好。 在 10 MB/s 網路設定檔中，高於 120 毫秒的抖動超過 5% 時，使用者會看到一般體驗。 在 1 MB/s 上，差異十分明顯 - 例如，在投影片放映中，使用者可能根本看不到動畫轉換，因為會略過畫面格。

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, 混合 PDF, PDF, 文字
10 MB/s 網路設定檔的大部分層面都接近 LAN。 1 MB/s 將提供正常體驗，但是使用者捲動時可能會有一些抖動，而螢幕上會有影像。

## <a name="flash-video-youtube"></a>Flash 視訊 (YouTube)
100 MB/s LAN 提供最佳體驗，而 10 MB/s 為可接受的體驗 (表示可以跟上畫面格速率，但抖動會增加)。 在 1 MB/s，抖動狀況極高，而且明顯。

## <a name="word-typing-word-remote-input"></a>Word 輸入 (Word 遠端輸入)
這是低頻寬使用案例。 在 256 KB/s，我們提供與 LAN 一樣好的體驗。

## <a name="learn-more"></a>詳細資訊
* [Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)](remoteapp-bandwidth.md)
* [Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量)](remoteapp-bandwidthtests.md)

