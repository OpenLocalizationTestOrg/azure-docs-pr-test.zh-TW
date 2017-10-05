---
title: "使用群組存取管理的後續步驟 | Microsoft Docs"
description: "管理安全性群組，以及如何使用這些群組管理資源的存取權的進階說明。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="80ca8-103">管理群組的擁有者</span><span class="sxs-lookup"><span data-stu-id="80ca8-103">Managing owners for a group</span></span>
<span data-ttu-id="80ca8-104">一旦資源擁有者將資源的存取權指派給 Azure AD 群組後，群組擁有者就會管理群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="80ca8-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="80ca8-105">資源擁有者實際上是委派權限給群組的擁有者，以指派使用者存取資源。</span><span class="sxs-lookup"><span data-stu-id="80ca8-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80ca8-106">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="80ca8-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="80ca8-107">指派群組擁有權</span><span class="sxs-lookup"><span data-stu-id="80ca8-107">Assigning group ownership</span></span>
<span data-ttu-id="80ca8-108">**將擁有者新增至群組**</span><span class="sxs-lookup"><span data-stu-id="80ca8-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="80ca8-109">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，選取 [Active Directory]，然後開啟您組織的目錄。</span><span class="sxs-lookup"><span data-stu-id="80ca8-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="80ca8-110">選取 [群組]  索引標籤，然後開啟您想要在其中新增擁有者的群組。</span><span class="sxs-lookup"><span data-stu-id="80ca8-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="80ca8-111">選取 [新增擁有者] 。</span><span class="sxs-lookup"><span data-stu-id="80ca8-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="80ca8-112">在 [新增擁有者] 頁面上，選取您想要新增為此群組擁有者的使用者，並確定這個名稱新增至 [已選取] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="80ca8-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="80ca8-113">**移除群組中的擁有者**</span><span class="sxs-lookup"><span data-stu-id="80ca8-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="80ca8-114">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，選取 [Active Directory]，然後開啟您組織的目錄。</span><span class="sxs-lookup"><span data-stu-id="80ca8-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="80ca8-115">選取 [群組]  索引標籤，然後開啟您想要從中移除擁有者的群組。</span><span class="sxs-lookup"><span data-stu-id="80ca8-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="80ca8-116">選取 [擁有者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="80ca8-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="80ca8-117">選取您要從這個群組中移除的擁有者，然後選取 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="80ca8-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="80ca8-118">其他資訊</span><span class="sxs-lookup"><span data-stu-id="80ca8-118">Additional information</span></span>
<span data-ttu-id="80ca8-119">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="80ca8-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="80ca8-120">使用 Azure Active Directory 群組管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="80ca8-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="80ca8-121">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="80ca8-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="80ca8-122">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="80ca8-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="80ca8-123">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="80ca8-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="80ca8-124">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80ca8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
