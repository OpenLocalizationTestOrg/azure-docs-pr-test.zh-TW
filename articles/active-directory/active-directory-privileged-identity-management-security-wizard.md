---
title: "aaaThe Azure AD Privileged Identity Management 安全性精靈"
description: "hello 第一次使用 hello Azure Active Directory Privileged Identity Management 延伸模組，您會有安全性精靈 」。 本文說明 hello 使用 hello 精靈的步驟。"
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="cbcbf-104">使用 Azure AD Privileged Identity Management 中的 hello 安全性精靈</span><span class="sxs-lookup"><span data-stu-id="cbcbf-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="cbcbf-105">如果您是第一個人 toorun hello Azure Privileged Identity Management (PIM) 為您的組織，您會使用精靈。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="cbcbf-106">hello 精靈可協助您了解的特殊權限的身分識別的 hello 安全性風險以及如何 toouse PIM tooreduce 這些風險。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="cbcbf-107">您不需要 toomake hello 精靈中的任何變更 tooexisting 角色指派的話 toodo 於稍後。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="cbcbf-108">哪些 tooexpect</span><span class="sxs-lookup"><span data-stu-id="cbcbf-108">What tooexpect</span></span>
<span data-ttu-id="cbcbf-109">您的組織開始使用 PIM 之前，會變成永久變更的所有角色指派： hello 使用者一律都會在這些角色即使目前不需要其權限。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="cbcbf-110">hello hello 精靈第一個步驟會顯示高特殊權限角色的清單，且使用者人數目前在這些角色。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="cbcbf-111">您可以鑽研 tooa 進一步了解使用者的特定角色 toolearn 如果其中一個或多個不熟悉。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="cbcbf-112">hello 第二個步驟的 hello 精靈可讓您有機會 toochange 系統管理員的角色指派。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="cbcbf-113">您必須至少有一個全域系統管理員，這一點很重要，而且要有多個具備組織帳戶 (而非 Microsoft 帳戶) 的特殊權限角色管理員。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="cbcbf-114">如果只有一個特殊權限的角色系統管理員，hello 組織將無法能 toomanage PIM 如果刪除該帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="cbcbf-115">此外，保留角色指派永久如果使用者具有 Microsoft 帳戶 （如 Skype 和 Outlook.com tooMicrosoft 服務中使用 toosign 帳戶）。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="cbcbf-116">如果您計劃 toorequire MFA 啟用該角色，該使用者會遭到鎖定。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="cbcbf-117">您所做的變更之後，將不會再顯示 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="cbcbf-118">hello 下次您或其他特殊權限的角色系統管理員使用 PIM，您會看到 hello PIM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="cbcbf-119">如果您會喜歡 tooadd 或從角色移除使用者，或從永久性 tooeligible 變更指派，閱讀更多在[如何 tooadd 或移除使用者角色](active-directory-privileged-identity-management-how-to-add-role-to-user.md)。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="cbcbf-120">如果您想要 toogive 更多使用者存取 toomanage PIM，深入了解在[toogive 如何存取在 PIM toomanage](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="cbcbf-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbcbf-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbcbf-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

