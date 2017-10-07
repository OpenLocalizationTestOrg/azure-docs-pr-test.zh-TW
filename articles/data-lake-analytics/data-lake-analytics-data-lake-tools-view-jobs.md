---
title: "aaaUse 作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視 |Microsoft 文件"
description: "深入了解如何 toouse 作業瀏覽器和 Azure Data Lake Analytics 工作的工作檢視。 "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>使用適用於 Azure Data Lake Analytics 作業的作業瀏覽器和作業檢視
hello Azure 資料湖分析服務封存已送出工作中的[查詢存放區](#query-store)。 在本文中，您學會 toouse 作業瀏覽器和 Azure 資料湖 Tools for Visual Studio toofind hello 歷程記錄中的工作檢視工作資訊。 

根據預設，hello 資料湖分析服務會 hello 工作 30 天的時間。 hello 逾期期限可從 hello Azure 入口網站設定，藉由設定自訂的 hello 到期原則。 您不會到期之後無法 tooaccess hello 作業資訊。 

## <a name="prerequisites"></a>必要條件
請參閱[適用於 Visual Studio 的 Azure Data Lake 工具](data-lake-analytics-data-lake-tools-get-started.md#prerequisites)。

## <a name="open-hello-job-browser"></a>開啟 hello 作業瀏覽器
存取 hello 作業瀏覽器透過**伺服器總管 > Azure > Data Lake Analytics > 工作**Visual Studio 中。  您可以使用 hello 作業瀏覽器，存取資料湖分析帳戶 hello 查詢存放區。 作業瀏覽器會顯示查詢存放區上保留，hello 顯示基本的工作資訊及 hello 正確顯示在工作檢視詳細的作業資訊。

## <a name="job-view"></a>作業檢視
工作檢視會顯示 hello 工作的詳細的資訊。 tooopen 作業，您可以按兩下 hello 作業瀏覽器中的工作或工作檢視，即可從 hello Data Lake 功能表開啟它。 您應該會看到一個對話方塊，填入 hello 作業的 URL。

![Data Lake 工具 Visual Studio 作業瀏覽器](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

作業檢視包含︰

* 工作摘要
  
    重新整理作業檢視 hello toosee hello 執行工作的最新的資訊。
  
  * 作業狀態 (圖形)：
    
      工作狀態會列出 hello 工作階段：
    
      ![Azure Data Lake Analytics 作業階段狀態](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * 正在準備： 上傳指令碼 toohello 雲端，編譯和最佳化使用 hello 編譯服務的 hello 指令碼。
    * 排入佇列： 作業佇列的 whey 他們正在等候資源不足或 hello 作業超過 hello 最大並行的工作每個帳戶的限制。 hello 優先順序設定會決定 hello 一連串佇列作業-hello 低 hello 數字 hello hello 優先順序越高。
    * 執行： hello 作業實際上正在執行 Data Lake Analytics 帳戶中。
    * 正在完成： hello 作業即將完成 （例如，完成 hello 檔案）。
      
      hello 作業可能會在每個階段中失敗。 例如，編譯 hello 準備階段，在 hello 排入佇列階段中，逾時錯誤和錯誤等 hello 執行階段中的執行錯誤。
  * 基本資訊
    
      hello 基本作業資訊會顯示在 hello 的 hello 工作摘要面板的下半部。
    
      ![Azure Data Lake Analytics 作業階段狀態](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * 作業的結果︰成功或失敗。 在每個階段 hello 作業可能會失敗。
    * 總持續時間︰提交時間和結束時間之間的時鐘時間 (持續時間)。
    * 計算時間總計： hello 總和的每個頂點的執行時間，您可以考慮為 hello 時間 hello 工作執行中只能有一個端點。 端點的詳細資訊，請參閱 tooTotal 頂點 toofind。
    * 提交/開始/結束時間： hello 時間當 hello 資料湖分析服務收到作業提交/啟動 toorun hello 作業/結束 hello 工作成功與否。
    * 編譯/已排入佇列/執行： Hello 準備/已排入佇列/執行階段期間，所用時鐘時間。
    * 執行 hello 作業所使用的帳戶： hello Data Lake Analytics 帳戶。
    * 作者： hello 使用者送出 hello 工作，它可以是實際人員的帳戶或系統帳戶。
    * Hello 工作的優先順序： hello 優先順序。 hello 低 hello 數字，hello hello 優先順序越高。 它只會影響 hello hello 佇列中的 hello 工作序列。 設定較高的優先順序，不會優先於執行中的作業。
    * 平行處理原則： hello 要求並行 Azure 資料湖分析單位 (ADLAUs)，也稱為頂點的最大數目。 目前，一個頂點等於 tooone VM 具有兩個虛擬核心和 6 GB 的 RAM，但無法升級此未來 Data Lake Analytics 更新。
    * 需要 toobe 處理 hello 工作完成之前的剩餘的位元組： 位元組。
    * 讀取/寫入的位元組： 已讀取/寫入 hello 工作已經開始執行後的位元組。
    * 總頂點： hello 作業會分成多個工作片段，每個工作會呼叫頂點。 這個值描述多少個工作片段 hello 工作所組成。 您可以將頂點視為基本處理單位，也就是 Azure Data Lake Analytics 單位 (ADLAU)，且頂點可以在平行處理原則中執行。 
    * 完成/執行/失敗： hello 完成/執行/失敗頂點的計數。 端點可以失敗的原因是 tooboth 使用者程式碼和系統失敗，但 hello 系統重試失敗的頂點自動幾次。 如果重新嘗試後仍失敗 hello 頂點，hello 整個作業會失敗。
* 作業圖形
  
    U-SQL 指令碼代表 hello 邏輯的輸入的資料 toooutput 資料轉換。 hello 指令碼會編譯和最佳化 hello 準備階段 tooa 實體的執行計畫。 作業圖形是 tooshow hello 實體的執行計畫。  hello 下列圖表說明 hello 程序：
  
    ![Azure Data Lake Analytics 作業階段狀態](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    作業分成許多的工作片段。 每份工作片段稱為頂點。 hello 頂點分組為超級頂點 （也稱為 「 階段 」），並視覺化為作業圖形。 hello 綠色階段 placards hello 作業圖形中的顯示 hello 階段。
  
    每個頂點階段中的正在進行 hello 相同種類的工作與 hello 的不同部份相同資料。 例如，如果您有一個 TB 資料的檔案，而且有數百個頂點在讀取它，則每個頂點都會讀取其中一個區塊。 Hello，這些端點會群組成相同的階段和執行相同工作相同的輸出檔的不同部份。
  
  * <a name="state-information"></a>階段資訊
    
      在特定的階段中，hello placard 中會顯示一些數字。
    
      ![Azure Data Lake Analytics 作業圖形階段](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 擷取: hello 的階段，名為的數目和 hello 作業方法的名稱。
    * 84 頂點： hello 的頂點總數在這個階段中。 hello 圖表示此階段中分為多少個工作片段。
    * 12.90 s/頂點： hello 頂點平均執行時間為此階段。 此圖中的計算方式是加總 (每個頂點執行時間) / (頂點總計數)。 這表示如果您無法指派所有執行中的平行處理原則的 hello 頂點，hello 整個階段已完成在 12.90 s。 這也表示，如果所有 hello 中的工作會循序完成此階段，hello 成本是 #vertices * 的平均回應時間。
    * 已寫入 850,895 個資料列︰在這個階段中寫入的資料列總計數。
    * R/W︰在這個階段中讀取/寫入的資料量 (位元組)。
    * Colors： 中使用的色彩 hello 階段 tooindicate 不同的端點狀態。
      
      * 綠色表示 hello 頂點成功。
      * 橙色表示 hello 頂點重試一次。 重試的 hello 頂點失敗，但是自動重試，而且成功 hello 系統的整體 hello 階段已順利完成。 如果 hello 頂點重試，但仍然失敗，hello 色彩會變成紅色，hello 整個作業失敗。
      * 紅色則表示失敗，這表示某些頂點必須已由 hello 系統重試幾次，但仍然失敗。 這個情況會造成 hello 整個作業 toofail。
      * 藍色表示特定頂點正在執行。
      * 白色指出 hello 頂點正在等候。 hello 頂點可能會等候 toobe 排程一旦 ADLAU 就會變成可用，或它正在等候輸入其輸入的資料可能不會準備。
      
      您可以依一個狀態將滑鼠游標暫留，hello 階段找到更多詳細資料：
      
      ![Azure Data Lake Analytics 作業圖形階段詳細資料](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * 頂點： Hello 頂點詳細說明，多少的頂點總數，已完成多少頂點，比方說，是它們失敗或仍然/等候執行中，依此類推。
  * 跨/內部組合讀取的資料︰檔案和資料會儲存在分散式檔案系統的多個組合中。 hello 值此處描述的資料量已讀取在 hello 相同 pod 或跨 pod。
  * 計算時間總計： hello 總和 hello 階段中每個頂點執行時間，您可以考慮將它在執行中只有一個頂點的 hello 時間如果您在 hello 階段中所有工作。
  * 資料和資料列寫入/讀取： 指出多少資料列已讀取/寫入，或需要 toobe 讀取。
  * 頂點讀取失敗︰描述多少頂點在讀取資料時失敗。
  * 會捨棄重複的頂點： hello 系統如果頂點的速度太慢，可能會排定多個頂點 toorun hello 相同的一件工作。 Hello 頂點的其中一個已成功完成後，將會捨棄 reductant 頂點。 重複的頂點捨棄記錄 hello 數目會捨棄有重複項目為 hello 階段中的頂點。
  * 頂點撤銷： hello 頂點已順利完成，但取得稍後重新執行到期 toosome 原因。 例如，如果下游頂點失去輸入的中繼資料，它會要求 hello 上游頂點 toorerun。
  * 頂點排程執行： hello hello 頂點已排程的總時間。
  * 讀取的最小/平均/最大頂點資料： hello 最小/平均/最大值的每個頂點讀取資料。
  * 持續時間： hello 時鐘時間階段所需，您需要 tooload 設定檔 toosee 這個值。
  * 工作播放
    
      資料湖分析執行的作業和封存 hello 頂點執行資訊的 hello 工作，例如 hello 頂點啟動時，停止，失敗及淘汰方式等。所有 hello 資訊自動 hello 查詢存放區中記錄及儲存在其工作設定檔。 您可以下載 hello 工作設定檔，透過 「 負載設定檔 」，在工作檢視，您可以檢視 hello 作業播放下載 hello 工作設定檔之後。
    
      作業播放會發生什麼情況 hello 叢集中的操控視覺效果。 作業播放可讓您觀看作業執行進度，並在很短的時間內 (通常少於 30 秒) 以視覺化方式偵測出效能異常和瓶頸。
  * 作業熱度圖顯示 
    
      熱度圖工作可以透過作業圖形的 hello 顯示下拉式清單中選取。 
    
      ![Azure Data Lake Analytics 作業圖形熱度圖顯示](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      它會顯示 hello I/O、 時間和輸送量熱度圖的作業，您可以尋找 hello 作業要花費在大部分的 hello 時間，或者您的工作是否為 I/O 界限工作等等。
    
      ![Azure Data Lake Analytics 作業圖形熱度圖範例](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * 進度： hello 工作執行進度，請參閱中的資訊[接移資訊](#stage-information)。
    * 讀取/寫入的資料： hello 熱門地圖的讀取/寫入，每個階段中的總資料。
    * 計算時間： hello 熱門地圖的總和 （每個頂點執行時間），您可以將此視為如何長時間花費如果 hello 階段中的所有工作都執行時，只有 1 的頂點。
    * 每個節點的平均執行時間： hello 熱門地圖的總和 （每個頂點執行時間） / （頂點數字）。 這表示如果您無法指派所有執行中的平行處理原則的 hello 頂點，hello 整個階段就會完成此時間範圍內。
    * 輸入/輸出輸送量： hello 熱門地圖的輸入/輸出的每個階段的輸送量，您可以確認您的工作是否是透過此 I/O 繫結的工作。
* 中繼資料作業
  
    您可以在 U-SQL 指令碼中執行某些中繼資料作業，例如建立資料庫、捨棄資料表等。這些作業會在編譯之後顯示於中繼資料作業。 您可以在這裡找到判斷提示、建立實體並捨棄實體。
  
    ![Azure Data Lake Analytics 作業檢視中繼資料作業](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* 狀態記錄
  
    hello 狀態記錄也會視覺化工作摘要中，但您可以取得更多詳細資料。 您可以找到 hello 的詳細資訊，例如當 hello 作業已備妥，排入佇列，開始執行、 已結束。 此外，您也可以找到 hello 作業已編譯的次數 (hello CcsAttempts: 1)，當實際上是 hello 工作分派的 toohello 叢集 (hello 詳細資料： 分派作業 toocluster) 等等。
  
    ![Azure Data Lake Analytics 作業檢視狀態記錄](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* 診斷
  
    hello 工具自動診斷作業執行。 當作業中有一些錯誤或效能問題時您會收到警示。 請注意，您必須 toodownload 設定檔 tooget 完整這裡的資訊。 
  
    ![Azure Data Lake Analytics 作業檢視診斷](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * 警告︰警示會在此處顯示編譯器警告。 您可以按一下 「 x 的問題 」 連結 toohave 更多詳細資料會顯示 hello 警示。
  * 頂點執行時間過長︰如果任一個頂點用盡時間 (例如 5 小時)，問題就會顯示在這裡。
  * 資源使用狀況︰如果您配置過多或不足所需的平行處理原則，問題就會顯示在這裡。 也可以按一下資源使用量 toosee 更多詳細資料，並進行假設狀況 toofind 更好的資源配置 （如需詳細資訊，請參閱本指南）。
  * 記憶體檢查︰如果任一個頂點使用超過 5 GB 的記憶體，問題就會顯示在這裡。 如果作業執行使用的記憶體超過系統限制，則系統可能會終止作業執行。

## <a name="job-detail"></a>作業詳細資料
工作詳細資料顯示 hello hello 工作，包括指令碼、 資源和頂點執行檢視的詳細的資訊。

![Azure Data Lake Analytics 作業詳細資料](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* 指令碼
  
    hello hello 作業的 U-SQL 指令碼會儲存在 hello 查詢存放區。 您可以檢視 hello 原始 U-SQL 指令碼，並視需要重新提交。
* 資源
  
    您可以找到儲存在 hello 透過資源的查詢存放區中的 hello 作業編譯輸出。 比方說，您可以尋找 「 algebra.xml"，也就是使用的 tooshow hello 作業圖形 hello 您註冊的組件等這裡。
* 頂點執行檢視
  
    它會顯示頂點執行詳細資料。 hello 工作設定檔會保存每個頂點執行記錄，例如讀取/寫入，執行階段狀態、 等等的總資料。透過這個檢視，您可以取得作業如何執行的詳細資料。 如需詳細資訊，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)。

## <a name="next-steps"></a>後續步驟
* toolog 診斷資訊，請參閱[存取 Azure 資料湖分析診斷記錄檔](data-lake-analytics-diagnostic-logs.md)
* toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。
* toouse 頂點執行檢視，請參閱[使用 hello 頂點資料湖 Tools for Visual Studio 中的執行檢視](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

