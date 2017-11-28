---
title: "Azure Active Directory 中的條件式存取的 aaaBest 作法 |Microsoft 文件"
description: "了解您在設定條件式存取原則時應該知道的事件及應避免的動作。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="3cfd0-104">Azure Active Directory 中條件式存取的最佳做法</span><span class="sxs-lookup"><span data-stu-id="3cfd0-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="3cfd0-105">此主題提供與您在設定條件式存取原則時應該知道的事件及應避免的動作相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="3cfd0-106">閱讀本主題之前，您應該熟悉 hello 概念和術語 hello 述[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3cfd0-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="3cfd0-107">您應該知道的事情</span><span class="sxs-lookup"><span data-stu-id="3cfd0-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="3cfd0-108">Toomake 原則工作的必要條件？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="3cfd0-109">當您建立新的原則時，未選取任何使用者、群組、應用程式或存取控制項。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![雲端應用程式](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="3cfd0-111">toomake 原則運作，您必須設定下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3cfd0-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="3cfd0-112">何事</span><span class="sxs-lookup"><span data-stu-id="3cfd0-112">What</span></span>           | <span data-ttu-id="3cfd0-113">方式</span><span class="sxs-lookup"><span data-stu-id="3cfd0-113">How</span></span>                                  | <span data-ttu-id="3cfd0-114">理由</span><span class="sxs-lookup"><span data-stu-id="3cfd0-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="3cfd0-115">**雲端應用程式**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-115">**Cloud apps**</span></span> |<span data-ttu-id="3cfd0-116">您需要 tooselect 一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="3cfd0-117">條件式存取原則 hello 目標是 tooenable 您 toofine 微調授權的使用者可以存取您的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="3cfd0-118">**使用者和群組**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-118">**Users and groups**</span></span> | <span data-ttu-id="3cfd0-119">您必須至少一個 tooselect 使用者或群組是授權您選取的 tooaccess hello 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="3cfd0-120">永遠不會觸發未指派使用者和群組的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="3cfd0-121">**存取控制**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-121">**Access controls**</span></span> | <span data-ttu-id="3cfd0-122">您必須至少一個 tooselect 存取控制。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="3cfd0-123">原則處理器需要 tooknow 哪些 toodo 如果符合條件。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="3cfd0-124">在 新增 toothese 基本需求，在許多情況下，您也應該設定條件。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="3cfd0-125">雖然沒有已設定的條件，也可以運作的原則，條件是 hello 驅動因素，來微調存取 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![雲端應用程式](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="3cfd0-127">如何評估指派？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-127">How are assignments evaluated?</span></span>

<span data-ttu-id="3cfd0-128">所有指派邏輯上都會使用 **AND** 運算子。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="3cfd0-129">如果您有多個指派設定，tootrigger 原則，必須滿足所有指派。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="3cfd0-130">如果您需要 tooconfigure 位置條件適用於 tooall 連線從您的組織網路之外，您可以達成的：</span><span class="sxs-lookup"><span data-stu-id="3cfd0-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="3cfd0-131">包含**所有位置**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-131">Including **All locations**</span></span>
- <span data-ttu-id="3cfd0-132">排除**所有信任的 IP**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="3cfd0-133">如果您擁有 hello Azure 傳統入口網站中的原則和設定的 Azure 入口網站，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="3cfd0-134">這兩項原則會強制執行由 Azure Active Directory 和 hello 使用者只在符合所有需求時，取得存取權。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="3cfd0-135">如果您擁有 hello Intune Silverlight 入口網站中的原則和 hello Azure 入口網站，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="3cfd0-136">這兩項原則會強制執行由 Azure Active Directory 和 hello 使用者只在符合所有需求時，取得存取權。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="3cfd0-137">如果我有多個原則設定相同的使用者的 hello，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="3cfd0-138">每個登入，Azure Active Directory 會評估所有原則，並可確保之前已授與存取權 toohello 使用者符合所有需求。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="3cfd0-139">條件式存取是否適用於 Exchange ActiveSync？</span><span class="sxs-lookup"><span data-stu-id="3cfd0-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="3cfd0-140">是，您可以在條件式存取原則中使用 Exchange ActiveSync。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="3cfd0-141">您應該避免做的事</span><span class="sxs-lookup"><span data-stu-id="3cfd0-141">What you should avoid doing</span></span>

<span data-ttu-id="3cfd0-142">hello 條件式存取架構為您提供絕佳的設定彈性。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="3cfd0-143">不過，很大的彈性也表示您應該仔細檢閱每個組態原則先前 tooreleasing 它 tooavoid 非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="3cfd0-144">在此內容中，您應該特別特別注意 tooassignments 例如會影響完整集**所有使用者 / 群組 / 雲端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="3cfd0-145">在您環境中，您應該避免 hello 的設定：</span><span class="sxs-lookup"><span data-stu-id="3cfd0-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="3cfd0-146">**針對所有使用者、所有雲端應用程式：**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="3cfd0-147">**封鎖存取** - 此組態會封鎖您整個組織，這絕對不是一個好方法。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="3cfd0-148">**需要相容的裝置**-使用者，不要已註冊其裝置的資訊，此原則會封鎖所有存取，包括存取 toohello Intune 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="3cfd0-149">如果您是系統管理員沒有已註冊的裝置，這項原則會阻止您從取回 hello Azure 入口網站 toochange hello 原則。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="3cfd0-150">**需要加入網域**-此原則的封鎖存取具有也 hello 潛在 tooblock 所有使用者存取您組織中如果您沒有加入網域的裝置尚未。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="3cfd0-151">**針對所有使用者、所有雲端應用程式、所有裝置平台：**</span><span class="sxs-lookup"><span data-stu-id="3cfd0-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="3cfd0-152">**封鎖存取** - 此組態會封鎖您整個組織，這絕對不是一個好方法。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="3cfd0-153">常見案例</span><span class="sxs-lookup"><span data-stu-id="3cfd0-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="3cfd0-154">應用程式需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3cfd0-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="3cfd0-155">許多環境中有其他人需要比 hello 較高的保護層級的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="3cfd0-156">這種，例如 hello 擁有存取 toosensitive 資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="3cfd0-157">如果您想 tooadd 另一層保護 toothese 應用程式，您可以設定條件式存取原則，當使用者同時存取這些應用程式要求多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="3cfd0-158">從不受信任的網路存取時需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3cfd0-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="3cfd0-159">此案例中是類似 toohello 前一個案例，因為它會增加多因素驗證的需求。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="3cfd0-160">不過，hello 主要差異是這項需求的 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="3cfd0-161">當應用程式存取 toosensitve 資料與已 hello 焦點的 hello 前一個案例時，這種情況的 hello 焦點是受信任的位置。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="3cfd0-162">換句話說，如果使用者從您不信任的網路存取應用程式，您可能需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="3cfd0-163">只有受信任的裝置可以存取 Office 365 服務</span><span class="sxs-lookup"><span data-stu-id="3cfd0-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="3cfd0-164">如果您使用 Intune 在您的環境中，您可以立即開始使用 hello Azure 主控台中的 hello 條件式存取原則介面。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="3cfd0-165">許多 Intune 客戶使用條件式存取 tooensure 只有受信任的裝置才可以存取 Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="3cfd0-166">這表示，行動裝置向 Intune 註冊並符合相容性原則的需求，Windows 電腦會聯結的 tooan 在內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="3cfd0-167">重要的改進是，您不需要 tooset hello hello Office 365 服務的每個相同的原則。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="3cfd0-168">當您建立新的原則時，設定 hello 雲端應用程式 tooinclude 每個您想使用 tooprotect 使用條件式存取的 hello O365 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cfd0-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3cfd0-169">Next steps</span></span>

<span data-ttu-id="3cfd0-170">如果您想如何 tooconfigure 條件式存取原則，請參閱的 tooknow[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3cfd0-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
