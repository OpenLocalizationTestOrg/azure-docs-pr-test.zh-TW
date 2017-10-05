---
title: "Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證 | Microsoft Docs"
description: "示範如何在 Azure Active Directory B2C 中的取用者註冊期間停用電子郵件驗證的主題"
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="dbbdf-103">Azure Active Directory B2C: 在取用者註冊期間停用電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="dbbdf-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="dbbdf-104">啟用時，Azure Active Directory (Azure AD) B2C 會提供讓使用者透過提供電子郵件地址並建立本機帳戶來註冊應用程式的能力。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="dbbdf-105">Azure AD B2C 可透過要求取用者在註冊程序期間驗證其身分以確保電子郵件地址的有效性。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="dbbdf-106">它也會防止惡意自動化程序為應用程式產生假帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="dbbdf-107">某些應用程式開發人員偏好在註冊程序期間跳過電子郵件驗證，改為讓取用者稍後在掙電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="dbbdf-108">為支援此方式，您可以將 Azure AD B2C 設定為停用電子郵件驗證。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="dbbdf-109">這樣做可建立較為順暢的註冊程序，並提供區分已驗證電子郵件地址與未驗證電子郵件地址之取用者的彈性。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="dbbdf-110">根據預設值，註冊原則會開啟電子郵件驗證。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="dbbdf-111">使用下列步驟將它關閉：</span><span class="sxs-lookup"><span data-stu-id="dbbdf-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="dbbdf-112">遵循下列步驟以[瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="dbbdf-113">視您要針對註冊設定的項目而定，按一下 [註冊原則] 或 [註冊或登入原則]。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="dbbdf-114">按一下您的原則 (例如 "B2C_1_SiUp") 以將它開啟。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="dbbdf-115">按一下刀鋒視窗頂端的 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="dbbdf-116">按一下 [頁面 UI 自訂功能]。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="dbbdf-117">按一下 [本機帳戶註冊頁面]。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="dbbdf-118">按一下 [註冊屬性] 區段下 [名稱] 欄中的 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="dbbdf-119">將 [需要驗證] 選項切換至 [否]。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="dbbdf-120">按一下底部的 [確定]，直到您到達 [編輯原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="dbbdf-121">按一下刀鋒視窗頂端的 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="dbbdf-122">大功告成！</span><span class="sxs-lookup"><span data-stu-id="dbbdf-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="dbbdf-123">在註冊程序期間停用電子郵件驗證可能會導致收到垃圾郵件。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="dbbdf-124">若停用預設的項目，建議您新增自己的驗證系統。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="dbbdf-125">我們歡迎意見反應和建議！</span><span class="sxs-lookup"><span data-stu-id="dbbdf-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="dbbdf-126">如果您無法完成此主題，或者有改進此內容的建議，非常歡迎您在頁面底部提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="dbbdf-127">對於功能要求，請將它們新增到 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="dbbdf-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>