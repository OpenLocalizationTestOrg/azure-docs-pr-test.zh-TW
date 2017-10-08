---
title: "aaaTroubleshoot 中使用 Visual Studio 的 Azure App Service web 應用程式"
description: "了解如何 tootroubleshoot Azure web 應用程式使用遠端偵錯、 追蹤和記錄工具內建的 tooVisual Studio 2013。"
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式
## <a name="overview"></a>概觀
本教學課程示範如何 toouse Visual Studio 工具，可協助偵錯 web 應用程式中的[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，在執行[偵錯模式](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)遠端或藉由檢視應用程式記錄檔和 web 伺服器記錄檔。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

您將了解：

* Visual Studio 中提供的 Azure Web 應用程式管理功能有哪些。
* 如何 toouse Visual Studio 遠端檢視 toomake 快速變更遠端 web 應用程式中。
* 如何 toorun 從遠端同時在專案的偵錯模式是在 Azure 中執行，web 應用程式和 web 工作。
* 如何 toocreate 應用程式追蹤記錄檔，並檢視時 hello 應用程式會建立它們。
* 如何 tooview web 伺服器記錄檔，包括詳細的錯誤訊息和失敗的要求追蹤。
* 如何 toosend 診斷記錄 tooan Azure 儲存體帳戶，並那里檢視。

如果您有 Visual Studio Ultimate，您也可以使用 [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) 進行偵錯。 本教學課程未涵蓋 IntelliTrace。

## <a name="prerequisites"></a>必要條件
本教學課程適用於 hello 開發環境、 web 專案和您在設定的 Azure web 應用程式[開始使用 Azure 和 ASP.NET][GetStarted]。 Hello WebJobs 的區段中，您將需要 hello 應用程式中建立[hello Azure WebJobs SDK 快速入門][GetStartedWJ]。

hello 程式碼範例顯示在本教學課程適用於 C# MVC web 應用程式，但是 hello 疑難排解程序是 hello Visual Basic 和 Web Form 應用程式相同。

hello 教學課程假設您使用 Visual Studio 2015 或 2013年。 如果您使用 Visual Studio 2013，hello WebJobs 功能都需要[Update 4](http://go.microsoft.com/fwlink/?LinkID=510314)或更新版本。

hello 資料流記錄功能只適用於.NET Framework 4 或更新版本為目標的應用程式。

## <a name="sitemanagement"></a>Web 應用程式組態與管理
Visual Studio 提供存取 tooa 子集 hello web 應用程式管理功能和 hello 中可用的組態設定[Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。 本節將說明使用 **伺服器總管**可用的項目。 toosee hello 最新 Azure 整合的功能，現在試試看**Cloud Explorer**也。 您可以從 hello 開啟這兩個視窗**檢視**功能表。

1. 如果您未登入 tooAzure Visual Studio 中，按一下 hello**連接 tooAzure**按鈕**伺服器總管**。

    替代方式是 tooinstall 啟用存取 tooyour 帳戶的管理憑證。 如果您選擇 tooinstall 憑證，以滑鼠右鍵按一下 hello **Azure**節點**伺服器總管**，然後按一下**管理和篩選訂閱**hello 內容功能表中。 在 hello**管理 Azure 訂用帳戶**對話方塊方塊中，按一下 hello**憑證**索引標籤，然後再按一下**匯入**。 請遵循 hello 指示 toodownload，然後再匯入訂用帳戶檔案 (也稱為*.publishsettings*檔案) 為您的 Azure 帳戶。

   > [!NOTE]
   > 如果您下載訂閱檔案、 資料夾會儲存在它 tooa 外部來源的程式碼目錄 （例如，在 hello 下載資料夾中），然後再刪除它一次 hello 匯入已完成。 惡意使用者獲得存取 toohello 訂用帳戶檔案，可以編輯、 建立，並刪除您的 Azure 服務。
   >
   >

    如需從 Visual Studio 中連接 tooAzure 資源的詳細資訊，請參閱[管理帳戶、 訂用帳戶及管理角色](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert)。
2. 在 [伺服器總管] 中，展開 [Azure]，然後展開 [App Service]。
3. 展開包含您在建立 hello web 應用程式的 hello 資源群組[開始使用 Azure 和 ASP.NET][GetStarted]，然後以滑鼠右鍵按一下 hello web 應用程式節點，再按一下**的檢視設定**.

    ![在伺服器總管中檢視設定](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    hello **Azure Web 應用程式**索引標籤會出現，以及您可以看到那里 hello web 應用程式管理和設定工作在 Visual Studio 中可用。

    ![Azure Web 應用程式視窗](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    在本教學課程將 hello 記錄和追蹤的下拉式清單使用。 您也可以使用遠端偵錯，但是您將使用不同的方法 tooenable 它。

    此視窗中的 hello 應用程式設定和連接字串方塊的相關資訊，請參閱[Azure Web 應用程式： 如何應用程式字串與連接字串工作](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

    如果您想 tooperform web 應用程式管理工作無法完成在此視窗中，按一下**管理入口網站中開啟**tooopen 瀏覽器視窗 toohello Azure 入口網站。

## <a name="remoteview"></a>在伺服器總管中存取 Web 應用程式檔案
您通常會部署 web 專案以 hello`customErrors`加上旗標 hello Web.config 檔案組太`On`或`RemoteOnly`，這表示不會很有幫助的錯誤訊息時項目發生錯誤。 許多錯誤您得到的也是 hello 的類似是 hello 的下列其中一個頁面。

**'/' 應用程式中有伺服器錯誤：**

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**發生錯誤：**

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**hello 網站無法顯示 hello 頁面**

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Hello 最簡單方式 toofind hello hello 項錯誤的原因通常是 tooenable hello hello 前面螢幕擷取畫面中的第一個詳細的錯誤訊息說明如何 toodo。 需要 hello 中的變更已部署 Web.config 檔案。 您可以編輯 hello *Web.config* hello 專案和重新部署的 hello 專案，在檔案或建立[Web.config 轉換](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)和部署偵錯組建，但還有更快的方法： 在**方案總管**直接檢視和編輯 hello 遠端 web 應用程式中的檔案使用 hello*遠端檢視*功能。

1. 在**伺服器總管**，依序展開**Azure**，依序展開**App Service**、 依序展開 hello 資源群組中，位於您 web 應用程式和 web 應用程式的 hello 節點。

    您會看到節點可讓您存取 toohello web 應用程式的內容檔案和記錄檔。
2. 展開 hello**檔案** 節點，然後按兩下 hello *Web.config*檔案。

    ![開啟 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio 會從 hello 遠端 web 應用程式開啟 hello Web.config 檔案，並顯示 hello 標題列中的 [遠端] 的下一個 toohello 檔案名稱。
3. 加入下列行 toohello hello`system.web`項目：

    `<customErrors mode="Off"></customErrors>`

    ![編輯 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. 重新整理顯示 hello 無用的錯誤訊息： hello 瀏覽器，現在您可以取得詳細的錯誤訊息，如下列範例中的 hello:

    ![詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (將顯示為紅色太 hello 一行加入建立顯示 hello 錯誤*Views\Home\Index.cshtml*。)

編輯 hello Web.config 檔案是一個範例在哪些 hello 能力 tooread 和編輯的檔案，Azure web 應用程式上進行疑難排解的案例。

## <a name="remotedebug"></a>遠端偵錯 Web 應用程式
如果 hello 詳細的錯誤訊息不會提供足夠的資訊，而且您無法重新建立本機 hello 錯誤，另一個方式 tootroubleshoot 就是從遠端 toorun 偵錯模式中。 您可以設定中斷點、 直接管理記憶體、 逐步執行程式碼，以及甚至變更 hello 程式碼路徑。

遠端偵錯無法在 Visual Studio 的 Express 版本中運作。

本節說明如何從遠端使用 hello toodebug 您專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。

1. 開啟 hello web 專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。
2. 開啟 *Controllers\HomeController.cs*。
3. 刪除 hello`About()`中其所在位置的方法，並插入 hello 下列程式碼。

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)上 hello`ViewBag.Message`列。
5. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後按一下**發行**。
6. 在 hello**設定檔**下拉式清單中，選取 hello 相同設定檔中使用該您[開始使用 Azure 和 ASP.NET][GetStarted]。
7. 按一下 hello**設定**索引標籤，然後變更**組態**太**偵錯**，然後按一下**發行**。

    ![於偵錯模式中發行](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. 在部署之後完成，您的瀏覽器會開啟 toohello Azure web 應用程式，關閉 hello 瀏覽器的 URL。
9. 在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，接著按一下 [連結偵錯工具]。

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    hello 瀏覽器會自動開啟 tooyour 首頁上，在 Azure 中執行。 您可能會有 toowait 20 秒或因此而 Azure 會設定 hello 伺服器進行偵錯。 此延遲時間只會發生 hello 偵錯模式中執行 web 應用程式的第一次。 後續時間內 hello 未來的 48 小時，當您啟動偵錯一次將不會有延遲。

    **注意：**如果您有任何無法啟動 hello 偵錯工具，再試一次 toodo 它使用**Cloud Explorer**而不是**伺服器總管**。
10. 按一下**有關**hello 功能表中。

     Visual Studio 停止 hello 中斷點並 hello 程式碼在 Azure 中，不在本機電腦上執行。
11. 將滑鼠停留在 hello`currentTime`變數 toosee hello 時間值。

     ![檢視 Azure 偵錯模式中執行的變數](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     您會看到的 hello 時間是 hello Azure 的伺服器時間，可能在不同的時區，於本機電腦。
12. 輸入新的值為 hello`currentTime`變數，例如 「 現在在 Azure 中執行 」。
13. 按 F5 toocontinue 執行。

     hello 有關在 Azure 中執行的頁面會顯示您輸入 hello currentTime 變數 hello 新值。

     ![含有新值的關於頁面](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> 遠端偵錯 WebJobs
本節說明如何從遠端使用 hello 專案和 web 應用程式的 toodebug 您在中建立[hello Azure WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk.md)。

本節中所顯示的 hello 功能只在 Visual Studio 2013 Update 4 或更新版本可用。

遠端偵錯僅適用於連續的 WebJobs。 排程與隨選 WebJobs 不支援偵錯。

1. 開啟 hello web 專案中建立[hello Azure WebJobs SDK 快速入門][GetStartedWJ]。
2. 在 hello ContosoAdsWebJob 專案中，開啟*Functions.cs*。
3. [設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)hello hello 第一個陳述式`GnerateThumbnail`方法。

    ![設定中斷點](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. 在**方案總管 中**，以滑鼠右鍵按一下 hello web 專案 （非 hello WebJob 專案），然後按一下**發行**。
5. 在 hello**設定檔**下拉式清單中，選取 hello 相同設定檔中使用該您[hello Azure WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk.md)。
6. 按一下 hello**設定**索引標籤，然後變更**組態**太**偵錯**，然後按一下**發行**。

    Visual Studio 會部署 hello web 和 WebJob 專案和您的瀏覽器會開啟 toohello Azure web 應用程式的 URL。
7. 在 [伺服器總管] 中，依序展開 [Azure] > [App Service] > 您的資源群組Web > 您的 Web 應用程式 > [WebJob] > [連續]，然後使用滑鼠右鍵按一下 [ContosoAdsWebJob]。
8. 按一下 [連結偵錯工具] 。

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    hello 瀏覽器會自動開啟 tooyour 首頁上，在 Azure 中執行。 您可能會有 toowait 20 秒或因此而 Azure 會設定 hello 伺服器進行偵錯。 此延遲時間只會發生 hello 偵錯模式中執行 web 應用程式的第一次。 hello 下一次附加 hello 偵錯有工具將不會有延遲，如果您在 48 小時內操作。
9. 在 hello web 瀏覽器開啟的 toohello Contoso 廣告首頁上，建立新的廣告。

    建立 ad 將會導致佇列訊息 toobe 建立，這會由 hello WebJob 挑選並處理。 當 hello WebJobs SDK 呼叫 hello 函式 tooprocess hello 佇列訊息時，hello 程式碼會叫用中斷點。
10. Hello 偵錯工具在中斷點中斷時，您可以檢查，並執行 hello 雲端 hello 程式時，變更變數的值。 在 hello 下列圖例 hello 偵錯工具會顯示 hello hello blobInfo 物件傳來 toohello GenerateThumbnail 方法的內容。

     ![偵錯工具中的 blobInfo 物件](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. 按 F5 toocontinue 執行。

     hello GenerateThumbnail 方法完成建立 hello 縮圖。
12. 在 hello 瀏覽器中重新整理 hello 索引頁面，您會看見 hello 縮圖。
13. 在 Visual Studio 中，請按 SHIFT + F5 toostop 偵錯。
14. 在**伺服器總管**，hello ContosoAdsWebJob 節點上按一下滑鼠右鍵，然後按一下**檢視儀表板**。
15. 使用您的 Azure 認證，登入，然後按一下 hello WebJob 名稱 toogo toohello 頁面上您的 web 工作。

     ![按一下 ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     hello 儀表板會顯示該 hello GenerateThumbnail 最近執行的函式。

     (hello 您按一下 下一次**檢視儀表板**、 您沒有在中，toosign 和 hello 瀏覽器連結直接 toohello 頁面為您的 web 工作。)
16. 按一下 hello 函式名稱 toosee 詳細 hello 函式執行。

     ![函數詳細資料](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

如果您的函式[寫入記錄檔](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)，您可以按一下**ToggleOutput** toosee 它們。

## <a name="notes-about-remote-debugging"></a>遠端偵錯注意事項
* 不建議在生產環境中執行偵錯模式。 如果您的生產環境 web 應用程式未向外延展 toomultiple 伺服器執行個體中，偵錯會使 hello 回應 tooother 要求 web 伺服器。 如果您這樣做有多個 web 伺服器執行個體，當您附加 toohello 偵錯工具就會是隨機的執行個體，而且您有任何方式 tooensure 該後續的瀏覽器要求將會傳送 toothat 執行個體。 此外，您通常不會部署偵錯組建 tooproduction，而且編譯器最佳化的發行組建可能會使它不可能發生什麼事的 tooshow 一行一行地在原始程式碼中。 針對生產環境問題的疑難排解，您的最佳資源將是應用程式追蹤與 Web 伺服器記錄。
* 進行遠端偵錯時，避免長時間在中斷點停止運作。 Azure 會將停止超過幾分鐘的處理序視為無回應的處理序，並將其關閉。
* 您正在偵錯時，hello 伺服器傳送資料 tooVisual Studio 中，但是可能會影響頻寬費用。 如需關於頻寬費率的詳細資訊，請參閱 [Azure 定價](https://azure.microsoft.com/pricing/calculator/)。
* 請確定該 hello`debug`屬性 hello `compilation` hello 中的項目*Web.config* tootrue 設定檔。 當您發行偵錯版組建組態時，它是預設設定 tootrue。

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* 如果您發現該 hello 偵錯工具不會逐步執行您想 toodebug 程式碼，您可能必須 toochange hello Just My Code 設定。  如需詳細資訊，請參閱[限制逐步執行 tooJust My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code)。
* 當您啟用 hello 遠端偵錯功能，且在 48 小時後 hello 功能會自動關閉 hello 伺服器上會啟動計時器。 此 48 小時的限制是為了安全與效能起見而設計的功能。 您可以輕鬆地 hello 功能重新開啟您要的次數。 當您不需要偵錯時，建議您將其保持為停用。
* 您可以手動附加 hello 偵錯工具 tooany 程序，不只 hello web 應用程式處理序 (w3wp.exe)。 如需如何 toouse 偵錯 Visual Studio 中的模式的詳細資訊，請參閱[Visual Studio 偵錯](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)。

## <a name="logsoverview"></a>診斷記錄概觀
Azure web 應用程式中執行的 ASP.NET 應用程式可以建立下列類型的記錄檔的 hello:

* **應用程式追蹤記錄**<br/>
  hello 應用程式會建立這些記錄檔藉由呼叫方法的 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx)類別。
* **Web 伺服器記錄**<br/>
  hello web 伺服器會建立每個 HTTP 要求 toohello web 應用程式的記錄項目。
* **詳細的錯誤訊息記錄**<br/>
  hello web 伺服器會建立 HTML 網頁失敗的 HTTP 要求 （其會導致狀態碼 400 或更新版本） 的一些額外資訊。
* **失敗要求追蹤記錄**<br/>
  hello web 伺服器會建立為失敗的 HTTP 要求的詳細的追蹤資訊的 XML 檔案。 hello web 伺服器也會提供 XSL 檔案 tooformat hello XML 的瀏覽器中。

記錄影響 web 應用程式效能，因此 Azure 可讓您 hello 能力 tooenable 或視需要停用記錄檔的每個型別。 對於應用程式記錄，您可以指定只寫入高於特定嚴重性層級的記錄。 當您建立新的 Web 應用程式時，預設會停用所有記錄功能。

記錄檔寫入 toofiles *LogFiles* hello 您 web 應用程式，並且是可透過 FTP 存取的檔案系統中的資料夾。 Web 伺服器記錄檔和應用程式記錄檔也可以寫入 tooan Azure 儲存體帳戶。 您可以保留更大的磁碟區的儲存體帳戶，而不是在 hello 檔案系統中的記錄檔。 當您使用 hello 檔案系統時，您限制的 tooa 最大值是 100 mb 的記錄檔。 (檔案系統記錄僅適用於短期保留之用。 Azure 後，刪除舊記錄檔 toomake 出空間給新的 hello 限制為止。）  

## <a name="apptracelogs"></a>建立並檢視應用程式追蹤記錄
本節中，您將會執行下列工作 hello:

* 將追蹤陳述式 toohello web 專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。
* 當您在本機執行 hello 專案時，請檢視 hello 記錄檔。
* 在 Azure 中執行的 hello 應用程式所產生時，請檢視 hello 記錄檔。

如需 toocreate 應用程式在 WebJobs 的記錄檔資訊，請參閱[如何與 Azure 佇列儲存體使用 toowork hello WebJobs SDK-toowrite 記錄的方式](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)。 hello 下列指示來檢視記錄檔與控制它們如何儲存在 Azure 中適用於也 tooapplication WebJobs 所建立的記錄檔。

### <a name="add-tracing-statements-toohello-application"></a>加入追蹤陳述式 toohello 應用程式
1. 開啟*Controllers\HomeController.cs*，並取代 hello `Index`， `About`，和`Contact`方法以 hello 下列程式碼中順序 tooadd`Trace`陳述式和`using`陳述式如`System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. 新增`using System.Diagnostics;`hello 檔案的陳述式 toohello 頂端。

### <a name="view-hello-tracing-output-locally"></a>在本機輸出檢視 hello 追蹤
1. 按下 F5 toorun hello 應用程式中的偵錯模式。

    hello 預設追蹤接聽項寫入所有的追蹤輸出 toohello**輸出**視窗中的，連同其他偵錯輸出。 hello 如下圖所示 hello hello 輸出追蹤陳述式，就像加入 toohello`Index`方法。

    ![偵錯視窗中的追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    hello 下列步驟顯示如何 tooview 追蹤輸出網頁，而不需要在偵錯模式中編譯。
2. 開啟 hello 應用程式 Web.config 檔案 (其中一個位於 hello 專案資料夾中的 hello)，然後加入`<system.diagnostics>`hello hello 結尾之前的 hello 檔案結尾處的項目`</configuration>`項目：

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    hello`WebPageTraceListener`可讓您檢視追蹤輸出，藉由瀏覽過`/trace.axd`。
3. 新增<a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">追蹤項目</a>下`<system.web>`在 hello Web.config 檔案中，如下列範例中的 hello:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. 按 CTRL + F5 toorun hello 應用程式。
5. 在 hello hello 瀏覽器視窗的網址列中加入*trace.axd* toohello URL，然後按 Enter （hello URL 會類似 toohttp://localhost:53370/trace.axd）。
6. 在 hello**應用程式追蹤**頁面上，按一下**檢視詳細資料**hello 第一行 (無法 hello BrowserLink 列)。

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    hello**要求詳細資料**頁面出現時，在 hello**追蹤資訊**> 一節，您會看到您加入 toohello hello 追蹤陳述式從 hello 輸出`Index`方法。

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    根據預設， `trace.axd` 只能在本機使用。 如果您想 toomake 它可從遠端的 web 應用程式，您可以加入`localOnly="false"`toohello `trace` hello 中的項目*Web.config*檔案 hello 下列範例所示：

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    不過，啟用`trace.axd`在生產環境中的 web 應用程式通常不建議基於安全性理由，並在 hello 下列各節中，您會看到您更輕鬆的方式 tooread 追蹤記錄的 Azure web 應用程式中。

### <a name="view-hello-tracing-output-in-azure"></a>在 Azure 中檢視 hello 追蹤輸出
1. 在**方案總管 中**，hello web 專案上按一下滑鼠右鍵，然後按一下**發行**。
2. 在 hello**發行 Web**對話方塊中，按一下 **發行**。

    Visual Studio 發行您的更新之後，它會開啟瀏覽器視窗 tooyour 首頁 (假設未清除**目的地 URL**上 hello**連接** 索引標籤)。
3. 在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，然後選取 [檢視串流記錄]。

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    hello**輸出**視窗會顯示您所連接的 toohello 記錄串流服務，並會將通知行記錄 toodisplay 不會按照每一分鐘。

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. 在 hello 瀏覽器視窗，其中顯示您應用程式的首頁，按一下 **連絡人**。

    您在幾秒 hello 來自 hello 錯誤層級的追蹤輸出內加入 toohello`Contact`方法會出現在 hello**輸出**視窗。

    ![輸出視窗中的錯誤追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio 只會顯示錯誤層級追蹤，因為這是當您啟用 hello 記錄檔監視服務的 hello 預設設定。 當您建立新的 Azure web 應用程式時，所有的記錄預設會停用，因為先前開啟 hello 設定 頁面時看見：

    ![應用程式記錄功能關閉](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    不過，當您選取**檢視串流記錄**，Visual Studio 會自動變更**應用程式 Logging(File System)**太**錯誤**，這表示錯誤層級記錄檔報告。 在追蹤記錄的所有訂單 toosee，您可以變更此設定太**Verbose**。 當您選取低於錯誤的嚴重性層級時，將一併回報較高嚴重性層級的所有記錄。 因此當您選取詳細資訊時，您會同時看到資訊、警告與錯誤記錄。  

1. 在**伺服器總管**hello web 應用程式，以滑鼠右鍵按一下，然後按**檢視設定**如先前般。
2. 變更**的應用程式記錄 （檔案系統）**太**Verbose**，然後按一下**儲存**。

    ![設定追蹤層級 tooVerbose](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. 現在顯示 hello 瀏覽器視窗中您**連絡人**頁面上，按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。

    在幾秒內，hello**輸出** 視窗會顯示所有的追蹤輸出。

    ![詳細資訊追蹤輸出](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    在本節中，您已使用 Azure Web 應用程式設定來啟用與停用記錄功能。 您也可以啟用和停用透過修改 hello Web.config 檔案的追蹤接聽項。 不過，修改 hello Web.config 檔案會導致 hello 應用程式網域 toorecycle，但在啟用記錄功能，透過 hello web 應用程式設定並不需要的。 如果 hello 問題會很長的時間 tooreproduce，或斷斷續續，回收 hello 應用程式定義域可能"修正 」 並強迫您 toowait 直到它再次發生。 在 Azure 中啟用診斷功能不會出現此情況，因此您可以立即開始擷取錯誤資訊。

### <a name="output-window-features"></a>輸出視窗功能
hello **Azure 記錄檔** 索引標籤的 hello**輸出**視窗有數個按鈕和文字方塊：

![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

這些執行 hello 下列函式：

* 清除 hello**輸出**視窗。
* 啟用或停用自動換行。
* 啟動或停止監視記錄。
* 指定的記錄 toomonitor。
* 下載記錄。
* 依據搜尋字串或規則運算式篩選記錄。
* 關閉 hello**輸出**視窗。

如果您輸入搜尋字串或規則運算式時，Visual Studio 會篩選在 hello 用戶端記錄資訊。 這表示 hello 顯示 hello 記錄檔之後，您可以輸入 hello 準則**輸出**視窗，而且您可以變更篩選條件而不需要 tooregenerate hello 記錄檔。

## <a name="webserverlogs"></a>檢視 Web 伺服器記錄
Web 伺服器記錄檔記錄所有 HTTP 活動 hello web 應用程式。 在順序 toosee 中 hello**輸出**視窗有 tooenable hello 的 web 應用程式，並告知 Visual Studio 的 toomonitor 它們。

1. 在 hello **Azure Web 應用程式組態** 索引標籤中開啟**伺服器總管**，也變更 Web 伺服器記錄**上**，然後按一下**儲存**.

    ![啟用 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. 在 [hello**輸出**視窗中，按一下 hello**指定哪些 Azure 記錄檔 toomonitor** ] 按鈕。

    ![指定哪些 Azure 記錄檔 toomonitor](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. 在 hello **Azure 記錄選項**對話方塊中，選取**Web 伺服器記錄檔**，然後按一下**確定**。

    ![監視 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. 在顯示 hello web 應用程式的 hello 瀏覽器視窗中按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。

    hello 應用程式記錄檔通常會先出現，後面接著 hello web 伺服器記錄檔。 您可能必須 toowait hello 一些記錄 tooappear。

    ![輸出視窗中的 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

根據預設，當您第一次啟用 web 伺服器記錄檔時使用 Visual Studio 中，Azure 會寫入 hello 記錄 toohello 檔案系統。 或者，您可以使用 hello Azure 入口網站 web 伺服器記錄檔的 toospecify 應該要撰寫 tooa blob 容器的儲存體帳戶。

如果您使用 hello tooenable 入口網站的 web 伺服器記錄 tooan Azure 儲存體帳戶，然後再停用記錄在 Visual Studio 中，當您重新啟用登入 Visual Studio 會還原您的儲存體帳戶設定。

## <a name="detailederrorlogs"></a>檢視詳細的錯誤訊息記錄
針對導致錯誤回應代碼 (400 或以上) 之 HTTP 要求，詳細的錯誤訊息記錄可提供部分額外資訊。 在訂單 toosee 中 hello**輸出**視窗中，您有 tooenable hello 的 web 應用程式，並告知 Visual Studio 的 toomonitor 它們。

1. 在 [hello **Azure Web 應用程式組態**] 索引標籤中開啟**伺服器總管**，變更**詳細的錯誤訊息**太**上**，和然後按一下**儲存**。

    ![啟用詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. 在 [hello**輸出**視窗中，按一下 hello**指定哪些 Azure 記錄檔 toomonitor** ] 按鈕。
3. 在 hello **Azure 記錄選項**對話方塊中，按一下**所有記錄檔**，然後按一下**確定**。

    ![監視所有記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. 在 hello hello 瀏覽器視窗的網址列中加入額外的字元 toohello URL toocause 404 錯誤 (例如， `http://localhost:53370/Home/Contactx`)，然後按 Enter。

    幾秒之後 hello 詳細的錯誤記錄檔會出現在 Visual Studio hello**輸出**視窗。

    ![輸出視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    控制並按一下滑鼠左鍵 hello 連結 toosee hello 記錄輸出格式的瀏覽器中：

    ![瀏覽器視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>下載檔案系統記錄
您可以在 hello 監視任何記錄檔**輸出**視窗也可以下載為*.zip*檔案。

1. 在 hello**輸出**視窗中，按一下**下載串流記錄**。

    ![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    檔案總管 中開啟 tooyour*下載*資料夾以 hello 下載選取的檔案。

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. 擷取 hello *.zip*檔案，而且您會看到下列資料夾結構的 hello:

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * 應用程式的追蹤記錄檔位於*.txt*檔案在 hello *LogFiles\Application*資料夾。
   * Web 伺服器記錄檔位於*.log*檔案在 hello *LogFiles\http\RawLogs*資料夾。 您可以使用一種工具，例如[記錄檔剖析器](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659)tooview 和管理這些檔案。
   * 詳細的錯誤訊息記錄檔位於*.html*檔案在 hello *LogFiles\DetailedErrors*資料夾。

     (hello*部署*原始檔控制發行; 建立檔案的資料夾是沒有任何項目相關的 tooVisual Studio 發行功能。 hello *Git*資料夾是追蹤相關的 toosource 控制發行和 hello 記錄檔案串流服務。)  

## <a name="storagelogs"></a>檢視儲存體記錄
應用程式的追蹤記錄檔也可以傳送 tooan Azure 儲存體帳戶，您可以在 Visual Studio 中檢視它們。 您會建立儲存體帳戶、 啟用 hello 傳統入口網站中的儲存體記錄及檢視這些 hello toodo**記錄** 索引標籤的 hello **Azure Web 應用程式**視窗。

您可以傳送記錄檔 tooany 或所有三個目的地：

* hello 檔案系統。
* 儲存體帳戶資料表。
* 儲存體帳戶 Blob。

您可以為每個目的地指定不同的嚴重性層級。

資料表可讓您輕鬆 tooview 上線，記錄檔的詳細資料，以及它們支援資料流。您可以查詢資料表中的記錄檔，並查看新的記錄檔，正在建立時的方式。 輕鬆 toodownload 記錄檔中的檔案和 tooanalyze blob 讓它們使用 HDInsight，因為 HDInsight 知道如何使用 blob 儲存體 toowork。 如需詳細資訊，請參閱 **資料儲存體選項 (運用 Azure 建構真實的雲端應用程式)** 中的 [Hadoop 與 MapReduce](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options)(英文)。

您目前沒有檔案系統記錄檔集 tooverbose 層級;hello 下列步驟引導您設定的資訊層級的記錄檔 toogo toostorage 帳戶資料表。 資訊層級代表所有藉由呼叫 `Trace.TraceInformation`、`Trace.TraceWarning` 與 `Trace.TraceError` 的記錄都會顯示出來，但不會顯示藉由呼叫 `Trace.WriteLine` 所建立的記錄。

儲存體帳戶提供更多的儲存體和記錄檔的長期保留比較 toohello 檔案系統。 追蹤記錄檔 toostorage 傳送應用程式的另一個好處就是您取得一些額外的資訊不會從檔案系統記錄檔的每個記錄檔。

1. 以滑鼠右鍵按一下**儲存體**底下 hello Azure 的節點，然後按一下**建立儲存體帳戶**。

![建立儲存體帳戶](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. 在 [hello**建立儲存體帳戶**] 對話方塊中，輸入 hello 儲存體帳戶的名稱。

    hello 名稱必須是必須是唯一的 (沒有其他的 Azure 儲存體帳戶可以有 hello 相同的名稱)。 如果您輸入的 hello 名稱已在使用您會得到機會 toochange 它。

    hello 儲存體帳戶將會是 URL tooaccess *{name}*。.core.windows.net。
2. 設定 hello**地區或同質群組**下拉式選單 toohello 區域最接近 tooyou。

    此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。 此教學課程中您選擇不明顯的差異，但生產環境 web 應用程式要為您的 web 伺服器和您在 hello 的儲存體帳戶 toobe 相同區域 toominimize 延遲和資料輸出費用。 hello web 應用程式 （您將在稍後建立） 應該在為關閉，可能 toohello 瀏覽器存取 web 應用程式的順序 toominimize 延遲地區執行。
3. 設定 hello**複寫**下拉式清單也列出**本機備援**。
   
    儲存體帳戶啟用地理複寫時，儲存的 hello 內容是複寫的 tooa 次要資料中心 tooenable 容錯移轉 toothat 位置發生重大災害 hello 主要位置中。 地理區域複寫會引發額外成本。 針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。 如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。
4. 按一下 [建立] 。

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. Hello Visual Studio 中**Azure Web 應用程式**視窗中，按一下 hello**記錄**索引標籤，然後再按一下**管理入口網站中設定記錄**。

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![設定記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    這會開啟 hello**設定**hello 傳統入口網站 web 應用程式中的索引標籤。
6. Hello 傳統入口網站中的**設定**索引標籤上，向下捲動 toohello 應用程式診斷 區段，然後再變更**的應用程式記錄 （資料表儲存體）**太**上**。
7. 變更**記錄層級**太**資訊**。
8. 按一下 [管理資料表儲存體] 。

    ![按一下 [管理資料表儲存體]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    在 [hello**管理資料表儲存體應用程式診斷**] 方塊中，您可以選擇儲存體帳戶，如果您有一個以上。 您可以建立新的資料表，或是使用現有的資料表。

    ![管理資料表儲存體](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. 在 hello**管理資料表儲存體應用程式診斷**方塊按一下 hello 核取記號 tooclose hello 方塊。
10. Hello 傳統入口網站中的**設定**索引標籤上，按一下 **儲存**。
11. 在顯示 hello 應用程式的 web 應用程式的 hello 瀏覽器視窗中按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。

     產生瀏覽這些網頁的 hello 記錄資訊會寫入 toohello 儲存體帳戶。
12. 在 hello**記錄檔**hello 索引標籤**Azure Web 應用程式**視窗在 Visual Studio 中，按一下 **重新整理**下**診斷摘要**。

     ![按一下 [重新整理]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     hello**診斷摘要**區段預設會顯示記錄檔中的 hello 過去 15 分鐘內。 您可以變更 hello 期間 toosee 詳細的記錄檔。

     (如果您收到 「 找不到資料表 」 錯誤，請確認您已經瀏覽 toohello 頁面執行 hello 追蹤在您啟用之後，**的應用程式記錄 （儲存體）**並在您按一下之後**儲存**。)

     ![儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     請注意，在此檢視您看到**處理序識別碼**和**Thread ID**針對每個記錄檔，就無法取得 hello 檔案系統記錄檔中。 您可以直接檢視 hello Azure 儲存體資料表，以查看其他欄位。
13. 按一下 [View all application logs] 。

     hello 追蹤記錄檔資料表會出現在 hello Azure 儲存體資料表檢視器。

     (如果您收到 「 序列包含任何項目 」 的錯誤，請開啟**伺服器總管**，展開您的儲存體帳戶下 hello hello 節點**Azure**節點，然後再以滑鼠右鍵按一下**資料表**按一下**重新整理**。)

     ![資料表檢視中的儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     此檢視會顯示在其他任何檢視中都不會看到的額外欄位。 此檢視也可讓您 toofilter 記錄來建構查詢中使用特殊的查詢產生器 UI。 如需詳細資訊，請參閱 [使用伺服器總管瀏覽儲存體資源](http://msdn.microsoft.com/library/ff683677.aspx)中的「使用表格資源 - 篩選實體」。
14. toolook 在 hello 詳細資料，是單一資料列中，按兩下 hello 資料列的其中一個。

     ![伺服器總管中的追蹤資料表](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>檢視失敗要求追蹤記錄
當您需要的 IIS 中的案例，例如 URL 重寫或驗證問題的 HTTP 要求中的特殊處理的 toounderstand hello 詳細資料，失敗的要求追蹤記錄檔很有用。

Azure web 應用程式使用 hello 相同失敗要求的追蹤功能已可透過 IIS 7.0 及更新版本。 您沒有存取 toohello IIS 設定，以設定哪些錯誤會記錄，不過。 當您啟用失敗要求追蹤時，將擷取所有錯誤。

您可以使用 Visual Studio 來啟用失敗要求追蹤，但是您無法在 Visual Studio 中加以檢視。 這些記錄是 XML 檔案。 hello 串流記錄服務只會監視會被視為在純文字模式下可讀取的檔案： *.txt*， *.html*，和*.log*檔案。

您可以直接透過 FTP 或在本機使用 FTP 工具 toodownload 之後在瀏覽器中檢視失敗的要求追蹤記錄它們 tooyour 本機電腦。 在本節中，您將在瀏覽器中直接檢視。

1. 在 [hello**組態**hello] 索引標籤**Azure Web 應用程式**視窗中開啟**伺服器總管**，變更**失敗要求的追蹤**太**上**，然後按一下**儲存**。

    ![啟用失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. 在 hello hello 顯示 hello web 應用程式的瀏覽器視窗的網址列中加入額外的字元 toohello URL，然後按一下 Enter toocause 404 錯誤。

    這會導致建立失敗的要求追蹤記錄檔 toobe 和 hello 下列步驟顯示如何 tooview 或下載 hello 記錄檔。
3. 在 Visual Studio，在 hello**組態**] 索引標籤的 hello **Azure Web 應用程式**視窗中，按一下 [**管理入口網站中開啟**。
4. 在 hello [Azure 入口網站](https://portal.azure.com)**設定**刀鋒視窗，web 應用程式中，按一下**部署認證**，然後輸入新的使用者名稱和密碼。

    ![新的 FTP 使用者名稱與密碼](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    * * 當您登入，您會有與 hello web 應用程式名稱的前置詞 tooit toouse hello 完整使用者名稱。 例如，如果您輸入 「 myid"做為使用者名稱，而且 hello 站台 」 myexample 」，您身分登入 」 myexample\myid"。
5. 在新的瀏覽器視窗中，移會顯示在下方的 toohello URL **FTP 主機名稱**或**FTPS 主機名稱**在 hello **Web 應用程式**web 應用程式 刀鋒視窗。
6. 使用您稍早 （包括 hello web 應用程式的名稱前置詞 hello 使用者名稱） 所建立的 hello FTP 認證登入。

    hello 瀏覽器顯示 hello hello web 應用程式的根資料夾。
7. 開啟 hello *LogFiles*資料夾。

    ![開啟 LogFiles 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. 開啟 hello 資料夾名為 W3SVC 加上數字的值。

    ![開啟 W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    hello 資料夾包含已記錄在您啟用失敗的要求追蹤之後的任何錯誤的 XML 檔案和瀏覽器可以使用 tooformat hello XML XSL 檔。

    ![W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. 按一下您想要針對 toosee 追蹤資訊的 hello 失敗要求的 hello XML 檔。

    hello 如下圖所示的範例錯誤 hello 追蹤資訊的一部分。

    ![瀏覽器中的失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>後續步驟
您已經看到如何 Visual Studio 可讓您輕鬆 tooview Azure web 應用程式所建立的記錄檔。 hello 下列各節提供連結 toomore 資源相關主題：

* Azure Web 應用程式疑難排解
* Visual Studio 偵錯
* 在 Azure 中遠端偵錯
* 在 ASP.NET 應用程式中追蹤
* 分析 Web 伺服器記錄
* 分析失敗要求追蹤記錄
* 偵錯雲端服務

### <a name="azure-web-app-troubleshooting"></a>Azure Web 應用程式疑難排解
如需疑難排解在 Azure App Service web 應用程式的詳細資訊，請參閱下列資源的 hello:

* [如何 toomonitor web 應用程式](/manage/services/web-sites/how-to-monitor-websites/)
* [使用 Visual Studio 2013 調查 Azure Web 應用程式中的記憶體流失](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx)。 Microsoft ALM 部落格文章，討論 Visual Studio 中分析 Managed 記憶體問題的功能。
* [您應該了解的 Azure Web 應用程式線上工具](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/)。 取自 Amit Apple 的部落格文章。

有關特定疑難排解問題，請啟動執行緒 hello 遵循論壇的其中一個：

* [hello hello ASP.NET 網站上的 Azure 論壇](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET)。
* [hello MSDN 上的 Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/)。
* [StackOverflow.com](http://www.stackoverflow.com)。

### <a name="debugging-in-visual-studio"></a>Visual Studio 偵錯
如需有關如何 toouse 偵錯 Visual Studio 中的模式的詳細資訊，請參閱 hello [Visual Studio 偵錯](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)MSDN 主題和[偵錯秘訣與 Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx)。

### <a name="remote-debugging-in-azure"></a>在 Azure 中遠端偵錯
如需 Azure web 應用程式和 Webjob 的遠端偵錯的詳細資訊，請參閱下列資源的 hello:

* [簡介 tooRemote 偵錯 Azure App Service Web 應用程式](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)。
* [簡介 tooRemote 偵錯 Azure App Service Web 應用程式第 2 部-內遠端偵錯](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [簡介 tooRemote Azure App Service Web 應用程式組件 3-多重執行個體環境和 GIT 上偵錯](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [WebJobs 偵錯 (影片)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

如果您的 web 應用程式使用 Azure Web 應用程式開發介面或行動服務後端，而且需要請參閱 toodebug [Visual Studio 中偵錯.NET 後端](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)。

### <a name="tracing-in-aspnet-applications"></a>在 ASP.NET 應用程式中追蹤
有追蹤 hello 網際網路上沒有完整且最新的介紹 tooASP.NET。 hello 最佳做法被開始使用舊的簡介資料寫入如需 Web Form 因為 MVC 不存在，而且補充的較新的部落格文章著重於特定的問題。 某些有用位置 toostart 是 hello 下列資源：

* [監視與遙測 (運用 Azure 建構真實的雲端應用程式) (英文)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)。<br>
  針對追蹤 Azure 雲端應用程式所建議的電子書章節。
* [ASP.NET 追蹤](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  舊但仍是絕佳的資源的基本介紹 toohello 主旨。
* [追蹤接聽程式](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  追蹤接聽程式的相關資訊，但不會有提及 hello[組態區段](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx)。
* [逐步解說︰整合 ASP.NET 追蹤與 System.Diagnostics 追蹤](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  這太老舊，但包含一些額外資訊 hello 入門文件未涵蓋的範圍。
* [追蹤 ASP.NET MVC Razor 檢視](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Razor 檢視中的追蹤，除了 hello 文章也會說明如何 toocreate 錯誤篩選中的順序 toolog MVC 應用程式中的所有未處理例外狀況。 如需所有 toolog 的未都處理例外狀況，在 Web Form 應用程式，請參閱 hello Global.asax 範例[錯誤處理常式的完整範例](http://msdn.microsoft.com/library/bb397417.aspx)MSDN 上。 在 MVC 或 Web Form 中，如果您想 toolog 某些例外狀況，但讓 hello 預設架構處理生效，您可以攔截並重新擲回如 hello 下列範例所示：

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [資料流從 hello Azure 命令列的診斷追蹤記錄 （加上初探 ！）](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  如何 toouse hello 命令列 toodo 此教學課程顯示如何在 Visual Studio 中的 toodo。 [Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) (英文) 工具可供您偵錯 ASP.NET 應用程式。
* [使用 Azure Web Apps 記錄和診斷功能 - 與 David Ebbo 合作](/documentation/videos/azure-web-site-logging-and-diagnostics/)以及[來自 Web Apps 的串流記錄 - 與 David Ebbo 合作](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  (英文) 影片，由 Scott Hanselman 與 David Ebbo 共同錄製。

錯誤記錄的替代 toowriting 您自己的追蹤程式碼是 toouse 開放原始碼記錄架構，例如[ELMAH](http://nuget.org/packages/elmah/)。 如需詳細資訊，請參閱 [Scott Hanselman 關於 ELMAH 的部落格文章](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)(英文)。

另外請注意您不需要 toouse ASP.NET，或如果您想串流處理 tooget System.Diagnostics 追蹤會記錄來自 Azure。 hello Azure web 應用程式串流記錄服務會串流任何*.txt*， *.html*，或*.log*在 hello 中找到的檔案*LogFiles*資料夾。 因此，您可以建立自己的記錄系統寫入 toohello 檔案系統的 hello web 應用程式，而且您的檔案會自動串流處理並下載。 您只需要 toodo 會寫入應用程式程式碼檔案建立在 hello *d:\home\logfiles*資料夾。

### <a name="analyzing-web-server-logs"></a>分析 Web 伺服器記錄
如需分析 web 伺服器記錄檔的詳細資訊，請參閱下列資源的 hello:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  用於檢視 Web 伺服器記錄 (*.log* 檔案) 中資料的工具。
* [疑難排解 IIS 效能問題或使用 LogParser 的應用程式錯誤](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  您可以使用 tooanalyze web 伺服器的簡介 toohello 記錄檔剖析器工具記錄。
* [Robert McMurray 關於使用 LogParser 的部落格文章](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [hello IIS 7.0、 IIS 7.5 和 IIS 8.0 中的 HTTP 狀態碼](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>分析失敗要求追蹤記錄
hello Microsoft TechNet 網站包含[使用失敗要求的追蹤](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing)區段，這可能有助於了解如何 toouse 這些記錄檔。 不過，本文主要著重在 IIS 內設定失敗要求追蹤功能，這是您無法在 Azure Web Apps 中執行的功能。

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
