---
title: "aaaAzure 資料目錄必要條件 |Microsoft 文件"
description: "深入了解您需要開始使用 Azure 資料目錄 tooget hello 必要條件。"
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
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="2e0af-103">Azure 資料目錄必要條件</span><span class="sxs-lookup"><span data-stu-id="2e0af-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="2e0af-104">您可以設定 Azure 資料目錄之前，您需要 tootake care of 幾件事。</span><span class="sxs-lookup"><span data-stu-id="2e0af-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="2e0af-105">別擔心，這個過程不需要很長時間。</span><span class="sxs-lookup"><span data-stu-id="2e0af-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="2e0af-106">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="2e0af-106">Azure subscription</span></span>
<span data-ttu-id="2e0af-107">tooset 安裝資料目錄，您必須是 hello 擁有者或共同擁有者的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e0af-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="2e0af-108">Azure 訂用帳戶可協助您組織存取 toocloud 服務資源，例如資料目錄。</span><span class="sxs-lookup"><span data-stu-id="2e0af-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="2e0af-109">訂用帳戶也可協助您控制如何根據資源使用量產生報告、計費及付費。</span><span class="sxs-lookup"><span data-stu-id="2e0af-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="2e0af-110">每一個訂用帳戶可以有個別的計費和付款設定；因此，依照部門、專案及分處等，您可以有不同的訂用帳戶和不同的計劃。</span><span class="sxs-lookup"><span data-stu-id="2e0af-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="2e0af-111">每個雲端服務所屬 tooa 訂用帳戶，並設定資料目錄之前，需要 toohave 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e0af-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="2e0af-112">詳細資訊，請參閱 toolearn[管理帳戶、 訂用帳戶及管理角色](../active-directory/active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="2e0af-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="2e0af-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e0af-113">Azure Active Directory</span></span>
<span data-ttu-id="2e0af-114">tooset 安裝資料目錄，您必須登入 Azure Active Directory (Azure AD) 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e0af-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="2e0af-115">Azure AD 會提供簡單的方法，以您的商務 toomanage 識別和存取，在 hello 雲端和內部部署。</span><span class="sxs-lookup"><span data-stu-id="2e0af-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="2e0af-116">使用者可以使用單一工作或學校帳戶進行單一登入 tooany 雲端，然後在內部部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e0af-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="2e0af-117">資料目錄會使用 Azure AD tooauthenticate 登入。</span><span class="sxs-lookup"><span data-stu-id="2e0af-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="2e0af-118">詳細資訊，請參閱 toolearn[什麼是 Azure Active Directory？](../active-directory/active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="2e0af-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2e0af-119">使用 hello [Azure 入口網站](http://portal.azure.com/)，您可以登入個人 Microsoft 帳戶或 Azure Active Directory 公司或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e0af-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="2e0af-120">使用資料目錄註冊 tooset 或是 hello Azure 入口網站或 hello[資料目錄入口網站](http://www.azuredatacatalog.com)，您必須使用 Azure Active Directory 帳戶，而不是個人的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="2e0af-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="2e0af-121">Active Directory 原則組態</span><span class="sxs-lookup"><span data-stu-id="2e0af-121">Active Directory policy configuration</span></span>
<span data-ttu-id="2e0af-122">您可能會遇到的情況，您可以登入 toohello 資料目錄入口網站，而，但是當您嘗試 toosign toohello 資料來源註冊工具中的，您會遇到的錯誤訊息，讓您無法登入。</span><span class="sxs-lookup"><span data-stu-id="2e0af-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="2e0af-123">只有當您在 hello 公司網路，或可能只有當您要連線從外部 hello 公司網路時，可能會發生此問題的行為。</span><span class="sxs-lookup"><span data-stu-id="2e0af-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="2e0af-124">hello 資料來源註冊工具會使用表單驗證 toovalidate 您對 Active Directory 的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="2e0af-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="2e0af-125">toohelp 成功登入，Active Directory 系統管理員必須啟用表單驗證 hello 全域驗證原則中。</span><span class="sxs-lookup"><span data-stu-id="2e0af-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="2e0af-126">Hello 全域驗證原則，在驗證方法可以啟用個別的內部網路和外部網路連接，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="2e0af-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="2e0af-127">如果要連線的 hello 網路不啟用表單驗證，可能會發生登入錯誤。</span><span class="sxs-lookup"><span data-stu-id="2e0af-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Active Directory 全域驗證原則](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="2e0af-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e0af-129">Next steps</span></span>
<span data-ttu-id="2e0af-130">如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e0af-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
