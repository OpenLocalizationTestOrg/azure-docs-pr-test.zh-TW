---
title: "開始使用 Azure AD Privileged Identity Management 的 aaaGet |Microsoft 文件"
description: "了解如何 toomanage 特殊權限身分識別與 Azure 入口網站中的 hello Azure Active Directory Privileged Identity Management 應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="33c69-103">開始使用 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="33c69-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="33c69-104">您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。</span><span class="sxs-lookup"><span data-stu-id="33c69-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="33c69-105">此範圍包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="33c69-105">This scope includes access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="33c69-106">這篇文章會告訴您如何 tooadd hello Azure AD PIM 應用程式 tooyour Azure 入口網站的儀表板。</span><span class="sxs-lookup"><span data-stu-id="33c69-106">This article tells you how tooadd hello Azure AD PIM app tooyour Azure portal dashboard.</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="33c69-107">新增 hello Privileged Identity Management 的應用程式</span><span class="sxs-lookup"><span data-stu-id="33c69-107">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="33c69-108">使用 Azure AD Privileged Identity Management 之前，您會需要 tooadd hello 應用程式 tooyour Azure 入口網站的儀表板。</span><span class="sxs-lookup"><span data-stu-id="33c69-108">Before you use Azure AD Privileged Identity Management, you need tooadd hello application tooyour Azure portal dashboard.</span></span>

1. <span data-ttu-id="33c69-109">登入 toohello [Azure 入口網站](https://portal.azure.com/)您目錄的全域管理員身分。</span><span class="sxs-lookup"><span data-stu-id="33c69-109">Sign in toohello [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="33c69-110">如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="33c69-110">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="33c69-111">選取您希望 toouse PIM hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="33c69-111">Select hello directory where you want toouse PIM.</span></span>
3. <span data-ttu-id="33c69-112">選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。</span><span class="sxs-lookup"><span data-stu-id="33c69-112">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="33c69-113">請檢查**Pin toodashboard** ，然後按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="33c69-113">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="33c69-114">hello Privileged Identity Management 的應用程式會開啟。</span><span class="sxs-lookup"><span data-stu-id="33c69-114">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="33c69-115">如果您正在 hello 第一個人 toouse Azure AD Privileged Identity Management 目錄中，您會自動指派給 hello**安全性系統管理員**和**特殊權限的角色管理員**角色在 [hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="33c69-115">If you're hello first person toouse Azure AD Privileged Identity Management in your directory, you are automatically assigned hello **Security administrator** and **Privileged role administrator** roles in hello directory.</span></span> <span data-ttu-id="33c69-116">只有特殊權限角色管理員才能管理使用者的角色指派。</span><span class="sxs-lookup"><span data-stu-id="33c69-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="33c69-117">此外，您可以選擇 toorun hello[安全性精靈 」。](active-directory-privileged-identity-management-security-wizard.md)</span><span class="sxs-lookup"><span data-stu-id="33c69-117">In addition, you may choose toorun hello [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="33c69-118">會引導您經由 hello 初始探索與指派體驗。</span><span class="sxs-lookup"><span data-stu-id="33c69-118">that walks you through hello initial discovery and assignment experience.</span></span>

## <a name="navigate-tooyour-tasks"></a><span data-ttu-id="33c69-119">瀏覽 tooyour 工作</span><span class="sxs-lookup"><span data-stu-id="33c69-119">Navigate tooyour tasks</span></span>
<span data-ttu-id="33c69-120">一旦設定 Azure AD Privileged Identity Management 之後，每當您開啟 hello 應用程式時看到 hello 瀏覽] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="33c69-120">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span> <span data-ttu-id="33c69-121">使用此刀鋒視窗 tooaccomplish 身分識別管理工作。</span><span class="sxs-lookup"><span data-stu-id="33c69-121">Use this blade tooaccomplish your identity management tasks.</span></span>

![PIM 的最上層工作 - 螢幕擷取畫面](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="33c69-123">**我角色**會帶您角色指派 tooyou tooa 清單。</span><span class="sxs-lookup"><span data-stu-id="33c69-123">**My Roles** takes you tooa list of roles that are assigned tooyou.</span></span> <span data-ttu-id="33c69-124">您可以在此區段中啟動任何您具備資格的角色。</span><span class="sxs-lookup"><span data-stu-id="33c69-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="33c69-125">**核准要求 (預覽)** 會顯示目錄中來自使用者的擱置啟用要求清單。</span><span class="sxs-lookup"><span data-stu-id="33c69-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="33c69-126">深入了解。</span><span class="sxs-lookup"><span data-stu-id="33c69-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="33c69-127">**擱置的要求 （預覽）**會顯示任何目前的要求進行 toohave tooactivate。</span><span class="sxs-lookup"><span data-stu-id="33c69-127">**Pending Requests (Preview)** displays any current requests toohave made tooactivate.</span></span>
* <span data-ttu-id="33c69-128">**檢閱存取**採用 tooany 暫止的存取會檢閱您需要 toocomplete，是否在檢閱您自己或其他人的存取。</span><span class="sxs-lookup"><span data-stu-id="33c69-128">**Review Access** takes you tooany pending access reviews that you need toocomplete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="33c69-129">**Azure AD 目錄角色**位於 hello '管理' 區段是特殊權限的角色 admins toomanage 角色指派、 變更角色的啟用設定、 開始存取檢閱等等 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="33c69-129">**Azure AD Directory Roles** located under hello 'Manage' section is hello dashboard for privileged role admins toomanage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="33c69-130">此儀表板中的 hello 選項會停用不是特殊權限的角色系統管理員的人。</span><span class="sxs-lookup"><span data-stu-id="33c69-130">hello options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33c69-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33c69-131">Next steps</span></span>
<span data-ttu-id="33c69-132">hello [Azure AD Privileged Identity Management 概觀](active-directory-privileged-identity-management-configure.md)包含上如何管理系統管理存取權，以及在組織中的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="33c69-132">hello [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
