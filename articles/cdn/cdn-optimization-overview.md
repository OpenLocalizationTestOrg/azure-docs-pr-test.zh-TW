---
title: "aaaOptimize Azure 內容傳遞，您的案例"
description: "如何 toooptimize 傳遞您針對特定案例的內容"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>最佳化您案例的 Azure 內容傳遞

傳遞內容 tooa 大型全球使用者時，很重要 tooensure hello 最佳化傳遞的內容。 hello Azure 內容傳遞網路可以最佳化 hello 傳遞經驗 hello 您擁有的內容類型為基礎。 內容可以是網站、即時串流、影片或供下載的大型檔案。 當您建立的內容傳遞網路 (CDN) 端點時，指定情節中 hello**適合**選項。 您的選擇會決定哪一個最佳化是套用的 toohello 內容傳遞從 hello CDN 端點。

最佳化的選項為 toouse 設計的最佳作法行為 tooimprove 內容傳遞的效能和更佳的原始卸載。 您案例的選擇會影響效能，藉由修改部分快取物件區塊化，和 hello 來源失敗重試原則的設定。 

本文提供各種最佳化功能概觀和使用時機。 如需有關的功能和限制的詳細資訊，請參閱 hello 個別文件的每個個別的最佳化類型。

> [!NOTE]
> 您**適合**選項可以隨著您選取的 hello 提供者。 CDN 提供者會套用不同的方式，視 hello 案例而定的增強功能。 

## <a name="provider-options"></a>提供者選項

Akamai 支援從 hello Azure 內容傳遞網路：

* 一般 Web 傳遞 

* 一般媒體串流處理

* 點播視訊媒體串流處理

* 大型檔案下載

* 動態網站加速 

hello Azure 內容傳遞網路從 Verizon 支援只有一般 web 傳遞。 它可以用於點播視訊和大型檔案下載。 您不需要 tooselect 最佳化類型。

強烈建議您測試不同的提供者 tooselect hello 最佳提供者為您的傳遞之間的效能變化。

## <a name="select-and-configure-optimization-types"></a>選取並設定最佳化類型

toocreate 新端點，會選取最符合 hello 案例的最佳化類型以及您想要 hello 端點 toodeliver 的內容類型。 **一般 web 傳遞**hello 預設選取項目。 您可以更新任何現有的 Akamai 端點在任何時間的 hello 最佳化選項。 這項變更不會干擾從 hello CDN 傳遞。 

1. 選取標準 Akamai 設定檔中的端點。

    ![端點選取範圍 ](./media/cdn-optimization-overview/01_Akamai.png)

2. 在 [設定] 下選取 [最佳化]。 然後從 hello 選取類型**適合**下拉式清單。

    ![選取最佳化和類型](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>特定案例最佳化

您可以最佳化 hello CDN 端點，其中一個 hello 下列案例。 

### <a name="general-web-delivery"></a>一般 Web 傳遞

一般 web 傳遞是 hello 最常見的最佳化選項。 它是專為一般 Web 內容最佳化所設計，例如網頁和 Web 應用程式。 此最佳化也可用於檔案和視訊下載。

一般網站包含靜態和動態的內容。 靜態內容包括影像、 JavaScript 程式庫和樣式表可以快取和傳遞 toodifferent 使用者。 動態內容是為個別的使用者個人化，例如新聞項目所量身訂做 tooa 使用者設定檔。 動態內容不是快取，因為它是唯一的 tooeach 使用者，例如購物車內容。 一般 Web 傳遞可以最佳化整個網站。 

> [!NOTE]
> 如果您使用 hello Akamai 從 Azure 內容傳遞網路，您可能想 toouse 此最佳化如果平均檔案大小小於 10 MB。 如果您的平均檔案大小大於 10 MB，請選取**大型檔案的下載**從 hello**適合**下拉式清單。

### <a name="general-media-streaming"></a>一般媒體串流處理

如果您需要 toouse hello 端點的即時資料流和 video-on-demand 串流時，我們建議一般媒體資料流最佳化。

媒體串流處理是區分大小寫的時間，因為封包抵達晚期 hello 用戶端上可能會造成降低的檢視經驗，例如經常緩衝處理的視訊內容。 媒體串流最佳化降低 hello 延遲的媒體內容傳遞，並提供使用者 smooth 串流處理體驗。 

Azure 媒體服務的客戶經常發生此狀況。 當您使用 Azure 媒體服務時，您會取得一個串流端點，可用於即時和隨選資料流處理。 此案例，客戶不需要 tooswitch tooanother 端點從即時 tooon 隨選串流其變更時。 一般媒體串流處理最佳化支援這種情況。

hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。

toolearn 進一步了解媒體串流處理最佳化，請參閱[媒體串流最佳化](cdn-media-streaming-optimization.md)。

### <a name="video-on-demand-media-streaming"></a>點播視訊媒體串流處理

點播視訊媒體串流處理最佳化會改善點播視訊串流處理內容。 如果您使用端點 video-on-demand 串流處理時，您可能想 toouse 此選項。

hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。

toolearn 進一步了解媒體串流處理最佳化，請參閱[媒體串流最佳化](cdn-media-streaming-optimization.md)。

> [!NOTE]
> Hello 端點主要是提供 video-on-demand 內容，如果使用此最佳化類型。 hello 這個最佳化與 hello 一般媒體串流最佳化之間的主要差異是 hello 連線重試逾時。hello 逾時是使用即時資料流案例更短 toowork。

### <a name="large-file-download"></a>大型檔案下載

如果您使用 hello Akamai 從 Azure 內容傳遞網路，您必須使用大於 1.8 g b 的大型檔案下載 toodeliver 檔案。 hello Verizon 從 Azure 內容傳遞網路沒有檔案下載在其一般 web 傳遞最佳化的大小限制。

如果您使用 hello Akamai 從 Azure 內容傳遞網路，下載大型檔案適合用於內容大於 10 MB。 如果您的平均檔案大小小於 10 MB，您可能想 toouse 一般 web 傳遞。 如果平均檔案大小會持續大於 10 MB，可能是更有效率的 toocreate 大型檔案的個別端點。 例如，韌體或軟體更新通常是大型檔案。

hello Azure 內容傳遞網路從 Verizon 使用 hello 一般 web 傳遞最佳化類型 toodeliver 串流處理媒體內容。

toolearn 進一步了解大型的檔案最佳化功能，請參閱[大型檔案最佳化](cdn-large-file-optimization.md)。

### <a name="dynamic-site-acceleration"></a>動態網站加速

 Akamai 和 Verizon 的內容傳遞網路設定檔都提供動態網站加速。 此最佳化牽涉到額外的費用 toouse。 如需詳細資訊，請參閱 hello 定價頁面。

動態站台加速包括 hello 延遲和動態內容的效能獲益的各種技術。 相關技術包括路由和網路最佳化、TCP 最佳化等等。 

您可以使用此最佳化 tooaccelerate web 應用程式，其中包含許多不是可快取的回應。 範例包括搜尋結果、簽出交易或即時資料。 您可以繼續靜態資料的 toouse 核心 CDN 快取的功能。 



