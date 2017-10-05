---
title: "使用群組管理 SaaS 應用程式的存取權 | Microsoft Docs"
description: "如何使用 Azure Active Directory Premium 或 Basic 中的群組指派與 Azure Active Directory 整合的 SaaS 應用程式存取權。"
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="e97d7-103">使用群組管理 SaaS 應用程式的存取權</span><span class="sxs-lookup"><span data-stu-id="e97d7-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="e97d7-104">使用 Azure Active Directory (Azure AD) 搭配 Azure AD Premium 或 Azure AD Basic 授權，您可以使用群組指派與 Azure AD 整合之 SaaS 應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="e97d7-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="e97d7-105">例如，如果您想要指派行銷部門使用五個不同 SaaS 應用程式的存取權，可以建立一個包含行銷部門中的使用者的群組，然後將該群組指派給行銷部門需要的這五個 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e97d7-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="e97d7-106">如此一來，您可以在同一個地方管理行銷部門的成員資格以節省時間。</span><span class="sxs-lookup"><span data-stu-id="e97d7-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="e97d7-107">接著當使用者新增為行銷群組的成員時，會將這些使用者指派給應用程式，並在使用者從行銷群組中移除時，從應用程式中移除其指派。</span><span class="sxs-lookup"><span data-stu-id="e97d7-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e97d7-108">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="e97d7-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="e97d7-109">此功能可以搭配您能夠從 Azure AD 應用程式庫中新增的數百種應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="e97d7-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="e97d7-110">**將群組存取權指派給 SaaS 應用程式**</span><span class="sxs-lookup"><span data-stu-id="e97d7-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="e97d7-111">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，於左側導覽列上選取 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="e97d7-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="e97d7-112">選取 [目錄]  索引標籤，然後開啟您要將群組存取權指派給 Saas 應用程式所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="e97d7-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="e97d7-113">選取 [應用程式]  索引標籤。選取您從「應用程式資源庫」中新增的應用程式，然後按一下 [使用者和群組] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e97d7-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="e97d7-114">在 [使用者和群組] 索引標籤的 [開頭為] 欄位中，輸入您要為其指派存取權的群組名稱，然後選取右上方的核取記號。</span><span class="sxs-lookup"><span data-stu-id="e97d7-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="e97d7-115">您只需要輸入群組名稱的第一個部分。</span><span class="sxs-lookup"><span data-stu-id="e97d7-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="e97d7-116">選取群組，然後選取 [指派存取權]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e97d7-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="e97d7-117">在看到確認訊息時選取 [是]  。</span><span class="sxs-lookup"><span data-stu-id="e97d7-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="e97d7-118">目前對應用程式的群組式指派並不支援巢狀群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="e97d7-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="e97d7-119">您也可以直接或透過群組中的成員資格，查看哪些使用者指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="e97d7-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="e97d7-120">若要這樣做，請將 [顯示下拉式清單] 從 [群組] 變更為 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e97d7-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="e97d7-121">此清單會顯示目錄中的使用者，以及每個使用者是否指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="e97d7-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="e97d7-122">此清單也會顯示獲指派的使用者是直接 (指派類型顯示為 [直接])，還是透過群組成員資格 (指派類型顯示為 [繼承]) 指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="e97d7-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="e97d7-123">只有在啟用 Azure AD Premium 或 Azure AD Basic 之後，您才可以看到 [使用者和群組] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e97d7-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="e97d7-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e97d7-124">Next steps</span></span>
<span data-ttu-id="e97d7-125">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="e97d7-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e97d7-126">使用 Azure Active Directory 群組管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="e97d7-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e97d7-127">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="e97d7-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e97d7-128">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e97d7-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="e97d7-129">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="e97d7-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e97d7-130">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e97d7-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
