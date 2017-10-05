---
title: "搭配 Azure RemoteApp 使用 App-V 應用程式 | Microsoft Docs"
description: "了解如何在 Azure RemoteApp 中使用 App-V 應用程式"
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>在 Azure RemoteApp 使用 App-V 應用程式
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

您可以需要加入網域的 Azure RemoteApp 混合式集合中，使用 App-V 應用程式。

開始之前，請務必使用最新的更新安裝 App-V 5.1 用戶端。 您必須建立包含 App-V 用戶端的 [自訂映像](remoteapp-create-custom-image.md) 。  

搭配 Azure RemoteApp 使用現有的 App-V 基礎結構很容易。 由於混合式集合是部署到 Azure VNET，它可以存取您的網域控制站，而且 VM 已加入網域，所以您可以利用您現有的 App-V 基礎架構和部署方法，輕易地在 Azure RemoteApp 內裝載 App-V 應用程式。 以下是您應該根據您目前擁有的 App-V 部署類型，注意的一些考量：

| 組態選項 |  | Positive | Neutral |
| --- | --- | --- | --- |
| 傳遞方法 |串流 (隨選) |應用程式永遠是最新和全新 |第一次的延遲 |
| 裝載 |最快；應用程式已存在於 VM 上 |膨脹 - 佔據映像空間 (127 GB 限制) | |
| 應用程式位置儲存體 |共用的內容 |在 Azure RemoteApp 執行個體的記憶體中執行的應用程式 |會耗用記憶體和與應用程式所在的串流 (檔案) 伺服器的良好連線 |
| 磁碟 (快取) |快速執行。 應用程式不相依於內容來源的可用性 |膨脹 - 佔據映像空間 (127 GB 限制) | |
| 目標 |User |需要完整獨立的 App-V 基礎結構 | |
| 全域 (電腦) |預先發佈或使用發佈伺服器做為目標 |如果您想要更新應用程式 (大) 則需要更新您的 Azure 映像。 會佔用映像的一些空間。 | |

 您建立自訂映像和混合式集合之後，發佈您的應用程式、指派使用者並享受裝載於傳遞至任何位置任何裝置的 Azure RemoteApp 中的現有 App-V 應用程式。

