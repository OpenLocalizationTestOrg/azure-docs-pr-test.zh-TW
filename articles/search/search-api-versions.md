---
title: "aaaAPI 版本的 Azure 搜尋 |Microsoft 文件"
description: "Azure 搜尋 REST Api 和 hello 的用戶端程式庫中 hello.NET SDK 版本原則。"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Azure 搜尋服務中的 API 版本
「Azure 搜尋服務」會定期推出功能更新。 有時候，但不是一定這些更新會需要我們 toopublish 我們 API toopreserve 回溯相容性的新版本。 發行新版本可讓您 toocontrol 何時及如何整合您的程式碼中搜尋服務更新。

規則，我們嘗試 toopublish 新版本才有必要，因為它可能涉及一些努力 tooupgrade 您程式碼 toouse 新 API 版本。 如果我們需要 toochange hello API 回溯相容性方式中的某些層面，我們只會發行新版本。 因為修正 tooexisting 功能，或因為變更現有應用程式開發介面的介面區的新功能，就可能發生此情況。

我們會遵循相同的 SDK 更新規則的 hello。 hello Azure 搜尋 SDK 遵循 hello[語意版本設定](http://semver.org/)規則，這表示它的版本有三個部分： 主要和次要、 組建編號 (例如，1.1.0)。 我們將會發行新的主要版本的 hello SDK 只在發生中斷回溯相容性的變更。 非中斷功能更新，我們會增加 hello 次要版本，對於 bug 修正我們只會增加 hello 組建版本。

> [!NOTE]
> 您的 Azure 搜尋服務執行個體支援多個 REST API 版本，包括 hello 最新版本。 您可以繼續 toouse 版本時，它不會再 hello 最新的其中一個，但我們建議您移轉您的程式碼 toouse hello 最新版本。 當使用 hello REST API，您必須指定 hello API 版本 hello api-version 參數透過每個要求中。 當使用 hello.NET SDK，hello 您所使用的 SDK hello 版本會決定 hello 對應 hello REST API 的版本。 如果您使用較舊的 SDK，您可以繼續 toorun 未變更該程式碼即使 hello 服務升級的 toosupport 較新的 API 版本。

## <a name="snapshot-of-current-versions"></a>目前版本的快照
以下是目前版本的所有程式設計介面 tooAzure 搜尋 hello 的快照集。

| 介面 | 最新主要版本 | 狀態 |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |正式推出，2016 年 11 月發行 |
| [.NET SDK 預覽版](https://aka.ms/search-sdk-preview) |2.0 預覽版 |預覽版，2016 年 8 月發行 |
| [服務 REST API](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |正式推出 |
| [服務 REST API (預覽)](search-api-2015-02-28-preview.md) |2015-02-28-Preview |預覽 |
| [.NET 管理 SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |正式推出 |
| [管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |正式推出 |

Hello REST Api，包括 hello`api-version`每次呼叫是必要。 這使得輕鬆 tootarget 特定版本，例如預覽應用程式開發介面。 hello 下列範例說明如何 hello`api-version`參數會指定：

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> 雖然每個要求都有`api-version`，我們建議您改用 hello 相同版本的所有 API 要求。 特別是當新的 API 版本引入舊版本無法辨識的屬性或作業時更建議您這樣做。 混合的 API 版本可能會有非預期的結果，應該予以避免。
>
> hello 服務 REST API 和管理 REST API 會各自的版本。 版本號碼如有類似，純屬巧合。

正式推出 （或 GA） Api 可以用在生產環境中，而且是主體 tooAzure 服務等級協定。 預覽版本具有不一定已移轉的 tooa GA 版本的實驗性功能。 **我們強烈建議您避免在實際執行的應用程式中使用預覽 API。**

## <a name="about-preview-and-generally-available-versions"></a>關於預覽與正式推出版本
Azure 搜尋一律預先釋放透過 hello REST API 的實驗性功能第一次，然後透過 hello.NET SDK 的發行前版本。

預覽功能並不保證 toobe 移轉 tooa GA 版本。 在 GA 版本中的功能會被視為穩定，而且不像是 toochange hello 例外狀況的小型的回溯相容性修正和增強功能，而預覽功能可供測試和實驗，以收集意見反應 hello 目標功能設計和實作。

不過，由於主旨 toochange 是預覽功能，我們建議您不要撰寫相依性，不需要預覽版本的實際執行程式碼。 如果您使用較舊的預覽版本，我們建議您移轉 toohello 上市 (GA) 版本。

Hello.NET SDK： 進行程式碼移轉的指引，請參閱[升級 hello.NET SDK](search-dotnet-sdk-migration.md)。

一般可用性意指 Azure 搜尋現在低於 hello 服務等級協定 (SLA)。 hello SLA，請參閱[Azure 搜尋服務等級協定](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。
