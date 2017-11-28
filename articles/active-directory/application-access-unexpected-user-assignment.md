---
title: "aaaHow tooAssign 使用者 tooapplications |Microsoft 文件"
description: "了解使用者如何取得指派 tooan 租用戶中的應用程式"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="47ef0-103">如何 tooassign 使用者 tooapplications</span><span class="sxs-lookup"><span data-stu-id="47ef0-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="47ef0-104">本文將協助您 toounderstand 使用者取得如何指派 tooan 租用戶中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="47ef0-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="47ef0-105">如何使用者取得指派 tooan 在 Azure AD 中的應用程式？</span><span class="sxs-lookup"><span data-stu-id="47ef0-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="47ef0-106">使用者 tooaccess 應用程式，則必須先指派 tooit 以某種方式。</span><span class="sxs-lookup"><span data-stu-id="47ef0-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="47ef0-107">作業只能由系統管理員、 商務委派，或某些情況下，hello 使用者本身。</span><span class="sxs-lookup"><span data-stu-id="47ef0-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="47ef0-108">下面將描述使用者可以指派 tooapplications hello 方式：</span><span class="sxs-lookup"><span data-stu-id="47ef0-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="47ef0-109">系統管理員[指派使用者](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)直接 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="47ef0-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="47ef0-110">系統管理員[指派群組](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)hello 使用者所屬 toohello 應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="47ef0-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="47ef0-111">已從內部部署同步的群組</span><span class="sxs-lookup"><span data-stu-id="47ef0-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="47ef0-112">建立 hello 雲端中的靜態安全性群組</span><span class="sxs-lookup"><span data-stu-id="47ef0-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="47ef0-113">A[動態安全性群組](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal)hello 雲端中建立</span><span class="sxs-lookup"><span data-stu-id="47ef0-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="47ef0-114">建立 hello 雲端中的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="47ef0-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="47ef0-115">hello[所有使用者](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)群組</span><span class="sxs-lookup"><span data-stu-id="47ef0-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="47ef0-116">系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooallow 應用程式使用使用者 tooadd hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)**新增應用程式**功能**無商務核准**</span><span class="sxs-lookup"><span data-stu-id="47ef0-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="47ef0-117">系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooallow 應用程式使用使用者 tooadd hello[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)**新增應用程式**功能，但只有 w**ith 先前組選取的公司核准者核准**</span><span class="sxs-lookup"><span data-stu-id="47ef0-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="47ef0-118">系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)tooallow 使用者 toojoin 太指派應用程式群組**無商務核准**</span><span class="sxs-lookup"><span data-stu-id="47ef0-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="47ef0-119">系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)tooallow 使用者 toojoin 應用程式，但只能指派一組**與先前組選取的公司核准者核准**</span><span class="sxs-lookup"><span data-stu-id="47ef0-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="47ef0-120">系統管理員指派授權 tooa 使用者直接針對第一個合作對象應用程式，例如[Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="47ef0-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="47ef0-121">Hello 使用者的授權 tooa 群組隸屬的 tooa 第一個合作對象應用程式，例如系統管理員指派[Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="47ef0-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="47ef0-122">[Tooan 應用程式，系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)toobe 由所有使用者，而且使用者在登入時 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="47ef0-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="47ef0-123">使用者[tooan 應用程式，同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)自行登入 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="47ef0-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="47ef0-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47ef0-124">Next steps</span></span>
[<span data-ttu-id="47ef0-125">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="47ef0-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
