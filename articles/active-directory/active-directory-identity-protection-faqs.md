---
title: "aaaAzure Active Directory 識別身分保護常見問題集 |Microsoft 文件"
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
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="dfeea-103">Azure Active Directory Identity Protection 常見問題集</span><span class="sxs-lookup"><span data-stu-id="dfeea-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="dfeea-104">為什麼有些風險事件會有「已關閉 (系統)」狀態？</span><span class="sxs-lookup"><span data-stu-id="dfeea-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="dfeea-105">**答：**這些是 Azure Active Directory 識別身分保護偵測到並稍後再關閉，因為已不再視為高風險 hello 事件的事件。</span><span class="sxs-lookup"><span data-stu-id="dfeea-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="dfeea-106">這些事件不會計入 hello 使用者的風險層級。</span><span class="sxs-lookup"><span data-stu-id="dfeea-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="dfeea-107">是否需要 toobe hello Azure 入口網站中的全域管理員 toouse 識別身分保護？</span><span class="sxs-lookup"><span data-stu-id="dfeea-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="dfeea-108">**答：****否**。</span><span class="sxs-lookup"><span data-stu-id="dfeea-108">**A:** **No**.</span></span> <span data-ttu-id="dfeea-109">您可以安全讀取器、 安全性系統管理員或全域管理員 toouse 識別身分保護。</span><span class="sxs-lookup"><span data-stu-id="dfeea-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="dfeea-110">要如何取得 Identity Protection？</span><span class="sxs-lookup"><span data-stu-id="dfeea-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="dfeea-111">**答：**看到[開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)回應 toothis 問題。</span><span class="sxs-lookup"><span data-stu-id="dfeea-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="dfeea-112">Azure Active Directory Premium 2 試用版到期時會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="dfeea-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="dfeea-113">**答：**如果您的 Azure Active Directory Premium 2 試用版已過期在 Azure Active Directory Free、 Basic 或 Premium 1 版本中，您必須啟用識別身分保護，您仍必須存取 tooit 即使不 compliance 與授權。</span><span class="sxs-lookup"><span data-stu-id="dfeea-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
