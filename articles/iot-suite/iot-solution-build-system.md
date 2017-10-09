---
title: "MyDriving Azure IoT 範例 - 建置 | Microsoft Docs"
description: "建置應用程式的方式的完整示範 tooarchitect IoT 系統使用 Microsoft Azure，包括資料流分析、 機器學習和事件中心。"
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>建置和部署 hello MyDriving 方案 tooyour 環境
MyDriving 是物聯網 (IoT) 方案，它會收集您的行車資料、使用機器學習服務處理資料，再將資料呈現在您的行動電話上。 hello 後端包含各種不同的 Microsoft Azure 提供的服務。 hello 用戶端可能 Android、 iOS 或 Windows 10 手機。

我們建立 hello MyDriving 方案 toogive 您開始建立您自己的 IoT 系統使用。 從 hello [MyDriving GitHub 上的儲存機制](https://github.com/Azure-Samples/MyDriving)，您可以取得 Azure 資源管理員指令碼 toodeploy hello 後端架構成您自己的 Azure 帳戶。 從該點，您可以重新設定 hello 不同的服務、 修改 hello 查詢 toosuit 您自己的資料，並以此類推。 您可以找到這些指令碼-以及 hello 行動裝置應用程式、 hello Azure 應用程式服務 API 專案，以及更多-hello MyDriving 儲存機制中的程式碼。

如果還未嘗試 hello 應用程式，請查看 hello [Get 指南](iot-solution-get-started.md)。

沒有在 hello hello 架構詳細的帳戶[MyDriving 參考指南](http://aka.ms/mydrivingdocs)。 在 [摘要] 中，有幾個部分，我們設定 toocreate 相似的專案：

* **用戶端應用程式** 會在 Android、iOS 和 Windows 10 手機上執行。 我們使用 hello Xamarin 平台 tooshare 大部分 hello 碼，儲存在 GitHub `src/MobileApp`。 hello 應用程式會實際執行兩個不同的函式：
  * 它會轉送遙測從 hello 主機板診斷 (OBD) 裝置，並從它自己的位置服務 toohello 系統雲端後端。
  * 這是可讓使用者查詢其行車記錄的使用者介面。
* A**雲端服務**內嵌即時 hello 道路路線資料，並加以處理。 建立此服務的 hello 主要工作是 toochoose、 參數化，和連接各種不同的 Azure 服務。 某些 hello 組件需要指令碼 toofilter 及處理 hello 內送資料。 我們使用 Azure Resource Manager 範本 tooconfigure hello 的所有組件。
* A**行動服務應用程式**是 hello 背後 hello hello 裝置應用程式的使用者介面組件的 web 服務。 其主要工作是 tooquery hello 資料庫儲存的已處理的資料。 其程式碼位於 GitHub 上的 `src/MobileAppService`下。
* **Visual Studio 和 Xamarin** 是我們的開發環境。 使用 Xamarin，做為 Visual Studio 的元件，以及做為獨立的整合式的開發環境 (IDE) 存在，toobuild hello 跨平台裝置的程式碼。 toobuild hello iOS 程式碼，它是必要的 toohave Xamarin OS X 電腦上執行的執行個體。 必要時，也可以當做從 Visual Studio 管理的代理程式來執行。
* **單元測試**hello 裝置的應用程式會在 Xamarin Test Cloud 中執行。
* **GitHub**是我們儲存所有 hello 程式碼、 指令碼和範本的 hello 儲存機制。
* **Visual Studio Team Services**是 toomanage hello 連續建置和測試 hello web 服務與裝置的應用程式已使用的雲端服務。
* **HockeyApp**是使用的 toodistribute hello 裝置程式碼的版本。 還會收集當機和使用狀況報告以及使用者意見反應。
* **Visual Studio Application Insights**監視器 hello 行動裝置 web 服務。

以下示範如何設定上述所有項目。 

> [!NOTE] 
> 許多 hello 步驟是選擇性的。
>
>

## <a name="sign-up-for-accounts"></a>註冊帳戶
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx)。 這個免費程式提供讓您輕鬆存取 toomany 開發者工具與服務，包括 Visual Studio、 Visual Studio Team Services 和 Azure。 它會提供給您 12 個月每月美金 $25 元的 Azure 點數。 它也包含訂閱 tooPluralsight 訓練和 Xamarin 大學。 您也可以另外註冊 [Azure](https://azure.com) 和 [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx) 的免費層，但這不會提供 Azure 點數。
* [HockeyApp](https://rink.hockeyapp.net/) (選擇性)，用於管理行動應用程式的測試散發及收集遙測。
* [Xamarin](https://xamarin.com/) （必要），建置 hello 行動裝置應用程式並執行偵錯執行和測試[Xamarin Test Cloud](https://xamarin.com/test-cloud)。
* [GitHub](https://github.com/Azure-Samples/MyDriving/) （選擇性） toocreate 免費公用儲存機制 （付費私用儲存機制） 您的程式碼。 或者，您可以使用 hello 基本方案中的私用儲存機制的 Visual Studio Team Services。
* [Power BI](https://powerbi.microsoft.com/) （選擇性） toocreate 豐富的視覺化 hello 整個系統上的資料。

> [!NOTE]
> 您不需要的 GitHub 帳戶 tooaccess hello MyDriving 中的程式碼[hello GitHub MyDriving 儲存機制](https://github.com/Azure-Samples/MyDriving)。
> 
> 

## <a name="install-development-tools"></a>安裝開發工具
hello 下列安裝程式來開發 hello 完整的解決方案： iOS、 Android 和 Windows 10 行動裝置版與 Azure 跨平台應用程式後端。

或者，您可以 Mac 或 Windows toodevelop hello 行動應用程式上使用 Xamarin Studio，如果您並非正在運作的 hello Azure 備份結束。

有 [此設定的詳細說明](https://msdn.microsoft.com/library/mt613162.aspx)。

### <a name="windows-development-machine"></a>Windows 開發電腦
hello Windows 上的中央工具是 Visual Studio 中，處理 hello MyDriving 應用程式的 Android 和 Windows、 hello 應用程式服務 API 專案和微服務延伸模組。

Xamarin、Git、模擬器及其他實用元件已全部與 Visual Studio 整合。

安裝：

* [Visual Studio 和 Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (任何版本 - Community 版免費)。
* [適用於通用 Windows 平台的 SQLite](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936)。 需要 toobuild hello Windows 10 行動裝置版的程式碼。
* [Azure SDK for Visual Studio](https://www.visualstudio.com/vs/azure-tools/)。 可讓您在 Azure 中，執行應用程式，以及命令列工具來管理 Azure hello SDK。
* [Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric)。 需要的 toobuild hello[微服務](../service-fabric/service-fabric-get-started.md)延伸模組。

請確定您擁有 hello 右 Visual Studio 擴充功能。 確認在 [工具] 下會看到 **Android、iOS、Xamarin…**。 如果沒有，請開啟 Visual Studio 中，搜尋 Xamarin，並遵循 hello 提示 tooinstall 它。 此外，請檢查是否已安裝 **Git for Windows**。 如果沒有，請在 Visual Studio 中進行搜尋，並遵循 hello 提示 tooinstall 它。 

### <a name="mac-development-machine"></a>Mac 開發電腦
hello Mac (Yosemite 或更新版本) 如果您想 toodevelop 適用於 iOS，則需要。 雖然我們 Windows toodevelop 上，使用 Visual Studio 搭配 Xamarin 及管理所有 hello 程式碼時，Xamarin 會使用訂單 toobuild 在 Mac 上安裝代理程式，而且登 hello iOS 程式碼。

![在 Windows 上開發及在 Mac 上建置](./media/iot-solution-build-system/image1.png)

（或者，您可以使用 Xamarin Studio 直接在 hello Mac toodevelop 跨平台應用程式上。）

如果您不想 tooinclude iOS 做為目標平台，您不需要 hello Mac。

安裝：

* [適用於 iOS 的 Xamarin Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/)。 您也可以在執行 Windows 虛擬機器的 Mac 上，設定 Visual Studio 和 Xamarin。 請參閱 MSDN 上的 [針對 Mac 使用者的設定、安裝和驗證](https://msdn.microsoft.com/library/mt488770.aspx) 。
* [Azure 開發工具](https://azure.microsoft.com/downloads/) (選擇性)。

啟用 hello mac 上的遠端登入 開啟 [系統偏好設定] > [共用]，然後選取 [遠端登入]。

當您在 Windows 上的 Visual Studio 中開啟 iOS 專案時，hello Xamarin 外掛程式會提示您輸入 hello 識別碼 hello mac。

## <a name="fetch-hello-github-repository"></a>擷取 hello GitHub 儲存機制
擷取的本機副本[hello GitHub MyDriving 儲存機制](https://github.com/Azure-Samples/MyDriving)使用 hello **Download ZIP** GitHub、 Visual Studio 中或另一個 Git 用戶端中的按鈕。

將具有較短的路徑名稱，例如 c: hello 檔案 tooa 資料夾解壓縮\\程式碼。

或者，如果您想要向上 toodate 與 tookeep 或 tooour 程式碼撰寫，複製 hello 儲存機制，如下所示：

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>取得 Bing 地圖 API 金鑰
[註冊 Bing 地圖 API 金鑰](https://msdn.microsoft.com/library/ff428642.aspx)。

您需要這在行中的 22 tooreplace `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`。

## <a name="build-hello-demo-app"></a>建置 hello 示範應用程式
在 Visual Studio 中開啟這些方案：

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

您會收到提示，要求您︰

* 信任一些潛在不受信任的專案。 選擇 tooopen 如果您想繼續 toogo 它們。
* 如果您在全新的 Windows 10 電腦上工作，請設定開發人員模式。
* 提供您的 Xamarin 認證。
* 連接 toohello Xamarin mac。 如果您沒有 Mac，以滑鼠右鍵按一下 hello iOS 專案在 Visual Studio，然後再選取**卸載專案**。

重建 hello 方案。

如果您無法建置，請嘗試我們找到的 hello 解決方案 tooquirks:

* *不會載入 VINLookupApplication 專案*： 確定您安裝 hello [Azure SDK for Visual Studio](https://www.visualstudio.com/vs/azure-tools/)。
* *Service Fabric 專案無法建置*： 建置 hello 介面的專案，並確定您已安裝的 hello Service Fabric SDK。
* Android 應用程式未建置︰
  
  * 開啟 [工具] > [Android] > [Android SDK Manager]，然後確定已安裝 Android 6 (API 23)/SDK 平台。
  * 刪除此目錄，然後重新建置︰<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>取得 tooknow hello 程式碼
您也可以在 hello 解決方案中，找到：

* Azure 擴充功能：Service Fabric。
* Azure HDInsight：用於處理 Azure 中行程資料的指令碼。
* 行動裝置應用程式： hello 裝置應用程式。
* MobileAppsService/MyDrivingService: hello web 回結束。
* Power BI: hello 報表定義。
* Scripts：
  
  * 資源管理員： 範本 toobuild hello Azure 資源。
  * PowerShell： 指令碼 toorun hello 資源管理員範本。
  * Azure SQL Database：資料庫偵錯。
* SQL Database：CreateTables：結構描述定義。
* Azure Stream Analytics： 查詢該轉換 hello 內送資料流。

## <a name="run-hello-apps-in-development-mode"></a>開發模式中執行 hello 應用程式
採取動作 toorun hello 應用程式，請根據您所使用的 hello 裝置：

* 後端： 集 MyDrivingService 為 hello 啟始專案，然後按 F5 toorun hello 後端 web 服務。 它會開啟一個瀏覽器的檢視 hello API 清單。
* 行動用戶端： hello[行動裝置應用程式會以 Xamarin 開發](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/)。
  
  * Android：如需詳細資訊，請參閱 [以 Xamarin 對 Android 進行偵錯](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/)。
  * iOS：如需詳細資訊，請參閱 [在 iOS 中偵錯](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/)。
  * Windows Phone：如需詳細資訊，請參閱 [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/)。

## <a name="upload-hello-mobile-app-toohockeyapp"></a>上傳 hello 行動裝置應用程式 tooHockeyApp
HockeyApp 管理 hello 散發 Android、 iOS 或 Windows 應用程式 tootest 使用者，通知使用者的新版本。 它也會收集實用的當機報告、含螢幕擷取畫面的使用者意見反應及使用計量。

[開始上傳](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) 您的組建應用程式。 然後，登入太[HockeyApp](https://rink.hockeyapp.net)從開發電腦。 在 hello 開發人員儀表板上按一下**新的應用程式**，然後將內建的 hello 檔案拖曳到 hello 視窗。 （更新版本中，您可以自動化您的組建服務 toodo 這。）

現在，移至您的應用程式儀表板。

![Hello 應用程式儀表板上的 [概觀] 索引標籤](./media/iot-solution-build-system/image2.png)

每個平台上執行您的應用程式中重複 hello 程序。 然後，您可以執行下列 hello:

* 使用 hello[應用程式識別碼](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id)從 hello 儀表板 toosend 損毀資料和應用程式的意見。 在 MyDriving，更新 src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs 中的 hello 識別碼。
* [邀請測試使用者](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers)。 取得 URL toorecruit 測試人員的使用者。 它們將無法註冊您的小組 toosign，下載 hello 應用程式，而傳送意見反應。
* 如果您希望多開啟的 beta 版，請設定 hello 發佈 toopublic。 按一下 [管理應用程式] > [散發] > [下載 = 公用]。 現在，所有人都可以下載您的應用程式並傳送意見反應給您，而且當您公佈新版本時，他們將會看到通知。 您可能也會從這些使用者收到一些當機報告。
  
   ![Hello 儀表板上的小組](./media/iot-solution-build-system/image3.png)
* [連結的損毀報告 tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs)。 按一下 [管理應用程式] > [Visual Studio Team Services]。 HockeyApp 可在有當機報告或收到意見反應時，自動在 Team Services 中建立工作項目。

讀取多在 hello [HockeyApp 網站](https://hockeyapp.net)。

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>測試 Xamarin Test Cloud hello 行動應用程式
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/)自動化 UI 測試在 hello 雲端中的實際裝置上。 藉由使用 hello NUnit 架構，您可以撰寫 hello 使用者介面中執行您的應用程式的測試。

toouse Xamarin，您將 hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/)至您應用程式以 NuGet 封裝的 SDK。 您可以在 hello 示範應用程式中找到它，它並包含當您建立新的測試專案與 hello Xamarin 範本。

![Toofind hello hello 介面上的跨平台 SDK 的位置](./media/iot-solution-build-system/image4.png)

範例測試專案會隨附 hello hello 儲存機制中的應用程式。 請在 [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService) 中的 [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/ 下尋找。

如果您使用 Visual Studio Team Services 建置時，很容易 toowrite Xamarin UI 單元測試，並以您的組建的一部分。

## <a name="deploy-azure-services"></a>部署 Azure 服務
tooperform 的自動部署 Azure 服務和服務小組的組建服務，請參閱 toohello 詳細指示，在**scripts/README.md**。

Microsoft Azure 提供許多不同的服務，您可以使用 toobuild 雲端應用程式。 雖然有許多可以使用個別 （例如應用程式 Web 服務/應用程式），但它們在其最佳時，它們互連 tooform 整合的系統這樣我們使用 MyDriving 中。

它是可能 toocreate 和互連 Azure 服務，以手動方式，但更快且較可靠，toouse Azure Resource Manager 範本。 [資源管理員](../azure-resource-manager/resource-group-overview.md)hello 部署方案的資源和使 hello connect 兩者之間會自動執行。

您會發現 hello 範本 hello MyDriving 系統下 hello GitHub 儲存機制中[指令碼/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM)。 它提供的完整和精簡檢視我們的架構中的 hello 不同服務的互連方式。 我們會說明所有這些詳細 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)，但您可以只要閱讀 hello 範本本身了很多。

> [!NOTE]
> 大部分的 Azure 服務具有相關聯的成本，視 hello 定價層而定。 如果您是新 tooAzure，您可以[免費試用](https://azure.microsoft.com/free/)。 不過，如果您不打算 toouse hello MyDriving 系統中的某些元件，是確定 tooremove 它們 tooavoid 產生成本。 hello"估計營運成本 」 一節稍後在這篇文章提供一般服務費用的摘要。
> 
> 

### <a name="edit-hello-template"></a>編輯 hello 範本
toocustomize、 以部署也許 tooremove 不必要的元件或 tooadd 其他人，首先請副本案例\_complete.params.json 和案例\_complete.json toomake 變更中的。

您可以使用 hello 案例\_complete.params.json 檔案 toooverride 各種不同的預設值，例如 hello 服務 SKU 或 hello 儲存體複寫類型，hello 下表中所述。 hello 預設值選取 hello 成本最低的選項。

| **參數** | **說明** | **預設值** |
| --- | --- | --- |
| IoT 中樞 SKU |Azure IoT 中樞服務層 |F1 |
| 儲存體帳戶類型 |儲存體複寫類型 |標準 LRS |
| SQL 服務目標 |並行存取插槽耗用量 |DW100 |
| 主控方案 SKU |App Service 的服務方案 |F1 |

在 scenario\_complete.json 中：

* 搜尋"baseName 」，並將它變更為您所偏好 tooa 名稱。
* 搜尋 "Create"。 這些區段會各自建立一個資源。
* 設定 sqlServerAdminLogin 和 sqlServerAdminPassword toosuitable 值。
* 刪除區段建立的資源之前，請搜尋其名稱 hello 檔案中的其他位置是否有相依性。 請注意，建立服務的每個區段都會包含列出其相依性的 *dependsOn* 區段。

這裡 hello 的範本設定。 詳細資料位於 hello[參考指南](http://aka.ms/mydrivingdocs)。

| **服務** | **說明和詳細資料** |
| --- | --- |
| 儲存體帳戶 |hello 範本會建立三個帳戶： |
| -Stream Analytics 中，從接收彙總的遙測，並做為 Azure App Service 的資料表，將此資料透過 API 端點公開的 hello 備份存放區 SQL 資料庫。 | |
| 會從另一個資料流分析工作，toobe HDInsight 處理的歷程記錄資料的 blob 儲存體。 | |
| -   接收經過 HDInsight 處理的結果以搭配 Power BI 使用的 SQL Database。 | |
| Azure IoT 中樞 |建立雙向連線 tooeach 連接的裝置。 在 hello MyDriving 方案，hello 行動裝置應用程式可作為欄位閘道 toosend 資料 tooAzure IoT 中樞。 Azure IoT 中樞然後可做為輸入的 tooStream 分析。 |
| Azure 事件中心 |佇列 hello 輸出 tooextensions 使用 Azure Service Fabric 建立的資料流分析工作輸出。 |
| Azure SQL 資料倉儲 | |
| 串流分析作業 |使用查詢，也就是使用的 tooaggregate 連接輸入和輸出 hello 應用程式服務 Api，Azure Machine Learning、 延伸模組，與 Power BI 的即時和歷史資料。 |
| 機器學習服務工作區 |包括實驗、R 程式碼和 API 服務。 |
| Azure Data Factory |排程的機器學習服務重新訓練。 |
| Service Fabric 主控方案 |適用於擴充功能。 |
| App Service (「行動應用程式」) |主機 hello hello 行動裝置應用程式提供端點的行動應用程式 API 專案。 hello API 程式碼必須是已部署的 tooApp 從 Visual Studio 服務。 |
| 警示規則 |傳送電子郵件寄送如果 hello 應用程式回應指出失敗。 |
| Application Insights |監視效能的 hello App Service 中的應用程式開發介面。 您在 Visual Studio 中有 tooconfigure hello 連線。 |
| Azure 金鑰保存庫 |用於儲存 hello web 服務叢集的憑證。 |

### <a name="run-hello-template"></a>執行 hello 範本
在**scripts/README.md**，還有執行 hello 範本的詳細的指示。

tooprovision 使用 hello 指令碼，您的 Azure 帳戶中的所有這些服務執行的 hello 下列其中一個動作：

* 使用 PowerShell：
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *位置*為 hello [Azure 位置](https://azure.microsoft.com/regions/)，例如`North Europe`或`West US`。 使用`Get-AzureLocation`toofind 可用位置清單。
  * *resourceGroupName*是 hello 您要讓所有 hello 資源將屬於 toogive toohello 群組的名稱。 當您完成與 hello 資源時，可以藉由刪除此群組一起刪除它們。
* 以 Bash 執行 DeploymentScripts/Bash/deploy.sh。
* 開啟和建置 hello DeploymentScripts/VS/DeployARM.sln 的 Visual Studio 方案。

請注意，執行每個階段 hello 範本時，它會以新名稱建立一組新的資源。 toodelete hello 資源移 toohello 入口網站，並刪除 hello 資源群組。

如果因為任何原因失敗 hello 指令碼，您可以重新執行。

hello 指令碼可讓您 hello 選項在 Visual Studio Team Services 中設定持續整合。 如果您已設定 Team Services 專案，則會有 URL：https://yourAccountName.visualstudio.com。當詢問您輸入 hello 完整 URL。 您可以為 Team Services 專案提供新的或現有的名稱。

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>在 Visual Studio Team Services 中設定組建和測試定義
在此專案上使用 Team Services 主要是為了其建置和測試功能。 不過，它也提供絕佳的共同作業支援，例如使用看板進行工作管理、與工作和原始檔控制整合的程式碼檢閱，以及閘道組建。 它與其他工具適當地整合，例如 GitHub、Xamarin、HockeyApp，當然還包括 Visual Studio。 您可以透過 hello web 介面，或透過 Visual Studio 存取它，以更方便在任何時刻。

hello 步驟在 hello 組建和發行定義中使用不同的 hello Team Services 中可用的外掛程式服務[Marketplace](https://marketplace.visualstudio.com/VSTS)。 在加法 toobasic 公用程式 toorun 命令列或複製檔案，有一些的服務所叫用組建，方式是 Xamarin、 Android 和其他廠商，但卻連線 tooHockeyApp。

![Team Services 中的建置選項](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>組建定義
我們有 hello 主要目標的每個組建定義。 而針對功能和迴歸測試有不同的版本。 這會提供：

* MyDriving.Services （hello 後端 web hello 行動裝置應用程式的應用程式）
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android - 功能
  * MyDriving.Xamarin.Android - 迴歸
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS - 功能
  * MyDriving.Xamarin.iOS - 迴歸
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP - 功能
  * MyDriving.Xamarin.UWP - 迴歸

如果您想 toosee hello 完整詳細資料的組態設定，請參閱區段 4.7 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)，< 建置和發行組態 >。 它們遵循下列 hello 相同的一般模式。 hello 指令碼：

1. 還原 hello NuGet 封裝。 我們不在 hello 儲存機制，保留編譯的程式碼，因此 hello 的每個組建的第一個步驟是 toorestore hello 所需的 NuGet 封裝。
2. 啟動 hello 授權。 會執行 hello 組建 hello 雲端，因此在我們需要授權-特別的是，hello Xamarin 建置服務--我們有 tooactivate 我們授權 hello 目前組建電腦上的。 然後，我們將其停用立即之後，tooallow 它 toobe 另一部電腦上使用。
3. 是使用 hello 適當的服務。 我們使用 Xamarin 建置 hello 行動裝置應用程式，而且 Visual Studio 會建置 hello 後端 web 服務。
4. 建置測試。
5. 執行測試。 我們在 Xamarin Test Cloud 執行 hello 行動裝置應用程式測試。
6. 發行 hello 組建結果 toohello 置放位置。

hello 主要組建 hello 觸發程序會設定 toocontinuous 整合。 也就是每次程式碼會檢查 toohello 主要分支中，是執行 hello 組建。

![介面 hello 觸發程序所在組 toocontinuous 整合](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>發行定義
發行定義中所設多 hello 相同的方式。

Hello web 服務，我們設定部署為 Azure web 應用程式：

![用於將部署設定為 Azure Web 應用程式的介面](./media/iot-solution-build-system/image7.png)

然後我們設定 hello 發行觸發程序 toocontinuous 部署。 也就是說，每個簽入後面接著更新 toohello web 應用程式中成功的組建結果。

![設定 hello 發行觸發程序 toocontinuous 部署的介面](./media/iot-solution-build-system/image8.png)

行動裝置應用程式，我們將部署 tooHockeyApp:

![部署行動裝置應用程式 tooHockeyApp 介面](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>使用 Application Insights 探索遙測
[Application Insights](../application-insights/app-insights-overview.md)會收集有關 hello 效能和您的 web 服務的使用方式的遙測。 hello Application Insights SDK 傳送遙測從 hello 服務 toohello 在 Azure 中的 Application Insights 資源。

瀏覽 toohello Application Insights 資源設定該 hello 範本。 您可以瀏覽的 hello 效能圖表您[行動應用程式服務專案](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService)。 這些圖表會顯示伺服器要求和回應時間、失敗和例外狀況計數。 也有相依性回應時間-也就是呼叫 toohello 資料庫和 tooREST 應用程式開發介面，例如機器學習的圖表。 如果沒有任何效能問題，您將必須能夠 toosee 系統的哪些部分會造成它們。

![效能圖表範例](./media/iot-solution-build-system/image11.png)

如果您有 web 服務以手動方式設定時，它的簡單 tooget hello 相同的圖表。 在 hello web 服務刀鋒視窗中，按一下 **工具** > **延伸** > **新增**。 選取 [Application Insights] 。

![選取 Application Insights tooget hello 圖表介面](./media/iot-solution-build-system/image12.png)

hello 功能的運作方式檢測應用程式以 hello Application Insights SDK。

您可以新增自訂遙測 （或樂器某處 Azure 外部執行的應用程式）[加入 hello Application Insights SDK](../application-insights/app-insights-asp-net.md)在開發階段。 這是相依於 hello 應用程式，例如使用者的平均路線長度或總里程數有用 toolog 度量。 在 Visual Studio 中，hello 專案上按一下滑鼠右鍵，然後選取**加入 Application Insights**。

![選取 加入 Application Insights tooadd 自訂遙測介面](./media/iot-solution-build-system/image10.png)

如果 Application Insights 發現不尋常的失敗回應數目，就會傳送警示電子郵件。 您也可以針對各種計量 (例如回應時間) 設定自己的警示。

確認您的 web 服務永遠是最新，並執行，您可以設定只是 toobe[可用性測試](../application-insights/app-insights-monitor-web-app-availability.md)。 這些測試會偵測您從 hello 世界各地的不同位置的網站每隔 15 分鐘。 同樣地，如果您會得到一封電子郵件似乎那里 toobe 問題。

## <a name="estimate-operational-costs"></a>估計作業成本
它是非常便宜 toorun 這類在小規模的應用程式。 許多 hello 服務都有免費的入門級層，以便開發和小規模的作業成本很少。 而且當然您自己的應用程式沒有的 toouse MyDriving 中示範的 hello 的所有功能。

以下是我們在將 MyDriving 的 hello 開發組態設定成本的概略估計。 我們也指出一些「未」  用到的替代方案。 當您估計自己的成本時，這項資訊可能很有用。

我們假設︰

* 一個不到 5 人 (加上觀察專案關係人) 的小組。
* 執行約一個月。
* 100 位使用者，每天 4 趟行程。

> [!NOTE]
> 如果您是新的 tooAzure 沒有[免費帳戶](https://azure.microsoft.com/free/)。
> 
> 

| **服務/元件** | **注意事項** | **每月成本** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) 與 [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>跨平台開發環境 |Visual Studio Community。 (需要[Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions)如[Xamarin.Forms](https://xamarin.com/forms)，toodesign 跨平台從單一程式碼基底。) |美金 $0 元 |
| [Azure IoT 中心](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>雙向的資料連接 toodevices |8,000 則訊息 + 每則訊息 0.5 KB 免費。 |美金 $0 元 |
| [串流分析](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   大量串流資料處理 |啟用時，每小時每個串流單位收取美金 $0.031 元。 您選擇 hello; 的資料流單位數目設定多個 tooscale。 |美金 $23 元 |
| [機器學習服務](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> 自適性回應 |每月每個基座美金 $10 元。 <br/>                                                                                                                                                                                 + 3 小時實驗 \* 美金 $1 元 / 實驗小時。 <br/>                                                                                                                                                           + 3.5 小時 API CPU \* 美金 $2 元 / 生產 CPU 小時。 <br/>                                                                                                                                                          API CPU 時間假設每天重新訓練 5 分鐘，不過這會隨輸入資料愈多而增加。                   <br/>                                                                                                                                                                     + 計分 tooprocess 400 往返/日 2 分鐘/日。 |美金 $20 元 |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> 裝載行動後端 |B1 層--生產環境 Web 應用程式。 |美金 $56 元 |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> 組建、單元測試和發行管理；工作管理 |私人 Agent，5 位使用者。 |美金 $0 元 |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>監視 Web 服務和網站的效能和使用狀況 |免費層。 |美金 $0 元 |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> 散發 Beta 版應用程式，以及收集意見反應、使用狀況和當機資料 |新使用者有兩個免費的應用程式。<br/> 之後每月美金 $30 元。 |美金 $0 元 |
| [Xamarin](https://store.xamarin.com/)<br/> 多部裝置之統一平台上的程式碼 |免費試用版。 <br/>之後每月美金 $25 元。 |美金 $0 元 |
| [SQL Database](https://azure.microsoft.com/pricing/details/sql-database/)  |基本層；單一資料庫模型。 |美金 $5 元 |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (選擇性) |執行本機叢集。 |美金 $0 元 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> 對串流處理的靜態資料進行多元顯示及調查 |免費層：1GB，每小時 10,000 列，每天重新整理。 <br/> 針對 [更高限制](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/)、更多連接選項和共同作業，則為每月每位使用者美金 $10 元。 |美金 $0 元 |
| [儲存體](https://azure.microsoft.com/pricing/details/storage/) |L (本機備援) &lt; 100 G 美金 $0.024 元/GB。 |美金 $3 元 |
| [Data Factory](https://azure.microsoft.com/pricing/details/data-factory/) |每個活動美金 $0.60 元 \* (8 - 5 FOC)。 |美金 $2 元 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  用於每日重新訓練的隨選叢集 |3 個 A3 節點，每天 1 小時每小時美金 $0.32 元 * 31 天。 |美金 $30 元 |
| [事件中樞](https://azure.microsoft.com/pricing/details/event-hubs/) |基本為每月輸送量單位美金 $11 元 + 美金 $0.028 元的輸入。 |美金 $11 元 |
| OBD 硬體鎖 | |美金 $12 元 |
| **總計** | |**美金 $157 元** |

如需詳細資訊，請參閱：

* [Azure 服務配額與限制](../azure-subscription-service-limits.md#iot-hub-limits)
* [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>將您的意見反應傳給我們
因為我們建立 MyDriving toohelp 開始使用您自己的 IoT 系統時，我們可以確定您需要 toohear 您有關它的運作方式。 若發生下列情況，請告訴我們：

* 您遇到問題或挑戰。
* 沒有擴充點，會讓它更適合 tooyour 案例。
* 您尋找更有效率的方式 tooaccomplish 特定需求。
* 您有改善 MyDriving 或這份文件的任何其他建議。

toogive 意見反應，檔案的 [問題 GitHub 上] 或保留下列註解 (en-us-我們 edition)。

我們期待 toohearing 您 ！

## <a name="next-steps"></a>後續步驟
我們建議 hello [MyDriving 參考指南](http://aka.ms/mydrivingdocs)，這是 hello 設計 hello 系統和其元件的完整說明。

