---
title: "使用 Azure App Service 中的混合式連線的 aaaAccess 在內部部署資源"
description: "在 Azure App Service 中的 Web 應用程式和使用靜態 TCP 連接埠的內部部署資源之間建立連線"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>在 Azure App Service 中使用混合式連線存取內部部署資源
您可以連接會使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api 和大部分的自訂 Web 服務的 Azure App Service 應用程式 tooany 在內部部署資源。 本文章將示範如何 toocreate 應用程式服務與內部部署 SQL Server 資料庫之間的混合式連接。

> [!NOTE]
> hello 混合式連線功能 hello Web 應用程式部分是只用於 hello [Azure 入口網站](https://portal.azure.com)。 請參閱 toocreate BizTalk 服務中的連接[混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。 
> 
> 此內容也適用於 Azure App Service 中的 tooMobile 應用程式。 
> 
> 

## <a name="prerequisites"></a>必要條件
* Azure 訂閱。 若要取得免費訂閱，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
  
    如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
* toouse 在內部部署 SQL Server 或 SQL Server Express 的混合式連接的資料庫，TCP/IP 需要 toobe 靜態連接埠上啟用。 建議在 SQL Server 上使用預設執行個體，因為其使用靜態連接埠 1433。 如需安裝及設定 SQL Server Express 用於混合式連接的資訊，請參閱[連接 tooan 內部部署 SQL Server 從使用混合式連線的 Azure 網站](http://go.microsoft.com/fwlink/?LinkID=397979)。
* 您安裝 hello 在內部部署混合式連線管理員說明的代理程式 」 在本文稍後的 hello 電腦：
  
  * 透過連接埠 5671 必須能夠 tooconnect tooAzure
  * 必須是能夠 tooreach hello *hostname*:*portnumber*的內部部署資源。 

> [!NOTE]
> 本文章中的 hello 步驟假設您使用 hello 瀏覽器從 hello 主控 hello 在內部部署混合式連接的代理程式的電腦。
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立 web 應用程式
> [!NOTE]
> 如果您已經在 hello 的 toouse 本教學課程中的 Azure 入口網站中建立的 web 應用程式或行動裝置應用程式後端，您可以向前跳過[建立混合式連接和 BizTalk 服務](#CreateHC)並從該處開始。
> 
> 

1. Hello 左上角的 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動** > **Web 應用程式**。
   
    ![新 Web 應用程式][NewWebsite]
2. 在 hello **Web 應用程式**刀鋒視窗中，提供 URL，然後按一下 **建立**。 
   
    ![Website name][WebsiteCreationBlade]
3. 在幾分鐘之後, 建立 hello web 應用程式和其 web 應用程式 刀鋒視窗隨即出現。 hello 刀鋒視窗中是可垂直捲動的儀表板可讓您管理您的網站。
   
    ![Website running][WebSiteRunningBlade]
4. 是即時的 tooverify hello 站台，您可以按一下 hello**瀏覽**圖示 toodisplay hello 預設頁面。
   
    ![按一下瀏覽 toosee 您 web 應用程式][Browse]
   
    ![預設 Web 應用程式頁面][DefaultWebSitePage]

接下來，您將建立混合式連接和 hello web 應用程式的 BizTalk 服務。

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>建立混合式連線和 BizTalk 服務
1. 在您的 [Web 應用程式] 刀鋒視窗中按一下 [所有設定] > [網路] > [設定混合式連接端點]。
   
    ![混合式連線][CreateHCHCIcon]
2. 在 hello 混合式連線刀鋒視窗中，按一下 **新增**。
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. hello**新增混合式連接**刀鋒視窗隨即開啟。  由於這是您第一次的混合式連線，hello**新混合式連接**選項預設選取與 hello**建立混合式連接**刀鋒視窗會為您開啟。
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    在 hello**建立混合式連線刀鋒視窗**:
   
   * 如**名稱**，提供 hello 連接的名稱。
   * 如**Hostname**，輸入 hello hello 在內部部署電腦裝載您的資源名稱。
   * 如**連接埠**，輸入您在內部部署的資源使用 (SQL Server 預設執行個體 1433) 的 hello 連接埠號碼。
   * 按一下 [Biz Talk 服務] 
4. hello**建立 BizTalk 服務**刀鋒視窗隨即開啟。 輸入 hello BizTalk 服務的名稱，然後按一下**確定**。
   
    ![Create BizTalk service][CreateHCCreateBTS]
   
    hello**建立 BizTalk 服務**關閉刀鋒視窗中，您將返回 toohello**建立混合式連接**刀鋒視窗。
5. 在 hello 建立混合式連線刀鋒視窗中，按一下 **確定**。 
   
    ![Click OK][CreateBTScomplete]
6. Hello 程序完成時，hello 入口網站中的 hello 通知區域會通知您已成功建立 hello 連線。
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Hello web 應用程式的刀鋒視窗中，在 hello**混合式連線**圖示現在會顯示已建立 1 的混合式連接。
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

此時，您已完成 hello 雲端混合式連接的基礎結構的重要部分。 接下來，您將建立對應的內部部署部分。

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>安裝 hello 在內部部署混合式連線管理員 toocomplete hello 連線
1. 在 hello web 應用程式的刀鋒視窗中，按一下 **所有設定** > **網路** > **設定您的混合式連接端點**。 
   
    ![Hybrid connections icon][HCIcon]
2. 在 hello**混合式連線**刀鋒視窗，hello**狀態**hello 的資料行最近新增端點顯示**未連接**。 按一下 hello 連接 tooconfigure 它。
   
    ![Not connected][NotConnected]
   
    hello 混合式連線刀鋒視窗隨即開啟。
   
    ![NotConnectedBlade][NotConnectedBlade]
3. 在 hello 刀鋒視窗中，按一下 **接聽程式的安裝程式**。
   
    ![Click Listener Setup][ClickListenerSetup]
4. hello**混合式連接屬性**刀鋒視窗隨即開啟。 在下**在內部部署混合式連線管理員**，選擇**按一下這裡 tooinstall**。
   
    ![按一下這裡 tooinstall][ClickToInstallHCM]
5. 在 hello 應用程式執行安全性警告對話方塊中，選擇 **執行**toocontinue。
   
    ![選擇執行 toocontinue][ApplicationRunWarning]
6. 在 [hello**使用者帳戶控制**] 對話方塊中，選擇**是**。
   
   ![Choose Yes][UAC]
7. 下載並安裝您 hello 混合式連線管理員時。 
   
    ![安裝][HCMInstalling]
8. Hello 安裝完成時，按一下**關閉**。
   
    ![Click Close][HCMInstallComplete]
   
    在 hello**混合式連線**刀鋒視窗，hello**狀態**資料行現在會顯示**已連接**。 
   
    ![Connected Status][HCStatusConnected]

現在該 hello 混合式連接基礎結構已完成，您可以建立混合式應用程式使用它。 

> [!NOTE]
> hello 下列各節說明您如何 toouse 與行動應用程式的.NET 後端專案的混合式連接。
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>設定 hello 行動應用程式的.NET 後端專案 tooconnect toohello SQL Server 資料庫
在 App Service 中，Mobile Apps .NET 後端專案只是一個已安裝並初始化其他 Mobile Apps SDK 的 ASP.NET Web 應用程式。 toouse 的行動應用程式後端 web 應用程式，您必須[下載，並初始化 hello 行動應用程式的.NET 後端 SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk)。  

針對行動裝置應用程式，您也需要 toodefine 連接字串 hello 在內部部署資料庫，並修改 hello 後端 toouse 此連線。 

1. 在 Visual Studio 中，您的行動應用程式的.NET 後端開啟 hello Web.config 檔案中的 [方案總管] 中找出 hello **connectionStrings**區段中，新增類似 hello 下列，哪一個點 toohello 內部部署 SQL SqlClient 項目伺服器資料庫：
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    請記住 tooreplace `<**secure_password**>` hello 密碼為您建立與這個字串中*HybridConnectionLogin*。
2. 按一下**儲存**Visual Studio toosave hello Web.config 檔案中。
   
   > [!NOTE]
   > Hello 本機電腦上執行時，會使用此連線設定。 Azure 中執行時，這個設定會定義在 hello 入口網站中的 hello 連接設定所覆寫。
   > 
   > 
3. 展開 hello**模型**資料夾和開啟 hello 資料模型檔案，在為結束*Context.cs*。
4. 修改 hello **DbContext**執行個體建構函式 toopass hello 值`OnPremisesDBConnection`toohello 基底**DbContext**建構函式，類似下列程式碼片段的 toohello:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    hello 服務現在將使用 hello 新連線 toohello SQL Server 資料庫。

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>更新 hello 行動裝置應用程式後端 toouse hello 在內部部署連接字串
接下來，您需要 tooadd 應用程式設定這個新的連接字串，使其可以從 Azure 用。  

1. 在 hello [Azure 入口網站](https://portal.azure.com)hello web 應用程式後端程式碼中您的行動裝置應用程式，按一下 **所有設定**，然後**應用程式設定**。
2. 在 hello **Web 應用程式設定**刀鋒視窗中，向下捲動太**連接字串**並加入新**SQL Server**名為連接字串`OnPremisesDBConnection`值會類似`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    取代`<**secure_password**>`hello 安全密碼在內部部署資料庫。
   
    ![Connection string for on-premises database](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. 按**儲存**toosave hello 混合式連接和連接字串您剛建立。

此時，您可以重新發佈 hello 伺服器專案，並與現有的行動應用程式用戶端測試 hello 新的連接。 資料會讀取並寫入 toohello 在內部部署資料庫使用 hello 混合式連接。

<a name="NextSteps"></a>

## <a name="next-steps"></a>後續步驟
* 如需建立 ASP.NET web 應用程式使用混合式連接的資訊，請參閱[連接 tooan 內部部署 SQL Server 從使用混合式連線的 Azure 網站](http://go.microsoft.com/fwlink/?LinkID=397979)。 

### <a name="additional-resources"></a>其他資源
[混合式連線概觀](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist 介紹混合式連線 (第 9 頻道視訊)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[混合式連線網站](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[連接 tooan 內部部署 SQL Server 與 Azure 行動服務使用混合式連線 （Channel 9 影片）](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
