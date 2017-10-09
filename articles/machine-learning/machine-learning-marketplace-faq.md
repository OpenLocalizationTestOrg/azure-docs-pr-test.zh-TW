---
title: "aaa(deprecated) 常見問題集-發行，並使用在 Azure Marketplace 中的機器學習服務應用程式 |Microsoft 文件"
description: "（已被取代）Hello Azure Marketplace 中發佈的機器學習服務應用程式的相關常見問題集"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>（已被取代）發佈和使用 hello Azure Marketplace 中的機器學習服務應用程式： 常見問題集

> [!NOTE]
> DataMarket 和「資料服務」已進入淘汰階段，訂用帳戶將自 2017 年 3 月 31 日起淘汰並取消。 因此，這篇文章目前已過時。 
> 
> 或者，您可以發佈您的機器學習實驗 toohello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)hello 資料科學社群的 hello 權益。 如需詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)。


## <a name="questions-about-consuming-from-marketplace"></a>從 Marketplace 取用的相關問題
**1.為什麼會收到下列錯誤訊息之後我輸入的輸入 hello web 服務, 的 hello:**

**hello 要求是由後端逾時或後端錯誤所導致。hello 團隊正在調查 hello 問題。很抱歉造成您的 hello 不便。(500)**

您的輸入的參數可能不符合 toohello hello 特定 web 服務所需的格式。 請輸入的參數與此 web 服務的 hello 限制，參閱 toohello 對應文件連結 toofind hello 正確的格式。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2.複製 hello 」 瀏覽此資料集 」 頁面，並貼到另一個瀏覽器視窗中，哪些認證應該我使用 tooaccess hello 結果，及如何在看到的 hello web 服務的 hello API 連結看到它們嗎？**

您應該使用您的 Marketplace 帳戶做為 hello 使用者名稱和 hello 主要帳戶金鑰，與 hello 密碼。 可以找到 hello 主要帳戶金鑰在 hello**探索此資料集**頁面下 hello hello web 服務描述 (按一下 hello**顯示**按鈕)。 hello 結果可能會顯示 hello 瀏覽器中，或它可能還有下載，依據的瀏覽器使用。

**3.為什麼會收到下列錯誤訊息之後我輸入 hello 輸入 hello web 服務的 hello 」 瀏覽此資料集 」 頁面上, 的 hello:** 

**處理您的要求時發生未預期的錯誤。請再試一次。**

您的 web 服務的一個或多個輸入的參數可能超出 hello 長度限制時使用 hello hello marketplace 上的 web 服務**探索此資料集**頁面。 可以使用 HTTP POST 方法，再輸入長度呼叫 hello 服務。 如需範例，請參閱[範例方案，在機器學習和已發行的 tooMarketplace 使用 R](machine-learning-r-csharp-web-service-examples.md)。

**4.為何我看不 hello 「 API 總管 」 索引標籤 int hello 存放區中 hello Azure 傳統入口網站中的任何資料？** 

這是 hello Azure 傳統入口網站 Marketplace 的已知的問題。 hello 團隊正在 tooresolve 此問題。 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>透過 Azure Machine Learning 在 Marketplace 上發佈的相關問題
**1.為什麼我的 Web 服務不會重新整理標誌或影像的異動？** 

標誌和影像快取在 hello 發佈入口網站，就會在 hello 新標誌或 hello 入口網站上的映像 tooupdate too10 天。

**2.為何我的 web 服務，顯示一則錯誤訊息的服務商場 hello 「 詳細 」 索引標籤？**

連接 tooAzure 機器學習服務的服務詳細資料時，沒有已知的服務商場問題。 hello 團隊正在 tooresolve 此問題。

**3.為什麼 hello R hello Azure Machine Learning web 服務中的範例程式碼不適用於使用服務商場中的 hello web 服務？**

直接連接 tooAzure Machine Learning web 服務相較透過 hello Marketplace tooconnecting toothese web 服務時，不同 hello 驗證系統。 服務商場中的 hello 服務 OData 服務，而且您可以使用 GET 或 POST 方法的呼叫。 

**4.為何我的 web 服務的 hello 支援連結提供某些我提供不正確地更新嗎？**

hello 支援連結是全域每個 「 發行者 」、 非每個供應項目。 

**5.如何使用 Marketplace 中的批次輸入模式來發佈 Web 服務？**

hello 批次輸入的模式目前不支援在 Marketplace web 服務。

**6.使用者應連絡 tooget 說明如果我有疑問成為資料發行者，或如果我在發佈期間有問題嗎？**

請連絡 hello Azure Marketplace 小組< mailto:datamarketbd@microsoft.com >如需詳細資訊。

