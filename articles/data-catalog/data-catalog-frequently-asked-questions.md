---
title: "aaaAzure 常見問題集的資料目錄 |Microsoft 文件"
description: "與 Azure 資料目錄相關的常見問題集，包括資料來源探索、註解和管理功能。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Azure 資料目錄的常見問題集
本文章提供答案 toofrequently 詢問問題相關 toohello Azure 資料目錄服務。

## <a name="what-is-azure-data-catalog"></a>什麼是 Azure 資料目錄？
資料目錄是全面管理的雲端服務，託管在 Microsoft Azure 中，可作為企業資料來源的註冊系統和探索系統。 任何使用者，從分析師 toodata 科學家和開發人員，可以使用資料目錄來註冊、 探索、 了解，及取用資料來源。

## <a name="what-customer-challenges-does-it-solve"></a>它解決了哪些客戶面臨的挑戰？
資料類別目錄位址 hello 挑戰的探索資料來源和 「 暗色調資料 」，如此使用者可以探索及了解企業資料來源。

## <a name="what-are-its-target-audiences"></a>其目標對象為何？
資料目錄的設計目標為技術性和非技術性使用者，包括：

* 資料開發人員和商務智慧和分析的專業人員： 人員負責產生資料與分析資料的其他人 tooconsume 內容。
* 資料管理人： 資料、 其意義和方式想要使用的 toobe 有 hello hello 認知的人。
* 資料取用者： 人員需要 toobe 無法 tooeasily 探索、 了解，以及需要 toodo 他們的工作，使用自己選擇的 hello 工具 toohello 資料連接的人員。
* 中央 IT： 人員需要 toomake 數百個資料來源的可探索的商務使用者，和一段資料的使用方式，以及由誰需要 toomaintain 監督人員。

## <a name="what-is-its-availability-by-region"></a>其依區域的可用性為何？
資料目錄服務是目前已提供下列資料中心的 hello:

* 美國西部
* 美國東部
* 西歐
* 北歐
* 澳洲東部
* 東南亞

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>什麼是其上的資料資產的 hello 數目的限制？
hello 免費版本的資料目錄是有限的 too5，000 註冊的資料資產。

向上 too100 hello 標準版本的資料類別目錄支援，000 註冊資料資產。

## <a name="what-are-its-supported-data-source-and-asset-types"></a>其支援的資料來源和資產類型為何？
請參閱[資料目錄 DSR](data-catalog-dsr.md) 以取得目前支援的資料來源清單。

## <a name="how-do-i-request-support-for-another-data-source"></a>如何要求另一個資料來源的支援？
toosubmit 功能要求和其他意見反應，請移 toohello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。

## <a name="how-do-i-get-started-with-data-catalog"></a>如何開始使用資料目錄？
hello 最佳方式 tooget 移過啟動是[開始使用資料目錄](data-catalog-get-started.md)。 本文是 hello 服務中的 hello 功能的端對端概觀。

## <a name="how-do-i-register-my-data"></a>如何註冊我的資料？
tooregister 資料目錄中的資料：
1. 在 hello Azure 資料目錄入口網站中 hello**發行**區域中，開始 hello Azure 資料目錄註冊工具。 
2. 在 hello 資料目錄發行應用程式，使用登入 hello 相同認證，您會使用 tooaccess hello 資料目錄入口網站。
3. 選取 hello 資料來源和您想 tooregister hello 特定資產。

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>從已註冊的資料資產中會擷取哪些屬性？
hello 特定屬性不同於資料來源 toodata 來源，但一般而言，hello 資料目錄發行服務會擷取下列資訊的 hello:

* 資產名稱
* 資產類型
* 資產描述
* 屬性/資料行名稱
* 屬性/資料行資料類型
* 屬性/資料行描述

> [!IMPORTANT]
> 以資料目錄註冊資料資產不會移動或複製資料 toohello 雲端。 註冊資產從資料來源複本 hello 資產的中繼資料 tooAzure，但是 hello 資料會保留在 hello 現有資料來源位置。 hello 例外狀況 toothis 規則是如果您選擇 tooupload 預覽記錄或資料設定檔時登錄 hello 資產。 包含預覽，向上 too20 記錄會從每個資產複製並儲存為資料目錄中的快照集。 包含資料設定檔，是計算並 hello 中繼資料儲存在 hello 類別目錄中包含彙總資訊。 彙總的資訊可以包括 hello 資料表的大小，hello 每個資料行或 hello 最小值，最大值及平均值資料行的 null 值的百分比。 
>
>

