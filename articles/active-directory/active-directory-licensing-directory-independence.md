---
title: "Azure Active Directory 租用戶互動的特性 | Microsoft Docs"
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
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="ebe8d-103">了解多個 Azure Active Directory 租用戶如何互動</span><span class="sxs-lookup"><span data-stu-id="ebe8d-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="ebe8d-104">在 Azure Active Directory (Azure AD) 目錄中，每個租用戶都是完全獨立的資源：邏輯上獨立於您所管理之其他租用戶的對等。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="ebe8d-105">租用戶之間沒有任何父子關聯性。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="ebe8d-106">這個在租用戶之間的獨立性包括資源獨立性、系統管理獨立性，以及同步處理獨立性。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="ebe8d-107">資源獨立性</span><span class="sxs-lookup"><span data-stu-id="ebe8d-107">Resource independence</span></span>
* <span data-ttu-id="ebe8d-108">當您在某個租用戶中建立或刪除資源時，並不會影響另一個租用戶中的任何資源 (但有外部使用者有部分例外)。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="ebe8d-109">如果將您的其中一個網域名稱與某個租用戶搭配使用，該網域名稱就無法與任何其他租用戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="ebe8d-110">系統管理獨立性</span><span class="sxs-lookup"><span data-stu-id="ebe8d-110">Administrative independence</span></span>
<span data-ttu-id="ebe8d-111">如果 'Contoso' 租用戶的非系統管理使用者建立 'Test' 測試租用戶，則：</span><span class="sxs-lookup"><span data-stu-id="ebe8d-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="ebe8d-112">系統預設會將建立租用戶的使用者新增為該新租用戶的外部使用者，並將該租用戶中的全域管理員角色指派給他。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="ebe8d-113">'Contoso' 租用戶的系統管理員並沒有 'Test' 租用戶的直接系統管理權限，除非 'Test' 的系統管理員明確地授與他們這些權限。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="ebe8d-114">不過，'Contoso' 的系統管理員如果可控制建立 'Test' 的使用者帳戶，便可控制對 'Test' 租用戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="ebe8d-115">如果您為某個使用者新增/移除在某個租用戶中的系統管理員角色，此變更並不會影響到該使用者在另一個租用戶中擁有的系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="ebe8d-116">同步處理獨立性</span><span class="sxs-lookup"><span data-stu-id="ebe8d-116">Synchronization independence</span></span>
<span data-ttu-id="ebe8d-117">您可以單獨設定每個 Azure AD 租用戶，以從下列任一工具的單一執行個體同步處理資料：</span><span class="sxs-lookup"><span data-stu-id="ebe8d-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="ebe8d-118">Azure AD Connect 工具：可與單一 AD 樹系同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="ebe8d-119">Azure Active Directory Connector for Forefront Identity Manager：可與一或多個內部部署樹系和/或非 Azure AD 資料來源同步處理資料。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="ebe8d-120">新增 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="ebe8d-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="ebe8d-121">若要在 Azure 入口網站中新增 Azure AD 租用戶，請使用 Azure AD 全域管理員的帳戶登入[Azure 入口網站](https://portal.azure.com)，並且在左邊選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe8d-122">與其他 Azure 資源不同，您的租用戶並非 Azure 訂用帳戶的子資源。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="ebe8d-123">如果您的 Azure 訂用帳戶被取消或到期，您仍然可以使用 Azure PowerShell、Azure Graph API 或「Office 365 系統管理中心」來存取租用戶資料。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="ebe8d-124">您也可以將另一個訂用帳戶與租用戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="ebe8d-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="ebe8d-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebe8d-125">Next steps</span></span>
<span data-ttu-id="ebe8d-126">如需 Azure AD 授權問題和最佳做法的廣泛概觀，請參閱[什麼是 Azure Active Directory 租用戶授權？](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ebe8d-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
