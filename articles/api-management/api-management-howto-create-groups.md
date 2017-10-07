---
title: "使用 Azure API 管理中的群組 aaaManage 開發人員帳戶 |Microsoft 文件"
description: "了解如何 toomanage 開發人員帳戶使用 Azure API 管理中的群組"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>如何 toocreate 並用群組 toomanage 開發人員帳戶在 Azure API 管理
在 API 管理中，群組是產品 toodevelopers 使用的 toomanage hello 可見性。 產品為第一個提出的可見 toogroups，而這些群組中的開發人員可以檢視，然後訂閱 hello 群組相關聯的 toohello 產品。 

API 管理有下列不可變群組 hello。

* **管理員** - Azure 訂用帳戶管理員是此群組的成員。 系統管理員管理 API 管理服務執行個體，建立 hello Api、 操作及開發人員所使用的產品。
* **開發人員** - 已驗證開發人員入口網站使用者屬於此群組。 開發人員會使用您的應用程式開發介面建置應用程式的 hello 客戶。 開發人員會授與存取 toohello 開發人員入口網站，並建置呼叫 hello 作業的應用程式開發介面的應用程式。
* **來賓**-未經驗證的開發人員入口網站的使用者，例如造訪 hello 開發人員入口網站的 API 管理執行個體都會歸類到此群組的潛在客戶。 它們可以被授與特定的唯讀存取，例如 hello 能力 tooview 應用程式開發介面，但不是呼叫它們。

在加法 toothese 系統群組中，系統管理員可以建立自訂群組或[運用在相關聯的 Azure Active Directory 租用戶中的外部群組][leverage external groups in associated Azure Active Directory tenants]。 自訂和外部群組可一起提供開發人員的可見性的系統群組，以及存取 tooAPI 產品。 例如，您可以建立一個自訂群組具有特定關係的開發人員夥伴組織，並允許它們存取 toohello Api 從產品，其中包含相關的 Api。 使用者可以是多個群組的成員。

本指南說明 API 管理執行個體的管理員如何加入新的群組，並將這些群組與產品和開發人員建立關聯。

> [!NOTE]
> 此外 toocreating 和管理群組的 hello 發行者入口網站，您可以建立及管理群組使用 hello API 管理 REST API[群組](https://msdn.microsoft.com/library/azure/dn776329.aspx)實體。
> 
> 

## <a name="create-group"> </a>建立群組
toocreate 新的群組，請按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。 這會帶您 toohello API 管理發行者入口網站。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

按一下**群組**從 hello **API 管理**hello 左、，然後按一下功能表**加入群組**。

![Add new group][api-management-add-group]

輸入 hello 群組和選擇性描述，唯一的名稱，然後按一下**儲存**。

![Add new group][api-management-add-group-window]

hello 新群組隨即顯示在 hello 群組 索引標籤 tooedit hello**名稱**或**描述**hello 群組中，按一下 hello hello 清單中的 hello 群組的名稱。 toodelete hello 群組中，按一下 **刪除**。

![Group added][api-management-new-group]

既然 hello 建立群組時，它可以是產品和開發人員相關聯。

## <a name="associate-group-product"> </a>將群組與產品建立關聯
tooassociate 群組與產品中，按一下**產品**從 hello **API 管理**hello 功能表左、，然後按一下hello hello 所需的產品名稱。

![Set visibility][api-management-add-group-to-product]

選取 hello**可視性**tooadd 索引標籤和群組，以及 hello 產品 tooview hello 目前群組中移除。 tooadd 或移除群組中，選取，或取消選取 hello 核取方塊，針對 hello 需要群組，然後按一下**儲存**。

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd Azure Active Directory 群組，請參閱[如何 tooauthorize 開發人員帳戶使用 Azure Active Directory 在 Azure API 管理](api-management-howto-aad.md)。
> 
> 從 hello tooconfigure 群組**可視性**產品的索引標籤上，按一下 **管理群組**。
> 
> 

與群組相關聯的產品之後，該群組中的開發人員就可以檢視和訂閱 toohello 產品。

## <a name="associate-group-developer"> </a>將群組與開發人員建立關聯
與開發人員，tooassociate 群組按一下**使用者**從 hello **API 管理**hello 左、，然後再 hello 開發人員旁邊的核取 hello 方塊功能表想 tooassociate 與群組。

![新增開發人員 toogroup][api-management-add-group-to-developer]

一旦 hello 需要開發人員簽入，請按一下 hello 所需的群組中 hello**新增 tooGroup**下拉式清單。 開發人員可以從群組移除使用 hello**從群組移除**下拉式清單。 

![開發人員][api-management-add-group-to-developer-saved]

Hello 開發人員和 hello 群組之間加入 hello 關聯後，可以檢視在 hello**使用者** 索引標籤。

## <a name="next-steps"> </a>後續步驟
* 一旦開發人員新增 tooa 群組，也可以檢視和訂閱與該群組相關聯的 toohello 產品。 如需詳細資訊，請參閱 [如何在 Azure API 管理中建立和發佈產品][How create and publish a product in Azure API Management]。
* 此外 toocreating 和管理群組的 hello 發行者入口網站，您可以建立及管理群組使用 hello API 管理 REST API[群組](https://msdn.microsoft.com/library/azure/dn776329.aspx)實體。

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
