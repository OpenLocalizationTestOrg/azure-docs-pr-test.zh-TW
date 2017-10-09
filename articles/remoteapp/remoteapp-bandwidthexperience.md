---
title: "aaaAzure RemoteApp-如何網路頻寬和品質遇到工作一起？ | Microsoft Docs"
description: "了解 Azure RemoteApp 中的網路頻寬如何影響您使用者的體驗品質。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

當您查看 hello[整體網路頻寬](remoteapp-bandwidth.md)所需的 Azure RemoteApp，請考量下列因素的 hello-這些是所有系統一部分的動態影響 hello 整體的使用者經驗。 

* **可用的網路頻寬和目前的網路狀況**-一組給定的時間相同網路的 hello 參數 （中斷、 延遲、 抖動） 可能會影響 hello 應用程式串流處理體驗，這就表示降低整體的使用者體驗。 網路中可用的 hello 頻寬是壅塞、 隨機遺失、 延遲的函式，因為所有這些參數會影響 hello 壅塞控制機制，而在開啟控制項 hello 傳輸速度 tooavoid 衝突。  例如，失真網路或高延遲網路將會 hello 使用者經驗錯誤甚至 1000MB 頻寬的網路。 hello 中斷和延遲隨著 hello hello 上的使用者數目相同的網路，以及這些使用者 （例如，觀賞影片、 下載或上傳大型檔案、 列印） 的執行。
* **使用案例**-hello 體驗取決於哪些 hello 使用者做為個人和 hello 上的群組相同網路。 例如，讀取一張投影片需要只更新; 單一框架 toobe如果 hello 使用者 skims，並透過 hello 文字文件內容捲動，它們需要更新每秒畫面格數 toobe 較高的數目。 hello 回通訊，並制定 toohello 伺服器在此案例中最終會消耗更多的網路頻寬。 也請考量極端範例︰多位使用者觀賞高畫質影片 (例如 4K 解析度)、進行 HD 電話會議、玩 3D 視訊遊戲，或在 CAD 系統上工作。 所有這些動作甚至可能會讓真正高頻寬的網路無法使用。
* **畫面上的螢幕解析度和 hello 數目**-較多的網路頻寬是必要的 toofull 更新大螢幕與較小的螢幕。 hello 基礎技術很好的編碼和傳輸的已更新的 hello 螢幕 hello 區域但 hello 整個螢幕的狀態，需要 toobe 更新。 當 hello 使用者具有更高解析度螢幕 （例如 4k 解決方式） 時，該更新會需要更多的網路頻寬，比 （例如 1024x768px) 的較低解析度螢幕。 如果您使用數個螢幕進行重新導向，則適用這個相同的邏輯。 頻寬必須 tooincrease 與 hello 畫面數目。
* **剪貼簿和裝置的重新導向**-這是十分明顯的問題，但在許多情況下如果使用者儲存大量的資料 toohello 剪貼簿 中，會在一段時間的 hello 遠端桌面用戶端從該資訊 tootransfer toohello 伺服器。 hello 下游經驗可以受到 hello 體驗上游傳送嗨剪貼簿內容。 hello 同樣適用於裝置重新導向-如果掃描器或網路相機會產生大量資料，需要傳送 toobe toohello 上游伺服器，或在印表機需要 tooreceive 大型文件，或本機儲存體需要 hello 雲端 toocopy 中執行的 toobe 可用 tooan 應用程式大型的檔案，使用者可能會注意到畫面或暫時 「 凍結 」 視訊因為所需的 hello 裝置重新導向的 hello 資料增加 hello 網路頻寬需求。 

當您評估您的網路頻寬需求時，請確定 tooconsider 所有做為系統處理這些因素。

現在，返回 toohello[主要的網路頻寬文章](remoteapp-bandwidth.md)，或移動 tootesting 上您[網路頻寬](remoteapp-bandwidthtests.md)。

## <a name="learn-more"></a>詳細資訊
* [Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)](remoteapp-bandwidth.md)
* [Azure RemoteApp - testing your network bandwidth usage with some common scenarios (Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量)](remoteapp-bandwidthtests.md)
* [Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指導方針 (如果您無法自行測試))](remoteapp-bandwidthguidelines.md)

