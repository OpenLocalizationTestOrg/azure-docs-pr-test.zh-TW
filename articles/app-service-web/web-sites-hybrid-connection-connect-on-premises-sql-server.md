---
title: "aaaConnect tooon 內部部署 SQL Server，從使用混合式連線的 Azure App Service 中的 web 應用程式"
description: "Microsoft Azure 上建立 web 應用程式並將它連接 tooan 在內部部署 SQL Server 資料庫"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>從使用混合式連線的 Azure App Service 中的 web 應用程式連接 tooon 內部部署 SQL Server
混合式連線可以連接[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式使用靜態 TCP 連接埠的 tooon 內部部署資源。 支援的資源包括 Microsoft SQL Server、MySQL、HTTP Web API、App Service 和大部分的自訂 Web 服務。

在本教學課程中，您將學習如何 toocreate App Service web 應用程式在 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)連接 hello web 應用程式 tooyour 本機內部部署 SQL Server 資料庫使用 hello 新混合式連線功能，建立簡單的 ASP.NET將會使用 hello 混合式連接，並部署 hello 應用程式 toohello App Service web 應用程式的應用程式。 在 Azure 上的 hello 完成 web 應用程式是在內部部署的成員資格資料庫中儲存使用者認證。 hello 教學課程會假設沒有使用經驗，使用 Azure 或 ASP.NET。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> hello 混合式連線功能 hello Web 應用程式部分是只用於 hello [Azure 入口網站](https://portal.azure.com)。 請參閱 toocreate BizTalk 服務中的連接[混合式連線](http://go.microsoft.com/fwlink/p/?LinkID=397274)。  
> 
> 

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您將需要下列產品的 hello。 所有產品都有免費版本可使用，因此您可以免費進行 Azure 相關開發。

* **Azure 訂閱** - 如需免費訂閱，請參閱 [Azure 免費試用](/pricing/free-trial/)。
* **Visual Studio 2013** -toodownload 免費試用版的 Visual Studio 2013，請參閱[Visual Studio 下載](http://www.visualstudio.com/downloads/download-visual-studio-vs)。 請先安裝此項目再繼續作業。
* **Microsoft .NET Framework 3.5 Service Pack 1** - 如果您的作業系統是 Windows 8.1、Windows Server 2012 R2、Windows 8、Windows Server 2012、Windows 7 或 Windows Server 2008 R2，您可以在 [控制台] > [程式和功能] > [開啟或關閉 Windows 功能] 中啟用此項目。 否則，您可以從下載 hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)。
* **SQL Server 2014 Express with Tools** -Microsoft SQL Server Express 免費下載在 hello [Microsoft Web 平台的資料庫頁面](http://www.microsoft.com/web/platform/database.aspx)。 選擇 hello **Express** (不是 LocalDB) 版本。 hello **Express with Tools**版本包含 SQL Server Management Studio，您將在本教學課程中使用。
* **SQL Server Management Studio Express** -這是使用上面所提下載工具隨附於 SQL Server 2014 Express hello 但如果您需要 tooinstall 它分開，您可以下載並安裝從 hello [SQL Server Express下載頁面](http://www.microsoft.com/web/platform/database.aspx)。

hello 教學課程假設您有 Azure 訂閱，您已安裝 Visual Studio 2013，以及您已安裝或啟用.NET Framework 3.5。 hello 教學課程會示範 tooinstall SQL Server 2014 Express 中的設定，適用於 hello Azure 混合式連線功能 （使用靜態 TCP 連接埠的預設執行個體） 的方式。 開始之前 hello 教學課程，請從上面所述，如果您沒有安裝 SQL Server 的 hello 位置下載 SQL Server 2014 Express with Tools。

### <a name="notes"></a>注意事項
toouse 在內部部署 SQL Server 或 SQL Server Express 的混合式連接的資料庫，TCP/IP 需要 toobe 靜態連接埠上啟用。 SQL Server 上的預設執行個體會使用靜態連接埠 1433，但指定的執行個體則否。

您安裝代理程式 」 在內部部署混合式連線管理員 hello hello 電腦：

* 必須在有傳出連線 tooAzure:

| Port | 理由 |
| --- | --- |
| 80 |**必要** 可供 HTTP 連接埠進行憑證驗證以及可供進行資料連線 (選用)。 |
| 443 |**選用** 可供進行資料連線。 如果無法使用輸出連線 too443 時，會使用 TCP 連接埠 80。 |
| 5671 和 9352 |**建議** 但可供進行資料連線 (選用)。 請注意，此模式通常會產生較高的輸送量。 如果無法使用輸出連線 toothese 連接埠，則會使用 TCP 連接埠 443。 |

* 必須是能夠 tooreach hello *hostname*:*portnumber*的內部部署資源。

本文章中的 hello 步驟假設您使用 hello 瀏覽器從 hello 主控 hello 在內部部署混合式連接的代理程式的電腦。

如果您已符合上面所述的 hello 條件的環境和組態中安裝 SQL Server，您可以三級跳，而且開頭[建立 SQL Server 資料庫內部](#CreateSQLDB)。

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. 在內部部署中安裝 SQL Server Express、啟用 TCP/IP 及建立 SQL Server 資料庫
這個區段會顯示 SQL Server Express，tooinstall 如何啟用 TCP/IP，和建立資料庫，以便您的 web 應用程式會處理 hello Azure 入口網站。

### <a name="install-sql-server-express"></a>安裝 SQL Server Express
1. tooinstall SQL Server Express，執行 hello **SQLEXPRWT_x64_ENU.exe**或**SQLEXPR_x86_ENU.exe**您下載的檔案。 hello SQL Server 安裝中心精靈 隨即出現。
   
    ![SQL Server Install][SQLServerInstall]
2. 選擇**新的 SQL Server 獨立安裝或加入現有安裝的功能 tooan**。 Hello 的指示，直到取得 toohello 接受 hello 預設選項及設定，請依照下列**執行個體組態**頁面。
3. 在 hello**執行個體組態**頁面上，選擇**預設執行個體**。
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    根據預設，SQL Server hello 預設執行個體會靜態通訊埠 1433，SQL Server 用戶端要求是混合式連線功能需要什麼 hello。 指定的執行個體會使用動態連接埠和 UDP，而混合式連線並不加以支援。
4. 接受 hello 預設值在 hello**伺服器組態**頁面。
5. 在 hello**資料庫引擎組態**頁面的 **驗證模式**，選擇**混合模式 （SQL Server 驗證和 Windows 驗證）**，並提供密碼。
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    在本教學課程中，您將使用 SQL Server 驗證。 是您所提供，確定 tooremember hello 密碼，因為您稍後會需要。
6. 逐步執行 hello 精靈 toocomplete hello 安裝 hello 其餘部分。

### <a name="enable-tcpip"></a>啟用 TCP/IP
tooenable TCP/IP，您將使用 SQL Server 組態管理員，當您安裝 SQL Server Express 安裝。 中的 hello 步驟[啟用 TCP/IP 網路通訊協定的 SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx)才能繼續。

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>在內部部署中建立 SQL Server 資料庫
您的 Visual Studio Web 應用程式需要可由 Azure 存取的成員資格資料庫。 這需要 SQL Server 或 SQL Server Express 資料庫 （不 hello LocalDB 資料庫 hello MVC 範本會依預設），讓您將接著建立 hello 成員資格資料庫。

1. 在 SQL Server Management Studio 中，連接 toohello 您剛才安裝的 SQL Server。 (如果 hello**連接 tooServer**對話方塊不會不會自動出現，瀏覽過**物件總管] 中**hello 左窗格中，按一下 [**連接**，然後按一下 **Database Engine**。)![連接 tooServer][SSMSConnectToServer]
   
    針對 [伺服器類型]，選擇 [資料庫引擎]。 如**伺服器名稱**，您可以使用**localhost**或 hello 您所使用的 hello 電腦名稱。 選擇**SQL Server 驗證**，然後 hello sa 使用者名稱和密碼登入 hello 您稍早建立的。
2. toocreate 新的資料庫使用 SQL Server Management Studio，以滑鼠右鍵按一下**資料庫**在物件總管 中，，然後按一下**新資料庫**。
   
    ![Create new database][SSMScreateNewDB]
3. 在 hello**新資料庫** 對話方塊中，輸入 MembershipDB hello 資料庫名稱，然後按一下**確定**。
   
    ![Provide database name][SSMSprovideDBname]
   
    請注意，您不做任何變更 toohello 資料庫此時。 在執行時，則將 web 應用程式所自動更新版本加入 hello 成員資格資訊。
4. 在 [物件總管] 中，如果您展開**資料庫**，您會看到已建立該 hello 成員資格資料庫。
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. 在 hello Azure 入口網站中建立 web 應用程式
> [!NOTE]
> 如果您已經在 hello 的 toouse 本教學課程中的 Azure 入口網站中建立 web 應用程式，您可以向前跳過[建立混合式連接和 BizTalk 服務](#CreateHC)並從該處繼續。
> 
> 

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增** > **Web + 行動** > **Web 應用程式**。
   
    ![New button][New]
2. 設定您的 Web 應用程式，然後按一下建立 。
   
    ![Website name][WebsiteCreationBlade]
3. 在幾分鐘之後, 建立 hello web 應用程式和其 web 應用程式 刀鋒視窗隨即出現。 hello 刀鋒視窗中是可垂直捲動的儀表板可讓您管理您的 web 應用程式。
   
    ![Website running][WebSiteRunningBlade]
   
    是即時的 tooverify hello web 應用程式，您可以按一下 hello**瀏覽**圖示 toodisplay hello 預設頁面。

接下來，您將建立混合式連接和 hello web 應用程式的 BizTalk 服務。

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. 建立混合式連線和 BizTalk 服務
1. 傳回在 hello 入口網站，請移 toosettings，然後按一下**網路** > **設定您的混合式連接端點**。
   
    ![混合式連線][CreateHCHCIcon]
2. 在 hello 混合式連線刀鋒視窗中，按一下 **新增** > **新混合式連接**。
3. 在 hello**建立混合式連接**刀鋒視窗中：
   
   * 如**名稱**，提供 hello 連接的名稱。
   * 如**Hostname**，輸入您的 SQL Server 主機電腦 hello 電腦名稱。
   * 如**連接埠**，輸入 1433 (hello 預設 SQL Server 連接埠）。
   * 按一下**BizTalk 服務** > **新的 BizTalk 服務**，然後輸入 hello BizTalk 服務的名稱。
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. 按兩次 [確定]  。
   
    Hello 程序完成時，hello**通知**區域將會閃爍綠色**成功**和 hello**混合式連接**刀鋒視窗會顯示以 hello 新混合式連接hello 狀態為**未連接**。
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

此時，您已完成 hello 雲端混合式連接的基礎結構的重要部分。 接下來，您將建立對應的內部部署部分。

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. 安裝 hello 在內部部署混合式連線管理員 toocomplete hello 連線
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

現在該 hello 混合式連接基礎結構已完成，您將建立 web 應用程式使用它。

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. 建立基本的 ASP.NET web 專案、 編輯 hello 資料庫連接字串，並在本機執行 hello 專案
### <a name="create-a-basic-aspnet-project"></a>建立基本 ASP.NET 專案
1. 在 Visual Studio 中的 hello**檔案**功能表上，建立新的專案：
   
    ![New Visual Studio project][HCVSNewProject]
2. 在 hello**範本**hello 區段**新專案**對話方塊中，選取**Web**選擇**ASP.NET Web 應用程式**，然後按一下 **確定**。
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. 在 hello**新增 ASP.NET 專案** 對話方塊中，選擇**MVC**，然後按一下**確定**。
   
    ![Choose MVC][HCVSChooseMVC]
4. Hello 專案建立後，會顯示 hello 應用程式讀我檔案頁面。 請勿執行 hello web 專案。
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>編輯 hello hello 應用程式的資料庫連接字串
在此步驟中，您可以編輯 hello 會告訴您的應用程式的連接字串其中 toofind 本機的 SQL Server Express 資料庫。 hello 連接字串是 hello 應用程式的 Web.config 檔案，其中包含 hello 應用程式的組態資訊。

> [!NOTE]
> 應用程式使用您在 SQL Server Express，並不在 Visual Studio 的預設 LocalDB 一個 hello hello 資料庫的 tooensure，請務必執行您的專案之前完成此步驟。
> 
> 

1. 在方案總管 中，按兩下 hello Web.config 檔案。
   
    ![Web.config][HCVSChooseWebConfig]
2. 編輯 hello **connectionStrings**區段 toopoint toohello SQL Server 資料庫在本機電腦，在下列範例中的 hello hello 語法如下：
   
    ![連接字串][HCVSConnectionString]
   
    當您在撰寫 hello 連接字串，請注意 hello 下列：
   
   * 如果您要連接 tooa 具名執行個體，而不是預設執行個體 (例如，YourServer\SQLEXPRESS)，您必須設定您 SQL Server toouse 靜態連接埠。 如需設定靜態通訊埠資訊，請參閱[如何 tooconfigure 特定通訊埠上的 SQL Server toolisten](http://support.microsoft.com/kb/823938)。 根據預設，指定的執行個體會使用 UDP 和動態連接埠，而混合式連線並不加以支援。
   * 建議您指定 hello hello 連接字串上連接埠 (1433 根據預設，在 hello 範例所示)，使您可以確定您的本機 SQL Server 具有 TCP 已啟用，並且正在使用 hello 正確連接埠。
   * 請記住 toouse SQL Server 驗證 tooconnect，指定連接字串中的 hello 使用者識別碼和密碼。
3. 按一下**儲存**Visual Studio toosave hello Web.config 檔案中。

### <a name="run-hello-project-locally-and-register-a-new-user"></a>在本機執行 hello 專案，並註冊新的使用者
1. 現在，按一下 hello 瀏覽 按鈕，在偵錯在本機執行新的 web 專案。 此範例使用 Internet Explorer。
   
    ![Run project][HCVSRunProject]
2. 在 hello 右上方的 hello 預設網頁，選擇 **註冊**tooregister 新的帳戶：
   
    ![Register a new account][HCVSRegisterLocally]
3. 輸入使用者名稱和密碼：
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    這樣會自動建立資料庫，您會保留您的應用程式的 hello 成員資格資訊的本機 SQL Server 上。 其中一個 hello 資料表 (**dbo。AspNetUsers**) 保留 web 應用程式像是 hello 您剛才輸入的使用者認證。 您會看到此資料表在 hello 教學課程後面。
4. 關閉 hello 的 hello 預設網頁瀏覽器視窗。 這樣會阻止 Visual Studio 中的 hello 應用程式。

您現在準備好進行 hello 下一個步驟，也就是 toopublish hello 應用程式 tooAzure 並進行測試。

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. 發行 hello web 應用程式 tooAzure 並進行測試
現在，您將會發行您的應用程式 tooyour App Service web 應用程式，然後 toosee hello 混合式連接您先前設定的方式在本機電腦上的 web 應用程式 toohello 資料庫正在使用的 tooconnect。

### <a name="publish-hello-web-application"></a>發行 hello web 應用程式
1. 您可以下載您的 hello hello Azure 入口網站中的 App Service web 應用程式的發行設定檔。 在 web 應用程式的 hello 刀鋒視窗，按一下 **取得發行設定檔**，然後儲存 hello 檔案 tooyour 電腦。
   
    ![Download publish profile][PortalDownloadPublishProfile]
   
    接著，您會將此檔案匯入 Visual Studio Web 應用程式中。
2. 在 Visual Studio 中，以滑鼠右鍵按一下方案總管 中的 hello 專案名稱，然後選取**發行**。
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. 在 [hello**發行 Web** hello] 對話方塊，**設定檔**索引標籤上，選擇**匯入**。
   
    ![Import][HCVSPublishWebDialogImport]
4. 瀏覽 tooyour 下載發行設定檔，加以選取，然後按**確定**。
   
    ![瀏覽 tooprofile][HCVSBrowseToImportPubProfile]
5. 您發行的資訊匯入，並顯示 hello 上**連接**hello 對話方塊 索引標籤。
   
    ![Click Publish][HCVSClickPublish]
   
    按一下 [發行] 。
   
    當發行完成時，您的瀏覽器將會啟動，並顯示現在熟悉的 ASP.NET 應用程式--，不同之處在於現在是即時 hello Azure 雲端中 ！

接下來，您將使用您的即時 web 應用程式 toosee 混合式連線作用中。

### <a name="test-hello-completed-web-application-on-azure"></a>測試 hello 完成 Azure 上的 web 應用程式
1. Hello 最上層顯示權限的 Azure 上您網頁上，選擇 **登入**。
   
    ![Test log in][HCTestLogIn]
2. Web 應用程式現在正在您的應用程式服務連接 tooyour web 應用程式的成員資格資料庫，在本機電腦上。 tooverify，登入相同的認證，您輸入 hello 本機資料庫先前的 hello。
   
    ![Hello greeting][HCTestHelloContoso]
3. toofurther 測試新的混合式連線，登出您的 Azure web 應用程式並註冊為另一位使用者。 提供新的使用者名稱和密碼，然後按一下註冊 。
   
    ![Test register another user][HCTestRegisterRelecloud]
4. tooverify hello 新使用者的認證，透過您的混合式連線，本機資料庫中已儲存在本機電腦上開啟 SQL Management Studio。 在 物件總管 中，展開 hello **MembershipDB**資料庫，然後再展開**資料表**。 以滑鼠右鍵按一下 hello **dbo。AspNetUsers**成員資格資料表，並選擇**選取前 1000 個資料列**tooview hello 結果。
   
    ![檢視 hello 結果][HCTestSSMSTree]
5. 本機成員資格資料表現在會顯示這兩個帳戶-您在本機建立的其中一個 hello 與 hello hello Azure 雲端中建立的其中一個。 您建立 hello 雲端中的 hello 已儲存 tooyour 在內部部署資料庫，透過 Azure 的混合式連接功能。
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

您現在已建立並部署 ASP.NET web 應用程式使用 hello Azure 雲端中的 web 應用程式與內部部署 SQL Server 資料庫之間的混合式連接。 恭喜！

## <a name="see-also"></a>另請參閱
[混合式連線概觀](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist 介紹混合式連線 (第 9 頻道視訊)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[混合式連線概觀](/services/biztalk-services/)

[BizTalk 服務：儀表板、監視器、調整、設定和混合式連線索引標籤](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[透過絕佳的應用程式可攜性建置真實的混合式雲端 (第 9 頻道視訊)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[在 Azure App Service 中使用混合式連線存取內部部署資源](web-sites-hybrid-connection-get-started.md)

[ASP.NET 身分識別概觀](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
