---
title: "將使用者新增至您的 Azure RemoteApp 集合 | Microsoft Docs"
description: "了解如何將使用者新增至您的 Azure RemoteApp 集合"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="afc22-103">如何將使用者新增至您的 Azure RemoteApp 集合</span><span class="sxs-lookup"><span data-stu-id="afc22-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="afc22-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="afc22-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="afc22-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="afc22-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="afc22-106">您必須先授與使用者您集合的存取權，他們才能在 Azure RemoteApp 中看到和使用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="afc22-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="afc22-107">這是最簡單的部分：在 [ **使用者存取** ] 索引標籤上，輸入使用者的帳戶資訊，然後按一下核取記號。</span><span class="sxs-lookup"><span data-stu-id="afc22-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="afc22-108">您需要什麼帳戶資訊？</span><span class="sxs-lookup"><span data-stu-id="afc22-108">What account information do you need?</span></span> <span data-ttu-id="afc22-109">這取決於您建立的收藏類型 (雲端或混合式)，還有您是否正在該收藏中使用 Office 365 ProPlus。</span><span class="sxs-lookup"><span data-stu-id="afc22-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="afc22-110">支援的使用者識別</span><span class="sxs-lookup"><span data-stu-id="afc22-110">Supported user identities</span></span>
<span data-ttu-id="afc22-111">不同的集合類型 (雲端或混合式) 支援使用不同的使用者身分識別，存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="afc22-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="afc22-112">對於 RemoteApp 的混合式收藏，您必須設定內部部署的 Active Directory 網域基礎結構和具備目錄整合的 Azure Active Directory 租用戶 (及選擇性的單一登入)。</span><span class="sxs-lookup"><span data-stu-id="afc22-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="afc22-113">此外，您必須在內部部署的目錄中建立一些 Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="afc22-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="afc22-114">對於 RemoteApp 的雲端收藏，具有 Azure Active Directory 支援識別的任何使用者都可以被授與 RemoteApp 的使用者存取權以包含 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc22-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="afc22-115">請參閱下表。</span><span class="sxs-lookup"><span data-stu-id="afc22-115">See the table below.</span></span>

<span data-ttu-id="afc22-116">Office 365 使用者為 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="afc22-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="afc22-117">如果這些使用者有 Azure Active Directory 混合式、目錄同步處理的帳戶，就可以在 RemoteApp 混合式部署中授與他們使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="afc22-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="afc22-118">您可以使用這個表格快速參考在您的收藏中支援何種識別，以及 Active Directory 的需求為何。</span><span class="sxs-lookup"><span data-stu-id="afc22-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="afc22-119">使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="afc22-119">User accounts</span></span> | <span data-ttu-id="afc22-120">雲端</span><span class="sxs-lookup"><span data-stu-id="afc22-120">Cloud</span></span> | <span data-ttu-id="afc22-121">混合式</span><span class="sxs-lookup"><span data-stu-id="afc22-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afc22-122">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="afc22-122">Microsoft Account</span></span> |<span data-ttu-id="afc22-123">是</span><span class="sxs-lookup"><span data-stu-id="afc22-123">Yes</span></span> |<span data-ttu-id="afc22-124">否</span><span class="sxs-lookup"><span data-stu-id="afc22-124">No</span></span> |
| <span data-ttu-id="afc22-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="afc22-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="afc22-126">僅 Azure AD 雲端</span><span class="sxs-lookup"><span data-stu-id="afc22-126">Azure AD cloud only</span></span> |<span data-ttu-id="afc22-127">是</span><span class="sxs-lookup"><span data-stu-id="afc22-127">Yes</span></span> |<span data-ttu-id="afc22-128">否</span><span class="sxs-lookup"><span data-stu-id="afc22-128">No</span></span> |
| <span data-ttu-id="afc22-129">具有密碼同步的 ADsync</span><span class="sxs-lookup"><span data-stu-id="afc22-129">ADsync with password sync</span></span> |<span data-ttu-id="afc22-130">是</span><span class="sxs-lookup"><span data-stu-id="afc22-130">Yes</span></span> |<span data-ttu-id="afc22-131">是</span><span class="sxs-lookup"><span data-stu-id="afc22-131">Yes</span></span> |
| <span data-ttu-id="afc22-132">不具密碼同步的 ADsync</span><span class="sxs-lookup"><span data-stu-id="afc22-132">ADsync without password sync</span></span> |<span data-ttu-id="afc22-133">是</span><span class="sxs-lookup"><span data-stu-id="afc22-133">Yes</span></span> |<span data-ttu-id="afc22-134">否</span><span class="sxs-lookup"><span data-stu-id="afc22-134">No</span></span> |
| <span data-ttu-id="afc22-135">具 AD FS 的 ADsync</span><span class="sxs-lookup"><span data-stu-id="afc22-135">ADsync with AD FS</span></span> |<span data-ttu-id="afc22-136">是</span><span class="sxs-lookup"><span data-stu-id="afc22-136">Yes</span></span> |<span data-ttu-id="afc22-137">是</span><span class="sxs-lookup"><span data-stu-id="afc22-137">Yes</span></span> |
| <span data-ttu-id="afc22-138">[Azure 支援的第 3 方識別提供者](https://msdn.microsoft.com/library/azure/jj679342.aspx) (例如 Ping)</span><span class="sxs-lookup"><span data-stu-id="afc22-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="afc22-139">是</span><span class="sxs-lookup"><span data-stu-id="afc22-139">Yes</span></span> |<span data-ttu-id="afc22-140">是</span><span class="sxs-lookup"><span data-stu-id="afc22-140">Yes</span></span> |
| <span data-ttu-id="afc22-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="afc22-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="afc22-142">是</span><span class="sxs-lookup"><span data-stu-id="afc22-142">Yes</span></span> |<span data-ttu-id="afc22-143">是</span><span class="sxs-lookup"><span data-stu-id="afc22-143">Yes</span></span> |

<span data-ttu-id="afc22-144">請查看有關設定 RemoteApp 的 Active Directory 的 [詳細資訊](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="afc22-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="afc22-145">Azure Active Directory 使用者必須來自於與您的訂用帳戶相關聯的租用戶。</span><span class="sxs-lookup"><span data-stu-id="afc22-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="afc22-146">(您可以在入口網站的 [設定] 索引標籤上檢視和修改您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afc22-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="afc22-147">如需詳細資訊，請參閱[變更 RemoteApp 所使用的 Azure Active Directory 租用戶](remoteapp-changetenant.md))。</span><span class="sxs-lookup"><span data-stu-id="afc22-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="afc22-148">Office 365 ProPlus 使用者帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="afc22-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="afc22-149">如果您的收藏中使用 Office 365 ProPlus 範本映像， *或者* 如果您建立了使用 Office 365 的自訂映像，則您只能新增在您的訂用帳戶的預設網域中擁有 Office 365 訂閱的 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="afc22-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="afc22-150">如需詳細資訊，請參閱 [透過 Azure RemoteApp 使用 Office 365](remoteapp-o365.md) 。</span><span class="sxs-lookup"><span data-stu-id="afc22-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

