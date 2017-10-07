---
title: "從 Application Insights 遙測 aaaContinuous 匯出 |Microsoft 文件"
description: "匯出 Microsoft Azure 中的診斷和使用方式資料 toostorage，並從該處下載。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a>從 Application Insights 匯出遙測
要使用 tookeep 您遙測超過 hello 標準保留期間？ 或以某些特殊方式處理它？ 連續匯出很適合此用途。 您在 hello Application Insights 入口網站中看到的 hello 事件可能會在 Microsoft Azure 中的匯出的 toostorage JSON 格式。 您可以從該處下載您的資料，並寫入您指定任何程式碼需要 tooprocess 它。  

使用連續匯出，可能會產生額外的費用。 請檢查您的[定價模式](http://azure.microsoft.com/pricing/details/application-insights/)。

連續匯出設定之前，有一些其他替代方案，您可能會想 tooconsider:

* 在 hello 度量 或 搜尋 刀鋒視窗頂端的 hello 匯出按鈕可讓您傳送資料表和圖表 tooan Excel 試算表。

* [分析](app-insights-analytics.md) 可提供功能強大的遙測查詢語言。 它也可以匯出結果。
* 如果您想太[瀏覽 Power BI 中的資料](app-insights-export-power-bi.md)，您可以執行，而不使用連續匯出。
* hello[資料存取 REST API](https://dev.applicationinsights.io/)可讓您以程式設計方式存取您的遙測。

連續匯出複製您的資料 toostorage （其中它可以保留的只要您喜歡） 之後，就仍然可以使用 Application Insights 中的 hello 一般[保留期限](app-insights-data-retention-privacy.md)。

## <a name="setup"></a> 建立連續匯出
1. 在 hello 應用程式的 Application Insights 資源，請在開啟連續匯出，然後選擇 **新增**:

    ![向下捲動並按一下 [連續匯出]](./media/app-insights-export-telemetry/01-export.png)

2. 選擇 hello 遙測資料型別想 tooexport。

3. 建立或選取[Azure 儲存體帳戶](../storage/common/storage-introduction.md)想 toostore hello 資料。

    > [!Warning]
    > 根據預設，hello 存放位置將會設定 toohello 與 Application Insights 資源的相同地理區域。 如果您儲存在不同的區域中，可能會產生傳輸費用。

    ![按一下 [加入]、[匯出目的地]、[儲存體帳戶]，然後建立新儲存區或選擇現有儲存區](./media/app-insights-export-telemetry/02-add.png)

4. 建立或選取在 hello 儲存體容器：

    ![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/create-container.png)

建立匯出之後，就會開始進行。 您只能取得到達後建立 hello 匯出的資料。

可以有大約一小時才 hello 儲存體中的資料會出現延遲。

### <a name="tooedit-continuous-export"></a>tooedit 連續匯出

如果您想 toochange hello 事件類型之後，只需編輯 hello 匯出：

![按一下 [選擇事件類型]](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>toostop 連續匯出

toostop hello 匯出中，按一下 停用。 當您按一下 [啟用] 時，hello 匯出會重新啟動以新的資料。 您不會取得匯出已停用時，到達 hello 入口網站中的 hello 資料。

toostop hello 匯出，它永久刪除。 這麼做不會將您的資料從儲存體刪除。

### <a name="cant-add-or-change-an-export"></a>無法加入或變更匯出？
* tooadd 或變更的匯出，您必須擁有者、 參與者或應用程式 Insights 參與者的存取權限。 [了解角色][roles]。

## <a name="analyze"></a> 您取得什麼事件？
hello 匯出的資料是 hello 未經處理的遙測，我們收到您的應用程式中，不同之處在於我們加入我們計算位置資料來自 hello 用戶端 IP 位址。

已捨棄的資料[取樣](app-insights-sampling.md)未包含在匯出的 hello 資料。

未包含其他計算的度量。 比方說，我們不要匯出平均 CPU utilisation，但是我們不要匯出 hello 原始遙測從中計算 hello 平均值。

hello 資料也包含任何 hello 結果[可用性 web 測試](app-insights-monitor-web-app-availability.md)您設定。

> [!NOTE]
> **取樣** 如果您的應用程式傳送大量資料，hello 取樣功能可能會運作，並傳送 hello 產生遙測的分數。 [深入了解取樣。](app-insights-sampling.md)
>
>

## <a name="get"></a>檢查 hello 資料
您可以檢查 hello 直接在 hello 入口網站中的儲存體。 按一下 [瀏覽]、選取您的儲存體帳戶，然後開啟 [容器]。

在 Visual Studio 中的 Azure 儲存體 tooinspect 開啟**檢視**， **Cloud Explorer**。 (如果您沒有該功能表命令，您需要 tooinstall hello Azure SDK： 開啟 hello**新專案** 對話方塊中，展開 Visual C# / 雲端，然後選擇 **取得 Microsoft Azure SDK for.NET**。)

當您開啟 Blob 存放區時，您會看到含有一組 Blob 檔案的容器。 hello 衍生自您的 Application Insights 資源名稱、 檢測金鑰、 遙測-/ 日期/時間類型的每個檔案的 URI。 （hello 資源名稱會全部小寫，和 hello 檢測金鑰省略連字號）。

![檢查 hello blob 存放區具有適當的工具](./media/app-insights-export-telemetry/04-data.png)

hello 日期和時間是 UTC，以及會 hello 遙測已儲放在 hello 存放區中，而不是 hello 時間產生。 如果您撰寫程式碼 toodownload hello 資料時，它可以透過 hello 資料以線性方式移動。

以下是 hello hello 路徑形式：

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`blob 建立的時間在 hello 內部暫存儲存體
* `blobDeliveryTimeUtc`是 hello 時間 blob 複製的 toohello 匯出目的地儲存體

## <a name="format"></a> 資料格式
* 每個 Blob 是包含多個以 '\n' 分隔的列的文字檔案。 它包含一段時間約半分鐘處理的 hello 遙測。
* 每個資料列都代表遙測資料點，例如要求或頁面檢視。
* 每列是未格式化的 JSON 文件。 如果您 toosit 和 stare 在它，Visual Studio 中開啟它，然後選擇編輯進階，格式檔案：

![使用適當工具檢視 hello 遙測](./media/app-insights-export-telemetry/06-json.png)

時間期間依刻度為單位，10000 刻度 = 1 毫秒。 例如，這些值會顯示 1 毫秒的時間 toosend hello 瀏覽器中，3 毫秒的要求 tooreceive hello 瀏覽器頁面，以及 1.8s tooprocess hello:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[詳細的資料的模型 hello 屬性類型和值的參考。](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>處理 hello 資料
小型標尺時，您可以撰寫一些程式碼 toopull 一樣，不過您的資料、 讀入試算表，並以此類推。 例如：

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

如需較大型的程式碼範例，請參閱[使用背景工作角色][exportasa]。

## <a name="delete"></a>刪除舊資料
請注意，您負責管理您的儲存體容量，並且刪除 hello 舊資料，如有必要。

## <a name="if-you-regenerate-your-storage-key"></a>如果您重新產生儲存體金鑰...
如果您變更 hello 金鑰 tooyour 儲存體，連續匯出，將會停止運作。 您將在 Azure 帳戶中看到通知。

開啟 hello 連續匯出刀鋒視窗，並編輯您的匯出。 編輯 hello 匯出目的地，但只要維持相同的存放裝置選取的 hello。 按一下 [確定] tooconfirm。

![編輯 hello 連續匯出、 開啟和關閉三個匯出目的地。](./media/app-insights-export-telemetry/07-resetstore.png)

將重新啟動 hello 連續匯出。

## <a name="export-samples"></a>匯出範例

* [匯出 tooSQL 使用資料流分析][exportasa]
* [串流分析範例 2](app-insights-export-stream-analytics.md)

在較大的縮放比例，請考慮[HDInsight](https://azure.microsoft.com/services/hdinsight/) -在 hello 雲端中的 Hadoop 叢集。 HDInsight 提供各種不同的技術，用於管理和分析大型的資料，而且您無法使用它 tooprocess 資料已匯出從 Application Insights。

## <a name="q--a"></a>問答集
* *但我想要的只是一次性下載圖表。*  

    是的，您可以這麼做。 在 hello hello 刀鋒視窗頂端，按一下**匯出資料**。
* *我設定匯出，但我的儲存區中沒有資料。*

    沒有 Application Insights 收到任何遙測從您的應用程式因為設定 hello 匯出？ 您將只會收到新資料。
* *我已嘗試 tooset 向上匯出，但是被拒絕存取*

    如果 hello 帳戶由您的組織所擁有，您必須 toobe hello 的擁有者或 contributors 群組的成員。
* *我可以匯出直線 toomy 自己的內部存放區嗎？*

    否，抱歉。 我們的匯出引擎目前僅適用於 Azure 儲存體。  
* *是否有任何限制 toohello 的數量您放在 my 存放區的資料？*

    否。 我們將會保留將資料推送直到您刪除 hello 匯出。 如果我們叫用 hello 外部 blob 儲存體限制，但這很龐大，我們將停止。 它是最多 tooyou toocontrol 您使用多少儲存空間。  
* *Hello 儲存體中應該查看多少 blob？*

  * 每個資料中，輸入您所選的 tooexport，新的 blob （如果有可用的資料） 會建立每隔一分鐘。
  * 此外，針對具有高流量的應用程式，則會配置額外的分割單位。 在此情況下，每個單位會每分鐘建立一個 Blob。
* *我重新產生 hello 金鑰 toomy 儲存體，或者變更 hello hello 容器名稱和 hello 匯出現在無法運作。*

    編輯 hello 匯出並開啟 hello 匯出目的地刀鋒視窗。 讓的 hello 相同存放裝置選取如往常一般，並按一下 [確定] tooconfirm。 匯出將重新開始。 如果 hello 變更是 hello 過去幾天內，您不必擔心會遺失資料。
* *可以暫停 hello 匯出？*

    是。 按一下 [停用]。

## <a name="code-samples"></a>程式碼範例

* [串流分析範例](app-insights-export-stream-analytics.md)
* [匯出 tooSQL 使用資料流分析][exportasa]
* [詳細的資料的模型 hello 屬性類型和值的參考。](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
