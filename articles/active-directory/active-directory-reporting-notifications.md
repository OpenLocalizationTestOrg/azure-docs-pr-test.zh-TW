---
title: "Azure Active Directory 報告通知"
description: "如何使用 Azure Active Directory 報告通知找出可疑登入。"
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
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="0dcd2-103">Azure Active Directory 報告通知</span><span class="sxs-lookup"><span data-stu-id="0dcd2-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="0dcd2-104">哪些報告會產生電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="0dcd2-104">What reports generate email notifications</span></span>
<span data-ttu-id="0dcd2-105">在此階段中，只有異常的登入活動報告會觸發電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="0dcd2-106">什麼是「異常的登入」？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="0dcd2-107">異常登入是指機器學習服務演算法已經根據結合異常登入位置和裝置的「不可能的行進」條件識別的登入活動。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="0dcd2-108">這可能表示駭客已嘗試使用此帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="0dcd2-109">誰會收到電子郵件通知？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-109">Who receives the email notifications?</span></span>
<span data-ttu-id="0dcd2-110">電子郵件會傳送給所有已獲指派 Active Directory Premium 授權的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="0dcd2-111">為了確保能夠送達，我們也會將電子郵件傳送到管理員的備用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="0dcd2-112">管理員應將 aad-alerts-noreply@mail.windowsazure.com 納入其安全寄件者清單中，以免遺漏電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="0dcd2-113">這些電子郵件的傳送頻率為何？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-113">How often are these emails sent?</span></span>
<span data-ttu-id="0dcd2-114">如果過去的 30 天內或自從最後一次傳送電子郵件後 (視何者日數較少) 發生 10 起新的異常登入活動，就會傳送本電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="0dcd2-115">如何存取電子郵件中提到的報告？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="0dcd2-116">當您按一下連結時，系統會將您重新導向至 Azure 傳統入口網站中的報告頁面。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="0dcd2-117">若要存取報告，您必須同時是：</span><span class="sxs-lookup"><span data-stu-id="0dcd2-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="0dcd2-118">您的 Azure 訂用帳戶的管理員或共同管理員</span><span class="sxs-lookup"><span data-stu-id="0dcd2-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="0dcd2-119">目錄中的全域管理員，並獲得指派的 Active Directory Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="0dcd2-120">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="0dcd2-121">我可以關閉這些電子郵件嗎？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-121">Can I turn off these emails?</span></span>
<span data-ttu-id="0dcd2-122">是，若要關閉 Azure 傳統入口網站中異常登入的相關通知，請按一下 [設定]，然後選取 [通知] 區段之下的 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="0dcd2-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="0dcd2-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dcd2-123">What's next</span></span>
* <span data-ttu-id="0dcd2-124">想知道有哪些安全性、稽核及活動報告可用嗎？</span><span class="sxs-lookup"><span data-stu-id="0dcd2-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="0dcd2-125">請查看 [Azure AD 安全性、稽核及活動報告](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="0dcd2-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="0dcd2-126">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="0dcd2-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="0dcd2-127">在登入和存取面板頁面加上公司商標</span><span class="sxs-lookup"><span data-stu-id="0dcd2-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

