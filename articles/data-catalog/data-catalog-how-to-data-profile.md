---
title: "aaaHow tooData 分析資料來源"
description: "如何 tooarticle 反白顯示 tooinclude 資料表和資料行層級資料設定檔註冊在 Azure 資料目錄中，資料來源時，以及如何 toouse 資料設定檔 toounderstand 資料來源。"
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>對資料來源進行資料分析
## <a name="introduction"></a>簡介
**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。 換句話說， **Azure 資料目錄**是協助人員相關的所有探索、 了解，以及使用資料來源，以及協助組織 tooget 其現有的資料來自多個值。 資料來源已向當**Azure 資料目錄**，它的中繼資料會複製，並以 hello 服務編製索引但 hello 劇本那里未結束。

hello**資料分析**功能**Azure 資料目錄**會檢查您的類別目錄中支援的資料來源的 hello 資料並收集統計資料，以及該資料的相關資訊。 它是簡單 tooinclude 資料資產的設定檔。 當您註冊資料資產時，選擇 [**包含資料設定檔**hello 資料來源註冊工具中。

## <a name="what-is-data-profiling"></a>什麼是資料分析
資料分析會檢查 hello hello 所註冊的資料來源中的資料，並收集統計資料，以及該資料的相關資訊。 在資料來源探索，這些統計資料可協助您判斷 hello 資料 toosolve hello 適合其商務問題。

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

hello 下列資料來源都支援程式碼剖析資料：

* SQL Server (包括 Azure SQL DB 和 Azure SQL 資料倉儲) 資料表和檢視
* Oracle 資料表和檢視
* Teradata 資料表和檢視
* Hive 資料表

在註冊資料資產時包含資料設定檔可幫助使用者回答資料來源的相關問題，包括︰

* 它可以是使用的 toosolve 我商務問題嗎？
* Hello 資料是否符合 tooparticular 標準或模式？
* 有哪些 hello 資料來源的 hello 異常狀況？
* 將此資料整合到應用程式時可能面臨哪些挑戰？

> [!NOTE]
> 您也可以加入文件 tooan 資產 toodescribe 資料無法如何整合到應用程式。 請參閱[如何 toodocument 資料來源](data-catalog-how-to-documentation.md)。
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Tooinclude 資料設定檔時登錄資料來源
它是簡單 tooinclude 您的資料來源的設定檔。 當您註冊資料來源，在 [hello**註冊物件 toobe**面板 hello 資料來源登錄的工具，請選擇**包含資料設定檔**。

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

toolearn 深入了解如何 tooregister 資料來源，請參閱[如何 tooregister 資料來源](data-catalog-how-to-register.md)和[開始使用 Azure 資料目錄](data-catalog-get-started.md)。

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>篩選包含資料設定檔的資料資產
您可以加入包含資料設定檔的 toodiscover 資料資產，`has:tableDataProfiles`或`has:columnsDataProfiles`做為其中一個搜尋詞彙。

> [!NOTE]
> 選取**包含資料設定檔**在 hello 資料來源註冊工具會包含資料表和資料行層級設定檔資訊。 不過，hello 資料目錄應用程式開發介面可讓資料資產 toobe 向只有一組所包含的設定檔資訊。
>
>

## <a name="viewing-data-profile-information"></a>檢視資料設定檔資訊
一旦您找到適合的資料來源與設定檔，您可以檢視 hello 設定檔詳細資料。 tooview hello 資料設定檔，選取的資料資產，並選擇**資料設定檔**hello 資料目錄入口網站視窗中。

![](media/data-catalog-data-profile/data-catalog-view.png)

[Azure 資料目錄]  中的資料設定檔會顯示資料表和資料行設定檔資訊，包括︰

### <a name="object-data-profile"></a>物件資料設定檔
* 資料列數目
* 資料表大小
* Hello 物件上次更新

### <a name="column-data-profile"></a>資料行資料設定檔
* 資料行資料類型
* 相異值數目
* 具有 NULL 值的資料列數目
* 資料行的最小值、最大值、平均值和標準差值

## <a name="summary"></a>摘要
資料分析提供統計資料，並註冊資料資產 toohelp 判斷 hello 適用性 hello 資料 toosolve 商務問題的相關資訊。 加上註解和記載資料來源後，資料設定檔可以讓使用者更深入了解資料。

## <a name="see-also"></a>另請參閱
* [如何 tooregister 資料來源](data-catalog-how-to-register.md)
* [開始使用 Azure 資料目錄](data-catalog-get-started.md)
