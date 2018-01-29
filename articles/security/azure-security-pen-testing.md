---
title: "滲透測試 | Microsoft Docs"
description: "本文提供滲透測試 (pentest) 程序和如何對 Azure 基礎結構中執行的應用程式執行滲透測試的概觀。"
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
ms.date: 12/08/2017
ms.author: yurid
ms.openlocfilehash: dd5c874406ec184a2526a9eb0843cd6f3b6b3aa1
ms.sourcegitcommit: 094061b19b0a707eace42ae47f39d7a666364d58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="pen-testing"></a>滲透測試
使用 Azure 進行應用程式測試和部署的其中一個優點是您可以快速建立環境。  您無需購置、取得和組裝自己的內部部署硬體。

這很好 - 但您仍然需要確定您審慎執行一般的安全性作業。 您所要做的事情之一是對您在 Azure 中部署的應用程式進行滲透測試。

您可能已經知道 Microsoft 會執行 [我們的 Azure 環境的滲透測試](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)。 這有助於促進 Azure 改進。 

我們不會為您對應用程式進行滲透測試，但我們了解，您會想要並需要對自己的應用程式執行滲透測試。 那是件好事，因為當您增強應用程式的安全性時，便有助於讓整個 Azure 生態系統更加安全。

怎麼辦？

自 2017 年 6 月 15，Microsoft 已不再需要預先核准，才可進行徹底測試與 Azure 資源。 要正式文件即將滲透測試對 Microsoft Azure 合作的客戶是鼓勵填寫[Azure 服務滲透測試通知表單](https://portal.msrc.microsoft.com/engage/pentest)。 此程序只被有關 Microsoft Azure，並不適用於任何其他 Microsoft 雲端服務。 

>[!IMPORTANT] 
>雖然告知 Microsoft 畫筆測試活動的已不再需要客戶必須仍然符合[Microsoft 雲端整合滲透測試往來的規則](https://technet.microsoft.com/en-us/mt784683)。 

您可以執行的標準測試包括：

* 對端點進行測試，以發掘 [開放式 Web 應用程式安全性專案 (OWASP) 的前 10 大弱點](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [模糊測試](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) 
* [連接埠掃描](https://en.wikipedia.org/wiki/Port_scanner) 

您不能執行的一種測試是任何種類的 [拒絕服務 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) 攻擊。 這包括起始 DoS 攻擊本身，或是執行可能會決定、示範或模擬任何類型的 DoS 攻擊的相關測試。

## <a name="next-steps"></a>後續步驟

- 您是否已準備好要開始對主控於 Microsoft Azure 的您的應用程式進行滲透測試？ 如果是，請前往 [滲透測試概觀](https://technet.microsoft.com/library/mt784683.aspx) 頁面，然後按一下頁面底部的 [建立測試要求] 按鈕。 