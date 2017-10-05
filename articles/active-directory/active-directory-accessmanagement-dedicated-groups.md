---
title: "Azure Active Directory 中的專用群組 | Microsoft Docs"
description: "在 Azure Active Directory 中如何建立專用群組與其運作方式的概觀。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="165ea-103">Azure Active Directory 中的專用群組</span><span class="sxs-lookup"><span data-stu-id="165ea-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="165ea-104">在 Azure Active Directory (Azure AD) 中，專用群組功能會針對 Azure AD 預先定義的群組自動建立並填入成員資格。</span><span class="sxs-lookup"><span data-stu-id="165ea-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="165ea-105">使用 Azure 傳統入口網站、Windows PowerShell Cmdlet 或以程式設計方式，均無法在專用群組中新增或移除成員。</span><span class="sxs-lookup"><span data-stu-id="165ea-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="165ea-106">專用群組需要 Azure AD Premium 授權已指派給 </span><span class="sxs-lookup"><span data-stu-id="165ea-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="165ea-107">負責管理群組規則的系統管理員</span><span class="sxs-lookup"><span data-stu-id="165ea-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="165ea-108">已由規則選取要成為群組成員的所有使用者</span><span class="sxs-lookup"><span data-stu-id="165ea-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="165ea-109">**啟用專用群組**</span><span class="sxs-lookup"><span data-stu-id="165ea-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="165ea-110">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，選取 [Active Directory]，然後開啟您組織的目錄。</span><span class="sxs-lookup"><span data-stu-id="165ea-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="165ea-111">選取 [群組]  索引標籤，然後開啟您想要編輯的群組。</span><span class="sxs-lookup"><span data-stu-id="165ea-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="165ea-112">選取 [設定] 索引標籤，然後將 [啟用專用群組] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="165ea-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="165ea-113">將 [啟用專用群組] 參數設定為 [是] 之後，您就可以將 [啟用「所有使用者」群組] 參數設定為 [是]，進一步讓目錄自動建立「所有使用者」專用群組。</span><span class="sxs-lookup"><span data-stu-id="165ea-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="165ea-114">接著，您也可以在 **[All Users] 群組欄位的 [顯示名稱]** 中輸入此專用群組的名稱進行編輯。</span><span class="sxs-lookup"><span data-stu-id="165ea-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="165ea-115">[All Users] 群組可用來將相同的權限指派給您目錄中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="165ea-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="165ea-116">例如，您可以將 [All Users] 專用群組的存取權指派給此應用程式，以便為您目錄中的所有使用者授與 SaaS 應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="165ea-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="165ea-117">專用的 [All Users] 群組包含目錄中的所有使用者，包括來賓與外部使用者。</span><span class="sxs-lookup"><span data-stu-id="165ea-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="165ea-118">如果需要從群組中排除外部使用者，您可以使用如下的屬性型動態規則來建立群組：</span><span class="sxs-lookup"><span data-stu-id="165ea-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="165ea-119">如需從群組中排除所有來賓，請使用如下的規則：</span><span class="sxs-lookup"><span data-stu-id="165ea-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="165ea-120">若要了解如何為動態群組成員資格建立「進階」  規則 (可包含多個比較的規則)，請參閱 [使用屬性來建立進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="165ea-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="165ea-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="165ea-121">Next steps</span></span>
<span data-ttu-id="165ea-122">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="165ea-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="165ea-123">使用 Azure Active Directory 群組管理資源的存取權</span><span class="sxs-lookup"><span data-stu-id="165ea-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="165ea-124">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="165ea-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="165ea-125">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="165ea-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="165ea-126">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="165ea-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
