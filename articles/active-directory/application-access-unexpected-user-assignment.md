---
title: "如何將使用者指派至應用程式 | Microsoft Docs"
description: "了解如何將使用者指派至租用戶中的應用程式"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="edc16-103">將使用者指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="edc16-103">How to assign users to applications</span></span>

<span data-ttu-id="edc16-104">本文協助您了解如何將使用者指派至租用戶中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="edc16-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="edc16-105">如何將使用者指派至 Azure AD 中的應用程式？</span><span class="sxs-lookup"><span data-stu-id="edc16-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="edc16-106">若要讓使用者存取應用程式，必須先設法將他們指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="edc16-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="edc16-107">可以由系統管理員、企業代理人，或有時是使用者本身來指派。</span><span class="sxs-lookup"><span data-stu-id="edc16-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="edc16-108">以下描述將使用者指派至應用程式的方法︰</span><span class="sxs-lookup"><span data-stu-id="edc16-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="edc16-109">系統管理員直接[指派使用者](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)至應用程式</span><span class="sxs-lookup"><span data-stu-id="edc16-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="edc16-110">系統管理員[指派群組](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) (使用者所屬的群組) 至應用程式，包括︰</span><span class="sxs-lookup"><span data-stu-id="edc16-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="edc16-111">已從內部部署同步的群組</span><span class="sxs-lookup"><span data-stu-id="edc16-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="edc16-112">在雲端中建立的靜態安全性群組</span><span class="sxs-lookup"><span data-stu-id="edc16-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="edc16-113">在雲端中建立的[動態安全性群組](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="edc16-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="edc16-114">在雲端中建立的 Office 365 群組</span><span class="sxs-lookup"><span data-stu-id="edc16-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="edc16-115">[所有使用者](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)群組</span><span class="sxs-lookup"><span data-stu-id="edc16-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="edc16-116">系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)，以允許使用者利用[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)的**新增應用程式**功能新增應用程式，而**不需要商務核准**</span><span class="sxs-lookup"><span data-stu-id="edc16-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="edc16-117">系統管理員啟用[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)，以允許使用者利用[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)的**新增應用程式**功能新增應用程式，但需要經過**一群選定商務核准者的事先核准**</span><span class="sxs-lookup"><span data-stu-id="edc16-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="edc16-118">系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)，以允許使用者加入已指派應用程式的群組，而**不需要商務核准**</span><span class="sxs-lookup"><span data-stu-id="edc16-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="edc16-119">系統管理員啟用[自助群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)，以允許使用者加入已指派應用程式的群組，但需要經過**一群選定商務核准者的事先核准**</span><span class="sxs-lookup"><span data-stu-id="edc16-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="edc16-120">系統管理員將第一方應用程式 (例如 [Microsoft Office 365](http://products.office.com/)) 的授權直接指派給使用者</span><span class="sxs-lookup"><span data-stu-id="edc16-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="edc16-121">系統管理員將第一方應用程式 (例如 [Microsoft Office 365](http://products.office.com/)) 的授權指派給使用者所屬的群組</span><span class="sxs-lookup"><span data-stu-id="edc16-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="edc16-122">[系統管理員同意應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)供所有使用者使用，然後使用者登入應用程式</span><span class="sxs-lookup"><span data-stu-id="edc16-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="edc16-123">使用者本身登入應用程式以[同意應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)</span><span class="sxs-lookup"><span data-stu-id="edc16-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="edc16-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edc16-124">Next steps</span></span>
[<span data-ttu-id="edc16-125">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="edc16-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
