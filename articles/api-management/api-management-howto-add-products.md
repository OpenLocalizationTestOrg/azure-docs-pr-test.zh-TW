---
title: "aaaHow toocreate 及發佈產品在 Azure API 管理"
description: "深入了解如何 toocreate 並發行產品在 Azure API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>如何 toocreate 及發佈產品在 Azure API 管理
在 Azure API 管理中，產品包含一或多個應用程式開發介面，以及使用量配額與 hello 使用條款。 產品發行之後，開發人員可以訂閱 toohello 產品，並開始 toouse hello 產品的 Api。 hello 主題將提供指南 toocreating 產品，以加入應用程式開發介面，和發行適用於開發人員。

## <a name="create-product"> </a>建立產品
作業可加入與 hello 發行者入口網站中設定 tooan API。 tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

按一下**產品**hello 左的 toodisplay hello 上的 [hello] 功能表中**產品**頁面，然後按一下**新增產品**。

![產品][api-management-products]

![New product][api-management-add-new-product]

輸入 hello 產品的描述性名稱在 hello**名稱**欄位以及在 hello hello 產品的描述**描述**欄位。

API 管理中的產品可以是 [開放] 或 [受保護]。 受保護的產品必須是它們可以用於，開啟時的訂閱的 toobefore 不用在訂用帳戶可以使用產品。 請檢查**需要訂用帳戶**toocreate 的受保護的產品，需要訂用帳戶。 這是 hello 預設設定。

請檢查**需要訂閱核准**如果您想要系統管理員 tooreview 並接受或拒絕的訂閱嘗試 toothis 產品。 如果 hello 方塊未選取，訂閱嘗試將會自動核准。 如需有關訂閱的詳細資訊，請參閱[檢視 「 訂閱者 」 tooa 產品][View subscribers tooa product]。

tooallow 開發人員帳戶 toosubscribe 多次 toohello 產品，請檢查 hello**允許多個訂閱**核取方塊。 如果未核取此方塊，每個開發人員帳戶可以訂閱一次 toohello 產品。

![無限制的多項訂閱][api-management-unlimited-multiple-subscriptions]

toolimit hello 計數的多個同時進行的訂閱，檢查 hello**同時訂閱的數目限制**核取方塊，然後輸入 hello 訂用帳戶限制。 在下列範例的 hello，同時訂閱是有限的 toofour 每個開發人員帳戶。

![四個多項訂閱][api-management-four-multiple-subscriptions]

一旦設定所有新的產品選項，按一下**儲存**toocreate hello 新產品。

![產品][api-management-products-page]

> 根據預設，新的產品為未發行，而是可見的唯一 toohello**管理員**群組。
> 
> 

tooconfigure 產品中，按一下 hello 中的 hello 產品名稱**產品** 索引標籤。

## <a name="add-apis"></a>新增應用程式開發介面 tooa 產品
hello**產品**頁面包含四個連結的組態：**摘要**，**設定**，**可視性**，和**訂閱者**。 hello**摘要** 索引標籤是您可以用它來新增應用程式開發介面和發行，或取消發行的產品。

![摘要][api-management-new-product-summary]

發行您的產品之前您需要 tooadd 一或多個應用程式開發介面。 toodo 此，依序按一下**新增應用程式開發介面 tooproduct**。

![Add APIs][api-management-add-apis-to-product]

選取 hello 預期應用程式開發介面和按一下**儲存**。

## <a name="add-description"></a>加入描述性資訊 tooa 產品
hello**設定**索引標籤可讓您 tooprovide hello 產品，例如其用途、 hello 應用程式開發介面，它提供的存取權，以及其他有用的資訊有關的詳細資訊。 hello 內容呼叫 hello 應用程式開發介面，且可以寫入純文字或 HTML 標記中的 hello 開發人員為目標。

![Product settings][api-management-product-settings]

請檢查**需要訂用帳戶**toocreate 受保護的產品需要使用，或清除訂閱 toobe hello 核取方塊 toocreate 已開啟的產品可以呼叫且不用訂用帳戶。

選取**需要訂閱核准**toomanually 如果您想要核准所有產品的訂閱要求。 依預設會自動同意所有產品訂閱。

tooallow 開發人員帳戶 toosubscribe 多次 toohello 產品，請檢查 hello**允許多個訂閱**核取方塊，並選擇性地指定限制。 如果未核取此方塊，每個開發人員帳戶可以訂閱一次 toohello 產品。

選擇性地填入 hello**使用條款**欄位描述的 「 訂閱者 」 必須接受訂單 toouse hello 產品中的 hello 產品 hello 使用條款。

## <a name="publish-product"> </a>發行產品
在呼叫 hello 應用程式開發介面的產品前，必須先發佈 hello 產品。 在 hello**摘要**hello 產品的索引標籤上，按一下 **發行**，然後按一下 **是，將它發行**tooconfirm。 按一下 toomake 先前發行的產品私用**取消發行**。

![Publish product][api-management-publish-product]

## <a name="make-visible"></a>使產品可見 toodevelopers
hello**可視性**索引標籤可讓您 toochoose 哪些角色可以 toosee hello 產品在 hello 開發人員入口網站並訂閱 toohello 產品。

![Product visibility][api-management-product-visiblity]

tooenable 或停用的群組中的 hello 開發人員的產品的可見性檢查或取消核取 hello hello 群組旁邊的核取方塊，然後按一下**儲存**。

> 如需詳細資訊，請參閱[toocreate 並用群組 toomanage 開發人員帳戶在 Azure API 管理的如何][How toocreate and use groups toomanage developer accounts in Azure API Management]。
> 
> 

## <a name="view-subscribers"></a>檢視 「 訂閱者 」 tooa 產品
hello **「 訂閱者 」**索引標籤會列出 hello 開發人員已訂閱 toohello 產品。 hello 詳細資料和設定每位開發人員可以檢視上 hello 開發人員的名稱即可。 在此範例中沒有開發人員尚未訂閱 toohello 產品。

![開發人員][api-management-developer-list]

## <a name="next-steps"> </a>後續步驟
一次 hello 所需的應用程式開發介面會加入與 hello 產品發行時，開發人員可以訂閱 toohello 產品，並開始 toocall hello 應用程式開發介面。 如需有關這些項目和進階產品組態的示範教學課程，請參閱 [如何在 Azure API 管理中建立和設定進階產品設定][How create and configure advanced product settings in Azure API Management]。

如需有關使用產品的詳細資訊，請參閱下列視訊 hello。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
