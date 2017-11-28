---
title: "在 Azure Active Directory aaaDedicated 群組 |Microsoft 文件"
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
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="60017-103">Azure Active Directory 中的專用群組</span><span class="sxs-lookup"><span data-stu-id="60017-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="60017-104">在 Azure Active Directory (Azure AD) 中，hello 專用的群組功能，自動建立，並於其中填入預先定義的 Azure AD 群組的成員資格。</span><span class="sxs-lookup"><span data-stu-id="60017-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="60017-105">專用群組的成員無法加入或移除使用 hello Azure 傳統入口網站中，Windows PowerShell cmdlet，或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="60017-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="60017-106">專用群組需要 Azure AD Premium 授權已指派給 </span><span class="sxs-lookup"><span data-stu-id="60017-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="60017-107">負責管理群組中的 hello 規則 hello 系統管理員</span><span class="sxs-lookup"><span data-stu-id="60017-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="60017-108">所有使用者都由 hello 選取都規則 toobe hello 群組的成員</span><span class="sxs-lookup"><span data-stu-id="60017-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="60017-109">**tooenable 專用群組**</span><span class="sxs-lookup"><span data-stu-id="60017-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="60017-110">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後開啟您的組織目錄。</span><span class="sxs-lookup"><span data-stu-id="60017-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="60017-111">選取 hello**群組**索引標籤，然後再開啟 hello 想 tooedit 的群組。</span><span class="sxs-lookup"><span data-stu-id="60017-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="60017-112">選取 hello**設定**索引標籤，然後再設定**啟用專用群組**太**是**。</span><span class="sxs-lookup"><span data-stu-id="60017-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="60017-113">一旦啟用專用群組切換的 hello 設定得**是**，您可以進一步啟用 hello 目錄 tooautomatically 建立 hello 所有使用者專用的群組設定 hello**啟用"All Users"群組**切換太**是**。</span><span class="sxs-lookup"><span data-stu-id="60017-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="60017-114">您接著還可以編輯此專用群組 hello 名稱輸入在 hello**顯示名稱為"All Users"群組**欄位。</span><span class="sxs-lookup"><span data-stu-id="60017-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="60017-115">hello 所有使用者群組可用 tooassign hello 相同使用者權限 tooall hello 目錄中的。</span><span class="sxs-lookup"><span data-stu-id="60017-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="60017-116">例如，您可以授與所有使用者在您的目錄存取 tooa SaaS 應用程式中指派 hello 所有使用者專用的群組 toothis 應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="60017-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="60017-117">hello 專用的所有使用者群組包含所有使用者，在 hello 目錄中，包括來賓與外部使用者。</span><span class="sxs-lookup"><span data-stu-id="60017-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="60017-118">如果您需要一組排除外部使用者，則您可以完成這項作業所建立的群組，並以屬性為基礎動態規則，例如 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="60017-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="60017-119">排除所有客體為群組，請使用例如 hello 下列規則：</span><span class="sxs-lookup"><span data-stu-id="60017-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="60017-120">有關如何 toolearn toocreate*進階*規則 （可以包含多個比較的規則） 的動態群組成員資格，請參閱[使用屬性 toocreate 進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="60017-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="60017-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60017-121">Next steps</span></span>
<span data-ttu-id="60017-122">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="60017-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="60017-123">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="60017-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="60017-124">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="60017-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="60017-125">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="60017-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="60017-126">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60017-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
