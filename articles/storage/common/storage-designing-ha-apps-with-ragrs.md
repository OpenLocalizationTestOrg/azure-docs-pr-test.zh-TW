---
title: "aaaDesigning 高度可用的應用程式使用 Azure 讀取存取異地備援儲存體 (RA-GRS) |Microsoft 文件"
description: "如何 toouse Azure RA-GRS 儲存體 tooarchitect 彈性的高可用性應用程式足夠 toohandle 中斷。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>使用 RA-GRS 設計高可用性應用程式

雲端式基礎結構的常見功能是提供高可用性平台來裝載應用程式。 以雲端為基礎的應用程式的開發人員必須考慮如何仔細 tooleverage 這個平台 toodeliver 高可用性應用程式 tootheir 使用者。 本文著重的特別開發人員如何使用 hello Azure 儲存體讀取權限地理備援儲存體 (RA-GRS) toomake 他們更多可用的應用程式。

有四種備援選項 - LRS (本地備援儲存體)、ZRS (區域備援儲存體)、GRS (異地備援儲存體) 和 RA-GRS (讀取權限異地備援儲存體)。 我們 toodiscuss GRS 和 RA-GRS 本文中。 使用 GRS 時，三份資料會保留在 hello 設定 hello 儲存體帳戶時，您選取的主要區域。 另外會以非同步方式在 Azure 所指定的次要區域中保留三個額外複本。 RA-GRS 是 hello GRS 相同的動作，差別在於您具有讀取權限 toohello 次要複本。 如需 hello 不同的 Azure 儲存體備援選項的詳細資訊，請參閱[Azure 儲存體複寫](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy)。 hello 複寫發行項也會顯示 hello 配對的 hello 主要和次要區域。

有包含在本文中和連結 tooa 完整的範例，您可以下載並執行 hello 端的程式碼片段。

## <a name="key-features-of-ra-grs"></a>RA-GRS 的主要功能

我們會討論如何之前 toouse RA-GRS 存放裝置，我們來談談其屬性和行為。

* Azure 儲存體維護的唯讀副本儲存在次要區域; 主要區域中的 hello 資料如先前所述，hello 儲存體服務位置決定的 hello 的 hello 次要區域。

