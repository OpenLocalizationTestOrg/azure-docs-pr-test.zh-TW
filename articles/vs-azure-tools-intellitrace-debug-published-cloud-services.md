---
title: "aaaDebugging 已發行的 Azure 雲端服務與 Visual Studio 和 IntelliTrace |Microsoft 文件"
description: "了解如何 toodebug 雲端服務與 Visual Studio 和 IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯
有了 IntelliTrace，您可以於角色執行個體在 Azure 中執行時，記錄其廣泛的偵錯資訊。 如果您需要 toofind hello 問題的原因，您可以使用 hello IntelliTrace 記錄檔 toostep，透過您的程式碼，從 Visual Studio 在 Azure 中執行一樣即可。 實際上，IntelliTrace 記錄索引鍵的程式碼執行和環境資料時以雲端服務在 Azure 中，執行 Azure 應用程式，並讓您重新執行從 Visual Studio 的 hello 記錄資料。 

如果您有安裝 Visual Studio Enterprise，而您的 Azure 應用程式以 .NET Framework 4 或更新版本為目標，則可以使用 IntelliTrace。 IntelliTrace 會收集 Azure 角色的資訊。 hello 這些角色的虛擬機器永遠會執行 64 位元作業系統。

或者，您可以使用[遠端偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623041)tooattach 直接 tooa 雲端服務是在 Azure 中執行。

> [!IMPORTANT]
> IntelliTrace 僅適用於偵錯，並且不應該用於生產環境部署。
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>為 IntelliTrace 設定 Azure 應用程式
tooenable IntelliTrace Azure 應用程式，您必須建立並發行 hello 應用程式，從 Visual Studio Azure 專案。 TooAzure 發行之前，您必須將 IntelliTrace 設定 Azure 應用程式中。 如果您發行應用程式但未設定 IntelliTrace，您會需要 toorepublish hello 專案。 如需詳細資訊，請參閱[使用 Visual Studio 專案發佈 Azure 雲端服務](http://go.microsoft.com/fwlink/p/?LinkId=623012)。

1. 當您準備就緒 toodeploy Azure 應用程式，請確認專案建置目標已設定太**偵錯**。

1. 在**方案總管 中**，以滑鼠右鍵按一下專案，然後 hello 內容功能表中選取**發行**。
   
1. 在 hello**發行 Azure 應用程式**對話方塊中，選取 hello Azure 訂用帳戶，並選取**下一步**。

1. 在 [hello**設定**頁面上，選取 hello**進階設定**] 索引標籤。

1. 開啟 hello**啟用 IntelliTrace**選項 toocollect IntelliTrace 記錄檔以取得您的應用程式發佈 hello 定域機組中時。
   
1. toocustomize hello 基本 IntelliTrace 組態中，選取**設定**下一步太**啟用 IntelliTrace**。

    ![IntelliTrace 設定連結](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. 在 [hello **IntelliTrace 設定**] 對話方塊中，您可以指定哪些事件 toolog、 是否 toocollect 呼叫資訊、 哪些模組和處理序 toocollect 的記錄，以及多少空間 tooallocate toohello 錄製。 如需有關 IntelliTrace 的詳細資訊，請參閱 [使用 IntelliTrace 進行偵錯](http://go.microsoft.com/fwlink/?LinkId=214468)。
   
    ![IntelliTrace 設定](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

hello IntelliTrace 記錄檔是 hello 大小上限 （hello 預設大小為 250 MB） 的 hello IntelliTrace 設定中指定的循環記錄檔。 IntelliTrace 記錄檔會收集的 tooa hello hello 虛擬機器的檔案系統中的檔案。 當您要求 hello 記錄檔時，快照集時間中該時間點取得，而下載 tooyour 本機電腦。

已發行的 tooAzure hello Azure 雲端服務。 之後，您可以判斷是否已啟用 IntelliTrace 從 hello Azure 中的節點**伺服器總管**hello 下列影像所示：

![伺服器總管 - 已啟用 IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>下載角色執行個體的 IntelliTrace 記錄檔
使用 Visual Studio，您可以依照下列步驟來下載角色執行個體的 IntelliTrace 記錄檔：

1. 在**伺服器總管**，依序展開 [hello**雲端服務**] 節點，並找出角色執行個體想 toodownload 為記錄檔。 

1. Hello 角色執行個體，以滑鼠右鍵按一下，然後從 hello s 內容功能表中，選取**檢視 IntelliTrace 記錄檔**。 

    ![[檢視 IntelliTrace 記錄檔] 功能表選項](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. hello IntelliTrace 記錄檔會在本機電腦上的下載的 tooa 檔案的目錄中。 您要求 hello IntelliTrace 記錄檔，每次建立新的快照。 Visual Studio 下載的 hello 記錄檔，同時顯示 hello 作業進度的 hello hello **Azure 活動記錄檔**視窗。 Hello 遵循圖所示，您可以展開 hello 作業 toosee hello 線條項目更多詳細資料。

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Hello IntelliTrace 記錄檔會下載時，您可以在 Visual Studio 中繼續 toowork。 當下載完成 hello 記錄之後時，會開啟 Visual Studio 中。

> [!NOTE]
> hello IntelliTrace 記錄檔可能包含例外狀況會產生該 hello 架構，並處理之後。 內部架構程式碼會在正常啟動角色時產生這些例外狀況，因此您可以放心忽略。
> 
> 

## <a name="next-steps"></a>後續步驟
- [進行 Azure 雲端服務偵錯的選項](vs-azure-tools-debugging-cloud-services-overview.md)
- [使用 Visual Studio 發佈 Azure 雲端服務](vs-azure-tools-publishing-a-cloud-service.md)