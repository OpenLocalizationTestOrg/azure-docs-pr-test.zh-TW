---
title: "Azure AD Privileged Identity Management 安全性精靈"
description: "第一次使用 Azure Active Directory Privileged Identity Management 擴充功能時，您將會看到安全性精靈。 本文說明使用精靈的步驟。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="0cf96-104">在 Azure AD Privileged Identity Management 中使用安全性精靈</span><span class="sxs-lookup"><span data-stu-id="0cf96-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="0cf96-105">如果您是貴組織中執行 Azure Privileged Identity Management (PIM) 的第一個人，您就會看到精靈。</span><span class="sxs-lookup"><span data-stu-id="0cf96-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="0cf96-106">精靈會協助您了解特殊權限身分識別的安全性風險，以及如何使用 PIM 來降低這些風險。</span><span class="sxs-lookup"><span data-stu-id="0cf96-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="0cf96-107">如果您想要稍後再進行變更，就不需要在精靈中對現有的角色指派進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="0cf96-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="0cf96-108">未來展望</span><span class="sxs-lookup"><span data-stu-id="0cf96-108">What to expect</span></span>
<span data-ttu-id="0cf96-109">在貴組織開始使用 PIM 之前，所有的角色指派都是永久的︰即使使用者目前不需要其權限，他們都一直保有這些角色。</span><span class="sxs-lookup"><span data-stu-id="0cf96-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="0cf96-110">精靈的第一個步驟會顯示高特殊權限角色的清單，以及這些角色中目前有多少使用者。</span><span class="sxs-lookup"><span data-stu-id="0cf96-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="0cf96-111">如果不清楚一或多個角色，您可以向內切入某個特定角色來深入了解使用者。</span><span class="sxs-lookup"><span data-stu-id="0cf96-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="0cf96-112">精靈的第二個步驟會讓您有機會變更系統管理員的角色指派。</span><span class="sxs-lookup"><span data-stu-id="0cf96-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="0cf96-113">您必須至少有一個全域系統管理員，這一點很重要，而且要有多個具備組織帳戶 (而非 Microsoft 帳戶) 的特殊權限角色管理員。</span><span class="sxs-lookup"><span data-stu-id="0cf96-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="0cf96-114">如果只有一個特殊權限角色管理員，若該帳戶遭到刪除，組織就無法管理 PIM。</span><span class="sxs-lookup"><span data-stu-id="0cf96-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="0cf96-115">此外，如果使用者擁有 Microsoft 帳戶 (他們用來登入 Skype 和 Outlook.com 這類 Microsoft 服務的帳戶)，請將角色指派設為永久。</span><span class="sxs-lookup"><span data-stu-id="0cf96-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="0cf96-116">如果您打算要求必須執行 MFA 才能啟用該角色，該使用者將會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="0cf96-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="0cf96-117">進行變更之後，將不會再次顯示精靈。</span><span class="sxs-lookup"><span data-stu-id="0cf96-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="0cf96-118">下次當您或其他特殊權限角色管理員使用 PIM 時，您將會看到 PIM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="0cf96-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="0cf96-119">如果您想要從角色新增或移除使用者，或將指派從永久變更為符合資格，請參閱 [如何新增或移除使用者的角色](active-directory-privileged-identity-management-how-to-add-role-to-user.md)。</span><span class="sxs-lookup"><span data-stu-id="0cf96-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="0cf96-120">如果您想要讓更多使用者存取管理 PIM，請參閱 [How to give access to manage Azure AD Privileged Identity Management (如何授與存取權以管理 Azure AD Privileged Identity Management)](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="0cf96-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf96-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cf96-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