* hello 唯讀複本是[最終一致](https://en.wikipedia.org/wiki/Eventual_consistency)hello hello 主要區域中的資料。

* Blob、 資料表和佇列，您可以查詢 hello 次要區域*上次同步處理時間*會告訴您發生 hello hello 主要 toohello 次要區域中的最後一個複寫的值。 (Azure 檔案儲存體不支援此動作，它目前沒有 RA-GRS 備援)。

* 您可以使用 hello 儲存體用戶端程式庫 toointeract hello 任一 hello 主要或次要區域中的資料。 您也可以重新導向讀取要求自動 toohello 次要區域如果逾時，讀取的要求 toohello 主要區域。

* 如果沒有主要的問題會影響 hello hello 主要區域中的 hello 資料存取範圍，hello Azure 團隊可能會觸發地理容錯移轉，此時 hello 指向 toohello 主要區域的 DNS 項目將會變更的 toopoint toohello 次要區域。

* 發生地理容錯移轉時，Azure 將會選取新的次要位置和複寫 toothat hello 資料的位置，然後指向次要 DNS 項目 tooit hello。 hello 次要端點將無法使用，直到 hello 儲存體帳戶已完成複寫。 如需詳細資訊，請參閱[如果 Azure 儲存體中斷，就會發生何種 toodo](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance)。

## <a name="application-design-considerations-when-using-ra-grs"></a>使用 RA-GRS 時的應用程式設計考量

這篇文章 hello 主要用途是 tooshow 您如何 toodesign 的應用程式，將會繼續 toofunction （雖然中容量有限） 即使在 hello 事件的重大的災害，在 hello 主要資料中心。 您可以切換 tooread hello 次要區域中，而有問題，並 hello 主要區域再次可用時，切換回具有您的應用程式 toohandle 暫時性或長時間執行的問題。

### <a name="using-eventually-consistent-data"></a>使用最終一致的資料

此建議的解決方案假設它是關係 tooreturn 可能過時資料 toohello 呼叫應用程式。 Hello 次要資料是最終一致的所以 hello 資料已寫入 toohello 主要，但是 hello 更新 toohello 次要已完成複寫時 hello 主要區域變成無法存取。

例如，客戶無法提交成功時，更新，然後 hello 主要可能會當機前 hello 更新傳播的 toohello 次要。 在此情況下，如果 hello 客戶會接著詢問 tooread hello 資料後備，他會收到 hello 過時資料，而非 hello 更新資料。 您必須決定這是否可接受的而且如果是，您將訊息 hello 客戶的方式。 您會看到如何 toocheck hello 上次同步處理時間稍後在本文章 toosee 中的 hello 次要資料如果 hello 次要處於最新狀態。

### <a name="handling-services-separately-or-all-together"></a>個別處理服務或一併處理所有服務

雖然不太可能，它可能會無法使用的一項服務 toobecome hello 其他服務仍然是完全正常運作時。 您可以控制代碼 hello 重試次數和唯讀模式，每個服務分開 （blob、 佇列、 資料表），或您可以同時處理的所有 hello 儲存體服務以一般方式重試次數。

比方說，如果您在應用程式中使用佇列和 blob，您可能決定 tooput toohandle 可重試錯誤時，不同的程式碼中的每一種。 然後重試收到 hello blob 服務，但仍然正常 hello 佇列服務，如果只有 hello 部分處理 blob 的應用程式都會受到影響。 如果您決定的 toohandle 所有儲存體服務會重試以一般方式並呼叫 toohello blob 服務傳回重試錯誤，然後要求 tooboth hello blob 服務和 hello 佇列服務將會受到影響。

最後，這取決於您的應用程式的 hello 複雜性。 您可以決定 toohandle hello 失敗服務，但改為 tooredirect 讀取所有儲存體服務 toohello 次要區域的要求時您 hello 主要區域中偵測到任何儲存體服務的問題，請在唯讀模式中執行 hello 應用程式。

### <a name="other-considerations"></a>其他考量

這些是 hello hello 本文其餘部分中，我們將討論其他考量。

*   處理重試讀取要求，使用 hello 斷路器模式

*   最終一致的資料和 hello 上次同步處理時間

*   測試

## <a name="running-your-application-in-read-only-mode"></a>在唯讀模式中執行您的應用程式

toouse RA-GRS 儲存體，您必須是能夠 toohandle 這兩個無法讀取的要求，失敗更新要求 （在此情況下這表示插入、 更新和刪除的更新）。 如果 hello 主要資料中心失敗，讀取要求的可重新導向的 toohello 次要資料中心，但因為 hello 次要唯讀狀態，無法更新要求。 基於這個理由，您需要某些方式 toorun 唯讀模式中的應用程式。

例如，您可以設定將送出的任何更新要求 toohello 儲存體服務之前檢查的旗標。 其中一個 hello 更新要求時，您可以略過它，並傳回適當的回應 toohello 客戶。 您甚至可能會想 toodisable 特定功能完全 hello 問題解決之前，並通知使用者這些功能會暫時無法使用。

如果您分別決定 toohandle 錯誤，以取得每個服務，您也必須 toohandle hello 能力 toorun 唯讀模式中的應用程式服務。 您可能會有唯讀旗標，為每個服務可啟用和停用和控制代碼 hello hello 程式碼中的適當位置中的適當旗標。

正在 toorun 無法在唯讀模式下的應用程式具有另一個好處 – 可讓您在進行主要應用程式升級期間 hello 能力 tooensure 有限的功能。 您可以觸發唯讀模式和點 toohello 次要資料中心，您的應用程式 toorun 確保沒有人正在存取 hello hello 主要區域中的資料時要進行升級。

## <a name="handling-updates-when-running-in-read-only-mode"></a>在唯讀模式中執行時處理更新

有很多種 toohandle 更新要求時在唯讀模式下執行。 我們不會全面討論此問題，但一般來說，有一些模式是您需要考量的。

1.  您可以回應 tooyour 使用者，告訴他們您目前沒有接收更新。 例如，連絡人管理系統無法啟用客戶 tooaccess 連絡資訊，但無法進行更新。

2.  您可以將更新加入其他區域中的佇列。 在此情況下，您會在不同區域中，撰寫您的待更新要求 tooa 佇列，然後的方式 tooprocess 這些要求，hello 主要資料中心再次上線之後。 在此案例中，您應該讓 hello 客戶知道 hello 更新要求會排入佇列供稍後處理。

3.  您可以撰寫您的更新 tooa 儲存體帳戶，另一個區域中。 接著當 hello 主要資料中心再次上線，您可以讓方式 toomerge 為 hello 主要資料，根據 hello hello 資料結構的更新。 例如，如果您要建立個別的檔案與 hello 名稱中的日期/時間戳記，您可以複製這些檔案後 toohello 主要區域。 這適用於某些工作負載，例如記錄和 iOT 資料。

## <a name="handling-retries"></a>處理重試

您如何知道哪些錯誤是可重試的？ 這取決於 hello 儲存體用戶端程式庫。 例如，404 錯誤 （找不到資源） 不是可重試因為重試一次它不可能 tooresult 成功。 Hello 相反地，500 錯誤是發生可重試因為伺服器發生錯誤，而且也可能只是暫時性的問題。 如需詳細資訊，請參閱 hello[開啟 hello ExponentialRetry 類別原始程式碼](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs)hello.NET 儲存體用戶端程式庫。 （尋找 hello ShouldRetry 方法）。

### <a name="read-requests"></a>讀取要求

如果沒有發生問題的主要儲存體讀取要求的可重新導向的 toosecondary 儲存體。 如前面所述在[最終使用一致的資料](#using-eventually-consistent-data)，它必須是可接受應用程式 toopotentially 閱讀過時資料。 如果您使用 hello 儲存體用戶端程式庫 tooaccess RA-GRS 資料，您可以設定 hello 的值來指定的讀取要求的 hello 重試行**LocationMode**屬性 tooone hello 以下的：

*   **Primaryonly 啟動**  (hello 預設值)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

當您將 hello **LocationMode**太**PrimaryThenSecondary**，如果 hello 初始讀取要求 toohello 主要端點失敗，發生可重試的錯誤、 hello 用戶端會自動將另一次讀取要求 toohello 次要端點。 如果伺服器逾時是 hello 錯誤，則 hello 用戶端將有 hello 逾時 tooexpire 的 toowait 才從 hello 服務收到可重試的錯誤。

有兩個基本上案例 tooconsider 當您決定如何 toorespond tooa 重試錯誤：

*   這是隔離的問題，而且 toohello 主要端點時，後續要求將不會傳回可重試的錯誤。 舉例來說，這可能發生在有暫時性網路錯誤時。

    在此案例中，沒有顯著的效能負面影響中沒有具有**LocationMode**設定得**PrimaryThenSecondary**因為這只會發生很少。

*   這是與 hello hello 主要區域中的儲存體服務中至少一個問題，而且 hello 主要區域中的所有後續要求 toothat 服務可能 tooreturn 可重試錯誤，一段時間。 舉例來說，這是 hello 主要區域是否完全無法存取。

    在此案例中，會對效能帶來負面影響因為您所有的讀取的要求會先嘗試 hello 主要端點，請等候 hello 逾時 tooexpire，然後切換 toohello 次要端點。

針對這些案例，您應該識別可那里 hello 主要端點進行中的問題，並傳送所有讀取要求直接 toohello 次要端點，藉由設定 hello **LocationMode**屬性太**SecondaryOnly**。 此時，您也應該變更 hello 應用程式 toorun 以唯讀模式。 這種方法稱為 hello[斷路器模式](https://msdn.microsoft.com/library/dn589784.aspx)。

### <a name="update-requests"></a>更新要求

hello 斷路器模式也可以套用的 tooupdate 要求。 不過，更新的要求不可重新導向的 toosecondary 儲存區，這是唯讀的。 這些要求，您應該保留 hello **LocationMode**屬性設定太**primaryonly 啟動**  (hello 預設值)。 toohandle 這些錯誤，您可以套用度量 toothese 要求 – 例如在一個資料列 – 10 失敗，並符合您的閾值時，切換到唯讀模式的 hello 應用程式。 您可以使用 hello 相同方法來傳回 tooupdate 模式所需 hello 斷路器模式的 hello 下一節中，如下所述。

## <a name="circuit-breaker-pattern"></a>斷路器模式

應用程式中使用 hello 斷路器模式可以防止它的作業可能 toofail 重複重試一次。 它可讓 hello 應用程式 toocontinue toorun，而非佔用 hello 作業會以指數方式重試時的時間。 它也會偵測 hello 錯誤已修正，此時時間 hello 應用程式可以 hello 再次嘗試操作。

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>如何 tooimplement hello 斷路器模式

tooidentify 持續性的問題與主要端點，您可以監視 hello 用戶端發生可重試錯誤的頻率。 由於每個案例有不同，您會有 toodecide hello 臨界值想 toouse hello 決策 tooswitch toohello 次要端點，並在唯讀模式下執行 hello 應用程式。 比方說，您可以決定 tooperform hello 參數，如果不成功的資料列中有 10 個錯誤。 另一個例子是 tooswitch 如果 90 %2 分鐘內的 hello 要求失敗。

Hello 第一個案例中，您可以只保留的 hello 失敗計數，如果沒有到達之前成功 hello toozero 後的最大值、 設定 hello 計數。 Hello 第二個案例中，它是 toouse 的其中一種方式 tooimplement hello MemoryCache 物件 （在.NET)。 每個要求都將加入 CacheItem toohello 快取、 設定 hello 值 toosuccess (1) 或失敗 (0)，並設定 hello 到期時間 too2 分鐘從現在 （或是指定任何時間限制）。 當達到的項目到期時間時，會自動移除 hello 項目。 這將會為您提供一個 2 分鐘循環的視窗。 請要求 toohello 對儲存體服務，每次您先使用 Linq 查詢跨 hello MemoryCache 物件 toocalculate hello 成功百分比方式加總 hello 值，並除以 hello 計數。 當 hello 成功百分比低於某個閾值 （如 10%) 時，設定 hello **LocationMode**屬性讀取要求太**SecondaryOnly**並切換到唯讀模式之前 hello 應用程式繼續進行。

錯誤的 hello 臨界值時 toomake hello 參數可能因服務 tooservice 在您的應用程式，因此您應該考慮讓它們可設定參數，請使用 toodetermine。 這也是以在該處您分別決定每個服務 toohandle 可重試錯誤，或成為其中一員，如先前所討論。

另一個考量是如何 toohandle 多個執行個體的應用程式，以及哪些 toodo，當您在每個執行個體中偵測可重試的錯誤。 例如，您可能有 20 的 Vm 執行以相同的應用程式載入的 hello。 您要個別處理每個執行個體嗎？ 如果一個執行個體啟動問題、 是否要 toolimit hello 回應 toojust 這個執行個體，或您想 tootry toohave 所有執行個體在回應 hello 相同一個執行個體發生問題時？ 分別處理 hello 執行個體，會比嘗試 toocoordinate hello 回應跨，更簡單，但做法取決於您的應用程式架構。

### <a name="options-for-monitoring-hello-error-frequency"></a>監視 hello 錯誤頻率的選項

您有三個主要選項時透過 toohello 次要區域和變更 tooswitch hello 唯讀模式中的應用程式 toorun 監視的重試次數 hello toodetermine 順序中的主要區域中的 hello 頻率。

*   加入的處理常式 hello [**正在重試**](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx)事件 hello [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx)物件傳遞 tooyour 儲存體要求 – 這是 hello方法會顯示在這份文件，而且 hello 隨附的範例中使用。 每當 hello 用戶端重試要求時，會引發這些事件，讓您 tootrack 頻率 hello 用戶端發生可重試錯誤上主要端點。

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   在 hello [**評估**](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx)方法中的自訂重試原則，您可以執行自訂程式碼，每當重試會發生。 加法 toorecording 重試發生失敗時，這也可讓您 hello 機會 toomodify 重試行中。

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   hello 第三種方法是 tooimplement 持續偵測您的主要儲存體端點與虛擬應用程式中的自訂監視元件讀取要求 （例如讀取小型 blob） toodetermine 其健全狀況。 這會佔用某些資源，但時間不是很長。 當探索問題時，達到臨界值時，您會接著執行 hello 參數太**SecondaryOnly**和唯讀模式。

在某些時候，您會想 tooswitch 後 toousing hello 主要端點，並允許更新。 如果使用其中一種 hello 上面所列的前兩個方法，只要無法切換後 toohello 主要端點，並執行可任意所選的時間內或作業的數目之後啟用更新模式。 您可以讓它再次瀏覽 hello 重試邏輯。 如果已修正 hello 問題，它將繼續 toouse hello 主要端點，並允許更新。 如果仍有問題，會一次後失敗的已設定的 hello 準則切換後 toohello 次要端點和唯讀模式。

Hello 第三個案例中，當執行 ping hello 主要儲存體端點再次變為無法成功，您可以觸發 hello 切換回太**primaryonly 啟動** 並繼續允許更新。

## <a name="handling-eventually-consistent-data"></a>處理最終一致的資料

RA-GRS 運作方式是從 hello 主要 toohello 次要區域複寫的交易。 此複寫程序可以確保 hello hello 次要區域中的資料將會*最終一致*。 這表示，所有 hello 主要區域中的 hello 交易最後會都出現在 hello 次要區域中，但可能會有延隔時間才會都出現，而且沒有任何的保證 hello 交易到達的 hello 相同順序中的 hello 次要區域可在其中它們當初套用 hello 主要區域中。 如果您的交易到達 hello 次要區域不按順序，您*可能*hello 服務趕上之前，請考慮您的資料不一致的狀態中的 hello 次要區域 toobe。

hello 下表顯示當您更新的員工 toomake hello 詳細資料時，可能會發生什麼情況的範例她的 hello 成員*管理員*角色。 對於此範例中的 hello 起見，這需要您更新 hello**員工**實體並更新**系統管理員角色**實體系統管理員的 hello 總數的計數。 請注意 hello 套用更新的順序 hello 次要區域中。

| <bpt id="p1">**</bpt>Time<ept id="p1">**</ept> | **交易**                                            | **複寫**                       | **上次同步處理時間** | **結果** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | 交易 A： <br> 會在主要區域中 <br> 插入員工實體 |                                   |                    | 交易 A 插入 tooprimary，<br> 但尚未複寫。 |
| T1       |                                                            | 交易 A <br> 已複寫到<br> 次要區域 | T1 | 交易 A 複寫 toosecondary。 <br>已更新上次同步處理時間。    |
| T2       | 交易 B：<br>更新<br> 主要區域中的<br> 員工實體  |                                | T1                 | 交易 B 寫入 tooprimary，<br> 但尚未複寫。  |
| T3       | 交易 C：<br> 更新 <br>administrator<br>角色實體，位於<br>primary |                    | T1                 | 交易寫入 tooprimary C<br> 但尚未複寫。  |
| *T4*     |                                                       | 交易 C <br>已複寫到<br> 次要區域 | T1         | C 的交易複寫 toosecondary。<br>無法更新 LastSyncTime，因為 <br>尚未複寫交易 B。|
| *T5*     | 從次要區域 <br>讀取實體                           |                                  | T1                 | 取得 hello 員工過時的值 <br> 因為交易 B 尚未 <br> 複寫。 取得 hello 新值<br> 的新值，因為 C<br> 已複寫。 上次同步處理時間仍然尚未<br> 更新，因為交易 B<br> 尚未複寫。 您可以說<br>系統管理員角色實體不一致， <br>因為 hello 實體日期/時間是之後 <br>hello 上次同步處理時間。 |
| *T6*     |                                                      | 交易 B<br> 已複寫到<br> 次要區域 | T6                 | *T6* - 透過 C 的所有交易都 <br>已複寫，上次同步處理時間<br> 已更新。 |

在此範例中，假設 hello 用戶端參數 tooreading 從 T5 hello 次要區域。 可順利讀取 hello**系統管理員角色**實體，在這個階段，但 hello 實體包含的系統管理員與 hello 數目不一致的 hello 計數的值**員工**實體此時標示為 hello 次要區域中的管理員。 您的用戶端可能只會顯示這個值，與 hello 風險，它是不一致的資訊。 或者，hello 用戶端無法嘗試 toodetermine 該 hello**系統管理員角色**處於可能不一致的狀態，因此 hello 更新是按順序，然後通知 hello 使用者，此事實。

toorecognize 有潛在的不一致的資料，hello 用戶端可以使用 hello hello 值*上次同步處理時間*，就可以隨時藉由查詢儲存體服務。 這會告訴您 hello 次要區域中的 hello 資料上次 hello 時間一致和時套用 hello 服務所有 hello 交易先前 toothat 點的時間。 在 hello 範例中，如上所示之後 hello 服務插入 hello,**員工**hello 次要區域中的實體，hello 上次同步處理時間設定太*T1*。 它會保持*T1*直到 hello 服務更新 hello**員工**時設定太 hello 次要區域中的實體*T6*。 如果 hello 用戶端會擷取 hello 上次同步處理時間，它會讀取位於 hello 實體*T5*，它可以比較它與 hello hello 實體上的時間戳記。 Hello hello 實體上的時間戳記必須晚於 hello 上次同步處理時間，然後 hello 實體是潛在的不一致的狀態，且您可以採取任何是 hello 適當的動作，您的應用程式。 使用此欄位必須了解當 hello 上次更新 toohello 主要已完成。

## <a name="testing"></a>測試

應用程式的行為如預期般發生可重試的錯誤時的重要 tootest 它。 例如，您需要 hello 應用程式切換 toohello 次要的 tootest 而且到唯讀模式時偵測到問題，並切換回 hello 主要區域何時可供使用一次。 toodo，您需要的方式 toosimulate 可重試錯誤，並控制在發生的頻率。

您可以使用[Fiddler](http://www.telerik.com/fiddler) toointercept 和修改指令碼中的 HTTP 回應。 此指令碼可以識別來自主要端點的回應，並變更 hello HTTP 狀態碼 tooone 該 hello 儲存體用戶端程式庫會辨識為可重試的錯誤。 這個程式碼片段會示範會攔截對 hello 回應 tooread 要求 Fiddler 指令碼的簡單範例**employeedata**資料表 tooreturn 502 狀態：

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

您無法擴充此範例 toointercept 廣泛的要求，而且只變更 hello **responseCode**上其中部分 toobetter 模擬真實世界的實例。 如需自訂 Fiddler 指令碼的詳細資訊，請參閱[修改要求或回應](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse)hello Fiddler 文件中。

如果您做了 hello 切換您的應用程式僅限 tooread 模式可設定的臨界值，它將會更容易 tootest hello 行為與非實際執行的交易量。

## <a name="next-steps"></a>後續步驟

* 如需有關讀取存取異地備援，包括如何設定 hello LastSyncTime，另一個範例，請參閱[Windows Azure 儲存體備援選項和讀取權限地理備援儲存體](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)。

* 如需完整範例，顯示如何 toomake hello hello 主要和次要端點之間來回切換，請參閱[Azure 範例-使用 RA-GRS 儲存體與 hello 斷路器模式](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs)。