> [!NOTE]
> 如有第一級的 SQL Server Analysis Services 資料來源的**描述**hello 發行應用程式擷取該屬性值的資料目錄 屬性中。 SQL Server 關聯式資料庫，其中缺少第一級**描述**hello 資料目錄發行應用程式 屬性，可從 hello 擷取 hello 值**ms_description**擴充屬性物件和資料行。 如需詳細資訊，請參閱[使用資料庫物件的擴充屬性](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx)。
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>多久應該花費 hello 目錄中的新註冊的資產 tooappear？
以資料目錄註冊資產之後，可能有一段 5 too10 秒才會出現在 hello 資料目錄入口網站中。

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>如何加上註解和已註冊的資料資產的 my 擴充 hello 中繼資料？
hello 最簡單方式 tooprovide 中繼資料的已註冊的資產是 tooselect hello 資料目錄入口網站中的 hello 資產和 hello 選物件然後輸入 hello 屬性 窗格或結構描述 窗格中的 hello 值。

您也可以提供一些中繼資料，例如專家和標記，在 hello 註冊程序。 您在 hello 資料目錄發行服務中提供的 hello 值適用於 tooall 當時所註冊的資產。 tooview hello 最近其他註解中，選取 hello hello 入口網站中註冊物件**檢視入口網站**hello 的 hello 資料目錄發行應用程式的最後一個畫面上的按鈕。

## <a name="how-do-i-delete-my-registered-data-objects"></a>如何刪除我已註冊的資料物件？
您可以從資料目錄刪除物件，在 hello 入口網站中選取 hello 物件，然後按一下hello**刪除** 按鈕。 移除 hello 物件從資料目錄移除它的中繼資料，但不會影響 hello 基礎資料來源。

## <a name="what-is-an-expert"></a>什麼是專家？
專家是指對資料物件具有獨特見解的人。 一個物件可能有多個專家。 專家不需要 toobe hello 「 擁有者 」 物件，但只是知道如何 hello 資料，應該使用的人。

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>如何共用資訊與 hello 資料目錄小組如果我在遇到問題？
tooreport 問題共用的詳細資訊，並詢問的問題，請移 toohello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>沒有 hello 與感興趣的其他資料來源的類別目錄工作嗎？
我們正積極新增更多的資料來源 tooData 類別目錄。 如果您想 toosee 支援特定資料來源時，建議它 （或如果已建議語音您的支援人員） 根據移 toohello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>如何為 Azure 資料目錄相關 toohello 資料目錄，在 Power BI for Office 365 嗎？
您可以將 Azure 資料目錄視為 hello Power BI 中的資料目錄的進化。 Spring 2017，Azure 資料目錄為使用的 tooenable hello 共用及探索 Excel 2016 中的查詢和 Power Query for Excel。 在 Excel 中的資料類別目錄功能是可用 toousers 與 Power BI Pro 授權。

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>權限的執行需要 tooregister 資產以資料目錄嗎？
toorun hello 資料目錄註冊工具，您需要 hello 可讓您從 hello 來源 tooread hello 中繼資料的資料來源的權限。 tooalso 包括預覽，您必須具有權限可讓您 tooread hello 物件所註冊的 hello 資料中。

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>資料目錄也會支援內部部署嗎？
資料目錄是可以使用雲端和內部部署資料來源 toodeliver 資料來源探索混合式雲端服務。 目前沒有計劃 hello 執行內部部署的資料目錄服務的版本。

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>可以從 hello 註冊的資料來源擷取更多或更豐富的中繼資料嗎？
我們正積極 tooexpand hello 功能的資料目錄。 如果您想從 hello 資料來源中擷取登錄期間 toohave 其他中繼資料，建議 （或如果已建議投票） 在 hello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。 在 hello 未來，我們將允許 tooadd 新資料來源類型擴充性 API 透過第三個合作對象。

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>以便只有特定人員可以探索它們如何限制 hello 的已註冊的資料資產的可見性？
選取 hello 資料資產中 hello 資料目錄，然後按一下hello **Take Ownership**  按鈕。 在資料目錄中的資料資產的擁有者可以變更 hello 可見性設定 tooeither 允許所有使用者 toodiscover hello 擁有資產，或限制可視性 toospecific 使用者。

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>如何使 hello 資料來源中的變更會反映在 hello 類別目錄更新資料資產的 hello 註冊？
tooupdate hello hello 類別目錄中已註冊的資料資產中繼資料時，只需重新註冊 hello 包含 hello 資產的資料來源。 Hello 資料來源中的任何變更，例如資料行要加入或移除資料表或檢視表，會更新在 hello 目錄中，但使用者提供的任何註釋會保留。

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>這裡沒有回答我的問題。 可以在何處尋求解答？
移 toohello [Azure 資料目錄論壇](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409)。 那裡提出的問題會在這裡找到答案。
