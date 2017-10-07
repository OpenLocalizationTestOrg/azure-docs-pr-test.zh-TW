---
title: "aaaUsing hello Azure CDN tooaccess blob 使用透過 HTTPS 的自訂網域"
description: "了解如何使用 blob 儲存體 tooaccess toointegrate hello Azure CDN 的 blob 使用自訂網域透過 HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: 678e24a7dde5cb2f8feea177bb47c92f61035e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>使用自訂網域中的 hello Azure CDN tooaccess blob，透過 HTTPS

Azure 內容傳遞網路 (CDN) 現在支援自訂網域名稱使用 HTTPS。
您可以利用此在 HTTPS 上使用自訂網域的功能 tooaccess 儲存體 blob。 toodo 因此，您必須先 tooenable Azure CDN 的 blob 端點和對應 hello CDN tooa 自訂網域名稱。 一旦您採取下列步驟，啟用 HTTPS 的自訂網域已經過簡化透過一種單鍵啟用，完成憑證管理，以及所有的任何額外的成本 toonormal CDN 定價。

這項功能非常重要的因為它可讓您 tooprotect hello 隱私權和機密的 web 應用程式資料在傳輸過程中的資料完整性。 使用 hello SSL 通訊協定 tooserve 流量透過 HTTPS 可確保已加密資料，當傳送 hello 跨網際網路。 HTTPS 提供信任與認證，並保護您的 Web 應用程式免於攻擊。

> [!NOTE]
> 此外 tooproviding SSL 支援自訂網域名稱，hello Azure CDN 可協助您調整應用程式 toodeliver 高頻寬內容 hello 世界各地。
> toolearn 詳細資訊，請參閱[hello Azure CDN 概觀](../cdn/cdn-overview.md)。
>
>

## <a name="quick-start"></a>快速入門

這些是您自訂的 blob 儲存體端點的 hello 步驟需要的 tooenable HTTPS:

1.  [整合 Azure 儲存體帳戶與 Azure CDN](../cdn/cdn-create-a-storage-account-with-cdn.md)。
    這篇文章會引導您在 hello Azure 入口網站中建立儲存體帳戶，如果您有尚未完成操作。
2.  [對應的 Azure CDN 內容 tooa 自訂網域](../cdn/cdn-map-content-to-custom-domain.md)。
3.  [在 Azure CDN 自訂網域上啟用 HTTPS](../cdn/cdn-custom-ssl.md)。

## <a name="shared-access-signatures"></a>共用存取簽章

如果您的 blob 儲存體端點設定的 toodisallow 匿名讀取權限，您將需要 tooprovide[共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)語彙基元，在每個要求您進行 tooyour 自訂網域。 根據預設，Blob 儲存體端點不允許匿名讀取權限。 如需共用存取簽章的詳細資訊，請參閱[管理對容器與 blob 的匿名讀取權限](storage-manage-access-to-resources.md)。

Azure CDN 不會遵守任何限制加入的 toohello SAS 權杖。 例如，所有 SAS 權杖都有到期時間。 這表示內容仍然使用過期的 SAS 存取，直到該內容會清除從 hello CDN 邊緣節點。 您可以控制多久快取資料 hello CDN 上所設定的 hello 快取的回應標頭。 如需指示請參閱[在 Azure CDN 中管理 Azure 儲存體 Blob 的到期](../cdn/cdn-manage-expiration-of-blob-content.md)。

如果您要建立 hello 的多個 SAS Url 相同的 blob 端點，我們建議您開啟您的 Azure CDN 的快取的查詢字串。 這是 tooensure，每個 URL 會被視為唯一的實體。 如需詳細資訊，請參閱[使用查詢字串控制 Azure CDN 快取行為](../cdn/cdn-query-string.md)。

## <a name="http-toohttps-redirection"></a>HTTP tooHTTPS 重新導向

您可以選擇 tooredirect HTTP 流量 tooHTTPS。 這需要從 Verizon hello Azure CDN premium 供應項目的使用。 您需要[覆寫 HTTP 使用的 Azure CDN 規則引擎的行為](../cdn/cdn-rules-engine.md)下列規則：

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Cdn 的端點名稱的"是指在您設定您的 CDN 端點的 toohello 名稱。 您可以從 hello 下拉式清單中選取此值。 [來源路徑] 是指您靜態內容所在來源儲存體帳戶中的 hello 路徑。
如果您裝載單一容器中的所有靜態內容，取代 hello 名稱，該容器的 [來源路徑]。

規則深入剖析，請參閱 hello [Azure CDN 規則引擎功能](../cdn/cdn-rules-engine-reference-features.md)。

## <a name="pricing-and-billing"></a>價格和計費

當您透過 Azure CDN 存取 blob 時，您必須支付[Blob 儲存體價格](https://azure.microsoft.com/pricing/details/storage/blobs/)hello 邊緣節點與 hello 原點 （Blob 儲存） 之間的流量和[CDN 價格](https://azure.microsoft.com/pricing/details/cdn/)從 hello 邊緣節點存取的資料。

例如，假設您的儲存體帳戶在美國西部，且使用 Azure CDN 存取它。 如果有人在 hello 英國嘗試的 tooaccess hello 的其中一個 hello CDN 透過該儲存體帳戶中的 blob，Azure 會先檢查最接近該 blob hello 英國 hello 邊緣節點。 如果找到，它會存取該副本 hello blob，並會使用 CDN 定價，因為它正在存取 hello CDN 上。 如果找不到，Azure 將會複製 hello blob toohello 邊緣節點，這會導致輸出和交易費用，以指定在 hello Blob 儲存體定價，並存取 hello 邊緣節點上，而導致 CDN 計費 hello 檔案。

查看 hello 時[CDN 定價頁面](https://azure.microsoft.com/pricing/details/cdn/)，請注意，HTTPS 支援的自訂網域名稱只適用於 Azure CDN 從 Verizon 產品 （Standard 和 Premium）。

## <a name="next-steps"></a>後續步驟

[針對 Blob 儲存體端點設定自訂網域名稱](storage-custom-domain-name.md)
