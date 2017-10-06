---
title: "Active Directory 應用程式註冊 aaaAzure |Microsoft 文件"
description: "本文說明如何 toouse 會 hello Azure 入口網站 tooregister 與 Azure Active Directory 應用程式"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>向 Azure Active Directory 租用戶註冊您的應用程式

您可以使用 Azure 入口網站 tooregister hello 您的應用程式，利用 Azure Active Directory (Azure AD) 租用戶。 這會建立 hello 應用程式，應用程式識別碼，並讓它 tooreceive 語彙基元。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，然後按一下**新增**。
4. 依照 hello 提示，並建立新的應用程式。 如果您想要 Web 應用程式或原生應用程式的特定範例，請查看我們的[快速入門](active-directory-developers-guide.md)。
  * Web 應用程式，提供 hello**登入 URL**，這是應用程式的 hello 基底 URL，使用者可以登入在例如`http://localhost:12345`。
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 原生應用程式，提供**重新導向 URI**，哪些 Azure AD 使用 tooreturn 權杖回應。 輸入值特定 tooyour 應用程式。 例如`http://MyFirstAADApp`
5. 當您完成註冊之後時，Azure AD 會指派給您的應用程式的唯一用戶端識別碼，hello 應用程式識別碼。

## <a name="update-application-settings-from-hello-azure-portal"></a>更新從 hello Azure 入口網站應用程式設定

您可以輕鬆地修改現有的應用程式的設定，使用 hello Azure 入口網站。 例如，您可能想 tooconfigure 回覆 URL，也就是，Azure AD 發出權杖的回應。 您也可以 tooconfigure 權限 tooother 應用程式，您的應用程式 tooaccess 的執行個體 tooallow hello Microsoft Graph API。 您可以執行這所有工作透過 hello 應用程式設定] 頁面。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，並從 hello 清單中選擇您的應用程式。
4. 按一下**設定**tooopen hello 的 hello 應用程式設定] 頁面上。
  * hello**屬性**頁面可讓您修改 hello hello 應用程式的一般資訊。 這包括 hello 應用程式名稱、 登入 URL hello 和 hello 登出 URL。
  * hello**回覆 Url**頁面可讓您 tooadd 回覆 URL，這可能會讓 Azure AD 會傳送權杖回應。
  * hello**擁有者**頁面可讓您 tooadd 應用程式擁有者。
  * hello**權限**頁面可讓您 tooconfigure hello 應用程式的權限。 比方說，tooaccess hello Microsoft Graph API 中，按一下 [**新增**選取**Microsoft Graph** hello API 選取器，然後選擇 hello 例如所需的權限**讀取目錄資料**.
  * hello**金鑰**頁面可讓您 tooadd 應用程式密碼。 hello 密碼只會顯示一次之後建立，因此請確定 toocopy 以便進一步使用於它。

## <a name="use-hello-inline-manifest-editor"></a>使用 hello 內嵌資訊清單編輯器

您可以使用 hello 內嵌資訊清單編輯器 toomodify 特定應用程式內容不會直接在公開 hello Azure 入口網站。 例如，您可以使用它 toomodify hello 應用程式的應用程式識別碼 URI 或 tooenable hello OAuth2.0 隱含流程，而不是 hello 預設授權授與程式碼流程。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 左側導覽窗格中，選擇 [**更服務**，按一下**應用程式註冊**，並從 hello 清單中選擇您的應用程式。
4. 按一下**資訊清單**從 hello 應用程式頁面 tooopen hello 內嵌資訊清單編輯器。
5. 您可以直接進行變更 toohello 資訊清單，並將它儲存，當您準備好。 或者，您可以下載 hello 資訊清單 tooopen 它在您最愛的編輯器和上傳 hello 更新資訊清單。

## <a name="next-steps"></a>後續步驟

1. 簽出 hello[快速入門](active-directory-developers-guide.md)如需使用 Azure AD 執行驗證的應用程式的詳細逐步解說。
2. 查看 [GitHub](https://github.com/azure-samples) 中完整的程式碼範例清單。
