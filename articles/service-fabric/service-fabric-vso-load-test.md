---
title: "aaaLoad 測試您的應用程式使用 Visual Studio Team Services |Microsoft 文件"
description: "了解 toostress 如何使用 Visual Studio Team Services 測試 Azure Service Fabric 應用程式。"
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>使用 Visual Studio Team Services 對您的應用程式執行負載測試
本文將說明如何 toouse Microsoft Visual Studio 負載測試功能 toostress 測試應用程式。 它會使用 Azure Service Fabric 具狀態服務後端和無狀態服務 Web 前端。 hello 這裡使用的範例應用程式是飛機位置模擬器。 您提供飛機識別碼、起飛時間和目的地。 hello 應用程式的後端處理 hello 要求，並對應 hello 正在飛機符合 hello 準則顯示 hello 前端。

hello 下列圖表說明您在測試的 hello Service Fabric 應用程式。

![Hello 範例飛機位置應用程式的圖表][0]

## <a name="prerequisites"></a>必要條件
之前開始，您必須 toodo hello 下列：

* 取得 Visual Studio Team Services 帳戶。 您可以在 [Visual Studio Team Services](https://www.visualstudio.com)取得一個免費帳戶。
* 取得並安裝 Visual Studio 2013 或 Visual Studio 2015。 本文使用 Visual Studio 2015 Enterprise 版本，但是 Visual Studio 2013 和其他版本應該也同樣可以運作。
* 部署您的應用程式 tooa 預備環境。 請參閱[toodeploy 應用程式 tooa 遠端叢集使用 Visual Studio](service-fabric-publish-app-remote-cluster.md)如需詳細資訊。
* 了解您的應用程式的使用模式。 這項資訊是使用的 toosimulate hello 負載模式。
* 了解 hello 進行負載測試的目標。 這可協助您解譯及分析 hello 負載測試結果。

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>建立及執行 hello Web 效能和負載測試專案
### <a name="create-a-web-performance-and-load-test-project"></a>建立 Web 效能和負載測試專案
1. 開啟 Visual Studio 2015。 選擇**檔案** > **新增** > **專案**功能表列 tooopen hello hello**新專案** 對話方塊。
2. 展開 hello **Visual C#**節點，然後選擇 **測試** > **Web 效能和負載測試專案**。 指定 hello 專案的名稱，然後選擇 [hello**確定**] 按鈕。

    ![Hello 新增專案 對話方塊的螢幕擷取畫面][1]

    您應該會在 [方案總管] 中看到新的 Web 效能和負載測試專案。

    ![顯示 hello 新專案的方案總管的螢幕擷取畫面][2]

### <a name="record-a-web-performance-test"></a>記錄 Web 效能測試
1. 開啟 hello.webtest 專案。
2. 選擇 hello**加入錄製**圖示 toostart 瀏覽器中的錄製工作階段。

    ![在瀏覽器中的 hello 加入錄製圖示的螢幕擷取畫面][3]

    ![在瀏覽器中的 hello Record 按鈕的螢幕擷取畫面][4]
3. 瀏覽 toohello Service Fabric 應用程式。 hello 錄製面板應該會顯示 hello web 要求。

    ![Hello 錄製面板中的 web 要求的螢幕擷取畫面][5]
4. 執行一系列您預期 hello 使用者 tooperform 的動作。 這些動作會使用模式 toogenerate hello 負載。
5. 當您完成時，選擇 hello**停止**按鈕 toostop 錄製。

    ![Hello [停止] 按鈕的螢幕擷取畫面][6]

    Visual Studio 中的 hello.webtest 專案應該有擷取的一系列的要求。 會自動取代動態參數。 此時，您可以刪除不屬於您的測試案例的任何額外、重複相依性要求。
6. 儲存 hello 專案，然後選擇 hello**執行測試**命令 toorun hello web 效能測試在本機，並確定一切運作正常。

    ![Hello 執行測試命令的螢幕擷取畫面][7]

### <a name="parameterize-hello-web-performance-test"></a>參數化 hello web 效能測試
您可以將它轉換 tooa 自動程式化 web 效能測試，然後編輯 hello 程式碼來參數化 hello web 效能測試。 或者，您可以繫結 hello web 效能測試 tooa 資料清單以便 hello 測試逐一 hello 資料。 請參閱[產生和執行自動程式化的 web 效能測試](https://msdn.microsoft.com/library/ms182552.aspx)如需如何 tooconvert hello web 效能測試 tooa 自動程式化測試詳細資料。 請參閱[加入資料來源 tooa web 效能測試](https://msdn.microsoft.com/library/ms243142.aspx)如需如何 toobind 資料 tooa web 效能測試。

針對此範例中，我們將轉換 hello web 效能測試 tooa 自動程式化測試，讓您可以將 hello 飛機識別碼取代產生的 GUID，並加入更多要求 toosend 班機 toodifferent 位置。

### <a name="create-a-load-test-project"></a>建立負載測試專案
負載測試專案所組成 hello web 效能測試和單元測試，以及其他指定的負載測試設定所描述的一或多個案例。 hello 下列步驟顯示如何 toocreate 負載測試專案：

1. Hello Web 效能和負載測試專案的捷徑功能表，選擇 **新增** > **負載測試**。 在 [hello**負載測試**精靈] 中，選擇 hello**下一步**按鈕 tooconfigure hello 測試設定。
2. 在 hello**負載模式**區段中，選擇是否要讓常數的使用者負載或逐步執行負載，就會開始與少數使用者以及增加 hello 使用者一段時間。

    如果您有良好的估計量 hello 使用者負載，並想的 toosee hello 目前系統的執行方式，選擇**常數載入**。 如果您的目標 toolearn 是否 hello 系統就會在各種負載一致的方式執行，請選擇**逐步執行負載**。
3. 在 hello**測試混合**區段中，選擇 hello**新增**按鈕，然後選取 hello 測試您想 tooinclude hello 負載測試中的。 您可以使用 hello**發佈**資料行 toospecify hello 執行每一項測試的測試總數百分比。
4. 在 hello**回合設定**區段中，指定 hello 負載測試持續期間。

   > [!NOTE]
   > hello**測試反覆項目**選項才可以使用只有當您執行負載測試使用 Visual Studio 在本機。
   >
   >
5. 在 hello**位置**區段**回合設定**，指定產生負載測試要求 hello 位置。 hello 精靈可能會提示您 toolog tooyour Team Services 帳戶中。 登入，然後選擇一個地理位置。 當您完成時，選擇 hello**完成** 按鈕。
6. 建立 hello 負載測試之後，開啟 hello.loadtest 專案，然後選擇 執行設定，例如 hello 目前**回合設定** > **回合設定 1 [Active]**。 這會開啟 hello hello 執行設定**屬性**視窗。
7. 在 [hello**結果**hello 區段**回合設定**屬性] 視窗、 hello**計時詳細資料儲存區**設定應該有**無**做為預設值。 變更此值太**所有個別細節**tooget hello 負載測試結果的詳細資訊。 請參閱[載入測試](https://www.visualstudio.com/load-testing.aspx)如需有關如何 tooconnect tooVisual Studio Team Services 和執行負載測試。

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>使用 Visual Studio Team Services 執行 hello 負載測試
選擇 hello**執行負載測試**命令 toostart hello 測試回合。

![Hello 執行負載測試命令的螢幕擷取畫面][8]

## <a name="view-and-analyze-hello-load-test-results"></a>檢視及分析 hello 負載測試結果
Hello 為負載測試進行時，圖表化 hello 效能資訊。 您應該會看到類似 toohello 下列圖形。

![負載測試結果的效能圖表的螢幕擷取畫面][9]

1. 選擇 hello**下載報表**hello hello 頁面頂端附近的連結。 下載 hello 報表之後，選擇 hello**檢視報表** 按鈕。

    在 [hello**圖形**] 索引標籤，您可以查看各種效能計數器的圖形。 在 hello**摘要**索引標籤上，hello 整體測試結果會出現。 hello**資料表**索引標籤會顯示成功和失敗的負載測試的 hello 總數。
2. 選擇在 hello hello 連結**測試** > **失敗**和 hello**錯誤** > **計數**資料行toosee 錯誤詳細資料。

    hello**詳細**索引標籤會顯示失敗的要求的虛擬使用者和測試案例資訊。 此資料非常適合如果 hello 負載測試包含多個案例。

請參閱[分析負載測試結果 hello hello 負載測試分析器的圖形檢視中](https://www.visualstudio.com/load-testing.aspx)如需有關檢視負載測試結果。

## <a name="automate-your-load-test"></a>自動化您的負載測試
Visual Studio Team Services 負載測試提供 Api toohelp 您管理負載測試和分析 Team Services 帳戶中的結果。 如需詳細資訊，請參閱 [雲端負載測試 Rest API](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 。

## <a name="next-steps"></a>後續步驟
* [監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
