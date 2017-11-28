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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="6f2c8-103">如何 toodebug SAML 型單一登入 tooapplications Azure Active Directory 中</span><span class="sxs-lookup"><span data-stu-id="6f2c8-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="6f2c8-104">偵錯 SAML 型應用程式整合時，通常很有幫助 toouse 這類工具[Fiddler](http://www.telerik.com/fiddler) toosee hello SAML 要求、 hello SAML 回應和 hello 實際 SAML 權杖中發出 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="6f2c8-105">藉由檢查 hello SAML 權杖中，您可以確保所有 hello 必要屬性、 hello hello SAML 主旨中的使用者名稱和 hello 如預期般，透過全都來自 URI 的簽發者。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="6f2c8-106">hello 回應從 Azure AD 包含 hello SAML 權杖通常是 hello https://login.windows.net，從 HTTP 302 重新導向之後發生的其中一個，而且已傳送的 toohello**回覆 URL** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="6f2c8-107">您可以檢視 hello SAML 權杖中選取這一行，然後選取 hello**偵測器 > WebForms** hello 右面板中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="6f2c8-108">從該處，以滑鼠右鍵按一下 hello **SAMLResponse**值，並選取**傳送 tooTextWizard**。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="6f2c8-109">然後選取**從 Base64**從 hello**轉換**功能表 toodecode hello 語彙基元，並檢視其內容。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="6f2c8-110">**請注意**: toosee hello 內容的此 HTTP 要求，Fiddler 可能會提示您的 HTTPS 流量，您將需要 tooconfigure 解密 toodo。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6f2c8-111">相關文章</span><span class="sxs-lookup"><span data-stu-id="6f2c8-111">Related Articles</span></span>
* [<span data-ttu-id="6f2c8-112">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="6f2c8-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="6f2c8-113">設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="6f2c8-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="6f2c8-114">如何 tooCustomize 中發出的宣告 hello SAML 權杖 Pre-Integrated 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f2c8-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png