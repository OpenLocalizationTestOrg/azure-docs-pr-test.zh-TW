---
title: "aaaPen 測試 |Microsoft 文件"
description: "hello 文件提供 hello 滲透測試 (pentest) 處理程序的概觀，以及如何執行 pentest 針對您在 Azure 基礎結構中執行的應用程式。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>滲透測試
Hello 優點的應用程式測試和部署使用 Microsoft Azure 的其中一個是，您不需要 tooput 一起在內部部署基礎結構 toodevelop、 測試及部署您的應用程式。 所有的 hello 基礎結構是由 hello Microsoft Azure 平台服務的處理。 您不需要 tooworry 有關 requisitioning、 取得和"軌道和堆疊 」 在內部部署硬體。

這是很棒 –，但您仍須確定您執行一般的安全性 toomake 審慎。 其中一個，您需要的 hello 事情 toodo 是滲透測試 hello 應用程式在 Azure 中部署。

您可能已經知道 Microsoft 會執行 [我們的 Azure 環境的滲透測試](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)。 這有助於改善我們的平台，並在改善安全性控制、推出新的安全性控制及改善我們的安全性程序方面引導我們的行動。

我們不畫筆測試您的應用程式，但我們並了解，您會想要而且需要 tooperform 畫筆測試自己的應用程式。 這是好的結果，，因為當您加強 hello 應用程式的安全性，協助讓 hello 整個 Azure 生態系統的更安全。

當您畫筆測試您的應用程式時，看起來可能會攻擊 toous。 我們會 [持續監視](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) 攻擊模式，並且在需要時會起始事件回應程序。 它無法協助您，這樣不會有幫助我們我們觸發事件的回應到期 tooyour 自己到期勤加注意畫筆測試。

哪些 toodo？

當您準備好 toopen 測試 Azure 託管應用程式，您可以選擇太[讓我們知道](https://portal.msrc.microsoft.com/en-us/engage/pentest)。 我們知道您要執行特定測試的 toobe，我們將不會不小心關閉，您 （例如封鎖您要從測試的 hello IP 位址），只要您的測試符合 toohello Azure 畫筆測試的條款和條件中所述[Microsoft 雲端整合滲透測試往來的規則](https://technet.microsoft.com/en-us/mt784683)。
您可以執行的標準測試包括：

* 測試您的端點 toouncover hello[開啟 Web 應用程式安全性專案 (OWASP) 的前 10 個弱點](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [模糊測試](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) 
* [連接埠掃描](https://en.wikipedia.org/wiki/Port_scanner) 

您不能執行的一種測試是任何種類的 [拒絕服務 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) 攻擊。 這包括起始 DoS 攻擊本身，或是執行可能會決定、示範或模擬任何類型的 DoS 攻擊的相關測試。

正在準備 tooget 入門畫筆測試 Microsoft Azure 中裝載之應用程式嗎？ 如果是，則透過 toohello 前端上[滲透測試概觀](https://technet.microsoft.com/library/mt784683.aspx)頁面 （和按一下 hello 建立在 hello hello 頁面底部的 [測試要求] 按鈕。 您也可以找到測試條款及條件與有用的連結上如何報告安全性缺陷相關的 tooAzure 或任何其他 Microsoft 服務的 hello 畫筆上的詳細資訊。
