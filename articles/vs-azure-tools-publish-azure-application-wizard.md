---
title: "aaaUsing hello Visual Studio 發行 Azure 應用程式精靈 |Microsoft 文件"
description: "了解如何 tooconfigure hello hello Visual Studio 發行 Azure 應用程式精靈中的各種設定"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>使用 hello Visual Studio 發行 Azure 應用程式精靈
開發 Visual Studio 中的 web 應用程式之後，您可以發行該應用程式 tooan Azure 雲端服務使用 hello**發行 Azure 應用程式**精靈。 

> [!NOTE]
> 本主題是關於部署 toocloud 服務，不 tooweb 站台。 如需部署 tooweb 站台資訊，請參閱[如何 tooDeploy Azure 網站](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false)。
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>存取 hello 發行 Azure 應用程式精靈

您可以存取 hello 發行 Azure 應用程式精靈，根據您所擁有的 Visual Studio 專案 hello 類型有兩種。

**如果您有 Azure 雲端服務專案︰**

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**發行**。

**如果您有未啟用 Azure 的 Web 應用程式專案︰**

1. 在 Visual Studio 中建立或開啟 Azure 雲端服務專案。

1. 在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**轉換** > **轉換 tooAzure 雲端服務專案**。 

1. 在**方案總管 中**、 以滑鼠右鍵按一下新建立的 hello Azure 專案，和 hello 內容功能表中選取**發行**。

## <a name="sign-in-page"></a>登入頁面

