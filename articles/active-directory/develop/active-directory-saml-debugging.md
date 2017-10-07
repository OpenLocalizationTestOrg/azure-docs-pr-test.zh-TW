---
title: "aaaHow toodebug SAML 型單一登入 tooapplications Azure Active Directory 中 |Microsoft 文件"
description: "深入了解如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中 "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中
偵錯 SAML 型應用程式整合時，通常很有幫助 toouse 這類工具[Fiddler](http://www.telerik.com/fiddler) toosee hello SAML 要求、 hello SAML 回應和 hello 實際 SAML 權杖中發出 toohello 應用程式。 藉由檢查 hello SAML 權杖中，您可以確保所有 hello 必要屬性、 hello hello SAML 主旨中的使用者名稱和 hello 如預期般，透過全都來自 URI 的簽發者。

![][1]

hello 回應從 Azure AD 包含 hello SAML 權杖通常是 hello https://login.windows.net，從 HTTP 302 重新導向之後發生的其中一個，而且已傳送的 toohello**回覆 URL** hello 應用程式。 

您可以檢視 hello SAML 權杖中選取這一行，然後選取 hello**偵測器 > WebForms** hello 右面板中的索引標籤。 從該處，以滑鼠右鍵按一下 hello **SAMLResponse**值，並選取**傳送 tooTextWizard**。 然後選取**從 Base64**從 hello**轉換**功能表 toodecode hello 語彙基元，並檢視其內容。

**請注意**: toosee hello 內容的此 HTTP 要求，Fiddler 可能會提示您的 HTTPS 流量，您將需要 tooconfigure 解密 toodo。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](../active-directory-apps-index.md)
* [設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫](../active-directory-saas-custom-apps.md)
* [如何 tooCustomize 中發出的宣告 hello SAML 權杖 Pre-Integrated 應用程式](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png