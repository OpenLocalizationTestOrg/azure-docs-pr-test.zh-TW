---
title: "aaaDeploy 您的應用程式 tooAzure 和 Azure 堆疊 |Microsoft 文件"
description: "了解 toodeploy 應用程式 tooAzure 和 Azure 的混合式 CI/CD 堆疊的管線。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: a468d7da6f34d04809ee98463a8c4146da581015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-apps-tooazure-and-azure-stack"></a>部署應用程式 tooAzure 和 Azure 堆疊
在混合式[連續整合](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[持續傳遞](https://www.visualstudio.com/learn/what-is-continuous-delivery/)(CI/CD) 管線可讓您 toobuild、 測試及部署您的應用程式 toomultiple 雲端。  在本教學課程中，您會建立範例環境 toolearn 混合式 CI/CD 管線可以幫助您：
 
> [!div class="checklist"]
> * 啟始程式碼認可 tooyour Visual Studio Team Services (VSTS) 儲存機制為基礎的新組建。
> * 使用者接受度測試您新建立的程式碼 tooAzure 來自動部署。
> * 一旦您的程式碼已通過測試，來自動部署 tooAzure 堆疊。 


## <a name="prerequisites"></a>必要條件
幾個元件需要的 toobuild 混合式 CI/CD 管線，可能需要一些時間 tooprepare。  如果您已經有其中某些元件，請確定它們符合 hello 需求，在開始之前。

本主題也假設您擁有 Azure 和 Azure Stack 的部分知識。 如果您想再繼續進行更多的 toolearn，是確定 toostart 使用這些主題：

- [簡介 tooAzure](https://docs.microsoft.com/azure/fundamentals-introduction-to-azure)
- [Azure Stack 重要概念](azure-stack-key-features.md)

### <a name="azure"></a>Azure
 - 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。
 - 建立 [Web 應用程式](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)，並將其設定為用於 [FTP 發行](../app-service-web/app-service-deploy-ftp.md)。  請記下 hello 新的 Web 應用程式 URL，因為它正稍後使用。


### <a name="azure-stack"></a>Azure Stack
 - [部署 Azure Stack](azure-stack-run-powershell-script.md)。  hello 安裝程序通常需要幾小時 toocomplete，因此據此計畫。
 - 部署[App Service](azure-stack-app-service-deploy.md) PaaS 服務 tooAzure 堆疊。
 - 建立 Web 應用程式，並將其設定為用於 [FTP 發行](azure-stack-app-service-enable-ftp.md)。  請記下 hello 新的 Web 應用程式 URL，因為它正稍後使用。  

### <a name="developer-tools"></a>開發人員工具
 - 建立 [VSTS 工作區](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。  hello 註冊程序會建立專案，名為"MyFirstProject。 」  
 - [安裝 Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio)和[tooVSTS 登入](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)
 - Toohello 專案連接和[在本機複製](https://www.visualstudio.com/docs/git/gitquickstart)。
 - 在 VSTS 中建立[代理程式集區](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues)。
 - 安裝 Visual Studio 和部署[VSTS 組建代理程式](https://www.visualstudio.com/docs/build/actions/agents/v2-windows)tooa Azure 堆疊上的虛擬機器。 
 

## <a name="create-app--push-toovsts"></a>建立應用程式與推入 tooVSTS

### <a name="create-application"></a>建立應用程式
在本節中，您會建立簡單的 ASP.NET 應用程式，並將它推送 tooVSTS。  這些步驟代表 hello 一般開發人員的工作流程，而無法調整為開發人員工具和語言。 

1.  開啟 Visual Studio。
2.  從 Team Explorer 空間 hello 和**方案...**區域中，按一下 **新增**。
3.  選取 [Visual C#]  >  [Web]  >  [ASP.NET Web 應用程式 (.NET Framework)]。
4.  提供 hello 應用程式的名稱，然後按**確定**。
5.  在 hello 下一個畫面上，保留 hello 預設 (Web form)，然後按一下**確定**。

### <a name="commit-and-push-changes-toovsts"></a>認可並推送變更 tooVSTS
1.  使用 Team Explorer，在 Visual Studio 中，選取 [hello] 下拉式清單，然後按一下**變更**。
2.  提供認可訊息，然後選取 [全部認可]。 您可能會提示的 toosave hello 方案檔，請按一下 [是] toosave 所有。
3.  經過認可之後，Visual Studio 會詢問 toosync 變更 tooyour 專案。 選取 [同步]。

    ![映像顯示 hello 認可螢幕完成認可](./media/azure-stack-solution-pipeline/image1.png)

4.  在 hello 同步處理 索引標籤下*連出*，您會看到您新的認可。  選取**推送**toosynchronize hello 變更 tooVSTS。

    ![顯示同步步驟的影像](./media/azure-stack-solution-pipeline/image2.png)

### <a name="review-code-in-vsts"></a>檢閱 VSTS 中的程式碼
您一次認可變更並推送 tooVSTS，檢查您的程式碼從 hello VSTS 入口網站。  選取**程式碼**，然後**檔案**hello 下拉式功能表中。  您可以看到您所建立的 hello 方案。

## <a name="create-build-definition"></a>建立組建定義
hello 建置程序會定義您的應用程式如何建置和封裝部署在每個認可的程式碼變更。 在本例中，我們使用 hello 包含範本 tooconfigure hello 建置流程的 ASP.NET 應用程式中，雖然這個組態可能是適用於根據您的應用程式。

1.  登入 tooyour VSTS 工作區，從網頁瀏覽器。
2.  從 hello 的橫幅中，選取**建置和發行**然後**建置**。
3.  選取 [+新增定義]。
4.  從範本 hello 清單，選取**ASP.NET （預覽）**選取**套用**。
5.  修改 hello *MSBuild 引數*欄位*建置方案*逐步執行至：

    `/p:DeployOnBuild=True /p:WebPublishMethod=FileSystem /p:DeployDefaultTarget=WebPublish /p:publishUrl="$(build.artifactstagingdirectory)\\"`

6.  選取 hello**選項**索引標籤，然後選取 hello 代理程式佇列 hello 組建代理程式的設定，您部署 tooa 虛擬機器 Azure 堆疊上。 
7.  選取 hello**觸發程序**索引標籤，然後啟用**連續整合**。
7.  按一下**儲存，並佇列**，然後選取 **儲存**從 hello 下拉式清單。 

## <a name="create-release-definition"></a>建立發行定義
hello 發行程序定義如何從 hello 上一個步驟的組建部署的 tooan 環境。  在本教學課程中，我們發行我們與 FTP tooan Azure Web 應用程式的 ASP.NET 應用程式。 tooconfigure 發行 tooAzure，使用下列步驟的 hello:

1.  從 hello VSTS 橫幅中，選取**建置和發行**然後**版本**。
2.  按一下綠色的 hello **+ 新定義**。
3.  選取 [空白] ，然後按一下 [下一步]。
4.  核取方塊 hello*連續部署*，然後按一下**建立**。

現在，您已建立空白的發行定義，並繫結它 toohello 組建，我們將新增 hello Azure 環境的步驟：

1.  按一下綠色的 hello  **+**  tooadd 工作。
2.  選取**所有**，然後從 [hello] 清單中，加入**FTP 上傳**選取**關閉**。
3.  選取 hello **FTP 上傳**您剛才加入的工作，並設定下列參數的 hello:
    
    | 參數 | 值 |
    | ----- | ----- |
    |驗證方法| 輸入認證|
    |伺服器 URL | 從 Azure 入口網站取出 Web 應用程式 FTP URL |
    |使用者名稱 | 建立 Web 應用程式的 FTP 認證時所設定的使用者名稱 |
    |密碼 | 建立 Web 應用程式的 FTP 認證時所建立的密碼|
    |來源目錄 | $(System.DefaultWorkingDirectory)\**\ |
    |遠端目錄 | /site/wwwroot/ |
    |保留檔案路徑 | 已啟用 (已勾選)|

4.  按一下 [儲存] 

最後，您可以設定 hello 發行定義 toouse hello 代理程式集區包含 hello 代理程式部署使用 hello 下列步驟：
1.  選取 hello 發行定義，然後按一下**編輯**。
2.  選取**代理程式上執行**從 hello 中間的資料行。  Hello 右邊資料行中，選取 hello 代理程式的佇列包含 hello Azure 堆疊上執行的組建代理程式。  
    ![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image3.png)


## <a name="deploy-your-app-tooazure"></a>部署應用程式 tooAzure
這個步驟會在 Azure 上使用您新建立的 CI/CD 管線 toodeploy hello ASP.NET 應用程式 tooa Web 應用程式。 

1.  從 VSTS 中的 hello 橫幅中，選取**建置和發行**，然後選取**建置**。
2.  按一下**...** hello 上建置先前建立的定義，然後選取**新組建排入佇列**。
3.  接受 hello 預設值，並按一下**確定**。  hello 組建開始，並顯示進度。
4.  Hello 建置完成之後，您可以藉由選取追蹤 hello 狀態**建置和發行**，然後選取**版本**。
5.  Hello 建置完成之後，請瀏覽 hello 網站使用 hello 時會建立 hello Web 應用程式的 URL。    


## <a name="add-azure-stack-toopipeline"></a>新增 Azure 堆疊 toopipeline
現在，您藉由部署 tooAzure 測試 CI/CD 管線，它會是時間 tooadd Azure 堆疊 toohello 管線。  在 hello 下列步驟，您可以建立新的環境，並加入 FTP 上傳工作 toodeploy 您應用程式 tooAzure 堆疊。  您也會加入做為 「 簽署 」 的程式碼發行 tooAzure 堆疊方式 toosimulate 版本位核准者。  

1.  在 hello 發行定義中，選取  **+ 加入環境**和**建立新環境**。
2.  選取 [空白] 並按一下 [下一步]。
3.  選取 [特定使用者] 並指定您的帳戶。  選取 [ **建立**]。
4.  重新命名選取的 hello 環境 hello 現有名稱，然後輸入*Azure 堆疊*。
5.  現在，hello Azure 堆疊環境中，選取項目，然後選取 **新增工作**。
6.  選取 hello **FTP 上傳**工作，並選取**新增**，然後選取**關閉**。


### <a name="configure-ftp-task"></a>設定 FTP 工作
既然您已建立版本，您需要設定 hello 發行 toohello Azure 堆疊上的 Web 應用程式所需的步驟。  就像您為 Azure 設定 hello FTP 上傳工作，您會設定為 Azure 堆疊 hello 工作：

1.  選取 hello **FTP 上傳**您剛才加入的工作，並設定下列參數的 hello:
    
    | 參數 | 值 |
    | -----     | ----- |
    |驗證方法| 輸入認證|
    |伺服器 URL | 從 Azure Stack 入口網站取出 Web 應用程式 FTP URL |
    |使用者名稱 | 建立 Web 應用程式的 FTP 認證時所設定的使用者名稱 |
    |密碼 | 建立 Web 應用程式的 FTP 認證時所建立的密碼|
    |來源目錄 | $(System.DefaultWorkingDirectory)\**\ |
    |遠端目錄 | /site/wwwroot/|
    |保留檔案路徑 | 已啟用 (已勾選)|

2.  按一下 [儲存] 

最後，設定 hello 發行定義 toouse hello 代理程式集區包含 hello 代理程式部署使用 hello 下列步驟：
1.  選取 hello 發行定義，然後按一下**編輯**
2.  選取**代理程式上執行**從 hello 中間的資料行。 Hello 右邊資料行中，選取 hello 代理程式的佇列包含 hello Azure 堆疊上執行的組建代理程式。  
    ![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image3.png)

## <a name="deploy-new-code"></a>部署新程式碼
您現在可以測試具有 hello 最後一個步驟發行 tooAzure 堆疊，hello 混合式 CI/CD 管線。  本節中，您可以修改 hello 站台的頁尾，並開始透過 hello 管線進行部署。  完成後，您會看到您的變更部署 tooAzure 供檢閱，則一旦核准 hello 版本時，它們並發行的 tooAzure 堆疊。

1. 在 Visual Studio 中，開啟 hello *site.master*檔案，並變更這一行：
    
    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
    `

    toothis:

    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application delivered by VSTS, Azure, and Azure Stack</p>
    `
3.  Hello 將變更認可並同步 tooVSTS。  
4.  從 hello VSTS 工作區中，檢查選取 hello 組建狀態**建置和發行** > **建置**
5.  您將會看到進行中的組建。  按兩下 hello 狀態，您可以觀看 hello 建置進度。  一旦您在 hello 主控台中看到 [已完成的組建]，移動 toocheck hello 發行從**建置和發行** > **釋放**。  按兩下 hello 版本。
6.  您將會收到一則發行需要檢閱的通知。 檢查 hello Web 應用程式 URL 並確認 hello 新的變更會出現。  核准在 VSTS 中的 hello 版本。
    ![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image4.png)
    
7.  請確認發行 tooAzure 堆疊瀏覽 hello 網站使用 hello 時會建立 hello Web 應用程式的 URL 已完成。
    ![顯示 ASP.NET 應用程式以及已變更頁尾的影像](./media/azure-stack-solution-pipeline/image5.png)


您現在可以使用新的混合式 CI/CD 管線作為其他混合式雲端模式的建置組塊。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toobuild CI/CD 的混合式管線的：

> [!div class="checklist"]
> * 會啟動新的組建程式碼認可 tooyour Visual Studio Team Services (VSTS) 儲存機制為基礎。
> * 將使用者接受度測試您新建立的程式碼 tooAzure 自動部署。
> * 一旦您的程式碼已通過測試，自動將部署 tooAzure 堆疊。 

有混合式 CI/CD 管線之後，繼續學習如何針對 Azure 堆疊 toodevelop 應用程式。

> [!div class="nextstepaction"]
> [開發 Azure Stack](azure-stack-developer.md)


