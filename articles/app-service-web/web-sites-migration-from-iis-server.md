---
title: "aaaMigrate 企業 web 應用程式 tooAzure 應用程式服務"
description: "顯示 toouse Web 應用程式移轉小幫手 tooquickly 要如何移轉現有的 IIS 網站 tooAzure App Service Web 應用程式"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>移轉企業 web 應用程式 tooAzure 應用程式服務
您可以輕鬆地移轉您現有的網站，執行在網際網路資訊服務 (IIS) 6 或更新版本太[App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。 

> [!IMPORTANT]
> 我們已在 2015 年 7 月 14 日終止對 Windows Server 2003 的支援。 如果您目前裝載您為 Windows Server 2003 的 IIS 伺服器上的網站，Web 應用程式就會是的 tookeep 上線，網站和 Web 應用程式移轉小幫手可協助您自動化 hello 移轉程序的低風險、 低成本和低人事方法。 
> 
> 

[Web 應用程式移轉小幫手](https://www.movemetothecloud.net/)可以分析 IIS 伺服器安裝，請找出哪些站台可以是移轉的 tooApp 服務、 反白顯示無法移轉或 hello 平台上，不支援的任何項目，然後再移轉您的網站，並相關聯的資料庫 tooAzure。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>在相容性分析期間驗證的元素
移轉小幫手 hello 建立任何可能會造成的問題或封鎖的問題可能導致無法成功從內部部署 IIS tooAzure App Service Web 應用程式移轉整備報表 tooidentify。 某些 hello 索引鍵的項目 toobe 注意的是：

* 連接埠繫結 - Web Apps 僅支援連接埠 80 (適用於 HTTP) 和連接埠 443 (適用於 HTTPS 流量)。 會忽略不同的通訊埠設定，而流量會路由的 too80 或 443。 
* 驗證 - Web Apps 預設支援匿名驗證以及應用程式所指定的表單驗證。 只有與 Azure Active Directory 和 ADFS 整合，才能使用 Windows 驗證。 目前不支援所有其他形式的驗證 (例如基本驗證)。 
* 全域組件快取 (GAC) – GAC 不支援在 Web 應用程式中的 hello。 如果您的應用程式參考組件的通常是部署 toohello GAC，您就需要 toodeploy toohello 應用程式在 Web 應用程式的 bin 資料夾。 
* IIS5 相容性模式 - Web Apps 不支援此模式。 
* 在 hello 中執行的應用程式集區-Web 應用程式中的，每個站台及其子應用程式相同的應用程式集區。 如果您的網站有多個子應用程式利用多個應用程式集區，將其合併 tooa 單一應用程式集區使用通用的設定，或移轉每個應用程式 tooa 個別 web 應用程式。
* COM 元件： Web 應用程式不允許在 hello 平台上的 hello 註冊的 COM 元件。 如果您的網站或應用程式使用的任何 COM 元件，您必須重新撰寫它們在 managed 程式碼，並將其部署與 hello 網站或應用程式。
* ISAPI 擴充程式 – Web 應用程式可以支援 hello 使用 ISAPI 擴充程式。 您需要 toodo hello 下列：
  
  * 部署 web 應用程式的 hello Dll 
  * 註冊使用 hello Dll [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * applicationHost.xdt 檔案置於 hello 網站根目錄，以 「 允許 arbitrart ISAPI 延伸模組 toobe 載入 」 所述的 hello 內容[本文一節](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    如需如何的範例 toouse XML 文件轉換到您的網站，請參閱[轉換您的 Microsoft Azure 網站](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx)。
* 不會移轉其他元件，例如 SharePoint、Front Page Server Extensions (FPSE)、FTP、SSL 憑證。

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>如何 toouse hello Web 應用程式移轉小幫手
本節逐步說明範例 tootoomigrate 幾個網站使用 SQL Server 資料庫，並在內部部署 Windows Server 2003 R2 (IIS 6.0) 電腦上執行：

1. 在 hello IIS 伺服器或用戶端電腦瀏覽過[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. 安裝 Web 應用程式移轉小幫手按一下 hello**專用 IIS 伺服器** 按鈕。 更多選項將會在未來附近的 hello 的選項。 
3. 按一下 hello **Install Tool**按鈕在電腦上的 Web 應用程式移轉小幫手 tooinstall。
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > 您也可以按一下**下載離線安裝**toodownload ZIP 檔案不在伺服器上安裝連線 toohello 網際網路。 或者，您可以按一下**上傳現有的移轉整備報表**，這是進階的選項 toowork，與現有移轉整備報表先前產生 （稍後說明）。
   > 
   > 
4. 在 hello**應用程式安裝**畫面上，按一下**安裝**tooinstall 您的電腦上。 必要時也會安裝對應的相依項目，如 Web Deploy、DacFX 和 IIS。 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   安裝後，Web Apps 移轉小幫手會自動啟動。
5. 選擇**將站台和資料庫移轉從遠端伺服器 tooAzure**。 輸入 hello 遠端伺服器 hello 系統管理認證，然後按一下**繼續**。 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   您當然可以選擇 toomigrate hello 的本機伺服器。 當您想從實際執行的 IIS 伺服器 toomigrate 網站時，則 hello 遠端選項會很有用。
   
   Hello 移轉工具會檢查在此時 hello IIS 伺服器的組態，例如網站、 應用程式、 應用程式集區，以及相依性 tooidentify 候選的網站進行移轉。 
6. hello 以下螢幕擷取畫面顯示三個網站 – **Default Web Site**， **TimeTracker**，和**CommerceNet4**。 全部都有相關聯的資料庫，我們想要 toomigrate。 選取所有 hello 站台，tooassess 然後再按一下**下一步**。
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. 按一下**上傳**tooupload hello 整備報表。 如果您按一下**檔案儲存在本機儲存**，您可以稍後再執行 hello 移轉工具，並且上傳 hello 儲存整備報表，如前文所述。
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   一旦您上傳 hello 整備報表時，Azure 會在執行整備分析和顯示 hello 結果。 讀取 hello 評估每個網站的詳細資料，並確定您了解，或是解決所有問題後再繼續。 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. 按一下**開始移轉**toostart hello 移轉。您現在將會重新導向的 tooAzure toolog 入您的帳戶。 請務必以具有作用中 Azure 訂用帳戶的帳戶進行登入。 如果您沒有 Azure 帳戶，可以在[這裡](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_)註冊免費試用。 
9. 選取 hello 租用戶帳戶、 Azure 訂用帳戶和地區 toouse 已移轉的 Azure web 應用程式和資料庫，然後按一下**開始移轉**。 您可以稍後再選取 hello 網站 toomigrate。
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. Hello 下一個畫面中您可以變更 toohello 預設移轉設定，例如：
    
    * 使用現有的 Azure SQL Database 或建立新的 Azure SQL Database，並設定其認證
    * 選取 hello 網站 toomigrate
    * 定義 hello Azure web 應用程式並將其連結的 SQL 資料庫的名稱
    * hello 通用及自訂設定網站層級設定
    
    hello 以下螢幕擷取畫面顯示以 hello 預設設定的移轉選取的所有 hello 網站。
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > hello**啟用 Azure Active Directory**核取方塊，在自訂設定整合 hello Azure web 應用程式與[Azure Active Directory](../active-directory/active-directory-whatis.md) (hello**預設目錄**)。 如需同步處理 Azure Active Directory 與內部部署 Active Directory 的詳細資訊，請參閱[目錄整合](http://msdn.microsoft.com/library/jj573653)。
    > 
    > 
11. 一旦您進行 hello 所需的所有變更，按一下 **建立**toostart hello 移轉程序。 hello 移轉工具會建立 hello Azure SQL Database 和 Azure web 應用程式，並再發行 hello 網站內容和資料庫。 hello 移轉工具，清楚地顯示 hello 移轉進度，且您會看到在 hello 結束時，哪些詳細資料 hello 站台移轉、 他們是否成功、 連結 toohello 新建的 Azure web 應用程式的摘要畫面。 
    
    如果任何錯誤，就會發生在移轉期間，hello 移轉工具 會清楚指出 hello 失敗和回復 hello 變更。 您也會無法 toosend hello 錯誤報告直接 toohello 工程小組，網址為按一下 hello**傳送錯誤報表**按鈕，與 hello 擷取的失敗的呼叫堆疊，並建立訊息本文。 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    如果移轉成功且沒有錯誤，您也可以按一下 hello**提供意見反應**直接按鈕 tooprovide 任何意見反應。 
12. 按一下 hello 連結 toohello Azure web 應用程式並確認已成功 hello 移轉。
13. 您現在可以管理 hello 移轉 Azure App Service 中的 web 應用程式。 toodo，登入 hello [Azure 入口網站](https://portal.azure.com)。
14. 在 [hello Azure 入口網站，開啟 hello Web 應用程式] 刀鋒視窗 toosee 移轉網站 （顯示為 web 應用程式），然後按一下其中任何一個 toostart 管理 hello web 應用程式，例如設定連續發行、 建立備份，自動調整，以及監視使用量或效能。
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