![登入頁面](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**帳戶**-選取的帳戶，或選取**將帳戶加入**hello 帳戶下拉式清單中。

**選擇您的訂用帳戶**-選擇部署的 hello 訂用帳戶 toouse。
   
## <a name="settings-page---common-settings-tab"></a>設定頁面 - 一般設定索引標籤   

![一般設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**雲端服務**-使用 hello 下拉式清單中，選取現有的雲端服務，或選取**&lt;新建 >**，並建立雲端服務。 hello 資料中心會顯示在括號內的每個雲端服務。 建議的 hello 資料中心位置 hello 雲端服務是 hello 相同為 hello hello 儲存體帳戶 （進階設定） 的資料中心位置。  

**環境** - 選取 [生產] 或 [預備]。 選擇在測試環境中的 hello 預備環境，如果您想 toodeploy 您的應用程式。 

**建置組態** - 選取 [偵錯] 或 [發行]。

**服務組態** - 選取 [雲端] 或 [本機]。
   
**啟用所有角色的遠端桌面**-核取此選項，如果您想 toobe 無法 tooremotely toohello 服務連接。 此選項主要用於疑難排解。 當您選取此核取方塊時，hello**遠端桌面組態** 對話方塊隨即出現。 選擇 hello**設定**連結 toochange hello 組態。
   
**啟用所有 web 角色的 Web Deploy** -核取此選項，tooenable hello 服務的 web 部署。 您必須選取 hello**啟用所有角色的遠端桌面**選項 toouse 這項功能。 如需詳細資訊，請參閱[[使用 Visual Studio 發佈 Azure 雲端服務](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx)。 

## <a name="settings-page---advanced-settings-tab"></a>設定頁面 - 進階設定索引標籤

![進階設定](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**部署標籤**-接受 hello 預設名稱，或輸入您所選擇的名稱。 tooappend hello 日期 toohello 部署標籤，選取保持 hello 核取方塊。 
   
**儲存體帳戶**-選取 hello 這個部署的儲存體帳戶 toouse * *&lt;新建 > toocreate 儲存體帳戶。 hello 資料中心會顯示在括號內的每個儲存體帳戶。 建議的 hello 資料中心位置 hello 儲存體帳戶是 hello 相同為 hello hello 雲端服務 （通用設定） 的資料中心位置。  
   
hello Azure 儲存體帳戶會儲存 hello 應用程式部署的 hello 封裝。 Hello 應用程式部署之後，hello 封裝會從 hello 儲存體帳戶中移除。

**失敗時刪除部署**-選取發行期間發生任何錯誤，如果刪除此選項 toohave hello 部署。 如果您要為您的雲端服務的 toomaintain 常數的虛擬 IP 位址，這應取消選取。

**部署更新**-選取此選項，如果您想 toodeploy 只更新的元件。 這種部署類型比完整部署更快速。 如果您要為您的雲端服務的 toomaintain 常數的虛擬 IP 位址應該檢查此。 

**部署更新-設定**-使用此對話方塊是 toofurther 可讓您指定要更新的 hello 角色 toobe 的方式。 如果您選擇**累加式更新**，應用程式的每個執行個體是更新之後，因此該 hello 應用程式永遠都是可用。 如果您選擇**同時更新**，在 hello 更新您的應用程式的所有執行個體相同的時間。 同時更新較為快速，但您的服務可能無法使用 hello 更新程序期間。 

![部署設定](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**啟用 IntelliTrace** -指定是否要讓 tooenable IntelliTrace。 有了 IntelliTrace，您可以於角色執行個體在 Azure 中執行時，記錄其廣泛的偵錯資訊。 如果您需要 toofind hello 問題的原因，您可以使用 hello IntelliTrace 記錄檔 toostep，透過您的程式碼，從 Visual Studio 在 Azure 中執行一樣即可。 如需使用 IntelliTrace 的詳細資訊，請參閱[使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)。 

**啟用程式碼剖析**-指定是否要 tooenable 效能分析。 hello Visual Studio 分析工具可讓您 tooget hello 情況在計算方面的雲端服務的執行方式的深入分析。 如需有關使用 hello Visual Studio 分析工具的詳細資訊，請參閱[測試 Azure 雲端服務的 hello 效能](./vs-azure-tools-performance-profiling-cloud-services.md)。

**啟用所有角色的遠端偵錯工具**-指定是否要 tooenable 遠端偵錯。 如需使用 Visual Studio 進行雲端服務偵錯的詳細資訊，請參閱[在 Visual Studio 中進行 Azure 雲端服務或虛擬機器的偵錯](./vs-azure-tools-debug-cloud-services-virtual-machines.md)。

## <a name="diagnostics-settings-page"></a>診斷設定頁面

![診斷設定](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

診斷可讓您 tootroubleshoot Azure 雲端服務 （或 Azure 虛擬機器）。 如需診斷的相關資訊，請參閱[為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。 如需 Application Insights 的相關資訊，請參閱[什麼是 Application Insights？](./application-insights/app-insights-overview.md)。

## <a name="summary-page"></a>摘要頁面

![摘要](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Profile 當做目標**-您可以選擇 toocreate 發行設定檔從您所選擇的 hello 設定。 例如，您可能會建立一個設定檔用於測試環境，並建立另一個用於生產。 toosave 這個設定檔，選擇 hello**儲存**圖示。 hello 精靈會建立 hello 設定檔，並將它儲存在 hello Visual Studio 專案中。 toomodify hello 設定檔名稱，開啟 hello **profile 當做目標**清單，，然後選擇**< 管理... >**。
   
   > [!NOTE]
   > hello 發行設定檔會出現在 Visual Studio 中的 [方案總管] 中，hello 設定檔設定寫入 tooa 副檔名為.azurePubxml 的檔案。 設定會儲存為 XML 標記的屬性。
   > 
   > 

## <a name="publishing-your-application"></a>發佈您的應用程式

一旦您設定您的專案部署的所有 hello 設定時，選取**發行**在 hello hello 對話方塊底部。 您可以監視 hello 處理序狀態在 hello**輸出**Visual Studio 中的視窗。

## <a name="next-steps"></a>後續步驟
- [移轉並發行 Web 應用程式 tooan 從 Visual Studio 的 Azure 雲端服務](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [了解如何 toouse Visual Studio toopublish Azure 雲端服務](./vs-azure-tools-publishing-a-cloud-service.md)
- [使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [測試 Azure 雲端服務的 hello 效能](./vs-azure-tools-performance-profiling-cloud-services.md)
- [為 Azure 雲端服務和虛擬機器設定診斷功能](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。 
- [什麼是 Application Insights？](./application-insights/app-insights-overview.md)