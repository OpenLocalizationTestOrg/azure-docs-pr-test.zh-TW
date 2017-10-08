---
title: "為 Azure MFA aaaAssign icenses |Microsoft 文件"
description: "了解如何 tooassign 使用者授權的 Microsoft Azure 多重要素驗證。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: ca324eb4d6622fdad8bd3d74b7e1595919e36535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-toousers"></a><span data-ttu-id="b6afc-103">指派的 Azure MFA、 Azure AD Premium 或 Enterprise Mobility 授權 toousers</span><span class="sxs-lookup"><span data-stu-id="b6afc-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license toousers</span></span>
<span data-ttu-id="b6afc-104">如果您已購買 Azure MFA、 Azure AD Premium 或 Enterprise Mobility Suite 授權，您不需要 toocreate Multi-factor Auth 提供者。</span><span class="sxs-lookup"><span data-stu-id="b6afc-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need toocreate a Multi-Factor Auth provider.</span></span> <span data-ttu-id="b6afc-105">一旦指派授權 hello tooyour 使用者，您可以開始啟用它們的 MFA。</span><span class="sxs-lookup"><span data-stu-id="b6afc-105">Once you assign hello licenses tooyour users, you can begin enabling them for MFA.</span></span>

## <a name="tooassign-a-license"></a><span data-ttu-id="b6afc-106">tooassign 授權</span><span class="sxs-lookup"><span data-stu-id="b6afc-106">tooassign a license</span></span>
1. <span data-ttu-id="b6afc-107">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b6afc-107">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="b6afc-108">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="b6afc-108">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="b6afc-109">在 hello Active Directory 頁面上，按兩下 hello 目錄具有您想 tooenable hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b6afc-109">On hello Active Directory page, double-click hello directory that has hello users you wish tooenable.</span></span>
4. <span data-ttu-id="b6afc-110">在 hello 頂端 hello 目錄 頁面上，選取**授權**。</span><span class="sxs-lookup"><span data-stu-id="b6afc-110">At hello top of hello directory page, select **Licenses**.</span></span>
   <span data-ttu-id="b6afc-111">![指派授權](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="b6afc-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="b6afc-112">在 hello 授權頁面上，選取  **Azure Multi-factor Authentication**， **Active Directory Premium**，或**Enterprise Mobility Suite**。</span><span class="sxs-lookup"><span data-stu-id="b6afc-112">On hello Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="b6afc-113">如果您只有一個，則它應該會自動選取。</span><span class="sxs-lookup"><span data-stu-id="b6afc-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="b6afc-114">在 hello hello 頁面底部，按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="b6afc-114">At hello bottom of hello page, click **Assign**.</span></span>
   <span data-ttu-id="b6afc-115">![指派授權](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="b6afc-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="b6afc-116">在出現 hello 方塊中，按一下 下一步 toohello 使用者或群組想 tooassign 授權。</span><span class="sxs-lookup"><span data-stu-id="b6afc-116">In hello box that comes up, click next toohello users or groups you want tooassign licenses to.</span></span>  <span data-ttu-id="b6afc-117">您應該會看到綠色核取記號出現。</span><span class="sxs-lookup"><span data-stu-id="b6afc-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="b6afc-118">按一下 hello 核取記號圖示 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="b6afc-118">Click hello check mark icon toosave hello changes.</span></span>
   <span data-ttu-id="b6afc-119">![指派授權](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="b6afc-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="b6afc-120">您應該會看到訊息，指出已指派多少授權以及多少授權已失敗。</span><span class="sxs-lookup"><span data-stu-id="b6afc-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="b6afc-121">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b6afc-121">Click **Ok**.</span></span>
   <span data-ttu-id="b6afc-122">![指派授權](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="b6afc-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6afc-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6afc-123">Next steps</span></span>

- <span data-ttu-id="b6afc-124">如需詳細資訊，請參閱[什麼是 Microsoft Azure Active Directory 授權？](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="b6afc-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
