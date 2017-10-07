---
title: "雲端服務 aaaTesting hello 效能 |Microsoft 文件"
description: "測試使用 hello Visual Studio 分析工具在雲端服務的 hello 效能"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>測試雲端服務的 hello 效能
## <a name="overview"></a>概觀
您可以在 hello 下列方式測試雲端服務的 hello 效能：

* 使用 Azure 診斷 toocollect 要求和連接和相關資訊，顯示從客戶觀點來看 hello 服務的執行方式的 tooreview 網站統計資料。 tooget 入門，請參閱[為 Azure 雲端服務和虛擬機器設定診斷功能](http://go.microsoft.com/fwlink/p/?LinkId=623009)。
* 使用 hello Visual Studio 分析工具 tooget hello 情況在計算方面 hello 服務的執行方式的深入分析。 如本主題所述，您可以使用 hello profiler toomeasure 效能服務在 Azure 中執行。 如需如何為服務 toouse hello profiler toomeasure 效能會在本機執行於計算模擬器，請參閱[測試 hello Azure 雲端服務在本機 hello 計算模擬器使用 hello Visual Studio 分析工具中的效能](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>選擇效能測試方法
### <a name="use-azure-diagnostics-toocollect"></a>使用 Azure 診斷 toocollect:
* 網頁或服務 (例如要求和連接) 的相關統計資料。
* 角色的統計資料，例如角色重新啟動的頻率。
* 整體記憶體使用量，例如 hello 百分比 hello 記憶體回收行程會接受或 hello 記憶體的時間資訊設定的執行中角色。

### <a name="use-hello-visual-studio-profiler-to"></a>使用 hello Visual Studio 分析工具：
* 判斷哪些函式需要 hello 大部分的時間。
* 測量每一部分密集運算的程式花費多少時間。
* 比較兩個版本服務的詳細效能報告。
* 分析記憶體配置，以比 hello 層級的個別記憶體配置更多詳細資料。
* 分析多執行緒程式碼中的並行處理問題。

當您使用 hello 程式碼剖析工具時，您可以在本機或 Azure 雲端服務在執行時收集資料。

### <a name="collect-profiling-data-locally-to"></a>在本機收集分析資料，以便：
* 測試 hello 屬於雲端服務，例如 hello 執行特定的背景工作角色，不需要實際模擬的負載的效能。
* 在受控制的情況下，隔離測試雲端服務的 hello 效能。
* 測試 hello 效能的雲端服務，才能將它部署 tooAzure。
* 測試雲端服務的 hello 效能未公開，而不干擾 hello 現有部署。
* 測試 hello hello 服務效能，而不會產生費用，在 Azure 中執行。

### <a name="collect-profiling-data-in-azure-to"></a>在 Azure 中收集分析資料，以便：
* 測試模擬或實際負載下的雲端服務的 hello 效能。
* 使用 hello 檢測方法收集程式碼剖析資料，如本主題稍後所述。
* Hello hello 服務效能測試中 hello 與在生產環境中的 hello 服務執行時相同的環境。

您通常會透過模擬負載 tootest 底下的雲端服務正常或壓力狀況。

## <a name="profiling-a-cloud-service-in-azure"></a>在 Azure 中分析雲端服務
當您發行雲端服務從 Visual Studio 時，您可以設定檔 hello 服務，並指定 hello hello 您想要的資訊可供程式碼剖析設定。 對每個角色的執行個體啟動分析工作階段。 如需有關如何 toopublish 您的服務，從 Visual Studio，請參閱[發行 Azure 雲端服務，從 Visual Studio tooan](https://msdn.microsoft.com/library/azure/ee460772.aspx)。

toounderstand 進一步了解效能分析在 Visual Studio 中，請參閱[初學者指南 tooPerformance 分析](https://msdn.microsoft.com/library/azure/ms182372.aspx)和[使用程式碼剖析工具分析應用程式效能](https://msdn.microsoft.com/library/azure/z9z62c29.aspx)。

> [!NOTE]
> 發佈雲端服務時，您可以啟用 IntelliTrace 或分析。 您不能同時啟用。
> 
> 

### <a name="profiler-collection-methods"></a>分析工具收集方法
您可以對分析使用不同的收集方法，根據效能問題：

* **CPU 取樣** - 這個方法會收集對 CPU 使用率問題的初始分析很實用的應用程式統計資料。 CPU 取樣是 hello 大多數效能調查的建議的方法。 當您收集 CPU 取樣資料時，您要分析的 hello 應用程式沒有影響很小。
* **檢測** - 這個方法會收集詳細的時間資料，對重點分析以及分析輸入/輸出效能問題非常實用。 hello 檢測方法會記錄每個項目、 結束和函式呼叫的 hello 函式的模組中執行剖析期間。 這個方法是適合用來收集一段程式碼的詳細的計時資訊，以及了解 hello 輸入和輸出作業對應用程式效能的影響。 執行 32 位元作業系統的電腦會停用這個方法。 此選項可以使用僅當您執行 hello 雲端服務在 Azure 中，不是在本機 hello 計算模擬器中。
* **.NET 記憶體配置**-此方法會使用 hello 取樣分析方法，收集.NET Framework 記憶體配置資料。 hello 收集的資料包含 hello 數目和配置的物件大小。
* **並行** - 這個方法會收集資源爭用資料，以及處理序與執行緒執行資料，對於分析多執行緒及多處理序的應用程式很實用。 hello 並行方法收集每個區塊執行程式碼，例如當執行緒等待鎖定釋出存取 tooan 應用程式資源 toobe 的事件資料。 這個方法對於分析多執行緒應用程式很實用。
* 您也可以啟用**階層互動分析**，其提供其他有關 hello 執行時間的資訊同步 ADO.NET 呼叫函式的一個或多個與通訊的多層式應用程式中資料庫。 您可以與任何 hello 程式碼剖析方法收集階層互動資料。 如需有關階層互動分析的詳細資訊，請參閱 [階層互動檢視](https://msdn.microsoft.com/library/azure/dd557764.aspx)。

## <a name="configuring-profiling-settings"></a>設定分析設定
hello 下列圖例顯示如何 tooconfigure hello 發行 Azure 應用程式 對話方塊從程式碼剖析設定。

![設定分析設定](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> tooenable hello**啟用程式碼剖析**核取方塊，您必須擁有 hello 程式碼剖析工具，您會使用 toopublish 您的雲端服務的 hello 本機電腦上安裝。 根據預設，當您安裝 Visual Studio 時，會安裝 hello 分析工具。
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure 程式碼剖析設定
1. 在 方案總管開啟 Azure 專案，hello 捷徑功能表，然後選擇 **發行**。 如需詳細步驟 toopublish 雲端服務，請參閱[發行雲端服務使用 hello Azure tools](http://go.microsoft.com/fwlink/p?LinkId=623012)。
2. 在 [hello**發行 Azure 應用程式**對話方塊中，選擇 hello**進階設定**] 索引標籤。
3. 程式碼剖析，tooenable 選取 hello**啟用程式碼剖析**核取方塊。
4. tooconfigure 程式碼剖析設定中，選擇 hello**設定**超連結。 hello 設定檔設定 對話方塊隨即出現。
5. 從 hello**何種程式碼剖析方法想您 toouse**選項按鈕，選擇 程式碼剖析，您需要 hello 類型。
6. toocollect hello 階層互動分析資料，選取 hello**啟用階層互動分析**核取方塊。
7. toosave hello 設定中，選擇 hello**確定** 按鈕。
   
    當您發行這個應用程式時，這些設定是使用的 toocreate hello 分析每個角色的工作階段。

## <a name="viewing-profiling-reports"></a>檢視分析報告
對為雲端服務中每個角色的執行個體建立分析工作階段。 tooview 您程式碼剖析報告每個工作階段從 Visual Studio，您可以檢視 hello 伺服器總管] 視窗，然後選擇 [Azure 計算節點 tooselect hello 的角色執行個體。 然後，您可以檢視分析報告 hello 下列圖例所示的 hello。

![檢視來自 Azure 的分析報告](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>程式碼剖析報告 tooview
1. tooview hello 伺服器總管 視窗中 Visual Studio 中，在 hello 功能表列選擇檢視中，伺服器總管。
2. 選擇 hello Azure 計算節點，然後選擇 hello 雲端服務的 hello Azure 部署節點，您從 Visual Studio 發行時選取 tooprofile。
3. hello 服務，為特定的執行個體，開啟 hello 快顯功能表中選擇 hello 角色，然後選擇 tooview 程式碼剖析報告執行個體，**檢視分析報告**。
   
    從 Azure 現在下載 hello.vsp 檔這份報告，並 hello 下載 hello 狀態會顯示在 hello Azure 活動記錄檔。 分析報告的 hello hello 下載完成時，會出現在 hello 名為 Visual Studio 編輯器中的索引標籤<Role name>  *<Instance Number>*  <identifier>.vsp。 Hello 報表的摘要資料隨即出現。
4. toodisplay 之不同檢視的 hello 報表，在 hello 目前的檢視清單中，選擇您要檢視 hello 類型。 如需詳細資訊，請參閱 [分析工具報告檢視](https://msdn.microsoft.com/library/azure/bb385755.aspx)。

## <a name="next-steps"></a>後續步驟
[偵錯雲端服務](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[發行 tooan Azure 雲端服務，從 Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

