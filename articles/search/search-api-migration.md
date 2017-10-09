---
title: "aaaUpgrading toohello Azure 搜尋服務 REST API 2016-09-01 版 |Microsoft 文件"
description: "升級 toohello Azure 搜尋服務 REST API 2016-09-01 版"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>升級 toohello Azure 搜尋服務 REST API 2016-09-01 版
如果您使用版本 2015年-02-28 或 2015年-02-28-預覽的 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx)，本文將協助您升級您的應用程式 toouse hello 下一步正式推出的 API 版本，2016年-09-01。

版本 2016年-09-01 的 hello REST API 包含從舊版的某些變更。 這些是大部分具有回溯相容性，因此變更程式碼應該只需要最少的工作 (視您之前使用的版本而定)。 請參閱[步驟 tooupgrade](#UpgradeSteps)如需有關指示 toochange 您程式碼 toouse hello 新的 API 版本。

> [!NOTE]
> 您的 Azure 搜尋服務執行個體支援多個 REST API 版本，包括 hello 最新版本。 您可以繼續 toouse 版本時，它不會再 hello 最新的其中一個，但我們建議您移轉您的程式碼 toouse hello 最新版本。

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>版本 2016-09-01 的新功能
版本 2016年-09-01 是 hello 的 hello 第二個版本 Azure 搜尋服務 REST API。 這個 API 版本的新功能包括︰

* [自訂分析器](https://aka.ms/customanalyzers)，可讓您 tootake hello 程序，將文字轉換為可編索引且可搜尋的語彙基元的控制。
* [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和[Azure 資料表儲存體](search-howto-indexing-azure-tables.md)索引子，可讓您 tooeasily 資料匯入 Azure 儲存體從 Azure 搜尋根據排程或隨。
* [欄位對應](search-indexer-field-mappings.md)，可讓您 toocustomize 如何索引子將資料匯入 Azure 搜尋。
* Etag，可讓您的索引、 索引子和資料來源的 tooupdate hello 定義並行安全的方式。 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>步驟 tooupgrade
如果您要升級版本 2015年-02-28，可能不會有 toomake 任何變更 tooyour 以外的程式碼，toochange hello 版本號碼。 hello 唯一情況下，您可能需要 toochange 程式碼時，就：

* 您的程式碼在 API 回應中傳回無法辨認的屬性時失敗。 您的應用程式預設應該會略過不了解的屬性。
* 您的程式碼仍然存在 API 要求，而且會嘗試 tooresend 它們 toohello 新 API 版本。 比方說，這可能是因為您的應用程式保存 hello 搜尋 API 所傳回的接續 token (如需詳細資訊，請尋找`@search.nextPageParameters`在 hello[搜尋 API 參考](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1))。

若下列情況下套用 tooyou，則您可能需要 toochange 您的程式碼據此。 否則，除非您想使用 hello toostart 任何變更應該是必要[新功能](#WhatsNew)的 2016年-09-01 版。

如果您要升級的版本 2015年-02-28-預覽，也適用於上述 hello，但您也必須注意，某些預覽功能不是在 2016年-09-01 版可用：

* Azure Blob 儲存體索引子支援包含 JSON 陣列中的 CSV 檔案和 Blob。
* 同義字
* "More like this" 查詢

如果您的程式碼會使用這些功能，就能 tooupgrade too2016-09-01，不會移除它們的使用方式。

> [!IMPORTANT]
> 請記住，預覽 API 是針對測試與評估，不應該用於生產環境。
> 
> 

## <a name="conclusion"></a>結論
如果您需要更多詳細資料上使用 hello Azure 搜尋服務 REST API，請參閱 hello 最近更新[API 參考](https://msdn.microsoft.com/library/azure/dn798935.aspx)MSDN 上。

歡迎您提供 Azure 搜尋服務的意見反應。 如果您遇到問題，則可以免費 tooask 我們 hello 的說明[Azure 搜尋 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)或[StackOverflow](http://stackoverflow.com/)。 如果您正在詢問問題有關 Azure 搜尋 StackOverflow，請確定 tootag 它與`azure-search`。

感謝您使用 Azure 搜尋服務！

