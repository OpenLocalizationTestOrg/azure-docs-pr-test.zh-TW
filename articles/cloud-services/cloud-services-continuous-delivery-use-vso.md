---
title: "在 Azure 中使用 Visual Studio Team Services 來持續傳遞 | Microsoft Docs"
description: "了解如何設定 Visual Studio Team Services 的 Team 專案，自動建置和部署至 Azure App Service 或雲端服務中的 Web 應用程式功能。"
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a>使用 Visual Studio Team Services 連續傳遞至 Azure
您可以將 Visual Studio Team Services 小組專案設定為自動建置和部署至 Azure Web 應用程式或雲端服務。  (如需如何使用「內部部署」  的 Team Foundation Server 來設定連續組建及部署系統的相關資訊，請參閱 [Azure 中雲端服務的連續傳遞](cloud-services-dotnet-continuous-delivery.md))。

本教學課程假設您已安裝 Visual Studio 2013 和 Azure SDK。 如果您還沒有 Visual Studio 2013，請至 [www.visualstudio.com](http://www.visualstudio.com) 選擇 [免費開始用] 連結來下載。 從[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)安裝 Azure SDK。

> [!NOTE]
> 您需要 Visual Studio Team Services 帳戶，才能完成本教學課程：您可以 [開啟免費的 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。
> 
> 

若要使用 Visual Studio Team Services 將雲端服務設定為自動建立和部署至 Azure，請依照下列步驟進行。

## <a name="1-create-a-team-project"></a>1：建立 Team 專案
請遵循 [這裡](http://go.microsoft.com/fwlink/?LinkId=512980) 的指示來建立您的 Team 專案，並將專案連結至 Visual Studio。 本逐步解說假設您使用 Team Foundation 版本控制 (TFVC) 做為原始檔控制解決方案。 如果您想使用 Git 進行版本控制，請參閱 [本逐步解說的 Git 版本](http://go.microsoft.com/fwlink/p/?LinkId=397358)(英文)。

## <a name="2-check-in-a-project-to-source-control"></a>2︰將專案簽入原始檔控制
1. 在 Visual Studio 中，開啟您要部署的方案，或建立新方案。
   您可以依照此逐步解說的步驟部署 Web 應用程式或雲端服務 (Azure 應用程式)。
   如果要建立新方案，請建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。 請確定專案以 .NET Framework 4 或 4.5 為目標，如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色和背景工作角色，然後對 Web 角色選擇網際網路應用程式。 出現提示時，選擇 [ **網際網路應用程式**]。
   如果要建立 Web 應用程式，請選擇 ASP.NET Web 應用程式的專案範本，然後選擇 [MVC]。 請參閱「 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md)」。
   
   > [!NOTE]
   > Visual Studio Team Services 目前僅支援 Visual Studio Web 應用程式的 CI 部署。 Web Site 專案超出範圍。
   > 
   > 
2. 開啟方案的內容功能表，選擇 [將方案加入至原始檔控制] 。
   
    ![][5]
3. 接受或變更預設值，然後選擇 [確定]  按鈕。 處理完成之後，[方案總管] 中會出現原始檔控制圖示。
   
    ![][6]
4. 開啟解決方案的捷徑功能表，選擇 [簽入] 。
   
    ![][7]
5. 在 **Team Explorer** 的 [暫止的變更] 區域中，輸入簽入註解，然後選擇 [簽入] 按鈕。
   
    ![][8]
   
    請注意簽入時用來包含或排除特定變更的選項。 如果已排除您要的變更，請選擇 [全部包含]  。
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a>3：將專案連線至 Azure
1. 您現有一個 VS Team Services 小組專案，且裡面有一些原始程式碼，可以準備將小組專案連接至 Azure。  在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取您的雲端服務或 Web 應用程式，或選取左下方的 **+** 圖示並選擇 [雲端服務] 或 [Web 應用程式]，然後選取 [快速建立]，建立新的雲端服務或 Web 應用程式。 請選擇 [使用 Visual Studio Team Services 設定發行]  連結。
   
    ![][10]
2. 在精靈中，於文字方塊中輸入 Visual Studio Team Services 帳戶的名稱，然後按一下 [立即授權]  連結。 可能會要求您登入。
   
    ![][11]
3. 在 [連接要求] 快顯對話方塊中，選擇 [接受] 按鈕，以授權 Azure 在 VS Team Services 中設定 Team 專案。
   
    ![][12]
4. 授權成功時，將出現含有 Visual Studio Team Services 小組專案清單的下拉清單。 選擇您在先前步驟中建立的小組專案，然後選擇精靈的勾選記號按鈕。
   
    ![][13]
5. 連結專案之後，將出現一些指示，指出如何將變更簽入至 Visual Studio Team Services 小組專案。  下次簽入時，Visual Studio Team Services 就會建立專案並部署至 Azure。  現在就試著按一下 [從 Visual Studio 簽入] 連結，再按一下 [啟動 Visual Studio] 連結 (或入口網站畫面底部同等的 [Visual Studio] 按鈕)。
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4：觸發重建和重新部署專案
1. 在 Visual Studio 的 **Team Explorer** 中，選擇 [原始檔控制總管] 連結。
   
    ![][15]
2. 瀏覽至方案檔並開啟。
   
    ![][16]
3. 在 [方案總管] 中，開啟檔案進行變更。 例如，在 MVC Web 角色中，變更 Views\\Shared 資料夾下的 `_Layout.cshtml` 檔案。
   
    ![][17]
4. 編輯網站的標誌，然後選擇 **Ctrl+S** 儲存檔案。
   
    ![][18]
5. 在 **Team Explorer** 中，選擇 [暫止的變更] 連結。
   
    ![][19]
6. 輸入註解，然後選擇 [簽入]  按鈕。
   
    ![][20]
7. 選擇 [首頁] 按鈕回到 **Team Explorer** 首頁。
   
    ![][21]
8. 選擇 [組建]  連結來檢視進行中的組件。
   
    ![][22]
   
    **Team Explorer** 會顯示簽入已觸發的組建。
   
    ![][23]
9. 按兩下進行中的組建名稱，檢視進行中組建的詳細記錄。
   
    ![][24]
10. 當組建進行時，查看您使用精靈將 TFS 連結至 Azure 時所建立的組建定義。  開啟組建定義的捷徑功能表，然後選擇 [編輯組建定義] 。
    
     ![][25]
    
     在 [觸發程序]  索引標籤中，您會看到已設為依預設每次簽入時建置的組建定義。
    
     ![][26]
    
     在 [處理序]  索引標籤中，您可以看到部署環境已設為您的雲端服務或 Web 應用程式的名稱。 如果您使用的是 Web 應用程式，則顯示的屬性跟下面的屬性不同。
    
     ![][27]
11. 如果不想要使用預設值，請指定屬性的值。 Azure 發行屬性在 [部署]  區段中。
    
     下表顯示 [部署]  區段中可用的屬性：
    
    | 屬性 | 預設值 |
    | --- | --- |
    | 允許未受信任的憑證 |如果為 false，SSL 憑證必須經過根授權單位簽署。 |
    | 允許升級 |允許部署更新現有的部署而非建立新的部署。 保留 IP 位址。 |
    | 不要刪除 |如果為 true，則不要覆寫現有不相關的部署 (允許升級)。 |
    | 部署設定的路徑 |Web 應用程式的 .pubxml 檔的路徑，這是儲存機制之根資料夾的相對路徑。 雲端服務則會忽略。 |
    | SharePoint 部署環境 |與服務名稱相同。 |
    | Azure 部署環境 |Web 應用程式或雲端服務的名稱。 |
12. 如果使用多個服務組態 (.cscfg 檔)，則可以在 [組建、進階、MSBuild 引數]  設定中指定所需的服務組態。 例如，若要使用 ServiceConfiguration.Test.cscfg，請設定 MSBuild 引數的命令列選項 `/p:TargetProfile=Test`。
    
     ![][38]
    
     現在應該已順利完成您的組建。
    
     ![][28]
13. 如果按兩下組建名稱，Visual Studio 會顯示 [組建摘要] ，包括與單元測試專案相關聯的任何測試結果。
    
     ![][29]
14. 在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取預備環境之後，您可以在 [部署] 索引標籤上檢視相關聯的部署。
    
     ![][30]
15. 瀏覽至網站的 URL。 若是 Web 應用程式，請按一下命令列的 [瀏覽] 按鈕。 若是雲端服務，請在 [儀表板] 頁面的 [快速概覽] 區段中選擇 URL，以顯示雲端服務的預備環境。 依預設，來自雲端服務連續整合的部署會發佈至預備環境。 您可以將 [替代雲端服務環境] 屬性設為 [生產] 來變更此設定。 此擷取畫面顯示網站 URL 在雲端服務儀表板頁面上的位置。
    
    ![][31]
    
    新的瀏覽器索引標籤會開啟來顯示您執行中的網站。
    
    ![][32]
    
    若為雲端服務，如果對專案進行其他變更，則會觸發更多組建，將累積多個部署。 最後一個會標示為「作用中」。
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5：重新部署舊版組建
此步驟適用於雲端服務，且為選用的。 在 Azure 傳統入口網站中，選擇先前的部署，然後選擇 [重新部署]  按鈕，將網站倒回到更早的簽入。  請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。

![][34]

## <a name="6-change-the-production-deployment"></a>6：變更生產部署
此步驟僅適用於雲端服務，不適用於 Web 應用程式。 準備就緒後，您可以在 Azure 傳統入口網站中選擇 [交換]  按鈕，將預備環境升級至生產環境。 新部署的預備環境會升級至「生產」，而先前的生產環境 (若有的話) 會變成預備環境。 「作用中」部署可能與生產和預備環境不同，但最近組建的部署歷程記錄都一樣，與環境無關。

![][35]

## <a name="7-run-unit-tests"></a>7：執行單元測試
此步驟僅適用於 Web 應用程式，不適用於雲端服務。 若要為部署的品質把關，您可以執行單元測試；如果測試失敗，則可以停止部署。

1. 在 Visual Studio 中，加入單元測試專案。
   
   ![][39]
2. 將專案參考加入您要測試的專案。
   
   ![][40]
3. 加入一些單元測試。 若要開始使用，請嘗試一律會通過的虛擬測試。
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. 編輯組建定義，選擇 [處理序] 索引標籤，然後展開 [測試] 節點。
5. 將 [在測試失敗時使組建失敗]  設為 True。 換句話說，除非通過測試，否則不會進行部署。
   
   ![][41]
6. 將新組建排入佇列。
   
   ![][42]
   
   ![][43]
7. 在建置進行時，檢查其進度。
   
    ![][44]
   
    ![][45]
8. 在建置完成時，檢查測試結果。
   
    ![][46]
   
    ![][47]
9. 嘗試建立將失敗的測試。 透過複製第一個測試、將其重新命名，並將 NotImplementedException 標記為預期的例外狀況的程式碼行加上註解，來加入新的測試。
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. 簽入變更，以將新組建排入佇列。
    
     ![][48]
11. 檢視測試結果，以查看失敗的詳細資料。
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>後續步驟
如需在 Visual Studio Team Services 中進行單元測試的詳細資訊，請參閱 [在建置中執行單元測試](http://go.microsoft.com/fwlink/p/?LinkId=510474)。 如果您使用的是 Git，請參閱[在 Git 中共用程式碼](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx)和[持續部署至 Azure App Service](../app-service-web/app-service-continuous-deployment.md)。  如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
