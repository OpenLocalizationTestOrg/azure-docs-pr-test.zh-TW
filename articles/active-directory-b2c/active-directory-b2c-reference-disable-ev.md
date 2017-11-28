---
title: "Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證 | Microsoft Docs"
description: "主題，示範如何 toodisable 電子郵件驗證期間註冊在 Azure Active Directory B2C 的取用者"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="8d66e-103">Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="8d66e-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="8d66e-104">啟用時，Azure Active Directory (Azure AD) B2C 提供一個消費者會 hello 註冊應用程式的能力 toosign 藉由提供電子郵件地址，並建立本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d66e-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="8d66e-105">Azure AD B2C 確保有效的電子郵件地址，藉由要求取用者 tooverify 它們 hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="8d66e-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="8d66e-106">它也可防止惡意的自動化程序產生假 hello 應用程式的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d66e-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="8d66e-107">某些應用程式開發人員偏好 tooskip 電子郵件驗證 hello 註冊程序，並改讓取用者驗證稍後 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8d66e-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="8d66e-108">toosupport Azure AD B2C 這可以是設定的 toodisable 電子郵件驗證。</span><span class="sxs-lookup"><span data-stu-id="8d66e-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="8d66e-109">如此一來建立更順暢的登入程序，並提供開發人員 hello 彈性 toodifferentiate hello 取用者已驗證與沒有這些取用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="8d66e-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="8d66e-110">根據預設值，註冊原則會開啟電子郵件驗證。</span><span class="sxs-lookup"><span data-stu-id="8d66e-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="8d66e-111">使用 hello 下列步驟 tooturn 它關閉：</span><span class="sxs-lookup"><span data-stu-id="8d66e-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="8d66e-112">[遵循這些步驟 toonavigate toohello B2C 功能刀鋒視窗上 hello Azure 入口網站](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。</span><span class="sxs-lookup"><span data-stu-id="8d66e-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="8d66e-113">視您要針對註冊設定的項目而定，按一下 [註冊原則] 或 [註冊或登入原則]。</span><span class="sxs-lookup"><span data-stu-id="8d66e-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="8d66e-114">按一下 原則 (例如，"B2C_1_SiUp 」) tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="8d66e-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="8d66e-115">按一下**編輯**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="8d66e-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8d66e-116">按一下 [頁面 UI 自訂功能]。</span><span class="sxs-lookup"><span data-stu-id="8d66e-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="8d66e-117">按一下 [本機帳戶註冊頁面]。</span><span class="sxs-lookup"><span data-stu-id="8d66e-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="8d66e-118">按一下**電子郵件地址**在 hello**名稱**hello 下的資料行**註冊屬性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="8d66e-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="8d66e-119">切換 hello**需要驗證**太選項**否**。</span><span class="sxs-lookup"><span data-stu-id="8d66e-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="8d66e-120">按一下**確定**底部 hello 直到您到達 hello**編輯原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8d66e-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="8d66e-121">按一下**儲存**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="8d66e-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="8d66e-122">大功告成！</span><span class="sxs-lookup"><span data-stu-id="8d66e-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="8d66e-123">停用電子郵件驗證 hello 註冊程序中的，可能會導致 toospam。</span><span class="sxs-lookup"><span data-stu-id="8d66e-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="8d66e-124">如果您停用其中一個 hello 預設，我們建議加入您自己的驗證系統。</span><span class="sxs-lookup"><span data-stu-id="8d66e-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="8d66e-125">我們一定是開啟 toofeedback，以及建議 ！</span><span class="sxs-lookup"><span data-stu-id="8d66e-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="8d66e-126">如果您有本主題中，任何問題，或有改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。</span><span class="sxs-lookup"><span data-stu-id="8d66e-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="8d66e-127">功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="8d66e-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
