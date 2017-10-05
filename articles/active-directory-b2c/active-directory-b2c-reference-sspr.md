---
title: "Azure Active Directory B2C：自助式密碼重設 | Microsoft Docs"
description: "此主題示範如何在 Azure Active Directory B2C 中為您的取用者設定自助式密碼重設"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="fc434-103">Azure Active Directory B2C：為您的取用者設定自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="fc434-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="fc434-104">自助式密碼重設功能可讓您的取用者 (已註冊本機帳戶的使用者) 自行重設自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="fc434-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="fc434-105">這可大幅減輕支援人員的負擔，特別是在您的應用程式具有數百萬名定期使用的取用者時更是如此。</span><span class="sxs-lookup"><span data-stu-id="fc434-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="fc434-106">目前僅支援使用已驗證的電子郵件地址做為復原方法。</span><span class="sxs-lookup"><span data-stu-id="fc434-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="fc434-107">我們將在未來新增其他復原方法 (例如已驗證的電話號碼、安全性問題等)。</span><span class="sxs-lookup"><span data-stu-id="fc434-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="fc434-108">本文適用於登入原則內容中使用的自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="fc434-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="fc434-109">如果您需要從應用程式叫用的可完全自訂密碼重設原則，請參閱 [這篇文章](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)。</span><span class="sxs-lookup"><span data-stu-id="fc434-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="fc434-110">依預設，您的目錄並不會開啟自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="fc434-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="fc434-111">使用下列步驟將其開啟：</span><span class="sxs-lookup"><span data-stu-id="fc434-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="fc434-112">以訂用帳戶管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="fc434-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="fc434-113">此為您建立目錄時所用的工作或學校帳戶，或者當時所用的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc434-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="fc434-114">瀏覽至左側導覽列上的 Active Directory 擴充。</span><span class="sxs-lookup"><span data-stu-id="fc434-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="fc434-115">在 [目錄]  索引標籤下方，找到您的目錄並按一下。</span><span class="sxs-lookup"><span data-stu-id="fc434-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="fc434-116">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fc434-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="fc434-117">向下捲動至 [使用者密碼重設原則] 區段，然後將 [使用者啟用密碼重設] 選項切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="fc434-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="fc434-118">請注意，已核取 [備用電子郵件地址]  選項，請保留原狀。</span><span class="sxs-lookup"><span data-stu-id="fc434-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![自助式密碼重設](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="fc434-120">按一下頁面底部的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="fc434-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="fc434-121">大功告成！</span><span class="sxs-lookup"><span data-stu-id="fc434-121">You're done!</span></span>

<span data-ttu-id="fc434-122">如果要進行測試，請針對所有將本機帳戶作為識別提供者的登入原則使用 [立即執行] 功能。</span><span class="sxs-lookup"><span data-stu-id="fc434-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="fc434-123">在本機帳戶登入頁面上 (您輸入電子郵件地址和密碼，或使用者名稱和密碼的頁面)，按一下 [無法存取您的帳戶？] 驗證取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="fc434-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="fc434-124">您可以使用 [公司商標功能](../active-directory/active-directory-add-company-branding.md)自訂自助式密碼重設頁面。</span><span class="sxs-lookup"><span data-stu-id="fc434-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

