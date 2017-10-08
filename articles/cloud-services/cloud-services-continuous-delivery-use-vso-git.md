---
title: "在 Azure 中的 Visual Studio Team Services 與 Git aaaContinuous 傳遞 |Microsoft 文件"
description: "了解如何 tooconfigure Visual Studio Team Services 的 team 的專案 toouse Git tooautomatically 建置和部署 Azure 應用程式服務或雲端服務中的 toohello Web 應用程式功能。"
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>使用 Visual Studio Team Services 和 Git 的持續傳遞 tooAzure
您可以使用 Visual Studio Team Services 團隊專案 toohost Git 儲存機制的原始程式碼，自動建置和 tooAzure web 應用程式部署或雲端服務，每當您推送認可 toohello 儲存機制。

您將需要 Visual Studio 2013 和 Azure SDK 安裝 hello。 如果您還沒有 Visual Studio 2013，下載選擇 hello**免費開始**連結[www.visualstudio.com](http://www.visualstudio.com)。安裝 hello 從 Azure SDK[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)。

> [!NOTE]
> 本教學課程需要 Visual Studio Team Services 帳戶 toocomplete： 您可以[免費開啟 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。
> 
> 

設定雲端服務 tooautomatically tooset 建置和部署使用 Visual Studio Team Services tooAzure，依照下列步驟。

## <a name="1-create-a-git-repository"></a>1：建立 Git 儲存機制。
1. 如果您還沒有 Visual Studio Team Services 帳戶，請在[這裡](http://go.microsoft.com/fwlink/?LinkId=397665)取得。 建立小組專案時，請選擇 Git 作為原始檔控制系統。 請遵循 hello 指示 tooconnect Visual Studio tooyour team 專案。
2. 在**Team Explorer**，選擇 hello**複製這個儲存機制**連結。
   
    ![][3]
3. 指定 hello hello 本機複本的位置，然後選擇 [hello**複製**] 按鈕。

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2： 建立專案，並加以認可 toohello 儲存機制
1. 在**Team Explorer**，在 hello**解決方案**區段中，選擇 hello**新增**連結 toocreate hello 本機儲存機制中新的專案。
   
    ![][4]
2. 您可以將 web 應用程式部署或雲端服務 （Azure 應用程式），由下列 hello 步驟在本逐步解說。 建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。 請確定 hello 專案的目標 hello.NET Framework 4 或更新版本。 如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色與背景工作角色。
   如果您想 toocreate web 應用程式，請選擇 hello **ASP.NET Web 應用程式**專案範本，然後選擇**MVC**。 如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md) 。
3. 開啟 hello hello 方案的捷徑功能表並選擇 **認可**。
   
    ![][7]
4. 如果這是 hello 第一次您在 Visual Studio Team Services 使用 Git，您必須 tooprovide 某些資訊 tooidentify 自行在 Git 中。 在 hello**暫止的變更**區域**Team Explorer**、 輸入您的使用者名稱和電子郵件地址。 輸入 hello 認可的註解，然後選擇 [hello**認可**] 按鈕。
   
    ![][8]
5. 請注意 hello 選項 tooinclude 或排除特定的變更，當您簽入。 如果 hello 變更您想要排除，請選擇**全部包含**。
6. 您現在已認可的 hello 變更 hello 儲存機制的本機複本中。 接下來，選擇 hello 同步這些變更與 hello 伺服器**同步**連結。

## <a name="3-connect-hello-project-tooazure"></a>3： 連接 hello 專案 tooAzure
1. 現在您有 Visual Studio Team Services 中具有某些來源中的程式碼它的 Git 儲存機制，您就準備 tooconnect 您的 git 儲存機制 tooAzure。  在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，選取 雲端服務或 web 應用程式，或建立一個新選擇 hello + 圖示 hello 左下方，然後選擇**雲端服務**或**Web 應用程式**然後**快速建立**。
   
    ![][9]
2. 雲端服務，選擇 hello**設定發行與 Visual Studio Team Services**連結。 針對 web 應用程式中，選擇 hello**設定從原始檔控制進行部署**連結。
   
    ![][10]
3. 在 hello 精靈中，在 hello 文字方塊中輸入 hello 您的 Visual Studio Team Services 帳戶名稱，然後選擇 hello**現在授權**連結。 您可能會要求 toosign 中。
   
    ![][11]
4. 在 hello**連線要求**快顯對話方塊中，選擇**接受**tooauthorize Azure tooconfigure 您 team 專案在 Visual Studio Team Services。
   
    ![][12]
5. 授權成功後，將出現含有 Visual Studio Team Services 之 Team 專案的下拉式清單。  選取 hello hello 先前步驟中，在您建立 team 專案名稱，然後選擇 hello 精靈的核取記號按鈕。
   
    ![][13]
   
    hello 推送認可 tooyour 儲存機制，Visual Studio Team Services 的下一次將建置和部署專案 tooAzure。

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4：觸發重建和重新部署專案
1. 在 Visual Studio 中，開啟檔案進行變更。 例如，變更 hello 檔案`_Layout.cshtml`hello 檢視下\\MVC web 角色中的共用資料夾。
   
    ![][17]
2. 編輯 hello 站台的 hello 頁尾文字，並儲存 hello 檔案。
   
    ![][18]
3. 在**方案總管 中**，hello 方案節點、 專案節點或 hello 檔案變更，您開啟 hello 捷徑功能表，然後選擇**認可**。
4. 輸入註解並選擇 [認可] 。
   
    ![][20]
5. 選擇 hello**同步**連結。
   
    ![][38]
6. 選擇 hello**推送**連結 toopush Visual Studio Team Services 在您認可 toohello 儲存機制。 (您也可以使用 hello**同步**按鈕 toocopy 您認可 toohello 儲存機制。 hello 的差別在於**同步**提取也 hello hello 儲存機制中的最新變更。)
   
    ![][39]
7. 選擇 hello**家用**按鈕 tooreturn toohello **Team Explorer**首頁。
   
    ![][21]
8. 選擇**建置**tooview hello 建置進行中。
   
    ![][22]
   
    **Team Explorer** 會顯示簽入已觸發的組建。
   
    ![][23]
9. tooview 詳細的記錄檔為 hello 建置進行時，連按兩下 hello 名稱 hello 建置進行中。
10. 進行中 hello 組建時，看看 hello 用 hello 精靈 toolink tooAzure 時所建立的組建定義。  開啟 hello hello 組建定義的捷徑功能表並選擇 **編輯組建定義**。
    
    ![][25]
11. 在 hello**觸發程序**索引標籤上，您會看到的 hello 組建定義 toobuild 上每個簽入，預設設定。 （雲端服務中，Visual Studio Team Services 建置和部署 hello 的主要分支 toohello 自動預備環境。 您仍然必須 toodo 手動步驟 toodeploy toohello 即時網站。 Web 應用程式中不是預備環境，它會將部署 hello 主要分支直接 toohello 即時網站。
    
    ![][26]
12. 在 hello**程序**索引標籤上，您可以看到 hello 部署環境設定的雲端服務或 web 應用程式的 toohello 名稱。
    
     ![][27]
13. 如果您想要比 hello 預設值不同的值，指定 hello 屬性的值。 hello 屬性 Azure 發行會在 hello**部署** 區段中，而且您可能也需要 tooset MSBuild 參數。 例如，在雲端服務專案中，toospecify 「 雲端 」，以外的服務組態中設定太 hello MSbuild 參數`/p:TargetProfile=[YourProfile]`其中*[YourProfile]*符合服務組態檔的名稱，例如使用ServiceConfiguration。*YourProfile*.cscfg。
    
     hello 下列資料表顯示 hello 可用的屬性中 hello**部署**> 一節：
    
    | 屬性 | 預設值 |
    | --- | --- |
    | 允許未受信任的憑證 |如果為 false，SSL 憑證必須經過根授權單位簽署。 |
    | 允許升級 |可讓 hello 部署 tooupdate 而不是建立一個新現有的部署。 會保留 hello IP 位址。 |
    | 不要刪除 |如果為 true，則不要覆寫現有不相關的部署 (允許升級)。 |
    | 路徑 tooDeployment 設定 |hello 路徑 tooyour.pubxml 檔案是 web 應用程式，相對 toohello hello 儲存機制根資料夾。 雲端服務則會忽略。 |
    | SharePoint 部署環境 |hello 與 hello 服務名稱的相同。 |
    | Azure 部署環境 |hello web 應用程式或雲端服務名稱。 |
14. 現在應該已順利完成您的組建。
    
     ![][28]
15. 如果您按兩下 hello 組建名稱時，Visual Studio 會顯示**組建摘要**，包括中的任何測試結果相關聯的單元測試專案。
    
     ![][29]
16. 在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，您可以檢視相關聯的 hello 部署上 hello**部署**索引標籤上，選取 預備環境的 hello 時。
    
     ![][30]
17. 瀏覽 tooyour 網站的 URL。 Web 應用程式中，只需選擇 hello**瀏覽**hello 入口網站中的按鈕。 雲端服務中，選擇 hello URL 在 hello**快速概覽**區段 hello**儀表板**顯示 hello 預備環境的頁面。
    
    從雲端服務的持續整合的部署都是預設的已發行的 toohello 預備環境。 您可以變更此設定 hello**替代雲端服務環境**屬性太**生產**。 以下是程式 hello 站台 URL 是在 hello 雲端服務的儀表板頁面上。
    
    ![][31]
    
    新的瀏覽器索引標籤會開啟 tooreveal 您執行的網站。
    
    ![][32]
18. 如果您進行的其他變更 tooyour 專案、 更建置您的觸發程序，和您將會累積多個部署。 hello 最近一個標示為 使用。
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5：重新部署舊版組建
此為選用步驟。 在 hello Azure 傳統入口網站，選擇先前的部署，然後選擇 **重新部署**toorewind 簽入之前您站台 tooan。 請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。

![][34]

## <a name="6-change-hello-production-deployment"></a>6： 變更 hello 生產環境部署
當您準備好時，您可以選擇升級 hello 臨時 toohello 生產環境**交換**hello Azure 傳統入口網站中。 新部署的 hello 臨時環境是已升級的 tooProduction 而 hello 先前生產環境中，如果有的話，會變成預備環境。 hello 作用中的部署可能會不同 hello 生產與預備環境，但最近組建 hello 部署歷程記錄是 hello 相同的環境而定。

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7：從工作分支部署。
當您使用 Git 時，您通常在工作分支中進行變更，並整合 hello 主要分支，當您開發達到完成的狀態。 Hello 專案的開發階段，您會想 toobuild 和部署 hello 工作分支 tooAzure。

1. 在**Team Explorer**，選擇 hello**首頁**按鈕，然後選擇 [hello**分支**] 按鈕。
   
    ![][40]
2. 選擇 hello**新分支**連結。
   
    ![][41]
3. 輸入 hello 名稱 hello 分支，例如 「 處理中 」，然後選擇 **建立分支**。 這樣會建立新的本機分支。
   
    ![][42]
4. 發行 hello 分支。 選擇在 hello 分支名稱**取消發行分支**，然後選擇 **發行**。
   
    ![][44]
5. 根據預設，只會變更 toohello 主要分支的觸發程序連續的組建。 連續建置工作分支，tooset 選擇 hello**建置**頁面**Team Explorer**，然後選擇 **編輯組建定義**。
6. 開啟 hello**來源設定** 索引標籤。在下**監視用於持續整合及建置分支**，選擇**按一下這裡 tooadd 新的資料列**。
   
    ![][47]
7. 指定在建立，例如 refs/heads/有效的 hello 分支。
   
    ![][48]
8. 進行變更以 hello 程式碼中，開啟 hello hello 變更檔案的捷徑功能表，然後選擇 **認可**。
   
    ![][43]
9. 選擇 hello**未同步處理認可**連結，然後選擇 hello**同步**按鈕或 hello**推送**連結 toocopy hello 變更 Visual Studio 中的 hello 工作分支的 toohello 副本Team Services。
   
   ![][45]
10. 瀏覽 toohello**建置**檢視，並尋找 hello 工作分支只收到觸發的 hello 組建。

## <a name="next-steps"></a>後續步驟
toolearn 秘訣在 Git 中使用 Visual Studio Team Services，請參閱[開發和共用您的程式碼中使用 Visual Studio 的 Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)及使用未受 Visual Studio Team Services toopublish 的 Git 儲存機制的相關資訊tooAzure，請參閱[連續部署 tooAzure App Service](../app-service-web/app-service-continuous-deployment.md)。 如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
