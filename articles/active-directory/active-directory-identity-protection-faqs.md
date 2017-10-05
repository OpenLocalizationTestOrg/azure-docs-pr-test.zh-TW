---
title: "Azure Active Directory Identity Protection 常見問題集 | Microsoft Docs"
description: "關於 Azure AD Identity Protection 的常見問題集"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="ea07a-103">Azure Active Directory Identity Protection 常見問題集</span><span class="sxs-lookup"><span data-stu-id="ea07a-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="ea07a-104">為什麼有些風險事件會有「已關閉 (系統)」狀態？</span><span class="sxs-lookup"><span data-stu-id="ea07a-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="ea07a-105">**答︰**這些是 Azure Active Directory Identity Protection 所偵測到，並在稍後因為事件已不再具有危險性而加以關閉的事件。</span><span class="sxs-lookup"><span data-stu-id="ea07a-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="ea07a-106">這些事件不會計入使用者的風險層級。</span><span class="sxs-lookup"><span data-stu-id="ea07a-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="ea07a-107">是否需要成為全域管理員，才能在 Azure 入口網站中使用 Identity Protection？</span><span class="sxs-lookup"><span data-stu-id="ea07a-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="ea07a-108">**答：****否**。</span><span class="sxs-lookup"><span data-stu-id="ea07a-108">**A:** **No**.</span></span> <span data-ttu-id="ea07a-109">成為安全性讀取者、安全性系統管理員或全域管理員都能使用 Identity Protection。</span><span class="sxs-lookup"><span data-stu-id="ea07a-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="ea07a-110">要如何取得 Identity Protection？</span><span class="sxs-lookup"><span data-stu-id="ea07a-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="ea07a-111">**答：**如需此問題的解答，請參閱[開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)。</span><span class="sxs-lookup"><span data-stu-id="ea07a-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="ea07a-112">Azure Active Directory Premium 2 試用版到期時會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="ea07a-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="ea07a-113">**答：**如果您的 Azure Active Directory Free、Basic 或 Premium 1 版本上的 Azure Active Directory Premium 2 試用版已到期，且您已啟用身分識別保護，即使您不符合授權，仍然可以存取它。</span><span class="sxs-lookup"><span data-stu-id="ea07a-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
