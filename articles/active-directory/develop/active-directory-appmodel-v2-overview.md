---
title: "aaaAzure Active Directory v2.0 端點 |Microsoft 文件"
description: "使用 Microsoft 帳戶和 Azure Active Directory 登入簡介 toobuilding 應用程式。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>以單一應用程式登入 Microsoft 帳戶和 Azure AD 使用者
在過去，應用程式開發人員想 toosupport 兩個人的 Microsoft 帳戶的 hello 從 Azure Active Directory 的工作帳戶但需要的 toointegrate 與兩個不同的系統。  hello **Azure AD v2.0 端點**導入了新的驗證 API 版本，可讓您在這兩種類型的帳戶使用一個簡單的整合 toosign。  使用 hello v2.0 端點的應用程式也可以使用 REST Api 從 hello [Microsoft Graph](https://graph.microsoft.io)使用任一種帳戶。

## <a name="getting-started"></a>開始使用
選擇您最愛的平台從下列清單 toobuild hello 使用我們的開放原始碼程式庫 （& s） 架構的應用程式。  或者，您可以使用我們 OAuth 2.0 和 OpenID Connect 通訊協定文件 toosend & 直接不使用驗證程式庫接收通訊協定訊息。

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>新功能
這裡 hello 資訊將有助於了解為何 （& s） 與 hello v2.0 端點可能不是。

* 深入了解 hello[類型的應用程式，您可以建立與 hello v2.0 端點](active-directory-v2-flows.md)。
* 了解 hello[限制、 限制和條件約束](active-directory-v2-limitations.md)與 hello v2.0 端點。
* 請參閱本概觀視訊 hello v2.0 端點：

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>參考
這些連結會是適合用來探索深度 hello 平台：

* [v2.0 通訊協定參考](active-directory-v2-protocols.md)
* [v2.0 權杖參考](active-directory-v2-tokens.md)
* [v2.0 程式庫參考](active-directory-v2-libraries.md)
* [範圍和同意 hello v2.0 端點中](active-directory-v2-scopes.md)
* [Microsoft Graph hello](https://graph.microsoft.io)

## <a name="help--support"></a>說明及支援
這些是 hello 最佳地方 tooget 說明與 Azure Active Directory 上進行開發。

* [Stack Overflow 的 `azure-active-directory` 和 `adal` 標籤](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Azure Active Directory 的意見反應](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> 如果您只需要 toosign 公司及學校帳戶，從 Azure Active Directory 中的，您應該開始我們[Azure AD 開發人員手冊 》](active-directory-developers-guide.md)。  hello v2.0 端點是用於開發人員明確 toosign 中 Microsoft 個人帳戶。

