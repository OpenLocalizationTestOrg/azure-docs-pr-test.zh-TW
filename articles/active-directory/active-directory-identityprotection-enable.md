---
title: "Azure Active Directory 識別身分保護 aaaEnabling |Microsoft 文件"
description: "深入了解如何 tooenable Azure Active Directory 識別身分保護。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: d26f466f5c7d6a425528a277d98c2c4b341ff8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="f8f8a-104">啟用 Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8f8a-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="f8f8a-105">Azure Active Directory Identity Protection 是一項新功能，可針對可疑的登入活動和潛在弱點提供整合檢視，並提供通知、補救建議及以風險為基礎的原則，來協助保護您的企業。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="f8f8a-106">hello 服務偵測到可疑活動的使用者和權限 （系統管理員） 身分識別基礎訊號像暴力密碼破解強制攻擊外, 洩認證，登入不熟悉的位置，從受感染的裝置，tooprotect 針對即時這些活動。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-106">hello service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, tooprotect against these activities in real-time.</span></span> <span data-ttu-id="f8f8a-107">更重要的是，根據這些可疑的活動，使用者風險嚴重性計算並風險為基礎的原則可以設定自動保護您組織的 hello 身分識別。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect hello identities of your organization.</span></span> <span data-ttu-id="f8f8a-108">如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="f8f8a-109">本主題顯示如何 tooenable Azure Active Directory 識別身分保護。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-109">This topics shows how tooenable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-tooenable-azure-active-directory-identity-protection"></a><span data-ttu-id="f8f8a-110">步驟 tooenable Azure Active Directory 識別身分保護</span><span class="sxs-lookup"><span data-stu-id="f8f8a-110">Steps tooenable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="f8f8a-111">[登入](https://ms.portal.azure.com/)tooyour 全域系統管理員身分的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-111">[Sign-on](https://ms.portal.azure.com/) tooyour Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="f8f8a-112">在 hello Azure 入口網站，按一下  **Marketplace**。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-112">In hello Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="f8f8a-113">![建立](./media/active-directory-identityprotection-enable/01.png "建立")</span><span class="sxs-lookup"><span data-stu-id="f8f8a-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="f8f8a-114">在 hello 應用程式清單中，按一下 **安全性 + 身分識別**。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-114">In hello applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="f8f8a-115">![建立](./media/active-directory-identityprotection-enable/02.png "建立")</span><span class="sxs-lookup"><span data-stu-id="f8f8a-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="f8f8a-116">按一下 [Azure AD Identity Protection] 。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="f8f8a-117">![建立](./media/active-directory-identityprotection-enable/03.png "建立")</span><span class="sxs-lookup"><span data-stu-id="f8f8a-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="f8f8a-118">在 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="f8f8a-118">On hello **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="f8f8a-119">![建立](./media/active-directory-identityprotection-enable/04.png "建立")</span><span class="sxs-lookup"><span data-stu-id="f8f8a-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8f8a-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8f8a-120">Next Steps</span></span>
* [<span data-ttu-id="f8f8a-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f8f8a-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

