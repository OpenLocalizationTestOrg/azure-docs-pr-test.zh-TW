---
title: "aaaAzure Active Directory 報告通知"
description: "如何 toouse hello Azure Active Directory 報告通知可疑的登入。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="06665-103">Azure Active Directory 報告通知</span><span class="sxs-lookup"><span data-stu-id="06665-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="06665-104">哪些報告會產生電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="06665-104">What reports generate email notifications</span></span>
<span data-ttu-id="06665-105">此時，只有 hello 異常的登活動報表觸發程序中的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="06665-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="06665-106">什麼是「異常的登入」？</span><span class="sxs-lookup"><span data-stu-id="06665-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="06665-107">異常的登入是已透過機器學習演算法，根據 「 不可能的旅遊 」 條件結合異常的登入位置和裝置的 hello 識別。</span><span class="sxs-lookup"><span data-stu-id="06665-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="06665-108">這可能表示駭客有已嘗試 toosign 中使用此帳戶。</span><span class="sxs-lookup"><span data-stu-id="06665-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="06665-109">誰會收到 hello 電子郵件通知？</span><span class="sxs-lookup"><span data-stu-id="06665-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="06665-110">hello 電子郵件傳送給獲得 Active Directory Premium 授權的 tooall 全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="06665-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="06665-111">tooensure 傳遞，我們將它傳送 toohello admins 替代電子郵件地址以及。</span><span class="sxs-lookup"><span data-stu-id="06665-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="06665-112">系統管理員應該包含aad-alerts-noreply@mail.windowsazure.com遺漏 hello 電子郵件安全寄件者清單中。</span><span class="sxs-lookup"><span data-stu-id="06665-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="06665-113">這些電子郵件的傳送頻率為何？</span><span class="sxs-lookup"><span data-stu-id="06665-113">How often are these emails sent?</span></span>
<span data-ttu-id="06665-114">如果 10 新異常登入活動會在 hello 過去 30 天內，或已傳送 hello 最後一個電子郵件，因為小者為準，會傳送 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="06665-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="06665-115">如何存取 hello 電子郵件中所述的 hello 報表？</span><span class="sxs-lookup"><span data-stu-id="06665-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="06665-116">當您按一下 hello 連結時，您會重新導向的 toohello hello Azure 傳統入口網站中的報表頁面。</span><span class="sxs-lookup"><span data-stu-id="06665-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="06665-117">順序 tooaccess hello 報表，您需要 toobe 這兩種：</span><span class="sxs-lookup"><span data-stu-id="06665-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="06665-118">您的 Azure 訂用帳戶的管理員或共同管理員</span><span class="sxs-lookup"><span data-stu-id="06665-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="06665-119">Hello 目錄中的全域管理員，並指派 Active Directory Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="06665-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="06665-120">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="06665-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="06665-121">我可以關閉這些電子郵件嗎？</span><span class="sxs-lookup"><span data-stu-id="06665-121">Can I turn off these emails?</span></span>
<span data-ttu-id="06665-122">[是]，關閉通知 tooturn 相關 tooanomalous 登入 hello Azure 傳統入口網站中，按一下**設定**，然後選取**已停用**下 hello**通知**> 一節。</span><span class="sxs-lookup"><span data-stu-id="06665-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="06665-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06665-123">What's next</span></span>
* <span data-ttu-id="06665-124">想知道有哪些安全性、稽核及活動報告可用嗎？</span><span class="sxs-lookup"><span data-stu-id="06665-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="06665-125">請查看 [Azure AD 安全性、稽核及活動報告](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="06665-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="06665-126">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="06665-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="06665-127">新增公司品牌 tooyour 登入及存取面板頁面</span><span class="sxs-lookup"><span data-stu-id="06665-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

