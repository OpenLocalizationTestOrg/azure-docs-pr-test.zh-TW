---
title: "aaaRegister 在 Azure 資料目錄中的資料來源 |Microsoft 文件"
description: "本文章重點說明如何 tooregister 在 Azure 資料目錄，包括 hello 中繼資料欄位中的資料來源擷取登錄期間。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>在 Azure 資料目錄中註冊資料來源
## <a name="introduction"></a>簡介
Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。 換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。 hello 第一個步驟 toomaking 資料來源可透過資料目錄探索是 tooregister 該資料來源。

## <a name="register-data-sources"></a>註冊資料來源
註冊是 hello 資料來源擷取中繼資料，並複製該資料 toohello 資料目錄服務的 hello 程序。 hello 資料仍會保留它目前位於何處，而且仍在 hello hello 系統管理員控制與 hello 目前系統的原則。

tooregister 資料來源，請勿 hello 遵循：
1. 在 hello Azure 資料目錄入口網站啟動 hello 資料目錄資料的來源註冊工具。 
2. 使用登入您的工作或學校帳戶，以 hello 相同 toosign 用於 toohello 入口網站的 Azure Active Directory 認證。
3. 選取您想 tooregister hello 資料來源。

如需逐步的詳細資訊，請參閱 hello[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。

您已註冊 hello 資料來源之後，hello 目錄會追蹤其位置，而且它的中繼資料的索引。 使用者可以搜尋、 瀏覽，並探索 hello 資料來源，並使用 hello 應用程式或其選擇的工具，以使用其位置 tooconnect tooit。

## <a name="supported-data-sources"></a>支援的資料來源
請參閱[資料目錄 DSR](data-catalog-dsr.md) 以取得目前支援的資料來源清單。

## <a name="structural-metadata"></a>結構化中繼資料
當您註冊的資料來源時，hello 註冊工具會擷取您所選取的 hello 物件 hello 結構的相關資訊。 這項資訊是參照的 tooas 結構化中繼資料。

所有物件，此結構的中繼資料包括 hello 物件的位置，以便探索 hello 資料的使用者可以使用自己選擇的 hello 用戶端工具中的該資訊 tooconnect toohello 物件。 其他的結構化中繼資料包含物件名稱和類型，以及屬性/資料行名稱和資料類型。

## <a name="descriptive-metadata"></a>描述性中繼資料
此外 toohello 核心 hello 資料來源擷取的結構化中繼資料、 hello 資料來源註冊工具會擷取具描述性的中繼資料。 SQL Server Analysis Services 和 SQL Server Reporting Services，此中繼資料是來自這些服務所公開的 hello 描述屬性。 針對 SQL Server，提供使用 hello ms 值\_擷取擴充屬性的描述。 Oracle 資料庫的 hello 資料來源註冊工具擷取 hello 註解從資料行 hello 所有\_ 索引標籤\_註解的檢視。

加法 toohello 描述性中繼資料中擷取 hello 資料來源，使用者可以使用 hello 資料來源註冊工具輸入描述性的中繼資料。 使用者可以加入標記，並可以識別 hello 物件所註冊的專家。 此描述性的中繼資料是所有複製 toohello 資料目錄服務，以及 hello 結構化中繼資料。

## <a name="include-previews"></a>包含預覽
根據預設，只有中繼資料會擷取從資料來源和複製的 toohello 資料目錄服務，但是了解資料來源通常更容易時您可以檢視它所包含的 hello 資料的範例。

使用 hello 資料來源的資料目錄註冊工具，您可以包含在每個資料表和檢視已註冊的 hello 資料的快照集預覽。 如果您在註冊期間選擇 tooinclude 預覽，hello 註冊工具包括從每個資料表和檢視 too20 記錄。 此快照集會然後複製 toohello 目錄以及 hello 結構化及描述性中繼資料。

> [!NOTE]
> 含有大量資料行的寬型資料表可能會在預覽中包含少於 20 筆的記錄。
>
>

## <a name="include-data-profiles"></a>包含資料設定檔
就如同包括預覽可以搜尋資料目錄中的資料來源的使用者提供有價值的內容，包括資料設定檔可讓您更輕鬆 toounderstand 探索資料來源。

您可以藉由使用 hello 資料來源的資料目錄註冊工具，包含每個資料表和檢視已註冊的資料設定檔。 如果您選擇 tooinclude 資料設定檔在註冊期間，hello 註冊工具包含有關 hello 資料彙總統計資料中每個資料表和檢視，包括：

* 資料列的資料與大小 hello hello 物件中的 hello 數目。
* hello hello hello 資料和 hello 物件結構描述的最新的更新日期。
* null 的記錄和資料行的相異值的 hello 數目。
* hello 最小值、 最大值、 平均和標準差資料行的值。

這些統計資料會複製 toohello 目錄以及 hello 結構化及描述性中繼資料。

> [!NOTE]
> 文字和日期資料行不會包含其資料設定檔中的平均值或標準差值統計資料。
>
>

## <a name="update-registrations"></a>更新註冊
登錄資料來源可在資料目錄中可探索當您使用 hello 中繼資料及選擇性在註冊期間所擷取的預覽。 如果 hello 資料來源必須在 hello 目錄中 （例如，如果 hello 物件結構描述已變更、 原本排除的資料表應該包含在內，或您想要包含在 hello 預覽 tooupdate hello 資料），更新 toobe hello 資料來源註冊工具可以重新執行。

重新註冊已註冊的資料來源會執行合併 “upsert” 作業：將會更新現有的物件，同時建立新的物件。 透過 hello 資料目錄入口網站的使用者提供的任何中繼資料會保留。

## <a name="summary"></a>摘要
因為它會複製結構化及描述性的中繼資料從資料來源 toohello 目錄服務，登錄在資料目錄中的 hello 資料來源可讓您更輕鬆 toodiscover 的 hello 資料，並了解。 註冊 hello 資料來源之後，您可以加上註解、 管理及使用 hello 資料目錄入口網站探索。

## <a name="next-steps"></a>後續步驟
如需註冊資料來源的詳細資訊，請參閱 hello[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。
