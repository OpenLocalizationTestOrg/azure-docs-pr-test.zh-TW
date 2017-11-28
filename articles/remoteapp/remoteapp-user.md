---
title: "aaaAdd 使用者 tooyour Azure RemoteApp 集合 |Microsoft 文件"
description: "深入了解如何 tooadd 使用者 tooyour Azure RemoteApp 集合"
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
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="96dd1-103">如何 tooadd 使用者 tooyour Azure RemoteApp 集合</span><span class="sxs-lookup"><span data-stu-id="96dd1-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="96dd1-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="96dd1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="96dd1-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="96dd1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="96dd1-106">您的使用者可以看到並使用 Azure RemoteApp 中的應用程式之前，您會有 toogrant 它們 tooyour 集合的存取。</span><span class="sxs-lookup"><span data-stu-id="96dd1-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="96dd1-107">這是 hello 簡單的部分： hello 上**使用者存取**索引標籤上，輸入 hello hello 使用者的帳戶資訊，然後按一下hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="96dd1-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="96dd1-108">您需要什麼帳戶資訊？</span><span class="sxs-lookup"><span data-stu-id="96dd1-108">What account information do you need?</span></span> <span data-ttu-id="96dd1-109">相依於 hello 集合型別所建立 （雲端或混合式） 以及您使用 Office 365 ProPlus 該集合中。</span><span class="sxs-lookup"><span data-stu-id="96dd1-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="96dd1-110">支援的使用者識別</span><span class="sxs-lookup"><span data-stu-id="96dd1-110">Supported user identities</span></span>
<span data-ttu-id="96dd1-111">hello 不同集合類型 （與混合式雲端） 支援存取 tooapplications 使用不同的使用者識別。</span><span class="sxs-lookup"><span data-stu-id="96dd1-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="96dd1-112">RemoteApp 的混合式集合，您需要 Active Directory 網域基礎結構，在內部部署以及與目錄整合 Azure Active Directory 租用戶 tooset （以及選擇性地單一登入）。</span><span class="sxs-lookup"><span data-stu-id="96dd1-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="96dd1-113">此外，您需要 toocreate hello 在內部部署目錄中的某些 Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="96dd1-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="96dd1-114">雲端的 RemoteApp 集合，只要使用者擁有 Azure Active Directory 支援身分識別可以授與使用者存取 tooRemoteApp tooinclude Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="96dd1-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="96dd1-115">請參閱 hello 表。</span><span class="sxs-lookup"><span data-stu-id="96dd1-115">See hello table below.</span></span>

<span data-ttu-id="96dd1-116">Office 365 使用者為 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="96dd1-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="96dd1-117">如果這些使用者有 Azure Active Directory 混合式、目錄同步處理的帳戶，就可以在 RemoteApp 混合式部署中授與他們使用者存取權。</span><span class="sxs-lookup"><span data-stu-id="96dd1-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="96dd1-118">您可以使用此表格識別支援在您的集合和 hello Active Directory 需求為何，快速參考。</span><span class="sxs-lookup"><span data-stu-id="96dd1-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="96dd1-119">使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="96dd1-119">User accounts</span></span> | <span data-ttu-id="96dd1-120">雲端</span><span class="sxs-lookup"><span data-stu-id="96dd1-120">Cloud</span></span> | <span data-ttu-id="96dd1-121">混合式</span><span class="sxs-lookup"><span data-stu-id="96dd1-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96dd1-122">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="96dd1-122">Microsoft Account</span></span> |<span data-ttu-id="96dd1-123">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-123">Yes</span></span> |<span data-ttu-id="96dd1-124">否</span><span class="sxs-lookup"><span data-stu-id="96dd1-124">No</span></span> |
| <span data-ttu-id="96dd1-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="96dd1-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="96dd1-126">僅 Azure AD 雲端</span><span class="sxs-lookup"><span data-stu-id="96dd1-126">Azure AD cloud only</span></span> |<span data-ttu-id="96dd1-127">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-127">Yes</span></span> |<span data-ttu-id="96dd1-128">否</span><span class="sxs-lookup"><span data-stu-id="96dd1-128">No</span></span> |
| <span data-ttu-id="96dd1-129">具有密碼同步的 ADsync</span><span class="sxs-lookup"><span data-stu-id="96dd1-129">ADsync with password sync</span></span> |<span data-ttu-id="96dd1-130">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-130">Yes</span></span> |<span data-ttu-id="96dd1-131">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-131">Yes</span></span> |
| <span data-ttu-id="96dd1-132">不具密碼同步的 ADsync</span><span class="sxs-lookup"><span data-stu-id="96dd1-132">ADsync without password sync</span></span> |<span data-ttu-id="96dd1-133">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-133">Yes</span></span> |<span data-ttu-id="96dd1-134">否</span><span class="sxs-lookup"><span data-stu-id="96dd1-134">No</span></span> |
| <span data-ttu-id="96dd1-135">具 AD FS 的 ADsync</span><span class="sxs-lookup"><span data-stu-id="96dd1-135">ADsync with AD FS</span></span> |<span data-ttu-id="96dd1-136">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-136">Yes</span></span> |<span data-ttu-id="96dd1-137">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-137">Yes</span></span> |
| <span data-ttu-id="96dd1-138">[Azure 支援的第 3 方識別提供者](https://msdn.microsoft.com/library/azure/jj679342.aspx) (例如 Ping)</span><span class="sxs-lookup"><span data-stu-id="96dd1-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="96dd1-139">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-139">Yes</span></span> |<span data-ttu-id="96dd1-140">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-140">Yes</span></span> |
| <span data-ttu-id="96dd1-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="96dd1-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="96dd1-142">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-142">Yes</span></span> |<span data-ttu-id="96dd1-143">是</span><span class="sxs-lookup"><span data-stu-id="96dd1-143">Yes</span></span> |

<span data-ttu-id="96dd1-144">請查看有關設定 RemoteApp 的 Active Directory 的 [詳細資訊](remoteapp-ad.md) 。</span><span class="sxs-lookup"><span data-stu-id="96dd1-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="96dd1-145">hello Azure Active Directory 使用者必須是來自與您訂用帳戶相關聯的 hello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="96dd1-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="96dd1-146">(您可以檢視並修改您的訂閱上 hello**設定**hello 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="96dd1-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="96dd1-147">請參閱[變更由 RemoteApp 所使用的 hello Azure Active Directory 租用](remoteapp-changetenant.md)如需詳細資訊。)</span><span class="sxs-lookup"><span data-stu-id="96dd1-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="96dd1-148">Office 365 ProPlus 使用者帳戶資訊</span><span class="sxs-lookup"><span data-stu-id="96dd1-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="96dd1-149">如果您使用 Office 365 ProPlus 範本映像 hello 集合中*或*如果您建立使用 Office 365 的自訂映像，您只允許有 Office 365 訂用帳戶的 hello 的 tooadd Azure Active Directory 使用者您的訂用帳戶的預設網域。</span><span class="sxs-lookup"><span data-stu-id="96dd1-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="96dd1-150">如需詳細資訊，請參閱 [透過 Azure RemoteApp 使用 Office 365](remoteapp-o365.md) 。</span><span class="sxs-lookup"><span data-stu-id="96dd1-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

