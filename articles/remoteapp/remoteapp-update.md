---
title: "更新 Azure RemoteApp 服務 | Microsoft Docs"
description: "了解如何更新 Azure RemoteApp 收藏"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>更新 Azure RemoteApp 中的收藏
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

無可避免地，總會有一次，您需要更新 Azure RemoteApp 收藏中的應用程式或映像。 如果您是使用 Azure RemoteApp 訂用帳戶隨附的其中一個映像，則在雲端或混合式收藏中，任何和所有的更新都是由 Azure RemoteApp 本身處理，因此您可以放手不管。

不過，如果您是使用自訂映像 (從頭建立的映像，或是修改其中一個我們的映像所建立的映像)，則您需負責維護映像和應用程式。 如果您需要更新映像或其內的任何應用程式，則需要建立映像的新的已更新版本，然後使用這個新的已更新映像取代集合中的現有映像。

因此，您該如何更新您的收藏？ 相當簡單：

1. 更新您在收藏中使用的映像。 套用所需的任何修補程式或更新，然後將它儲存成新的名稱。
2. 將該映像[上傳](remoteapp-uploadimage.md)或[匯入](remoteapp-image-on-azurevm.md)至 RemoteApp。
3. 現在，在 [收藏] 頁面上，按一下 [ **更新**]。
4. 從 [ **範本映像** ] 清單中選擇新的映像。
5. 以下是麻煩的部分 - 您必須決定如何處理任何目前正在使用收藏中應用程式的使用者。 您有下列選擇：
   
   * **更新後給與使用者 60 分鐘**。 一完成更新，Azure RemoteApp 就會顯示訊息給任何作用中使用者，告訴他們儲存工作並登出，然後重新登入。 60 分鐘之後，任何未登出的作用中使用者將自動登出。 使用者可以立即重新登入。
   * **立即登出使用者**。 一完成更新，就會自動登出所有使用者，而且沒有任何警告。 如果您選擇此選項，使用者可能會遺失資料。 不過，它們可以立即重新連接至應用程式。
6. 按一下核取記號以啟動更新。

