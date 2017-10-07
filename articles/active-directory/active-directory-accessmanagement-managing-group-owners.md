---
title: "aaaNext 步驟來使用群組管理的存取 |Microsoft 文件"
description: "進階方式-戶端管理安全性群組以及 toouse 這些群組 toomanage 存取 tooa 資源。"
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="707c8-103">管理群組的擁有者</span><span class="sxs-lookup"><span data-stu-id="707c8-103">Managing owners for a group</span></span>
<span data-ttu-id="707c8-104">一旦存取 tooa 資源 tooan Azure AD 群組已指派給資源擁有者，hello hello 群組成員資格受 hello 群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="707c8-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="707c8-105">hello 資源擁有者有效地委派 hello 權限 tooassign 使用者 toohello 資源 toohello 群組的擁有者 hello。</span><span class="sxs-lookup"><span data-stu-id="707c8-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="707c8-106">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="707c8-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="707c8-107">指派群組擁有權</span><span class="sxs-lookup"><span data-stu-id="707c8-107">Assigning group ownership</span></span>
<span data-ttu-id="707c8-108">**tooadd 的擁有者 tooa 群組**</span><span class="sxs-lookup"><span data-stu-id="707c8-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="707c8-109">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後開啟您的組織目錄。</span><span class="sxs-lookup"><span data-stu-id="707c8-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="707c8-110">選取 hello**群組**索引標籤，然後再開啟 hello 群組想 tooadd 擁有者。</span><span class="sxs-lookup"><span data-stu-id="707c8-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="707c8-111">選取 [新增擁有者] 。</span><span class="sxs-lookup"><span data-stu-id="707c8-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="707c8-112">在 hello**將擁有者加入**頁面上，選取 hello 使用者想 tooadd 做為此群組中，hello 擁有者，請確定這個名稱已加入 toohello**選取**窗格。</span><span class="sxs-lookup"><span data-stu-id="707c8-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="707c8-113">**tooremove 從群組的擁有者**</span><span class="sxs-lookup"><span data-stu-id="707c8-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="707c8-114">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**Active Directory**，然後開啟您的組織目錄。</span><span class="sxs-lookup"><span data-stu-id="707c8-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="707c8-115">選取 hello**群組**索引標籤，然後再開啟 hello 您想 tooremove 的擁有者群組。</span><span class="sxs-lookup"><span data-stu-id="707c8-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="707c8-116">選取 hello**擁有者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="707c8-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="707c8-117">選取 hello 擁有者，您想要從這個群組中，tooremove，然後選取**移除**。</span><span class="sxs-lookup"><span data-stu-id="707c8-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="707c8-118">其他資訊</span><span class="sxs-lookup"><span data-stu-id="707c8-118">Additional information</span></span>
<span data-ttu-id="707c8-119">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="707c8-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="707c8-120">使用 Azure Active Directory 群組來管理存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="707c8-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="707c8-121">設定群組設定的 Azure Active Directory Cmdlet</span><span class="sxs-lookup"><span data-stu-id="707c8-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="707c8-122">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="707c8-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="707c8-123">什麼是 Azure Active Directory？</span><span class="sxs-lookup"><span data-stu-id="707c8-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="707c8-124">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="707c8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
