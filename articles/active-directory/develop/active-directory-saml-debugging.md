---
title: "如何針對 Azure Active Directory 中的 SAML 型應用程式單一登入進行偵錯 | Microsoft Docs"
description: "了解如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式  "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="b3855-103">如何偵錯 SAML 型單一登入 Azure Active Directory 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="b3855-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="b3855-104">當偵錯 SAML 型的應用程式整合時，使用 [Fiddler](http://www.telerik.com/fiddler) 之類的工具查看 SAML 要求、SAML 回應和發行給應用程式實際的 SAML 權杖，通常很有幫助。</span><span class="sxs-lookup"><span data-stu-id="b3855-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="b3855-105">您可以藉由檢查 SAML 權杖，確保所有必要的屬性、SAML 主體中的使用者名稱和簽發者 URI 都能如預期通過。</span><span class="sxs-lookup"><span data-stu-id="b3855-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="b3855-106">包含 SAML 權杖的 Azure AD 回應，通常是 HTTP 302 從 https://login.windows.net 重新導向並傳送至已設定的應用程式**回覆 URL** 後，發生的那一個。</span><span class="sxs-lookup"><span data-stu-id="b3855-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="b3855-107">您可以選取這一行，然後在右窗格中選取 [偵測器] > [WebForms]，檢視 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="b3855-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="b3855-108">在這裡以滑鼠右鍵按一下 [SAMLResponse] 值並選取 [傳送至 TextWizard]。</span><span class="sxs-lookup"><span data-stu-id="b3855-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="b3855-109">然後選取 [轉換] 功能表的 [從 Base64]，解碼權杖並查看其內容。</span><span class="sxs-lookup"><span data-stu-id="b3855-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="b3855-110">**注意**：為查看這個 HTTP 要求的內容，Fiddler 可能會提示您設定解密 HTTPS 流量，請務必這麼做。</span><span class="sxs-lookup"><span data-stu-id="b3855-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b3855-111">相關文章</span><span class="sxs-lookup"><span data-stu-id="b3855-111">Related Articles</span></span>
* [<span data-ttu-id="b3855-112">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="b3855-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="b3855-113">設定對不在 Azure Active Directory 應用程式庫中的應用程式的單一登入</span><span class="sxs-lookup"><span data-stu-id="b3855-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="b3855-114">如何為預先整合的應用程式自訂在 SAML 權杖中發出的宣告</span><span class="sxs-lookup"><span data-stu-id="b3855-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png