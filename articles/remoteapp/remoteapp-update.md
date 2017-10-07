---
title: "aaaUpdate 您 Azure RemoteApp 集合 |Microsoft 文件"
description: "深入了解如何 tooupdate 您 Azure RemoteApp 集合"
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>更新 Azure RemoteApp 中的收藏
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

會有時間，無可避免地，當您需要 tooupdate hello 應用程式或映像在您的 Azure RemoteApp 集合。 如果您使用其中一個包含與您 Azure RemoteApp 訂用帳戶的雲端或混合式集合中的 hello 映像所有更新是由 Azure RemoteApp 本身，都處理，因此您可以輕鬆將。

不過，如果您使用自訂映像 （內建從頭或您所建立的修改其中一個我們映像），您必須負責維護 hello 映像和應用程式。 如果您的映像，或任何的內文中的 hello 應用程式，您會需要 tooupdate，您需要 toocreate hello 映像，然後按一下 取代 hello 現有映像的新更新版本的新更新映像集合中。

因此，您該如何更新您的收藏？ 相當簡單：

1. 更新您使用您的集合中的 hello 映像。 套用所需的任何修補程式或更新，然後將它儲存成新的名稱。
2. [上傳](remoteapp-uploadimage.md)或[匯入](remoteapp-image-on-azurevm.md)該映像 tooRemoteApp。
3. 現在，在 hello 集合頁面上，按一下**更新**。
4. 選擇 hello 新映像從 hello**範本映像**清單。
5. 以下是 hello 麻煩的部分-您需要如何 toodecide toodeal 與 hello 集合中目前正在使用應用程式的任何使用者。 您有下列選項的 hello:
   
   * **提供 hello 更新後的 60 分鐘給使用者**。 Hello 更新完成，因為 Azure RemoteApp 會顯示訊息 tooany 作用中的使用者告知的 toosave 其工作和記錄檔關閉並重新登入。 60 分鐘之後，任何未登出的作用中使用者將自動登出。 使用者可以立即重新登入。
   * **立即登出使用者**。 Hello 更新完成，如登出所有使用者自動而不發出警告。 如果您選擇此選項，使用者可能會遺失資料。 不過，它們可以重新連線 toohello 應用程式立即。
6. 按一下 hello 核取記號 toostart hello 更新。

