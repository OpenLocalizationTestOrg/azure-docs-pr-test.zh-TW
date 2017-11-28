---
title: "aaaAzure Active Directory 識別身分保護通知 |Microsoft 文件"
description: "了解通知如何支援您的調查活動。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="2f247-104">Azure Active Directory Identity Protection 通知</span><span class="sxs-lookup"><span data-stu-id="2f247-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="2f247-105">Azure AD Identity Protection 會傳送兩種類型的自動通知電子郵件的 toohelp 您管理使用者的風險和風險事件：</span><span class="sxs-lookup"><span data-stu-id="2f247-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="2f247-106">使用者遭到入侵的警示電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f247-106">User compromised alert email</span></span>
* <span data-ttu-id="2f247-107">每週精選文章電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f247-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="2f247-108">使用者遭到入侵的警示電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f247-108">User compromised alert email</span></span>
<span data-ttu-id="2f247-109">當 Azure AD Identity Protection 發現帳戶遭到入侵時，就會產生使用者遭到入侵的電子郵件警示。</span><span class="sxs-lookup"><span data-stu-id="2f247-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="2f247-110">hello 電子郵件包含連結 toohello 使用者加上旗標的風險 hello Identity Protection 儀表板中的報表。</span><span class="sxs-lookup"><span data-stu-id="2f247-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="2f247-111">建議您立即調查遭入侵之帳戶的通知。</span><span class="sxs-lookup"><span data-stu-id="2f247-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="2f247-112">每週精選文章電子郵件</span><span class="sxs-lookup"><span data-stu-id="2f247-112">Weekly digest email</span></span>
<span data-ttu-id="2f247-113">hello 每週摘要電子郵件會包含新的風險事件的摘要。</span><span class="sxs-lookup"><span data-stu-id="2f247-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="2f247-114">其中包括：</span><span class="sxs-lookup"><span data-stu-id="2f247-114">It includes:</span></span>

* <span data-ttu-id="2f247-115">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="2f247-115">Users at risk</span></span>
* <span data-ttu-id="2f247-116">可疑的活動</span><span class="sxs-lookup"><span data-stu-id="2f247-116">Suspicious activities</span></span>
* <span data-ttu-id="2f247-117">偵測到的弱點</span><span class="sxs-lookup"><span data-stu-id="2f247-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="2f247-118">連結 toohello 相關的識別身分保護中的報表</span><span class="sxs-lookup"><span data-stu-id="2f247-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="2f247-119">
![補救](./media/active-directory-identityprotection-notifications/400.png "補救")
</span><span class="sxs-lookup"><span data-stu-id="2f247-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="2f247-120">您可以關閉每週精選文章電子郵件的傳送。</span><span class="sxs-lookup"><span data-stu-id="2f247-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="2f247-121">
![使用者風險](./media/active-directory-identityprotection-notifications/62.png "使用者風險")
</span><span class="sxs-lookup"><span data-stu-id="2f247-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="2f247-122">**tooopen hello 相關的組態對話方塊**:</span><span class="sxs-lookup"><span data-stu-id="2f247-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="2f247-123">在 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="2f247-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="2f247-124">
   ![使用者的風險原則](./media/active-directory-identityprotection-notifications/401.png "使用者風險原則")
   </span><span class="sxs-lookup"><span data-stu-id="2f247-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="2f247-125">在 hello**一般**區段中，按一下**通知**。</span><span class="sxs-lookup"><span data-stu-id="2f247-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="2f247-126">
   ![使用者的風險原則](./media/active-directory-identityprotection-notifications/405.png "使用者風險原則")
   </span><span class="sxs-lookup"><span data-stu-id="2f247-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="2f247-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2f247-127">See also</span></span>
* [<span data-ttu-id="2f247-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="2f247-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
