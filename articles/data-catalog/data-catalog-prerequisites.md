---
title: "Azure 資料目錄必要條件 | Microsoft Docs"
description: "了解開始使用 Azure 資料目錄所需的必要條件。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="b9abf-103">Azure 資料目錄必要條件</span><span class="sxs-lookup"><span data-stu-id="b9abf-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="b9abf-104">您必須注意幾件事，才能設定 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="b9abf-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="b9abf-105">別擔心，這個過程不需要很長時間。</span><span class="sxs-lookup"><span data-stu-id="b9abf-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="b9abf-106">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="b9abf-106">Azure subscription</span></span>
<span data-ttu-id="b9abf-107">若要設定資料目錄，您必須是 Azure 訂用帳戶的擁有者或共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="b9abf-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="b9abf-108">Azure 訂用帳戶可協助您組織雲端服務資源 (例如 Azure 資料目錄) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="b9abf-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="b9abf-109">訂用帳戶也可協助您控制如何根據資源使用量產生報告、計費及付費。</span><span class="sxs-lookup"><span data-stu-id="b9abf-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="b9abf-110">每一個訂用帳戶可以有個別的計費和付款設定；因此，依照部門、專案及分處等，您可以有不同的訂用帳戶和不同的計劃。</span><span class="sxs-lookup"><span data-stu-id="b9abf-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="b9abf-111">每一個雲端服務都屬於某個訂用帳戶，在設定資料目錄之前，您必須先有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9abf-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="b9abf-112">若要深入了解，請參閱 [管理帳戶、訂用帳戶及管理角色](../active-directory/active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="b9abf-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="b9abf-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9abf-113">Azure Active Directory</span></span>
<span data-ttu-id="b9abf-114">若要設定資料目錄，您必須使用 Azure Active Directory (Azure AD) 使用者帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="b9abf-115">Azure AD 提供了簡單的方法，讓您的企業無論能輕鬆地管理雲端和內部部署中的身分識別與存取權。</span><span class="sxs-lookup"><span data-stu-id="b9abf-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="b9abf-116">使用者可以使用單一公司帳戶或學校帳戶，以單一登入方法登入任何雲端和內部部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9abf-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="b9abf-117">資料目錄採用 Azure AD 來驗證登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="b9abf-118">若要深入了解，請參閱[什麼是 Azure Active Directory？](../active-directory/active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b9abf-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b9abf-119">透過使用 [Azure 入口網站](http://portal.azure.com/)，您可以使用個人 Microsoft 帳戶或 Azure Active Directory 公司或學校帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="b9abf-120">若要使用 Azure 入口網站或[資料目錄入口網站](http://www.azuredatacatalog.com)設定資料目錄，您必須使用 Azure Active Directory 帳戶而非個人帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="b9abf-121">Active Directory 原則組態</span><span class="sxs-lookup"><span data-stu-id="b9abf-121">Active Directory policy configuration</span></span>
<span data-ttu-id="b9abf-122">您可能會遇到一種情況：您可以登入資料目錄入口網站，但在您嘗試登入資料來源註冊工具時會收到錯誤訊息，導致您無法登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="b9abf-123">僅在您處於公司網路或是從公司網路外部連接時，才會發生此問題行為。</span><span class="sxs-lookup"><span data-stu-id="b9abf-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="b9abf-124">資料來源註冊工具使用「表單驗證」，以根據 Active Directory 驗證使用者認證。</span><span class="sxs-lookup"><span data-stu-id="b9abf-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="b9abf-125">Active Directory 系統管理員必須在全域驗證原則中啟用表單驗證，才會成功登入。</span><span class="sxs-lookup"><span data-stu-id="b9abf-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="b9abf-126">在全域驗證原則中，您可以分別為內部網路和外部網路連線啟用驗證方法，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="b9abf-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="b9abf-127">如果您連線的網路未啟用表單驗證，可能會發生登入錯誤。</span><span class="sxs-lookup"><span data-stu-id="b9abf-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Active Directory 全域驗證原則](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="b9abf-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9abf-129">Next steps</span></span>
<span data-ttu-id="b9abf-130">如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b9abf-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
