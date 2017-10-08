---
title: "aaaAzure 資料目錄術語 |Microsoft 文件"
description: "本文章提供簡介 tooconcepts 和使用 Azure 資料目錄文件中的詞彙。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Azure 資料目錄術語
## <a name="catalog"></a>目錄
hello Azure 資料目錄是以雲端為基礎的中繼資料儲存機制中的資料來源和資料資產都可以註冊。 hello 類別目錄做為擷取自資料來源的結構化中繼資料和使用者所加入的描述性中繼資料的中央存放位置。

## <a name="data-source"></a>資料來源
資料來源是管理資料資產的系統或容器。 範例包括 SQL Server 資料庫、Oracle 資料庫、SQL Server Analysis Services 資料庫 (表格式或多維度) 和 SQL Server Reporting Services 伺服器。

## <a name="data-asset"></a>資料資產
資料資產是內含的資料來源，可以向 hello 目錄物件。 範例包括 SQL Server 資料表和檢視、Oracle 資料表和檢視、SQL Server Analysis Services 量值、維度和 KPI，以及 SQL Server Reporting Services 報表。

## <a name="data-asset-location"></a>資料資產位置
hello 目錄會將儲存的資料來源或資料資產，可以使用的 tooconnect toohello hello 位置來源使用的用戶端應用程式。 hello 格式和 hello 位置的詳細資料隨著 hello 資料來源類型。 比方說，SQL Server 資料表可以透過其四段名稱來識別 – 伺服器名稱、資料庫名稱、結構描述名稱、物件名稱 – 而 SQL Server Reporting Services 報表可以透過其 URL 來識別。

## <a name="structural-metadata"></a>結構化中繼資料
結構化中繼資料是從說明 hello 結構的資料資產的資料來源擷取的 hello 中繼資料。 這包括 hello 資產位置、 其物件名稱和類型，以及其他特定類型的特性。 例如，hello 結構化中繼資料資料表和檢視表包含 hello 名稱和 hello 物件資料行的資料類型。

## <a name="descriptive-metadata"></a>描述性中繼資料
描述性的中繼資料是描述 hello 用途或目的資料資產的中繼資料。 通常描述性的中繼資料已加入之目錄的使用者使用 hello Azure 資料目錄入口網站，但它也可從擷取 hello 資料來源登錄期間。 例如，hello Azure 資料目錄註冊工具將會擷取描述從 hello 描述屬性在 SQL Server Analysis Services 和 SQL Server Reporting Services，以及從 hello [ms_description 擴充屬性](https://technet.microsoft.com/library/ms190243.aspx)在 SQL Server 資料庫中，如果這些屬性已填入值。

## <a name="request-access"></a>要求存取
資料資產的描述性中繼資料可以包含 toorequest toohello 資料資產或資料來源的存取方式的詳細資訊。 這項資訊會看見 hello 資料資產的位置，並可以包含一或多個 hello 下列選項：

* hello hello 使用者或小組負責授與存取 toohello 資料來源的電子郵件地址。
* hello hello URL 記載的使用者必須遵循 toogain access toohello 資料來源的程序。
* hello 的身分識別和存取管理工具 (例如 Microsoft Identity Manager) 可以使用的 toogain access toohello 資料來源的 URL。
* 任意文字項目，描述使用者可以獲得存取 toohello 資料來源的方式。

## <a name="preview"></a>預覽
在 Azure 資料目錄中的預覽是 too20 記錄可以在註冊期間，從 hello 資料來源中擷取和儲存在 hello 與 hello 資料資產中繼資料的目錄中的快照。 hello 預覽可協助使用者探索資料資產深入了解其功能與用途。 換句話說，查看範例資料可以比看到剛才 hello 資料行名稱和資料類型更有價值。
預覽只支援資料表和檢視表，而必須明確選取的 hello 使用者在註冊期間。

## <a name="data-profile"></a>資料設定檔
在 Azure 資料目錄中的資料設定檔是有關已註冊的資料資產可以在註冊期間，從 hello 資料來源中擷取和儲存在 hello 與 hello 資料資產中繼資料的類別目錄資料表層級和資料行層級中繼資料的快照集。 hello 資料設定檔可協助使用者探索資料資產深入了解其功能與用途。 類似 toopreviews，資料設定檔必須明確選取的 hello 使用者在註冊期間。

> [!NOTE]
> 擷取的資料設定檔可以是昂貴的作業，大型資料表和檢視表，而且可能會大幅增加 hello 所需時間 tooregister 資料來源。
>
>

## <a name="user-perspective"></a>使用者觀點
在 Azure 資料目錄中，任何使用者都可以為已註冊的資料資產提供描述性中繼資料。 每個使用者擁有 hello 資料和其使用不同的檢視方塊。 例如，hello 負責在伺服器的系統管理員可能會提供其服務等級協定 (SLA) 的備份時間範圍; hello 詳細資料資料管理人可能提供連結 toodocumentation hello 的商務處理 hello 資料支援。而且分析師可能提供 hello 條款最相關的 tooother 分析師，而且它可以是最有價值 toothose 使用者需要 toodiscover 及了解 hello 資料中的描述。

每個這些檢視方塊是原本就相當重要，而且與 Azure 資料目錄每一位使用者可以提供是有意義的 toothem，而所有的使用者可以使用該資訊 toounderstand hello 資料和其用途的 hello 資訊。

## <a name="expert"></a>專家
專家是指公認對資料資產有其獨特「專家」觀點的使用者。 任何使用者都可以將自己或其他使用者加入成為資產的專家。 被列為專家並未傳達任何額外的權限，在 Azure 資料目錄。它可讓使用者 tooeasily 找出這些檢閱資產的描述性中繼資料時是最有可能 toobe 有用的檢視方塊。

## <a name="owner"></a>擁有者
擁有者是具有額外權限來管理 Azure 資料目錄中的資料資產的使用者。 使用者可以取得已註冊的資料資產的擁有權，而擁有者可以加入其他使用者成為共同擁有者。 如需詳細資訊，請參閱[如何 toomanage 資料資產](data-catalog-how-to-manage.md)  

> [!NOTE]
> 擁有權和管理都只能在 hello 標準版本的 Azure 資料目錄。
>
>

## <a name="registration"></a>註冊
註冊是從資料來源擷取資料資產中繼資料，並複製它 toohello Azure 資料目錄服務的 hello 動作。 然後就可以加註和探索已註冊的資料資產。

## <a name="see-also"></a>另請參閱
* [什麼是 Azure 資料目錄？](data-catalog-what-is-data-catalog.md) -這篇文章提供 hello Azure 資料目錄服務、 hello 值提供，以及它所支援的 hello 案例的概觀。
* [開始使用 Azure 資料目錄](data-catalog-get-started.md)-本文章提供端對端教學課程中，為您示範如何 toouse Azure 資料目錄的資料來源搜索。  
