---
title: "使用 Visual Studio 中的 已連接服務的 Azure 儲存體 aaaAdd |Microsoft 文件"
description: "新增 Azure 儲存體 tooyour 應用程式使用 hello Visual Studio 加入已連接服務對話方塊"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>使用 Visual Studio 的已連接服務加入 Azure 儲存體
Visual Studio 中，您可以使用連接任何 hello 遵循 tooAzure 儲存體使用 hello**加入已連接服務**對話方塊：

- C# 雲端服務
- .NET 後端行動服務
- ASP.NET 網站或服務
- ASP.NET Core 服務
- Azure WebJob 服務 

hello 已連接的服務功能加入所有需要的 hello 參考和連線程式碼 tooyour 專案，並會適當地修改您的設定檔。 

完成之後，hello**加入已連接服務**對話方塊會自動顯示文件詳述 hello 步驟需要的 toostart 使用 blob 儲存體、 佇列和資料表。

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>連接 tooAzure 儲存體使用 hello 已連接服務對話方塊
1. 在 Visual Studio 中開啟您的專案

1. 在**方案總管 中**，以滑鼠右鍵按一下 hello**已連接服務** 節點，然後從 hello 內容功能表，然後選取**加入已連接服務**。
   
    ![新增 Azure 已連接服務](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. 在 hello**已連接服務**頁面上，選取**雲端儲存體與 Azure 儲存體**。
   
    ![新增 Azure 儲存體](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. 在 hello **Azure 儲存體**對話方塊中，選取現有的儲存體帳戶，並選取**新增**。
   
    如果您需要 toocreate 儲存體帳戶，請移 toohello 下一個步驟。 否則，請略過 toostep 6。
    
    ![加入現有的儲存體帳戶 tooproject](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate 儲存體帳戶： 
   
   1. 選取**建立新的儲存體帳戶**在 hello hello 對話方塊底部。

   1. 填寫 hello**建立儲存體帳戶** 對話方塊中，然後選取**建立**。
      
       ![新的 Azure 儲存體帳戶](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. 當 hello **Azure 儲存體** 對話方塊隨即出現，hello 新儲存體帳戶會顯示 hello 清單中。 在 [hello] 清單中，選取 hello 新儲存體帳戶，然後選取**新增**。

1. hello 儲存體已連接的服務之下 hello**服務參考**您的專案節點。
   
## <a name="how-your-project-is-modified"></a>您的專案修改方式
當您完成 hello 對話方塊時，Visual Studio 會將參考加入和修改某些組態檔。 hello 特定變更 hello 專案類型而定： 

- ASP.NET 專案 - [發生什麼事 - ASP.NET 專案](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- ASP.NET Core 專案 - [發生什麼事 - ASP.NET 5 專案](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- 雲端服務專案 (Web 角色和背景工作角色) - [發生什麼事 - 雲端服務專案](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- WebJob 專案 - [發生什麼事 - WebJob 專案](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>後續步驟
- [MSDN 論壇︰Azure 儲存體](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Microsoft Azure 儲存體小組部落格 (英文)](http://blogs.msdn.com/b/windowsazurestorage/)
- [Azure 儲存體文件](https://docs.microsoft.com/azure/storage/)
