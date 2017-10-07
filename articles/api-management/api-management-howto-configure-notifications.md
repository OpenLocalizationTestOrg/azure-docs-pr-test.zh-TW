---
title: "aaaConfigure 通知和電子郵件範本，在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>如何 tooconfigure 通知和電子郵件範本，在 Azure API 管理
API 管理提供 hello 能力 tooconfigure 通知的特定事件及 tooconfigure hello 電子郵件範本，而且使用的 toocommunicate 與 hello 管理員和開發人員的 API 管理執行個體。 本主題說明如何 tooconfigure 通知 hello 可用的事件，並提供設定使用這些事件的 hello 電子郵件範本的概觀。

## <a name="publisher-notifications"> </a>設定發行者通知
按一下 tooconfigure 通知**發行者入口網站**API 管理服務的 hello Azure 入口網站中。 這會帶您 toohello API 管理發行者入口網站。

![發行者入口網站][api-management-management-console]

> [!NOTE] 
> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。

按一下**通知**從 hello **API 管理**hello 功能表左 tooview hello 可用的通知。

![Publisher notifications][api-management-publisher-notifications]

hello 下列事件的清單可以設定通知。

* **（需要核准） 的訂用帳戶要求**-hello 指定的電子郵件收件者和使用者會收到電子郵件通知訂閱要求的應用程式開發介面需要核准的產品。
* **新的訂閱**-hello 指定的電子郵件收件者和使用者會收到有關新的應用程式開發介面產品訂閱電子郵件通知。
* **組件庫的應用程式要求**-hello 指定的電子郵件收件者，並提交的 toohello 應用程式庫，新的應用程式時，使用者會收到電子郵件通知。
* **密件副本**-hello 指定的電子郵件收件者和使用者會收到電子郵件密件副本的所有傳送的電子郵件 toodevelopers。
* **新問題或評論**-hello 指定的電子郵件收件者和使用者會收到電子郵件通知時新問題或意見送出 hello 開發人員入口網站上。
* **關閉帳戶訊息**-hello 指定的電子郵件收件者，並關閉帳戶時，使用者會收到電子郵件通知。
* **接近的訂用帳戶配額限制**-hello 遵循電子郵件收件者和使用者會收到電子郵件通知訂用帳戶使用量取得關閉 toousage 配額。

針對每個事件，您可以指定電子郵件收件者使用 hello 電子郵件位址 文字方塊中，或從清單中選取使用者。

toospecify hello 電子郵件地址 toobe 收到通知，請在 [hello 電子郵件地址] 文字方塊中輸入密碼。 如果您有多個電子郵件地址，請以逗號分隔。

![Notification recipients][api-management-email-addresses]

toospecify hello 使用者 toobe 收到通知，請按一下**加入收件者**，核取 hello hello 使用者 toobe 通知時，旁邊的方塊，然後按一下**確定**。

> [!NOTE] 
> 只有系統管理員會顯示在 [hello] 清單中。


設定後 hello 通知收件者，請按一下**儲存**tooapply hello 更新通知收件者。

> [!NOTE] 
> 如果您離開 hello**發行者通知** 索引標籤 hello 發行者入口網站會提醒您若那里未儲存的變更。


## <a name="email-templates"> </a>設定電子郵件範本
API 管理提供電子郵件範本 hello 在 hello 課程中的管理和使用 hello 服務所傳送的電子郵件訊息。 提供下列電子郵件範本的 hello。

* 已核准應用程式庫提交
* 開發人員離職信
* 開發人員接近配額限制通知
* 邀請使用者
* 將新的註解加入 tooan 問題
* 收到新的問題
* 已啟用新的訂用帳戶
* 確認訂用帳戶已更新
* 拒絕訂用帳戶要求
* 收到訂用帳戶要求

可依需要修改這些範本。

tooview 並設定您的 API 管理執行個體的 hello 電子郵件範本，請按一下**通知**從 hello **API 管理**功能表靠左、 hello 和選取 hello**電子郵件範本**  索引標籤。

![Email templates][api-management-email-templates]

tooview 或修改特定範本，請選取從 hello**範本**下拉式清單。

![Email templates list][api-management-email-templates-list]

每一個電子郵件範本都有純文字的主旨，以及 HTML 格式的本文定義。 可依需要自訂每一個項目。

![Email template editor][api-management-email-template]

hello**參數**清單包含清單的參數，當插入 hello 主旨或內文，傳送嗨電子郵件時，將會取代的 hello 指定值。 tooinsert 參數，將您想 hello 參數 toogo，並按一下 hello 箭號 toohello hello 參數名稱左邊的 hello 游標。

按一下**預覽**或**傳送測試**toosee 如何 hello 電子郵件將會尋找或傳送測試電子郵件。

> [!NOTE] 
> hello 參數未取代成實際的值，當在預覽或傳送的測試。

toosave hello 變更 toohello 電子郵件範本，按一下 **儲存**，或按一下 toocancel hello 變更**取消**。
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
