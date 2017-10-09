---
title: "開始使用 aaaGet 預先設定的解決方案 |Microsoft 文件"
description: "請遵循此教學課程 toolearn toodeploy Azure IoT 套件預先方案的設定。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>開始使用預先設定的 hello 解決方案

Azure IoT 套件[預先設定的解決方案][ lnk-preconfigured-solutions]結合多個 Azure IoT 服務 toodeliver 端對端方案實作常見的 IoT 商務案例。 hello*遠端監視*預先設定的方案連接 tooand 監視您的裝置。 您可以藉由自動回應 toothat 的資料流的處理序使用 hello 方案 tooanalyze hello 資料資料流，從您的裝置和 tooimprove 業務的結果。

本教學課程會示範如何 tooprovision hello 遠端監視預先設定的解決方案。 它也會引導您透過預先設定的 hello 解決方案的 hello 基本功能。 您可以存取這些功能從 hello 方案*儀表板*部署預先設定的 hello 方案的一部分：

![遠端監視預先設定解決方案儀表板][img-dashboard]

toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。

> [!NOTE]
> 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>案例概觀

當您部署的 hello 遠端監視預先設定的解決方案時，它會預先填入資源，可讓您 toostep 透過常見的遠端監視案例。 在此案例中，數個裝置連線的 toohello 方案報告未預期的溫度值。 hello 下列各節說明您如何以：

* 識別 hello 裝置傳送未預期的溫度值。
* 設定這些裝置 toosend 更多詳細的遙測。
* 透過更新這些裝置上的 hello 韌體中修正 hello 問題。
* 請確認您的動作已解析 hello 問題。

此案例中的主要功能是可以執行所有這些動作從 hello 方案儀表板的遠端。 您不需要實際存取 toohello 裝置。

## <a name="view-hello-solution-dashboard"></a>檢視 hello 方案儀表板

hello 方案儀表板可讓您 toomanage hello 部署方案。 例如，您可以檢視遙測、新增裝置及設定規則。

1. 當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 遠端監視方案入口網站中的新索引標籤。

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. 根據預設，hello 方案入口網站會顯示 hello*儀表板*。 您可以瀏覽 tooother hello 方案入口網站左側 hello hello 頁面使用 hello 功能表區域。

    ![遠端監視預先設定解決方案儀表板][img-menu]

hello 儀表板會顯示下列資訊的 hello:

* 顯示每個裝置 hello 位置的地圖，連接 toohello 方案。 當您第一次執行 hello 方案時，有 25 個模擬的裝置。 hello 模擬的裝置都會實作為 Azure WebJobs 而且 hello 解決方案使用 hello Bing Maps API tooplot 資訊 hello 地圖上。 請參閱 hello[常見問題集][ lnk-faq] toolearn toomake hello 對應動態的方式。
* [遙測歷程記錄] 面板會從所選的裝置繪製近乎即時的溼度和溫度遙測，並顯示彙總資料，例如最大、最小和平均溼度。
* [警示歷程記錄] 面板會在遙測值超過臨界值時顯示最近的警示事件。 建立預先設定的 hello 解決方案加法 toohello 範例中，您可以定義您自己的警示。
* [作業] 面板顯示已排程作業的相關資訊。 您可以在 [管理作業] 頁面排程您自己的作業。

## <a name="view-alarms"></a>檢視警示

hello 警示歷程記錄面板會顯示五個裝置會比預期的遙測值更高的報告。

![Hello 方案儀表板上的 TODO 警示歷程記錄][img-alarms]

