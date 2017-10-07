---
title: "使用 Azure Active Directory Azure API 管理 aaaAuthorize 開發人員帳戶 |Microsoft 文件"
description: "深入了解如何使用 API 管理中的 Azure Active Directory tooauthorize 使用者。"
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>如何 tooauthorize 開發人員帳戶使用 Azure Active Directory 在 Azure API 管理
## <a name="overview"></a>概觀
本指南也說明如何 tooenable 存取 toohello 開發人員入口網站，讓使用者從 Azure Active Directory。 本指南也會顯示如何加入外部群組包含 Azure Active Directory 使用者 toomanage 群組 hello Azure Active Directory 使用者。

> 本指南中步驟 toocomplete hello 必須先有 Azure Active Directory 中哪些 toocreate 應用程式。
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>如何 tooauthorize 開發人員帳戶使用 Azure Active Directory
tooget 啟動，按一下**發行者入口網站**hello API 管理服務的 Azure 入口網站中。 這會帶您 toohello API 管理發行者入口網站。

![發行者入口網站][api-management-management-console]

> 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。
> 
> 

按一下**安全性**從 hello **API 管理**hello 左側，按一下功能表**外部識別**。

![外部身分識別][api-management-security-external-identities]

按一下 [ **Azure Active Directory**]。 請記下 hello**重新導向 URL**和切換 tooyour Azure Active Directory hello Azure 傳統入口網站中。

![外部身分識別][api-management-security-aad-new]

按一下 hello**新增**按鈕 toocreate 新的 Azure Active Directory 應用程式，然後選擇**加入我組織正在開發的應用程式**。

![加入新的 Azure Active Directory 應用程式][api-management-new-aad-application-menu]

輸入的名稱 hello 應用程式中，選取**Web 應用程式和/或 Web API**，然後按一下 下一步按鈕的 hello。

![新 Azure Active Directory 應用程式][api-management-new-aad-application-1]

如**登入 URL**，輸入 hello 登入您的開發人員入口網站的 URL。 在此範例中，hello**登入 URL**是`https://aad03.portal.current.int-azure-api.net/signin`。 

Hello**應用程式識別碼 URL**、 hello Azure Active Directory 中，輸入 hello 預設定義域或自訂網域，然後附加唯一字串 tooit。 在此範例中，hello 的預設網域**https://contoso5api.onmicrosoft.com**搭配 hello 尾碼**/api**指定。

![新 Azure Active Directory 應用程式屬性][api-management-new-aad-application-2]

按一下 hello 核取按鈕 toosave 和建立 hello 應用程式，並切換 toohello**設定**tooconfigure hello 新應用程式索引標籤上。

![新 Azure Active Directory 應用程式已建立][api-management-new-aad-app-created]

如果多個 Azure Active Directory 將 toobe 此應用程式使用，請按一下**是**如**應用程式是多租用戶**。 hello 預設值是**否**。

![是][api-management-aad-app-multi-tenant]

複製 hello**重新導向 URL**從 hello **Azure Active Directory**區段 hello**外部識別**hello 發行者入口網站中索引標籤，並將它貼到 hello **回覆 URL**文字方塊。 

![回覆 URL][api-management-aad-reply-url]

捲軸 toohello 底部 hello 設定索引標籤上，選取 hello**應用程式權限**下拉式清單中，並檢查**讀取目錄資料**。

![應用程式權限][api-management-aad-app-permissions]

選取 hello**委派權限**下拉式清單中，並檢查**啟用登入並讀取使用者的設定檔**。

![委派的權限][api-management-aad-delegated-permissions]

> 如需應用程式和委派的權限的詳細資訊，請參閱[存取 hello Graph API][Accessing hello Graph API]。
> 
> 

複製 hello**用戶端識別碼**toohello 剪貼簿。

![用戶端識別碼][api-management-aad-app-client-id]

切換後 toohello 發行者入口網站，並貼上在 hello**用戶端識別碼**複製 hello Azure Active Directory 應用程式組態中。

![用戶端識別碼][api-management-client-id]

切換後 toohello Azure Active Directory 設定，然後按一下 hello**選取持續時間**下拉式清單中 hello**金鑰**區段，並指定間隔。 在此範例中使用 **1 年** 。

![Key][api-management-aad-key-before-save]

按一下**儲存**toosave hello 組態和顯示 hello 金鑰。 將複製 hello 金鑰 toohello 剪貼簿。

> 記下此金鑰。 一旦您關閉 hello Azure Active Directory 設定 視窗中，無法再次顯示 hello 索引鍵。
> 
> 

![Key][api-management-aad-key-after-save]

交換器後 toohello 發行者入口網站和貼上 hello 金鑰貼入 hello**用戶端密碼**文字方塊。

![用戶端密碼][api-management-client-secret]

