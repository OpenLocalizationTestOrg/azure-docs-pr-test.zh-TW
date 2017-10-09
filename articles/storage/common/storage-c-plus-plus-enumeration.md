---
title: "以 c + + 的儲存體用戶端程式庫 hello aaaList Azure 儲存體資源 |Microsoft 文件"
description: "了解如何 toouse hello 列出 Microsoft Azure 儲存體用戶端程式庫的應用程式開發介面對於 c + + tooenumerate 容器，blob、 佇列時，資料表和實體。"
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>以 C++ 列出 Azure 儲存體資源
列出作業是與 Azure 儲存體金鑰 toomany 開發案例。 本文說明如何 toomost 有效率地列舉使用 hello 列出應用程式開發介面的 c + + hello Microsoft Azure 儲存體用戶端程式庫中提供的 Azure 儲存體中的物件。

> [!NOTE]
> 本指南的目標 hello Azure 儲存體用戶端程式庫的 c + + 版本 2.x，可透過[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp)。
> 
> 

hello 儲存體用戶端程式庫提供各種方法 toolist 或 Azure 儲存體中的查詢物件。 本文解決 hello 下列案例：

* 列出帳戶中的容器
* 列出容器或虛擬 Blob 目錄中的 Blob
* 列出帳戶中的佇列
* 列出帳戶中的資料表
* 查詢資料表中的實體

每個方法會使用不同案例的不同多載來顯示。

## <a name="asynchronous-versus-synchronous"></a>同步與非同步
因為 c + + 的儲存體用戶端程式庫 hello 之上 hello [REST c + + 程式庫](https://github.com/Microsoft/cpprestsdk)，我們使用原本就支援非同步作業[pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html)。 例如：

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

同步作業包裝 hello 對應的非同步作業：

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

如果您正在使用多個執行緒的應用程式或服務，我們建議您使用 hello 非同步 Api 而不用直接建立執行緒 toocall hello 同步處理應用程式開發介面，會大幅影響您的效能。

## <a name="segmented-listing"></a>分段列表
hello 標尺的雲端儲存體需要分割的清單。 例如，在 Azure blob 容器中可有超過 100 萬個 Blob，或在 Azure 資料表中可有超過 10 億個實體。 這些不是理論上的數字，而是實際的客戶使用量案例。

因此，這是不可行 toolist 單一回應中的所有物件。 反而，您可以使用分頁列出物件。 每個 hello 列出應用程式開發介面有*分割*多載。

hello 分割的清單作業回應包括：

* <i>_segment</i>，其中包含 hello 的單一呼叫 toohello 列出 API 傳回的結果集。
* *continuation_token*，toohello 下一次呼叫傳遞順序 tooget hello 下一頁結果中。 當有沒有更多結果 tooreturn 時，hello 接續 token 為 null。

例如，一般呼叫 toolist 容器中的所有 blob 可能看都起來像是下列程式碼片段的 hello。 會提供 hello 程式碼我們[範例](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

請注意 hello 參數可以控制在網頁中傳回結果的 hello 數目*max_results*在 hello 多載中的每個應用程式開發介面，例如：

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

如果您未指定 hello *max_results*參數，會傳回最大值 too5000 結果的單一頁面中的 hello 預設值。

也請注意，對 Azure 資料表儲存體的查詢可能會傳回任何記錄或較少的記錄比 hello hello 值*max_results*參數所指定，即使不是空的 hello 接續 token。 其中一個原因可能是該 hello 查詢無法在五秒內完成。 只要 hello 接續 token 不是空的 hello 查詢仍應繼續執行，您的程式碼不應該假設 hello 大小的結果區段。

hello 建議的模式，在大部分情況下的撰寫程式碼已分割，藉以提供明確的清單，或查詢，進行與 hello 服務 tooeach 要求的回應方式。 特別是對於 c + + 應用程式或服務，較低層級的 hello 列出進度的控制項可以協助控制記憶體和效能。

## <a name="greedy-listing"></a>窮盡列表
舊版的 hello c + + 的儲存體用戶端程式庫 (版本 0.5.0 預覽及更早版本) 包含非分割清單應用程式開發介面的資料表和佇列，如 hello 下列範例所示：

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

這些方法已做為分段 API 的包裝函式實作。 分割清單的每個回應，hello 程式碼會附加 hello 結果 tooa 向量，並掃描 hello 完整容器之後，傳回所有結果。

這種方法可能運作時 hello 儲存體帳戶或資料表包含少數的物件。 不過，增加的 hello 物件數目，hello 所需的記憶體可能會增加無限制，因為仍在記憶體中的所有結果。 一項列出作業可能需要很長的時間，在哪一個 hello 期間呼叫端具有其進度的相關資訊。

這些窮盡列出 hello SDK 中的應用程式開發介面請勿存在於 C#、 Java 或 hello JavaScript Node.js 環境。 tooavoid hello 潛在的問題使用這些窮盡 Api，它們會在中移除版本 0.6.0 預覽。

如果您的程式碼呼叫這些窮盡 API：

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

您應修改您的程式碼 toouse hello 分割列出應用程式開發介面：

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

藉由指定 hello *max_results* hello 區段的參數，您就可以平衡要求 hello 數目與您的應用程式的記憶體使用量 toomeet 效能考量之間。

此外，如果您使用不同客層之的清單的 Api，但 hello 資料儲存在 「 窮盡 」 樣式中的本機集合，我們也強烈建議您重構您的程式碼 toohandle 仔細大規模的本機集合中儲存資料。

## <a name="lazy-listing"></a>延遲列表
雖然窮盡清單產生潛在問題，並方便如果 hello 容器中沒有太多物件。

如果您也使用 C# 或 Oracle Java Sdk，您應該熟悉 hello 可列舉的程式設計模型，它提供了延遲樣式清單，其中 hello 的特定位移的資料會只擷取在必要時。 C + + hello 迭代器為基礎的範本也會提供類似的方法。

典型的延遲列表 API (以 **list_blobs** 為例) 如下所示：

```cpp
list_blob_item_iterator list_blobs() const;
```

會使用 hello 延遲清單模式的一般程式碼片段看起來可能像這樣：

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

請注意，延遲列表僅可用於同步模式。

相較於窮盡列表，延遲列表只會在必要時提取資料。 Hello 幕後提取資料從 Azure 儲存體 hello 的下一個迭代器將移至下一個區段時，才。 因此，記憶體使用量控制界限大小，且 hello 作業將會十分快速。

延遲清單應用程式開發介面包含在 hello 儲存體用戶端程式庫的 c + + 的版本 2.2.0。

## <a name="conclusion"></a>結論
在本文中，我們討論過 c + + 應用程式開發介面清單 hello 儲存體用戶端程式庫中的各種物件的不同多的載。 toosummarize:

* 在多個執行緒的案例中，強烈建議使用非同步 API。
* 在大部分的案例中，建議使用分段列表。
* 延遲的清單是依現狀 hello 文件庫中的同步案例中的便利包裝函式。
* 窮盡清單不建議使用，並已經移除了 hello 程式庫。

## <a name="next-steps"></a>後續步驟
如需 c + + Azure 儲存體和用戶端程式庫的詳細資訊，請參閱下列資源的 hello。

* [如何 toouse 從 c + + 的 Blob 儲存體](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [如何 toouse 從 c + + 的資料表儲存體](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [如何 toouse 佇列儲存體從 c + +](../storage-c-plus-plus-how-to-use-queues.md)
* [Azure Storage Client Library for C++ API 文件。](http://azure.github.io/azure-storage-cpp/)
* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)

