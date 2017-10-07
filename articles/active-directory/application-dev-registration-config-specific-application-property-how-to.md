---
title: "針對自訂開發的應用程式的特定欄位的 aaaHow toofill |Microsoft 文件"
description: "指引上 toofill 出特定欄位如何時您所註冊的自訂開發的應用程式與 Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>如何針對自訂開發的應用程式的特定欄位 toofill

這篇文章提供您 hello 應用程式註冊表單中的 hello 可用欄位的簡短描述 hello [Azure 入口網站](https://portal.azure.com)。

## <a name="register-a-new-application"></a>註冊新的應用程式

-   tooregister 新的應用程式中，瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。

-   從 hello 左側瀏覽窗格中，按一下  **Azure Active Directory。**

-   選擇 [應用程式註冊]，然後按一下 [新增]。

-   這會開啟 hello 應用程式註冊表單。

## <a name="fields-in-hello-application-registration-form"></a>Hello 應用程式註冊表單中的欄位


| 欄位            | 說明                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| 名稱             | hello hello 應用程式名稱。 至少應該有四個字元。                |
| 應用程式類型 | **Web 應用程式/Web API**：代表 Web 應用程式、Web API 或兩者的應用程式 
| |**原生**：可安裝在使用者裝置或電腦上的應用程式           |
| 登入 URL      | hello，使用者可以登入 toouse 在您的應用程式的 URL                                  |

一旦您已填入欄位的上方 hello，hello 應用程式在 hello Azure 入口網站中註冊，並將您重新導向 toohello 應用程式頁面。 hello**設定**hello 應用程式 窗格上的按鈕會開啟 hello 設定頁面上，具有多個欄位，為您 toocustomize 您的應用程式。 hello 下表描述 hello 設定 頁面中的所有 hello 欄位。 請注意，根據您建立的是 Web 應用程式或原生應用程式而定，您只會看見這些欄位的一部分。

| 欄位           | 說明                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 應用程式識別碼  | 當您註冊應用程式時，Azure AD 會將應用程式識別碼指派給您的應用程式。 hello 應用程式識別碼可以用 toouniquely 識別驗證要求 tooAzure AD，與 tooaccess 資源像 hello Graph API 中的應用程式。                                                          |
| 應用程式識別碼 URI      | 這應該是唯一的 URI，通常的 hello 表單**https://&lt;租用戶\_名稱&gt;/&lt;應用程式\_名稱&gt;。** 這用在 hello 授權授與流程，為哪些 hello 應該會發行權杖的唯一識別碼 toospecify hello 資源。 它也會變成 hello 發出存取權杖中的 hello '則' 宣告。 |
| 上傳新標誌 | 您可以使用這個 tooupload 標誌，應用程式。 hello 標誌必須是.bmp、.jpg 或.png 格式，而且 hello 檔案大小應該小於 100 KB。 hello 映像的 hello 尺寸應 215 x 215 像素，中央影像尺寸 94 x 94 像素為單位。                                                       |
| 首頁 URL   | 這是 hello 登入 URL，在應用程式登錄期間指定。                                                                                                                                                                                                                                              |
| 登出 URL      | 這個 hello 單一登出登出 URL。 Azure AD 會傳送登出要求 toothis URL hello 使用者與 Azure AD 中清除其工作階段使用任何其他已註冊的應用程式。                                                                                                                                       |
| 多重租用戶  | 這個參數會指定 hello 應用程式是否可由多個租用戶。 一般而言，這表示外部組織可以使用您的應用程式，其租用戶中註冊它，並授與存取 tootheir 組織的資料。                                                                   |
| 回覆 URL      | hello 回覆 Url 是 hello 端點，其中的 Azure AD 傳回您的應用程式要求的所有權杖。                                                                                                                                                                                                          |
| 重新導向 URI   | 原生應用程式，這是其中 hello 使用者是傳送的 toofollowing 成功授權。 Hello 的 azure AD 檢查重新導向的 URI 您的應用程式提供在 hello OAuth 2.0 要求符合其中一個 hello 入口網站中的 hello 登錄值。                                                            |
| 之間的信任            | 您可以建立金鑰 tooprogrammatically 存取的網站沒有任何使用者互動的 Azure AD 所保護的應用程式開發介面。 從 hello \*\*金鑰\*\*頁面上，輸入索引鍵的描述和 hello 到期日並儲存 toogenerate hello 金鑰。 將能 tooaccess 做確定 toosave 某處保護之後，於稍後。             |

## <a name="next-steps"></a>後續步驟
[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)