> [!NOTE]
> 包含在預先設定的 hello 方案中的規則會產生這些警示。 當裝置傳送嗨溫度值超過 60 時，此規則會產生警示。 您可以選擇定義您自己的規則和動作[規則](#add-a-rule)和[動作](#add-an-action)hello 左側功能表中。

## <a name="view-devices"></a>檢視裝置

hello*裝置*清單會顯示所有已註冊的 hello 裝置 hello 方案中。 Hello 裝置清單中，您可以檢視和編輯裝置中繼資料、 新增或移除裝置，並叫用在裝置上的方法。 您可以篩選和排序 hello hello 裝置清單中的裝置清單。 您也可以自訂 hello hello 裝置清單中顯示的資料行。

1. 選擇**裝置**tooshow hello 裝置清單，此解決方案。

   ![Hello 方案入口網站中檢視 hello 裝置清單][img-devicelist]

1. hello 裝置清單一開始會顯示 hello 佈建程序所建立的 25 個模擬的裝置。 您可以加入其他的虛擬和實體裝置 toohello 方案。

1. tooview hello 詳細資料的裝置 hello 裝置清單中選擇裝置。

   ![Hello 方案入口網站中檢視 hello 裝置詳細資料][img-devicedetails]

hello**裝置詳細資料**面板包含六個區段：

* 啟用您 toocustomize hello 裝置圖示、 停用裝置 hello、 加入規則，叫用方法，或傳送命令的連結集合。 如需命令 (裝置對雲端的訊息) 和方法 (直接方法) 的比較，請參閱[雲端對裝置的通訊指引][lnk-c2d-guidance]。
* hello**裝置兩個-標記**區段可讓您的裝置 hello tooedit 標記值。 您可以在 hello 裝置清單中顯示標記值，並使用標記值 toofilter hello 裝置清單。
* hello**裝置兩個-需要屬性**區段可讓您 tooset 屬性值傳送 toobe toohello 裝置。
* hello**裝置兩個-報告屬性**區段會顯示傳送嗨裝置的屬性值。
* hello**裝置屬性**> 一節顯示的資訊，例如 hello 裝置 hello 身分識別登錄從金鑰識別碼和驗證金鑰。
* hello**最近工作**區段會顯示最近鎖定此裝置的任何工作的相關資訊。

## <a name="filter-hello-device-list"></a>篩選器 hello 裝置清單

您可以使用篩選器 toodisplay 只有傳送未預期的溫度值的裝置。 hello 遠端監視預先設定的解決方案包括 hello**狀況不良的裝置**篩選 tooshow 裝置平均的溫度值大於 60。 您也可以[建立自己的篩選](#add-a-filter)。

1. 選擇**開啟已儲存的篩選器**toodisplay 可用的篩選器的清單。 然後選擇 **狀況不良的裝置**tooapply hello 篩選：

    ![顯示 hello 篩選清單][img-unhealthy-filter]

1. hello 裝置清單現在會顯示只有裝置平均的溫度值大於 60。

    ![檢視 hello 篩選過的裝置清單，顯示處於狀況不良的裝置][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>更新所需屬性

您現在已識別一組裝置，可能需要修復。 不過，您可以決定 hello 資料頻率為 15 秒是不夠的清除 hello 問題的診斷。 您有多個資料點 toobetter 變更 hello 遙測頻率 toofive 秒 tooprovide 診斷 hello 問題。 您可以將這個組態變更 tooyour 遠端裝置從 hello 方案入口網站。 您可以進行 hello 變更一次，評估 hello 影響，並接著處理 hello 結果。

請遵循這些步驟 toorun 變更 hello 作業**TelemetryInterval**預期 hello 受影響裝置的屬性。 當 hello 裝置收到 hello 新**TelemetryInterval**屬性值，變更其組態 toosend 遙測每隔五秒而不是每隔 15 秒：

1. 雖然您會在 hello 裝置清單中顯示的狀況不良的裝置 hello 清單，選擇 **作業排程器**，然後**編輯裝置兩個**。

1. 呼叫 hello 作業**變更遙測間隔**。

1. 變更 hello hello 值**所需的屬性**名稱**所需。Config.TelemetryInterval** toofive 秒。

1. 選擇 [排程]。

    ![變更 hello TelemetryInterval 屬性 toofive 秒][img-change-interval]

1. 您可以監視 hello 作業上 hello hello 進度**管理作業**hello 入口網站頁面中的。

> [!NOTE]
> 如果您想要個別裝置 toochange 所需的屬性值，使用 hello**所需的屬性**> 一節中 hello**裝置詳細資料**面板而不是執行作業。

這項作業設定 hello hello 值**TelemetryInterval**預期在 hello 裝置兩個屬性的所有 hello hello 篩選所選取的裝置。 hello 裝置從 hello 裝置兩個擷取這個值，並更新其行為。 當裝置擷取，並處理從裝置的兩個所需的屬性時，它會設定 hello 對應回報的值屬性。

## <a name="invoke-methods"></a>叫用方法

Hello 工作執行時，您會注意到在 hello 狀況不良的裝置清單中所有這些裝置具有舊 （早於 1.6 版） 韌體版本。

![檢視 hello 回報 hello 狀況不良的裝置的韌體版本][img-old-firmware]

此韌體版本可能會非預期的 hello hello 根本原因的溫度值，因為您知道其他狀況良好的裝置已最近更新的 tooversion 2.0。 您可以使用內建的 hello**舊的韌體裝置**篩選 tooidentify 舊的韌體版本與任何裝置。 從 hello 入口網站，然後您可以從遠端更新所有 hello 裝置仍在執行舊的韌體版本：

1. 選擇**開啟已儲存的篩選器**toodisplay 可用的篩選器的清單。 然後選擇 **舊的韌體裝置**tooapply hello 篩選：

    ![顯示 hello 篩選清單][img-old-filter]

1. hello 裝置清單現在會顯示只使用舊的韌體版本的裝置。 這份清單包括 hello 五個裝置由 hello**狀況不良的裝置**篩選器和三個額外的裝置：

    ![檢視 hello 篩選過的裝置清單，顯示舊的裝置][img-filtered-old-list]

1. 選擇 [作業排程器]，然後選擇 [叫用方法]。

1. 設定**工作名稱**太**韌體更新 tooversion 2.0**。

1. 選擇**InitiateFirmwareUpdate**為 hello**方法**。

1. 設定 hello **FwPackageUri**參數太**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**。

1. 選擇 [排程]。 hello 作業 toorun 現在 hello 預設值為。

    ![建立工作 tooupdate hello 韌體的 hello 選取裝置][img-method-update]

> [!NOTE]
> 如果您想 tooinvoke 個別的裝置上的方法，請選擇**方法**在 hello**裝置詳細資料**面板而不是執行作業。

這項作業會叫用 hello **InitiateFirmwareUpdate**直接 hello 篩選所選取的所有 hello 裝置上的方法。 裝置立即回應 tooIoT 集線器，然後以非同步方式啟動 hello 韌體更新程序。 hello 下列螢幕擷取畫面所示，hello 裝置會提供有關 hello 韌體更新程序，透過報告的屬性值，狀態資訊。 選擇 hello**重新整理**hello 裝置和工作清單中的圖示 tooupdate hello 資訊：

![工作清單會顯示 hello 韌體更新清單執行][img-update-1]
![顯示韌體更新狀態的裝置清單][img-update-2]
![工作清單顯示 hello 韌體更新清單完成][img-update-3]

> [!NOTE]
> 在實際執行環境中，您可以排程工作 toorun 指定的維護期間。

## <a name="scenario-review"></a>案例檢閱

在此案例中，您可以識別潛在問題某些遠端裝置上 hello 儀表板和篩選器使用 hello 警示歷程記錄。 您接著使用的 hello 篩選器和作業 tooremotely 設定 hello 裝置 tooprovide 詳細的資訊 toohelp 診斷 hello 問題。 最後，您可以在 hello 受影響裝置上使用篩選器和作業 tooschedule 維護。 如果您傳回 toohello 儀表板，您可以檢查，不再有任何來自您方案中的裝置的警示。 您可以使用篩選 hello 韌體的 tooverify 最新的方案中的所有 hello 裝置，且沒有其他的狀況不良的裝置：

![篩選會顯示所有裝置具有最新版本的韌體][img-updated]

![篩選會顯示所有裝置狀況良好][img-healthy]

## <a name="other-features"></a>其他功能

hello 下列章節說明一些其他功能的 hello 遠端監視預先設定的解決方案未描述 hello 前一個案例的一部分。

### <a name="customize-columns"></a>自訂資料行

您可以自訂顯示 hello 裝置清單中選擇的 hello 資訊**資料行編輯器**。 資料行顯示回報屬性和標籤值，您可以新增和移除這些資料行。 您也可以重新排列及重新命名資料行︰

   ![資料行編輯器 ionic hello 裝置清單][img-columneditor]

### <a name="customize-hello-device-icon"></a>自訂 hello 裝置圖示

您可以自訂顯示 hello hello 裝置清單中的 hello 裝置圖示**裝置詳細資料** 面板，如下所示：

1. 選擇 hello 鉛筆圖示 tooopen hello**編輯映像**面板裝置：

   ![開啟裝置影像編輯器][img-startimageedit]

1. 上傳新的映像，或使用其中一種 hello 現有的映像，然後選擇**儲存**:

   ![編輯裝置影像編輯器][img-imageedit]

1. hello 影像選取現在會顯示 hello**圖示**hello 裝置的資料行。

> [!NOTE]
> hello 映像會儲存在 blob 儲存體。 在 hello 裝置兩個標記包含連結 toohello 映像 blob 儲存體中。

### <a name="add-a-device"></a>新增裝置

當您部署預先設定的 hello 方案時，您會自動佈建 25 個您可以在 hello 裝置清單中看到的範例裝置。 這些裝置是在 Azure WebJob 中執行的 *模擬裝置* 。 模擬的裝置輕易地為您 tooexperiment 未 hello 需要 toodeploy 真正的實體裝置 hello 預先設定的解決方案。 如果您想 tooconnect 實際裝置 toohello 方案，請參閱 hello[連接您的裝置 toohello 遠端監視預先設定的解決方案][ lnk-connect-rm]教學課程。

hello 下列步驟說明如何 tooadd 模擬的裝置 toohello 方案：

1. 瀏覽後 toohello 裝置清單。

1. tooadd 是裝置，請選擇**+ 新增裝置**hello 左下角中。

   ![新增裝置 toohello 預先設定的解決方案][img-adddevice]

1. 選擇**加入新**上 hello**模擬裝置**磚。

   ![在儀表板中設定新的裝置詳細資料][img-addnew]

   在加法 toocreating 新模擬的裝置，您也可以將實體裝置如果您選擇 toocreate**自訂裝置**。 toolearn 進一步了解連接的實體裝置 toohello 解決方案，請參閱[連接您的裝置 toohello IoT 套件遠端監視預先設定的解決方案][lnk-connect-rm]。

1. 選取 [自行定義裝置識別碼]，然後輸入唯一的裝置識別碼名稱，例如 **mydevice_01**。

1. 選擇 [建立] 。

   ![儲存新的裝置][img-definedevice]

1. 在步驟 3 的**新增模擬的裝置**，選擇**完成**tooreturn toohello 裝置清單。

1. 您可以檢視您的裝置**執行**hello 裝置清單中。

    ![檢視裝置清單中的新裝置][img-runningnew]

1. 您也可以檢視 hello 模擬從新裝置 hello 儀表板上的遙測：

    ![從新裝置檢視遙測][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>停用並刪除裝置

您可以停用裝置，並且在已停用之後移除：

![停用並移除裝置][img-disable]

### <a name="add-a-rule"></a>新增規則

沒有您剛才加入 hello 新裝置的規則。 在本節中，您可以將 hello 溫度回報 hello 新裝置超過 47 度時，會觸發警示的規則。 開始之前，請注意，hello hello 儀表板上新的裝置 hello 遙測記錄顯示 hello 裝置溫度絕不會超出 45 度。

1. 瀏覽後 toohello 裝置清單。

1. tooadd 規則 hello 裝置，請選取您新的裝置中 hello**裝置清單**，然後選擇 **加入規則**。

1. 建立規則，其使用**溫度**hello 資料欄位，並使用為**AlarmTemp** hello 輸出 hello 溫度超出 47 度時：

    ![新增裝置規則][img-adddevicerule]

1. 您的變更，選擇 toosave**儲存和檢視規則**。

1. 選擇**命令**hello 新裝置 hello 裝置詳細資料窗格中。

    ![新增裝置規則][img-adddevicerule2]

1. 選取**ChangeSetPointTemp** hello 命令清單和組**SetPointTemp** too45。 然後選擇 [傳送命令]：

    ![新增裝置規則][img-adddevicerule3]

1. 瀏覽後 toohello 儀表板。 在一段時間之後, 您會看到新的項目在 hello**警示歷程記錄**窗格 hello 溫度回報您的新裝置時超過 hello 47 度臨界值：

    ![新增裝置規則][img-adddevicerule4]

1. 您可以檢閱和編輯您的所有規則上 hello**規則**hello 儀表板頁面：

    ![列出裝置規則][img-rules]

1. 您可以檢閱和編輯所有可以採取上 hello 回應 tooa 規則中的 hello 動作**動作**hello 儀表板頁面：

    ![列出裝置動作][img-actions]

> [!NOTE]
> 它是可能 toodefine 動作可以傳送電子郵件訊息，或在回應 tooa SMS 規則，或與某個特定業務系統進行整合[邏輯應用程式][lnk-logic-apps]。 如需詳細資訊，請參閱 hello[連接邏輯應用程式的 Azure IoT 套件遠端監視的 tooyour 預先設定的解決方案][lnk-logicapptutorial]。

### <a name="manage-filters"></a>管理篩選

在 hello 裝置清單中，您可以建立、 儲存及重新載入篩選器 toodisplay 自訂的裝置連線的 tooyour 中樞清單。 toocreate 篩選：

1. 選擇的裝置 hello 清單上方的 hello 編輯篩選器圖示：

    ![Hello 開啟篩選編輯器][img-editfiltericon]

1. 在 hello**篩選編輯器**，新增 hello 欄位、 運算子和值 toofilter hello 裝置清單。 您可以加入多個子句 toorefine 篩選器。 選擇**篩選**tooapply hello 篩選：

    ![建立篩選][img-filtereditor]

1. 此範例中，依製造商和型號的篩選 hello 清單：

    ![篩選的清單][img-filterelist]

1. toosave 您的篩選器，以自訂的名稱，選擇 hello**存**圖示：

    ![新增篩選][img-savefilter]

1. tooreapply 您先前儲存的篩選器選擇 hello**開啟已儲存的篩選器**圖示：

    ![開啟篩選][img-openfilter]

您可以根據裝置識別碼、裝置狀態、所需屬性、回報屬性和標籤，以建立篩選。 您可以新增您自己的自訂標籤 tooa 裝置在 hello**標記**hello 區段**裝置詳細資料**面板，或在多個裝置上執行作業 tooupdate 標記。

> [!NOTE]
> 在 hello**篩選編輯器**，您可以使用 hello**進階檢視**tooedit hello 查詢文字直接。

### <a name="commands"></a>命令

從 hello**裝置詳細資料**面板中，您可以傳送命令 toohello 裝置。 在裝置第一次啟動時，它會傳送 hello 的相關資訊的命令支援 toohello 方案。 如需命令和方法的 hello 差異的討論，請參閱[Azure IoT 中樞雲端到裝置選項][lnk-c2d-guidance]。

1. 選擇**命令**在 hello**裝置詳細資料**hello 選裝置的面板：

   ![儀表板中的裝置命令][img-devicecommands]

1. 選取**PingDevice**從 hello 命令清單。

1. 選擇 [傳送命令]。

1. 您可以看到 hello hello 命令歷程記錄中的 hello 命令狀態。

   ![儀表板中的命令狀態][img-pingcommand]

hello 方案追蹤每個命令時會傳送 hello 狀態。 一開始是 hello 結果**暫止**。 Hello 結果時 hello 裝置回報它已執行 hello 命令，設定得**成功**。

## <a name="behind-hello-scenes"></a>Hello 幕後

當您部署預先設定的解決方案時，hello 部署程序會在 hello 您選取的 Azure 訂用帳戶中建立多個資源。 您可以檢視這些資源中 hello Azure[入口網站][lnk-portal]。 hello 部署程序會建立**資源群組**根據您選擇您預先設定的解決方案 hello 名稱的名稱：

![Hello Azure 入口網站中預先設定的解決方案][img-portal]

您可以檢視每個資源的 hello 設定 hello 資源群組中的 hello 清單中選取。

您也可以檢視預先設定的 hello 方案 hello 原始程式碼。 遠端監視預先設定的方案原始碼 hello 處於 hello [azure iot-遠端-監視][ lnk-rmgithub] GitHub 儲存機制：

* hello **DeviceAdministration**資料夾包含 hello 原始程式碼 hello 儀表板。
* hello**模擬器**資料夾包含 hello 模擬的裝置 hello 原始程式碼。
* hello **EventProcessor**資料夾包含 hello 後端程序處理 hello 傳入遙測 hello 原始程式碼。

完成之後，您可以從您的 Azure 訂閱 hello 上刪除 hello 預先設定的解決方案[azureiotsuite.com] [ lnk-azureiotsuite]站台。 此站台可讓您 tooeasily 刪除所有 hello 當您建立預先設定的 hello 方案已佈建的資源。

> [!NOTE]
> 刪除所有項目 tooensure 相關 toohello 預先設定的解決方案，刪除上 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台，並不會刪除 hello hello 入口網站中的資源群組。

## <a name="next-steps"></a>後續步驟

既然您已部署預先設定的有效的解決方案，您可以繼續閱讀下列文章 hello 入門 IoT 套件：

* [遠端監視預先設定解決方案逐步解說][lnk-rm-walkthrough]
* [連接您的裝置 toohello 遠端監視預先設定的解決方案][lnk-connect-rm]
* [Hello azureiotsuite.com 網站的權限][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md