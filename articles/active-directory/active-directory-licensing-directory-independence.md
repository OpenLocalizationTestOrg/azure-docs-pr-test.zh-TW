---
title: "aaaCharacteristics 的 Azure Active Directory 租用戶 intercaction |Microsoft 文件"
description: "了解您的目錄為完全獨立的資源，以管理 Azure Active Directory 租用戶"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="c5aab-103">了解多個 Azure Active Directory 租用戶如何互動</span><span class="sxs-lookup"><span data-stu-id="c5aab-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="c5aab-104">在 Azure Active Directory (Azure AD) 中，每個租用戶已完全獨立的資源： 邏輯上獨立於對等體 hello 您管理其他租用戶。</span><span class="sxs-lookup"><span data-stu-id="c5aab-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="c5aab-105">租用戶之間沒有任何父子關聯性。</span><span class="sxs-lookup"><span data-stu-id="c5aab-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="c5aab-106">這個在租用戶之間的獨立性包括資源獨立性、系統管理獨立性，以及同步處理獨立性。</span><span class="sxs-lookup"><span data-stu-id="c5aab-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="c5aab-107">資源獨立性</span><span class="sxs-lookup"><span data-stu-id="c5aab-107">Resource independence</span></span>
* <span data-ttu-id="c5aab-108">如果您建立或刪除一個租用戶中的資源時，它沒有任何影響另一個租用戶中，具有 hello 外部使用者的部分例外狀況的任何資源。</span><span class="sxs-lookup"><span data-stu-id="c5aab-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="c5aab-109">如果將您的其中一個網域名稱與某個租用戶搭配使用，該網域名稱就無法與任何其他租用戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c5aab-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="c5aab-110">系統管理獨立性</span><span class="sxs-lookup"><span data-stu-id="c5aab-110">Administrative independence</span></span>
<span data-ttu-id="c5aab-111">如果 'Contoso' 租用戶的非系統管理使用者建立 'Test' 測試租用戶，則：</span><span class="sxs-lookup"><span data-stu-id="c5aab-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="c5aab-112">根據預設，建立租用戶的 hello 使用者會成為該新的租用戶和指派的 hello 該租用戶全域管理員角色的外部使用者。</span><span class="sxs-lookup"><span data-stu-id="c5aab-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="c5aab-113">租用戶 'Contoso' hello 系統管理員有沒有直接的系統管理權限 tootenant 'Test'，除非 'Test' 的系統管理員特別授與這些權限。</span><span class="sxs-lookup"><span data-stu-id="c5aab-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="c5aab-114">不過，'Contoso' 的系統管理員可以控制存取 tootenant 'Test' 如果它們控制 hello 使用者帳戶建立 'Test'。</span><span class="sxs-lookup"><span data-stu-id="c5aab-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="c5aab-115">如果您新增/移除一個租用戶中的使用者的系統管理員角色，hello 變更不會不會影響 hello 系統管理員角色的 hello 使用者具有另一個租用戶中。</span><span class="sxs-lookup"><span data-stu-id="c5aab-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="c5aab-116">同步處理獨立性</span><span class="sxs-lookup"><span data-stu-id="c5aab-116">Synchronization independence</span></span>
<span data-ttu-id="c5aab-117">您可以設定每個 Azure AD 租用獨立 tooget 資料從單一執行個體中的其中一個同步處理：</span><span class="sxs-lookup"><span data-stu-id="c5aab-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="c5aab-118">單一 AD 樹系 toosynchronize 資料 hello Azure AD Connect 工具。</span><span class="sxs-lookup"><span data-stu-id="c5aab-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="c5aab-119">hello Azure 作用中租用戶連接器 Forefront Identity Manager，toosynchronize 資料，其中包含一個或多個內部部署樹系和/或非 Azure AD 資料來源。</span><span class="sxs-lookup"><span data-stu-id="c5aab-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="c5aab-120">新增 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="c5aab-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="c5aab-121">tooadd hello Azure 入口網站中的 Azure AD 租用戶登入太[hello Azure 入口網站](https://portal.azure.com)與 Azure AD 全域管理員帳戶，然後在 hello 左邊，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="c5aab-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="c5aab-122">與其他 Azure 資源不同，您的租用戶並非 Azure 訂用帳戶的子資源。</span><span class="sxs-lookup"><span data-stu-id="c5aab-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="c5aab-123">如果您的 Azure 訂用帳戶取消或已過期，您仍然可以存取您使用 Azure PowerShell、 Azure Graph API，hello 或 hello Office 365 系統管理中心的租用戶資料。</span><span class="sxs-lookup"><span data-stu-id="c5aab-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="c5aab-124">您也可以將其他訂用帳戶與 hello 租用戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="c5aab-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="c5aab-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5aab-125">Next steps</span></span>
<span data-ttu-id="c5aab-126">如需 Azure AD 授權問題和最佳做法的廣泛概觀，請參閱[什麼是 Azure Active Directory 租用戶授權？](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c5aab-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
