---
title: "在 Azure 中的 Visual Studio Team Services 與 aaaContinuous 傳遞 |Microsoft 文件"
description: "了解如何 tooconfigure Visual Studio Team Services 的 team 的專案 tooautomatically 建置和部署 Azure 應用程式服務或雲端服務中的 toohello Web 應用程式功能。"
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>使用 Visual Studio Team Services 的持續傳遞 tooAzure
您可以設定 Visual Studio Team Services 團隊專案 tooautomatically 組建和部署 tooAzure web 應用程式或雲端服務。  (如需有關如何 tooset 連續的組建及部署使用系統資訊*內部*Team Foundation Server，請參閱[Azure 雲端服務的持續傳遞](cloud-services-dotnet-continuous-delivery.md)。)

本教學課程假設您有 Visual Studio 2013 和 Azure SDK 安裝 hello。 如果您還沒有 Visual Studio 2013，下載選擇 hello**免費開始**連結[www.visualstudio.com](http://www.visualstudio.com)。安裝 hello 從 Azure SDK[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)。

> [!NOTE]
> 本教學課程需要 Visual Studio Team Services 帳戶 toocomplete： 您可以[免費開啟 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。
> 
> 

設定雲端服務 tooautomatically tooset 建置和部署使用 Visual Studio Team Services tooAzure，依照下列步驟。

## <a name="1-create-a-team-project"></a>1：建立 Team 專案
遵循 hello[這裡](http://go.microsoft.com/fwlink/?LinkId=512980)toocreate 您 team 專案，並將它連結 tooVisual Studio。 本逐步解說假設您使用 Team Foundation 版本控制 (TFVC) 做為原始檔控制解決方案。 如果您想 toouse Git 進行版本控制，請參閱[本逐步解說的 hello Git 版本](http://go.microsoft.com/fwlink/p/?LinkId=397358)。

## <a name="2-check-in-a-project-toosource-control"></a>2： 檢查專案 toosource 控制項中
1. 在 Visual Studio 中，開啟您想要 toodeploy，或建立一個新的 hello 方案。
   您可以將 web 應用程式部署或雲端服務 （Azure 應用程式），由下列 hello 步驟在本逐步解說。
   如果您想 toocreate 新方案，建立新的 Azure 雲端服務專案或新的 ASP.NET MVC 專案。 請確定 hello 專案目標.NET Framework 4 或 4.5，而且如果您要建立雲端服務專案，加入 ASP.NET MVC web 角色和背景工作角色，然後選擇 hello web 角色的網際網路應用程式。 出現提示時，選擇 [ **網際網路應用程式**]。
   如果您想 toocreate web 應用程式中，選擇 hello ASP.NET Web 應用程式專案範本，然後選擇 MVC。 請參閱「 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md)」。
   
   > [!NOTE]
   > Visual Studio Team Services 目前僅支援 Visual Studio Web 應用程式的 CI 部署。 Web Site 專案超出範圍。
   > 
   > 
2. 開啟 hello hello 方案的內容功能表並選擇 **將方案加入 tooSource 控制項**。
   
    ![][5]
3. 接受或變更 hello 預設值，以及選擇 hello**確定** 按鈕。 Hello 程序完成之後，原始檔控制圖示會出現在**方案總管 中**。
   
    ![][6]
4. 開啟 hello hello 方案的捷徑功能表並選擇 **簽入**。
   
    ![][7]
5. 在 hello**暫止的變更**區域**Team Explorer**、 輸入 hello 簽入註解，然後選擇 hello**簽入**按鈕。
   
    ![][8]
   
    請注意 hello 選項 tooinclude 或排除特定的變更，當您簽入。 如果想要排除的變更，請選擇 hello**全部包含**連結。
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3： 連接 hello 專案 tooAzure
1. 現在您有一些原始程式碼的 VS Team Services team 專案中，您就準備好 tooconnect 您的小組專案 tooAzure。  在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，選取 雲端服務或 web 應用程式，或建立一個新選擇 hello  **+**  hello 左下方，然後選擇圖示**的雲端服務**或**Web 應用程式**然後**快速建立**。 選擇 hello**設定發行與 Visual Studio Team Services**連結。
   
    ![][10]
2. 在 hello 精靈中，輸入 hello 您的 Visual Studio Team Services 帳戶名稱在 hello 文字方塊中，按一下 hello**現在授權**連結。 您可能會要求 toosign 中。
   
    ![][11]
3. 在 hello**連線要求**快顯對話方塊中，選擇 hello**接受**按鈕 tooauthorize Azure tooconfigure 您的小組專案 VS Team Services 中。
   
    ![][12]
4. 授權成功時，將出現含有 Visual Studio Team Services 小組專案清單的下拉清單。 選擇 hello hello 先前步驟中，在您建立 team 專案名稱，然後選擇 hello 精靈的核取記號按鈕。
   
    ![][13]
5. 您的專案連結之後，您會看到一些簽入變更 tooyour Visual Studio Team Services 的 team 專案的指示。  在您下一步簽入時，Visual Studio Team Services 將會建置並部署專案 tooAzure。  再試一次按一下 hello 現在這個**簽入從 Visual Studio**連結，然後再 hello**啟動 Visual Studio**連結 (或對等的 hello **Visual Studio**在 hello 底部的按鈕hello 入口網站畫面）。
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4：觸發重建和重新部署專案
1. 在 Visual Studio 的**Team Explorer**，選擇 hello**原始檔控制總管**連結。
   
    ![][15]
2. 瀏覽 tooyour 方案檔，並將它開啟。
   
    ![][16]
3. 在 [方案總管] 中，開啟檔案進行變更。 例如，變更 hello 檔案`_Layout.cshtml`hello 檢視下\\MVC web 角色中的共用資料夾。
   
    ![][17]
4. 編輯 hello 站台的 hello 標誌，然後選擇  **Ctrl + S** toosave hello 檔案。
   
    ![][18]
5. 在**Team Explorer**，選擇 hello**暫止的變更**連結。
   
    ![][19]
6. 輸入註解，然後選擇 [hello**簽入**] 按鈕。
   
    ![][20]
7. 選擇 hello**家用**按鈕 tooreturn toohello **Team Explorer**首頁。
   
    ![][21]
8. 選擇 hello**建置**連結 tooview hello 建置進行中。
   
    ![][22]
   
    **Team Explorer** 會顯示簽入已觸發的組建。
   
    ![][23]
9. 按兩下 hello 進度 tooview 詳細的記錄檔中的 hello 組建名稱 hello 組建進行。
   
    ![][24]
10. 進行中 hello 組建時，看看您連結 TFS tooAzure 使用 hello 精靈時所建立的 hello 組建定義。  開啟 hello hello 組建定義的捷徑功能表並選擇 **編輯組建定義**。
    
     ![][25]
    
     在 hello**觸發程序**索引標籤上，您會看到 hello 組建定義設定在每個簽入 toobuild 預設。
    
     ![][26]
    
     在 hello**程序**索引標籤上，您可以看到 hello 部署環境設定的雲端服務或 web 應用程式的 toohello 名稱。 如果您正在使用 web 應用程式，您會看到 hello 屬性將會與不同如下所示。
    
     ![][27]
11. 如果您想要比 hello 預設值不同的值，指定 hello 屬性的值。 hello 屬性 Azure 發行會在 hello**部署**> 一節。
    
     hello 下列資料表顯示 hello 可用的屬性中 hello**部署**> 一節：
    
    | 屬性 | 預設值 |
    | --- | --- |
    | 允許未受信任的憑證 |如果為 false，SSL 憑證必須經過根授權單位簽署。 |
    | 允許升級 |可讓 hello 部署 tooupdate 而不是建立一個新現有的部署。 會保留 hello IP 位址。 |
    | 不要刪除 |如果為 true，則不要覆寫現有不相關的部署 (允許升級)。 |
    | 路徑 tooDeployment 設定 |hello 路徑 tooyour.pubxml 檔案是 web 應用程式，相對 toohello hello 儲存機制根資料夾。 雲端服務則會忽略。 |
    | SharePoint 部署環境 |hello 與 hello 服務名稱的相同。 |
    | Azure 部署環境 |hello web 應用程式或雲端服務名稱。 |
12. 如果您使用多個服務組態 （.cscfg 檔），您可以指定 hello 所需的服務組態中 hello**建置，進階，MSBuild 引數**設定。 例如，toouse ServiceConfiguration.Test.cscfg，會設定 MSBuild 引數行選項`/p:TargetProfile=Test`。
    
     ![][38]
    
     現在應該已順利完成您的組建。
    
     ![][28]
13. 如果您按兩下 hello 組建名稱時，Visual Studio 會顯示**組建摘要**，包括中的任何測試結果相關聯的單元測試專案。
    
     ![][29]
14. 在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，您可以檢視相關聯的 hello 部署上 hello**部署**索引標籤上，選取 預備環境的 hello 時。
    
     ![][30]
15. 瀏覽 tooyour 網站的 URL。 Web 應用程式中，只要按一下 hello**瀏覽**hello 命令列上的按鈕。 雲端服務中，選擇 hello URL 在 hello**快速概覽**區段 hello**儀表板**顯示 hello 預備環境的雲端服務的頁面。 從雲端服務的持續整合的部署都是預設的已發行的 toohello 預備環境。 您可以變更此設定 hello**替代雲端服務環境**屬性太**生產**。 這個螢幕擷取畫面會顯示在 hello 網站 URL 是 hello 雲端服務的儀表板頁面上。
    
    ![][31]
    
    新的瀏覽器索引標籤會開啟 tooreveal 您執行的網站。
    
    ![][32]
    
    雲端服務，如果您進行其他變更 tooyour 專案時，更建置您的觸發程序，和您將會累積多個部署。 hello 最新標示為 使用。
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5：重新部署舊版組建
這個步驟適用於 toocloud 服務，並為選擇性。 在 hello Azure 傳統入口網站中，選擇先前的部署，然後選擇 hello**重新部署**按鈕 toorewind 簽入之前您站台 tooan。  請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。

![][34]

## <a name="6-change-hello-production-deployment"></a>6： 變更 hello 生產環境部署
這個步驟適用於只有 toocloud 服務，不適用於 web 應用程式。 當您準備好時，您可以藉由選擇 hello 升級 hello 臨時 toohello 生產環境**交換**hello Azure 傳統入口網站中的按鈕。 新部署的 hello 臨時環境是已升級的 tooProduction 而 hello 先前生產環境中，如果有的話，會變成預備環境。 hello 作用中的部署可能會不同 hello 生產與預備環境，但最近組建 hello 部署歷程記錄是 hello 相同的環境而定。

![][35]

## <a name="7-run-unit-tests"></a>7：執行單元測試
這個步驟適用於只有 tooweb 應用程式，不是雲端服務。 tooput 品質把關上您的部署，您可以執行單元測試，以及如果他們，您可以停止 hello 部署。

1. 在 Visual Studio 中，加入單元測試專案。
   
   ![][39]
2. 新增您想要 tootest 專案參考 toohello 專案。
   
   ![][40]
3. 加入一些單元測試。 tooget 啟動，請一律會在傳遞的 dummy 測試。
   
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
4. 編輯 hello 組建定義中，選擇 hello**程序**索引標籤，然後展開 hello**測試**節點。
5. 設定 hello**在測試失敗時使組建**tooTrue。 這表示除非 hello 測試成功，就不會執行 hello 部署。
   
   ![][41]
6. 將新組建排入佇列。
   
   ![][42]
   
   ![][43]
7. 而繼續 hello 組建，檢查其進度。
   
    ![][44]
   
    ![][45]
8. Hello 組建完成時，請檢查 hello 測試結果。
   
    ![][46]
   
    ![][47]
9. 嘗試建立將失敗的測試。 藉由複製 hello 第一個加入新的測試、 重新命名，並註解化 hello 說明 NotImplementedException 沒有預期的例外狀況的程式碼行。
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Hello 的簽入變更 tooqueue 新組建。
    
     ![][48]
11. 檢視 hello 測試結果 toosee 詳細 hello 失敗。
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>後續步驟
如需在 Visual Studio Team Services 中進行單元測試的詳細資訊，請參閱 [在建置中執行單元測試](http://go.microsoft.com/fwlink/p/?LinkId=510474)。 如果您使用 Git，請參閱[共用程式碼在 Git 中的](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx)和[連續部署 tooAzure App Service](../app-service-web/app-service-continuous-deployment.md)。  如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。

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
