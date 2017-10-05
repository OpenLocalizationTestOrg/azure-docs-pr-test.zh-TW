---
title: "在 Azure 中使用 Git 和 Visual Studio Team Services 來持續傳遞 | Microsoft Docs"
description: "了解如何設定 Visual Studio Team Services 的 Team 專案，以使用 Git 自動建置和部署至 Azure App Service 或雲端服務中的 Web 應用程式功能。"
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a>使用 Visual Studio Team Services 和 Git 連續傳遞至 Azure
您可以使用 Visual Studio Team Services 的 Team 專案託管原始程式碼的 Git 儲存機制，並在每次將認可推送至儲存機制時，自動建置該機制並部署至 Azure Web 應用程式或雲端服務。

您需要安裝 Visual Studio 2013 和 Azure SDK。 如果您還沒有 Visual Studio 2013，請至 [www.visualstudio.com](http://www.visualstudio.com) 選擇 [免費開始用] 連結來下載。 從[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)安裝 Azure SDK。

> [!NOTE]
> 您需要 Visual Studio Team Services 帳戶，才能完成本教學課程：您可以 [開啟免費的 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。
> 
> 

若要使用 Visual Studio Team Services 將雲端服務設定為自動建立和部署至 Azure，請依照下列步驟進行。

## <a name="1-create-a-git-repository"></a>1：建立 Git 儲存機制。
1. 如果您還沒有 Visual Studio Team Services 帳戶，請在[這裡](http://go.microsoft.com/fwlink/?LinkId=397665)取得。 建立小組專案時，請選擇 Git 作為原始檔控制系統。 依照指示將 Visual Studio 連接至小組專案。
2. 在 **Team Explorer** 中，選擇 [複製這個儲存機制] 連結。
   
    ![][3]
3. 指定本機複本的位置，然後選擇 [複製]  按鈕。

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a>2：建立專案並認可至儲存機制
1. 在 **Team Explorer** 中，在 [方案] 區段中選擇 [新增] 連結，在本機儲存機制中建立新專案。
   
    ![][4]
2. 您可以依照此逐步解說的步驟部署 Web 應用程式或雲端服務 (Azure 應用程式)。 建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。 請確認專案以 .NET Framework 4 或更新版本為目標。 如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色與背景工作角色。
   如果要建立 Web 應用程式，請選擇 [ASP.NET Web 應用程式] 專案範本，然後選擇 [MVC]。 如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md) 。
3. 開啟方案的捷徑功能表，選擇 [認可] 。
   
    ![][7]
4. 如果是第一次在 Visual Studio Team Services 中使用 Git，您需要提供一些資訊在 Git 中識別您的身分。 在 **Team Explorer** 的 [暫止的變更] 區域中，輸入您的使用者名稱和電子郵件地址。 輸入認可的註解，然後選擇 [認可]  按鈕。
   
    ![][8]
5. 請注意簽入時用來包含或排除特定變更的選項。 如果已排除您要的變更，請選擇 [全部包含] 。
6. 您現在已在儲存機制的本機複本中認可變更。 接下來，選擇 [同步處理]  連結，將這些變更同步至伺服器。

## <a name="3-connect-the-project-to-azure"></a>3：將專案連線至 Azure
1. 現在，您在 Visual Studio Team Services 中有一個 Git 儲存機制，裡面還有一些原始程式碼，您可以準備將 Git 儲存機制連接至 Azure。  在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取您的雲端服務或 Web 應用程式，或選取左下方的 + 圖示並選擇 [雲端服務] 或 [Web 應用程式]，然後選取 [快速建立]，建立新的雲端服務或 Web 應用程式。
   
    ![][9]
2. 若是雲端服務，請擇 [使用 Visual Studio Team Services 設定發行]  連結。 若是 Web 應用程式，請選擇 [設定從原始檔控制進行部署]  連結。
   
    ![][10]
3. 在精靈中，於文字方塊中輸入 Visual Studio Team Services 帳戶的名稱，然後選擇 [立即授權]  連結。 可能會要求您登入。
   
    ![][11]
4. 在 [連接要求] 快顯對話方塊中，選擇 [接受]，授權 Azure 在 Visual Studio Team Services 中設定 Team 專案。
   
    ![][12]
5. 授權成功後，將出現含有 Visual Studio Team Services 之 Team 專案的下拉式清單。  選取您在先前步驟中建立的小組專案，然後選擇精靈的勾選記號按鈕。
   
    ![][13]
   
    您下次將認可推送至儲存機制時，Visual Studio Team Services 將會建置專案並部署至 Azure。

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4：觸發重建和重新部署專案
1. 在 Visual Studio 中，開啟檔案進行變更。 例如，在 MVC Web 角色中，變更 Views\\Shared 資料夾下的 `_Layout.cshtml` 檔案。
   
    ![][17]
2. 編輯網站的頁尾文字，然後儲存檔案。
   
    ![][18]
3. 在 [方案總管] 中，開啟方案節點、專案節點或您變更之檔案的快顯功能表，然後選擇 [認可]。
4. 輸入註解並選擇 [認可] 。
   
    ![][20]
5. 選擇 [ **同步處理** ] 連結。
   
    ![][38]
6. 選擇 [推送]  連結，將認可推送至 Visual Studio Team Services 中的儲存機制。 (您也可以使用 [同步處理]  按鈕，將認可複製到儲存機制。 差別在於 [同步處理]  還會從儲存機制中提取最新的變更)。
   
    ![][39]
7. 選擇 [首頁] 按鈕回到 **Team Explorer** 首頁。
   
    ![][21]
8. 選擇 [組建]  來檢視進行中的組建。
   
    ![][22]
   
    **Team Explorer** 會顯示簽入已觸發的組建。
   
    ![][23]
9. 若要在組建進行時檢視詳細記錄，請按兩下進行中組建的名稱。
10. 當組建進行時，查看您使用精靈連結至 Azure 時所建立的組建定義。  開啟組建定義的捷徑功能表，然後選擇 [編輯組建定義] 。
    
    ![][25]
11. 在 [觸發程序]  索引標籤中，您會看到組建定義已設為依預設每次簽入時建置。 (若是雲端服務，Visual Studio Team Services 會自動建置主要分支並部署至預備環境。 您仍然必須執行手動步驟來部署至即時網站。 對於沒有預備環境的 Web 應用程式，它會將主要分支直接部署到即時網站。
    
    ![][26]
12. 在 [處理序]  索引標籤中，您可以看到部署環境已設為您的雲端服務或 Web 應用程式的名稱。
    
     ![][27]
13. 如果不想要使用預設值，請指定屬性的值。 Azure 發佈屬性在 [部署]  區段中，您也可能需要設定 MSBuild 參數。 例如，在雲端服務專案中，若要指定 "Cloud" 以外的服務組態，請將 MSbuild 參數設為 `/p:TargetProfile=[YourProfile]`，其中，[YourProfile] 符合一個以 ServiceConfiguration.YourProfile.cscfg 命名的服務組態檔。
    
     下表顯示 [部署]  區段中可用的屬性：
    
    | 屬性 | 預設值 |
    | --- | --- |
    | 允許未受信任的憑證 |如果為 false，SSL 憑證必須經過根授權單位簽署。 |
    | 允許升級 |允許部署更新現有的部署而非建立新的部署。 保留 IP 位址。 |
    | 不要刪除 |如果為 true，則不要覆寫現有不相關的部署 (允許升級)。 |
    | 部署設定的路徑 |Web 應用程式的 .pubxml 檔的路徑，這是儲存機制之根資料夾的相對路徑。 雲端服務則會忽略。 |
    | SharePoint 部署環境 |與服務名稱相同。 |
    | Azure 部署環境 |Web 應用程式或雲端服務的名稱。 |
14. 現在應該已順利完成您的組建。
    
     ![][28]
15. 如果按兩下組建名稱，Visual Studio 會顯示 [組建摘要] ，包括與單元測試專案相關聯的任何測試結果。
    
     ![][29]
16. 在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取預備環境之後，您可以在 [部署] 索引標籤上檢視相關聯的部署。
    
     ![][30]
17. 瀏覽至網站的 URL。 若是 Web 應用程式，請選擇入口網站中的 [瀏覽] 按鈕。 若是雲端服務，請在 [儀表板] 頁面的 [快速概覽] 區段中選擇 URL，以顯示預備環境。
    
    依預設，來自雲端服務連續整合的部署會發佈至預備環境。 您可以將 [替代雲端服務環境] 屬性設為 [生產] 來變更此設定。 以下是網站 URL 在雲端服務儀表板頁面上的位置。
    
    ![][31]
    
    新的瀏覽器索引標籤會開啟來顯示您執行中的網站。
    
    ![][32]
18. 如果對專案進行其他變更，則會觸發更多組建，將累積多個部署。 最後一個會標示為「作用中」。
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5：重新部署舊版組建
此為選用步驟。 在 Azure 傳統入口網站中，選擇先前的部署，然後選擇 [重新部署]  ，將網站倒回到更早的簽入。 請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。

![][34]

## <a name="6-change-the-production-deployment"></a>6：變更生產部署
準備就緒後，您可以在 Azure 傳統入口網站中選擇 [交換]  按鈕，將預備環境升級至生產環境。 新部署的預備環境會升級至「生產」，而先前的生產環境 (若有的話) 會變成預備環境。 「作用中」部署可能與生產和預備環境不同，但最近組建的部署歷程記錄都一樣，與環境無關。

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7：從工作分支部署。
使用 Git 時，您通常會在工作分支中進行變更，等到開發達到完成狀態時，再整合至主要分支。 在專案的開發階段期間，您可以建置工作分支並部署至 Azure。

1. 在 **Team Explorer** 中，選擇 [首頁] 按鈕，然後選擇 [分支] 按鈕。
   
    ![][40]
2. 選擇 [新增分支]  連結。
   
    ![][41]
3. 輸入分支的名稱，例如 "working"，然後選擇 [建立分支] 。 這樣會建立新的本機分支。
   
    ![][42]
4. 發佈分支。 在 [取消發佈的分支] 中選擇分支名稱，然後選擇 [發佈]。
   
    ![][44]
5. 依預設，只有主要分支的變更才會觸發連續組建。 若要設定工作分支的連續組建，請在 **Team Explorer** 中選擇 [組建] 頁面，然後選擇 [編輯組建定義]。
6. 開啟 [來源設定]  索引標籤。 在 [監視連續整合和組建的分支] 下，選擇 [按一下這裡加入新的列]。
   
    ![][47]
7. 指定您建立的分支，例如 refs/heads/working。
   
    ![][48]
8. 變更程式碼，開啟已變更之檔案的快顯功能表，然後選擇 [認可] 。
   
    ![][43]
9. 選擇 [未同步處理的認可] 連結，再選擇 [同步處理] 按鈕或 [推送] 連結，將變更複製到 Visual Studio Team Services 中工作分支的複本。
   
   ![][45]
10. 瀏覽至 [組建]  檢視，找出工作分支剛觸發的組建。

## <a name="next-steps"></a>後續步驟
如需深入了解有關使用 Git 搭配 Visual Studio Team Services 的祕訣，請參閱[使用 Visual Studio 在 Git 中開發和共用程式碼](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)；關於使用未受 Visual Studio Team Services 管理的 Git 儲存機制來發佈至 Azure 的詳細資訊，請參閱[持續部署至 Azure App Service](../app-service-web/app-service-continuous-deployment.md)。 如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。

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
