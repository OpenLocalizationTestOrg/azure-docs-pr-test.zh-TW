---
title: "aaaUsing 群組 toomanage 存取 tooSaaS 應用程式 |Microsoft 文件"
description: "如何在 Azure Active Directory Premium 或基本 tooassign toouse 群組存取 tooSaaS 應用程式與 Azure Active Directory 整合。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="960c8-103">使用群組 toomanage 存取 tooSaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="960c8-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="960c8-104">Azure AD Premium 或 Azure AD Basic 授權使用 Azure Active Directory (Azure AD)，您可以使用群組 tooassign 存取 tooa SaaS 應用程式與 Azure AD 整合。</span><span class="sxs-lookup"><span data-stu-id="960c8-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="960c8-105">比方說，如果您想 tooassign hello 行銷部門 toouse 五個不同 SaaS 應用程式的存取，您可以建立包含 hello 行銷部門中的 hello 使用者的群組，然後指派該群組 toothese 五個 SaaS 應用程式hello 行銷部門所需。</span><span class="sxs-lookup"><span data-stu-id="960c8-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="960c8-106">如此一來可以管理的行銷部門在同一個地方 hello hello 成員資格來節省時間。</span><span class="sxs-lookup"><span data-stu-id="960c8-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="960c8-107">然後會指派 toohello 應用程式會在新增為 hello 行銷群組成員，並有它們從 hello 行銷 群組中移除時從 hello 應用程式中移除其指派時。</span><span class="sxs-lookup"><span data-stu-id="960c8-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="960c8-108">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="960c8-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="960c8-109">這項功能可以搭配數百個您可以從新增 hello Azure AD 應用程式庫的應用程式。</span><span class="sxs-lookup"><span data-stu-id="960c8-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="960c8-110">**tooassign 群組 tooa SaaS 應用程式的存取權**</span><span class="sxs-lookup"><span data-stu-id="960c8-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="960c8-111">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**左側 hello hello 導覽列上。</span><span class="sxs-lookup"><span data-stu-id="960c8-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="960c8-112">選取 hello**目錄**索引標籤，然後再開啟 hello 想 tooassign 群組 tooa SaaS 應用程式的存取權的目錄。</span><span class="sxs-lookup"><span data-stu-id="960c8-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="960c8-113">選取 hello**應用程式** 索引標籤。選取您從 hello 應用程式庫新增應用程式，然後按一下hello**使用者和群組** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="960c8-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="960c8-114">在 hello**使用者和群組**索引標籤上，在 hello**開頭**欄位中輸入 hello 名稱要的 hello 群組 toowhich tooassign 存取，然後選取 hello hello 右上角的核取記號。</span><span class="sxs-lookup"><span data-stu-id="960c8-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="960c8-115">您只需要 tootype hello 第一個部分群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="960c8-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="960c8-116">選取 hello 群組，然後再選取 [hello**指派存取權**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="960c8-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="960c8-117">選取**是**您看見 hello 確認訊息。</span><span class="sxs-lookup"><span data-stu-id="960c8-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="960c8-118">在此時間以群組為基礎的指派 tooapplications 不支援巢狀的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="960c8-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="960c8-119">您也可以查看哪些使用者指派 toohello 應用程式，直接或透過群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="960c8-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="960c8-120">toodo，變更 hello**顯示下拉式清單中，從 「 群組 」**太**「 所有使用者 」**。</span><span class="sxs-lookup"><span data-stu-id="960c8-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="960c8-121">hello 清單會顯示 hello 目錄和每個使用者指派 toohello 應用程式中的使用者。</span><span class="sxs-lookup"><span data-stu-id="960c8-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="960c8-122">hello 清單也會顯示是否要指派給 hello 分派使用者 toohello 的應用程式直接 （指派類型顯示為 直接），或依照群組成員資格 （指派類型顯示為 繼承'。）</span><span class="sxs-lookup"><span data-stu-id="960c8-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="960c8-123">只在您啟用 Azure AD Premium 或 Azure AD Basic 之後，您可以看到 hello 使用者和群組 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="960c8-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="960c8-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="960c8-124">Next steps</span></span>
<span data-ttu-id="960c8-125">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="960c8-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="960c8-126">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="960c8-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="960c8-127">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="960c8-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="960c8-128">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="960c8-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="960c8-129">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="960c8-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="960c8-130">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="960c8-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
