---
title: "aaaUsing APP-V 應用程式與 Azure RemoteApp |Microsoft 文件"
description: "深入了解如何在 Azure RemoteApp toouse APP-V 應用程式。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>在 Azure RemoteApp 使用 App-V 應用程式
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您可以需要加入網域的 Azure RemoteApp 混合式集合中，使用 App-V 應用程式。

開始之前，請確定 tooinstall hello APP-V 5.1 的用戶端 hello 最新的更新。 您將需要 toocreate[自訂映像](remoteapp-create-custom-image.md)包含 hello APP-V 用戶端。  

它是簡單 toouse Azure RemoteApp 在您現有的 APP-V 基礎結構。 由於混合式集合部署到 Azure VNET 具有存取 tooyour 網域控制站，而且 hello Vm 是已加入網域，您可以利用您現有的 app-v 基礎架構和部署方法 tooeasyily APP-V 應用程式中主應用程式 Azure RemoteApp。 以下是您應該留意根據您目前沒有的 APP-V 應用程式部署的 hello 類型的一些考量：

| 組態選項 |  | Positive | Neutral |
| --- | --- | --- | --- |
| 傳遞方法 |串流 (隨選) |應用程式一律為最新和最新狀態的 hello |第一次的延遲 |
| 裝載 |最快。應用程式已存在於 hello VM 上 |膨脹 - 佔據映像空間 (127 GB 限制) | |
| 應用程式位置儲存體 |共用的內容 |在 Azure RemoteApp 執行個體的記憶體中執行的應用程式 |會吞掉記憶體和良好連線 toostreaming （檔案） 伺服器 hello 應用程式所在的位置 |
| 磁碟 (快取) |快速執行。 應用程式不相依於內容來源的可用性 |膨脹 - 佔據映像空間 (127 GB 限制) | |
| 目標 |User |需要完整獨立的 App-V 基礎結構 | |
| 全域 (電腦) |預先發佈或使用發佈伺服器做為目標 |如果您想 tooupdate hello 應用程式 （大型），需要 tooupdate Azure 映像。 會佔用映像的一些空間。 | |

 您建立自訂映像和混合式集合之後，發佈您的應用程式，請將使用者指派並享受裝載於 Azure RemoteApp 傳遞 tooany 裝置、 任何現有的 APP-V 應用程式。

