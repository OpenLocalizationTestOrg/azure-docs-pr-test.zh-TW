---
title: "Azure Active Directory B2C：自助式密碼重設 | Microsoft Docs"
description: "主題，示範如何 tooset 註冊自助式密碼重設您的取用者，於 Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="429de-103">Azure Active Directory B2C：為您的取用者設定自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="429de-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="429de-104">以 hello 自助式密碼重設功能，您消費者 （已註冊的本機帳戶） 可以重設他們自己的密碼。</span><span class="sxs-lookup"><span data-stu-id="429de-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="429de-105">這會大幅降低您的支援人員 hello 負擔，特別是當您的應用程式有數百萬個使用以規則為基礎的取用者。</span><span class="sxs-lookup"><span data-stu-id="429de-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="429de-106">目前僅支援使用已驗證的電子郵件地址做為復原方法。</span><span class="sxs-lookup"><span data-stu-id="429de-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="429de-107">Hello 未來，我們會加入額外的修復方法 （已驗證的電話號碼、 安全性問題等）。</span><span class="sxs-lookup"><span data-stu-id="429de-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="429de-108">本文件適用於 tooself 服務密碼重設登入原則的 hello 內容中使用。</span><span class="sxs-lookup"><span data-stu-id="429de-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="429de-109">如果您需要從應用程式叫用的可完全自訂密碼重設原則，請參閱 [這篇文章](active-directory-b2c-reference-policies.md#create-a-password-reset-policy)。</span><span class="sxs-lookup"><span data-stu-id="429de-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="429de-110">依預設，您的目錄並不會開啟自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="429de-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="429de-111">使用 hello 下列步驟 tooturn 它上：</span><span class="sxs-lookup"><span data-stu-id="429de-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="429de-112">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)為 hello 訂用帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="429de-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="429de-113">這是的 hello 相同工作或學校帳戶或 hello 與您用 toocreate 您目錄的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="429de-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="429de-114">瀏覽 toohello hello hello 左邊的巡覽列上的 Active Directory 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="429de-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="429de-115">尋找您的目錄下 hello**目錄**索引標籤，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="429de-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="429de-116">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="429de-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="429de-117">捲動 toohello**使用者密碼重設原則**> 一節，並切換 hello**使用者啟用密碼重設**太選項**是**。</span><span class="sxs-lookup"><span data-stu-id="429de-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="429de-118">請注意該 hello**替代電子郵件地址**核取選項，讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="429de-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![自助式密碼重設](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="429de-120">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="429de-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="429de-121">大功告成！</span><span class="sxs-lookup"><span data-stu-id="429de-121">You're done!</span></span>

<span data-ttu-id="429de-122">tootest 使用 hello 「 立即執行 」 功能上任何身分識別提供者具有本機帳戶的登入的原則。</span><span class="sxs-lookup"><span data-stu-id="429de-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="429de-123">Hello 本機帳戶登入頁面上 （在您輸入電子郵件地址和密碼，或使用者名稱和密碼），按一下**無法存取您的帳戶？** tooverify hello 經驗。</span><span class="sxs-lookup"><span data-stu-id="429de-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="429de-124">hello 自助式密碼重設頁面可以使用來自訂 hello[公司品牌功能](../active-directory/active-directory-add-company-branding.md)。</span><span class="sxs-lookup"><span data-stu-id="429de-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

