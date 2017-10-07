---
title: "aaaCreate Azure 事件中心 |Microsoft 文件"
description: "建立 Azure 事件中樞命名空間和事件中心使用 hello Azure 入口網站"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>建立事件中樞命名空間和事件中心使用 hello Azure 入口網站

## <a name="create-an-event-hubs-namespace"></a>建立事件中樞命名空間
1. 登入 toohello [Azure 入口網站][Azure portal]，然後按一下**新增**hello 在左上方的囉 」 畫面。
1. 按一下 物聯網，然後按一下事件中樞。
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. 在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱。 hello 系統立即檢查 toosee hello 名稱是否可用。
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. 提供讓確定 hello 命名空間名稱之後，選擇 hello 定價層 （基本或標準）。 而且請 toocreate hello 資源選擇 Azure 訂用帳戶、 資源群組和位置。 
1. 按一下**建立**toocreate hello 命名空間。 您可能需要幾分鐘，讓 hello 系統 toofully 佈建 hello 資源 toowait。
2. 在 hello 入口網站清單的命名空間中，按一下新建立的命名空間的 hello。
2. 按一下 共用存取原則，然後按一下RootManageSharedAccessKey。
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. 按一下 hello 複製按鈕 toocopy hello **RootManageSharedAccessKey**連接字串 toohello 剪貼簿。 將這個連接字串儲存在暫存位置，例如 [記事本]，稍後 toouse。
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>建立事件中心

1. 在 hello 事件中樞命名空間清單中，按一下新建立的 hello 命名空間。      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. 在 hello 命名空間刀鋒視窗中，按一下 **事件中心**。
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. 在 hello hello 刀鋒視窗頂端，按一下**新增事件中樞**。
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. 輸入您的事件中樞名稱，然後按一下 [建立]。
   
    ![](./media/event-hubs-create/create-event-hub5.png)

現在建立事件中樞，和您擁有 hello 連接字串，您需要 toosend 與接收事件。

## <a name="next-steps"></a>後續步驟
toolearn 有關事件中心的詳細資訊，請前往下列連結：

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [事件中樞 API 概觀](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/