**允許租用戶**指定的目錄有存取 toohello hello API 管理服務執行個體的應用程式開發介面。 指定您想要 toogrant 存取 Azure Active Directory 執行個體 toowhich hello 的 hello 網域。 您可以使用換行符號、空格或逗號來分隔多個網域。

![允許的租用戶][api-management-client-allowed-tenants]


一旦 hello 想要指定組態，請按一下**儲存**。

![儲存][api-management-client-allowed-tenants-save]

一旦儲存 hello 變更了，指定 Azure Active Directory 可以登入 toohello 開發人員入口網站中的 hello 步驟在 hello hello 使用者[登入 toohello 開發人員入口網站使用的 Azure Active Directory 帳戶][Log in toohello Developer portal using an Azure Active Directory account].

可以指定多個網域在 hello**允許租用戶**> 一節。 任何使用者可以從不同 hello hello 應用程式註冊所在的原始網域的網域登入前，hello 不同網域的全域管理員必須授與權限 hello 應用程式 tooaccess 目錄資料。 toogrant 權限，hello 全域系統管理員應太`https://<URL of your developer portal>/aadadminconsent`(例如，https://contoso.portal.azure-api.net/aadadminconsent)，按一下 [提交] hello 網域名稱中的 hello 他們想 toogive 存取 tooand 的 Active Directory 租用戶的型別。 在 hello 下列範例中，全域系統管理員身分從`miaoaad.onmicrosoft.com`正嘗試 toogive 權限 toothis 特定開發人員入口網站。 

![權限][api-management-aad-consent]

Hello 下一個畫面中，在 hello 全域系統管理員可提示的 tooconfirm 賦予 hello 的權限。 

![權限][api-management-permissions-form]

> 如果非全域系統管理員嘗試 toolog 中之前的權限會授與全域系統管理員、 hello 登入嘗試失敗和錯誤畫面隨即出現。
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>如何 tooadd 外部的 Azure Active Directory 群組
啟用 Azure Active Directory 中使用者的存取權之後，您可以新增至 API 管理 toomore 的 Azure Active Directory 群組輕鬆地管理 hello 與之間的關聯 hello 群組中的 hello 開發人員想要的 hello 產品。

> tooconfigure 外部的 Azure Active Directory 群組，hello Azure Active Directory 必須先設定 hello 身分識別 索引標籤中遵循 hello hello 前一節中的程序。 
> 
> 

從 hello 加入外部 Azure Active Directory 群組**可視性**hello 產品想 toogrant 存取 toohello 群組 索引標籤。 按一下**產品**，然後按一下hello hello 所需的產品名稱。

![Configure product][api-management-configure-product]

切換 toohello**可視性**索引標籤，然後按一下**新增的群組，從 Azure Active Directory**。

![加入群組][api-management-add-groups]

選取 hello **Azure Active Directory 租用戶**hello 下拉式清單中，與在 hello hello 所需群組然後類型 hello 名稱**群組**toobe 加入文字方塊。

![選取群組][api-management-select-group]

此群組名稱可以在 hello**群組**hello 下列範例所示，您的 Azure Active directory，清單。

![Azure Active Directory 群組清單][api-management-aad-groups-list]

按一下**新增**toovalidate hello 群組名稱，並加入 hello 群組。 在此範例中，hello **Contoso 5 開發人員**就會加入外部群組。 

![Group added][api-management-aad-group-added]

按一下**儲存**toosave hello 新群組選取項目。

一旦已設定 Azure Active Directory 群組從一個產品，就是檢查 hello 可用 toobe**可視性** 索引標籤的 hello hello API 管理服務執行個體中的其他產品。

tooreview 並設定 hello 屬性外部一旦已加入的群組按一下 hello hello hello 群組名稱**群組** 索引標籤。

![管理群組][api-management-groups]

您可以從這裡編輯 hello**名稱**和 hello**描述**的 hello 群組。

![編輯群組][api-management-edit-group]

Hello 的使用者設定的 Azure Active Directory 登入 toohello 開發人員入口網站並檢視和訂閱他們擁有之可見性 hello 之後 > 一節中的 hello 指示 tooany 群組。

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>如何使用 Azure Active Directory 帳戶 toohello 開發人員入口網站中的 toolog
toolog hello 開發人員入口網站，使用 Azure Active Directory 帳戶設定在 hello 先前章節中，開啟新的瀏覽器視窗，使用 hello**登入 URL**從 hello Active Directory 應用程式組態，然後按一下**Azure Active Directory**。

![開發人員入口網站][api-management-dev-portal-signin]

輸入您 Azure Active Directory 中的 hello 的其中一個 hello 使用者的認證，然後按一下**登入**。

![Sign in][api-management-aad-signin]

如果需要其他資訊，可能會出現註冊表單的提示。 完成 hello 註冊表單，然後按一下**註冊**。

![註冊][api-management-complete-registration]

您的使用者現在已登入您 API 管理服務執行個體的 hello 開發人員入口網站中。

![註冊完成][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

