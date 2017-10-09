---
title: "aaaMicrosoft Azure 多重要素驗證的使用者狀態"
description: "了解 Azure MFA 中的使用者狀態"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a><span data-ttu-id="56624-103">如何 toorequire 雙步驟驗證的使用者或群組</span><span class="sxs-lookup"><span data-stu-id="56624-103">How toorequire two-step verification for a user or group</span></span>

<span data-ttu-id="56624-104">可供您要求使用雙步驟驗證的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="56624-104">There are two approaches for requiring two-step verification.</span></span> <span data-ttu-id="56624-105">hello 第一個選項是 tooenable 每個個別使用者的 Azure Multi-factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="56624-105">hello first option is tooenable each individual user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="56624-106">當使用者分別啟用時，它們一定會執行 （有一些例外，像是登入來自受信任的 IP 位址時，或記住 hello 開啟裝置的功能） 的雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="56624-106">When users are enabled individually, they always perform two-step verification (with some exceptions, like when they sign in from trusted IP addresses or if hello remembered devices feature is turned on).</span></span> <span data-ttu-id="56624-107">hello 第二個選項是 tooset 建立需要兩步驟驗證，在某些情況下的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="56624-107">hello second option is tooset up a conditional access policy that requires two-step verification under certain conditions.</span></span>

>[!TIP] 
><span data-ttu-id="56624-108">選擇其中一個這些方法 toorequire 雙步驟驗證，不可同時為兩者。</span><span class="sxs-lookup"><span data-stu-id="56624-108">Choose one of these methods toorequire two-step verification, not both.</span></span> <span data-ttu-id="56624-109">為使用者啟用 Azure MFA 的效力會凌駕任何條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="56624-109">Enabling a user for Azure MFA overrides any conditional access policies.</span></span>

## <a name="which-option-is-right-for-you"></a><span data-ttu-id="56624-110">您合適的選項</span><span class="sxs-lookup"><span data-stu-id="56624-110">Which option is right for you</span></span>

<span data-ttu-id="56624-111">**藉由變更使用者狀態啟用 Azure MFA**是 hello 要求雙步驟驗證的傳統方式。</span><span class="sxs-lookup"><span data-stu-id="56624-111">**Enabling Azure MFA by changing user states** is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="56624-112">它適用於這兩個 hello 雲端中的 Azure MFA 和 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="56624-112">It works for both Azure MFA in hello cloud and Azure MFA Server.</span></span> <span data-ttu-id="56624-113">您所啟用的所有 hello 使用者都擁有 hello 相同的體驗，每次登入時會 tooperform 雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="56624-113">All hello users that you enable have hello same experience, which is tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="56624-114">啟用使用者的效力會凌駕任何可能影響該使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="56624-114">Enabling a user overrides any conditional access policies that may affect that user.</span></span> 

<span data-ttu-id="56624-115">**使用條件式存取原則來啟用 Azure MFA** 是用來要求使用雙步驟驗證的更彈性方法。</span><span class="sxs-lookup"><span data-stu-id="56624-115">**Enabling Azure MFA with a conditional access policy** is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="56624-116">它只是，適用於 hello 雲端中的 Azure MFA 和條件式存取是[付費功能的 Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features)。</span><span class="sxs-lookup"><span data-stu-id="56624-116">It only work for Azure MFA in hello cloud, though, and conditional access is a [paid feature of Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span> <span data-ttu-id="56624-117">您可以建立適用於 toogroups 與個別使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="56624-117">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="56624-118">您可以對高風險群組施加比低風險群組更多的限制，或者，也可以只針對高風險雲端應用程式要求雙步驟驗證，至於低風險的雲端應用程式則略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="56624-118">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> 

<span data-ttu-id="56624-119">這兩個選項會提示使用者 tooregister Azure Multi-factor Authentication hello 之後 hello 需求開啟登入的第一次。</span><span class="sxs-lookup"><span data-stu-id="56624-119">Both of these options prompt users tooregister for Azure Multi-Factor Authentication hello first time that they sign in after hello requirements turn on.</span></span> <span data-ttu-id="56624-120">這兩個選項也會使用可設定的 hello [Azure Multi-factor Authentication 設定](multi-factor-authentication-whats-next.md)</span><span class="sxs-lookup"><span data-stu-id="56624-120">Both options also work with hello configurable [Azure Multi-Factor Authentication settings](multi-factor-authentication-whats-next.md)</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="56624-121">藉由變更使用者狀態來啟用 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="56624-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="56624-122">Azure Multi-factor Authentication Server 中的使用者帳戶具有下列三種不同狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="56624-122">User accounts in Azure Multi-Factor Authentication have hello following three distinct states:</span></span>

| <span data-ttu-id="56624-123">狀態</span><span class="sxs-lookup"><span data-stu-id="56624-123">Status</span></span> | <span data-ttu-id="56624-124">說明</span><span class="sxs-lookup"><span data-stu-id="56624-124">Description</span></span> | <span data-ttu-id="56624-125">受影響的非瀏覽器應用程式</span><span class="sxs-lookup"><span data-stu-id="56624-125">Non-browser apps affected</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="56624-126">已停用</span><span class="sxs-lookup"><span data-stu-id="56624-126">Disabled</span></span> |<span data-ttu-id="56624-127">hello 預設狀態之新使用者未註冊 Azure Multi-factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="56624-127">hello default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="56624-128">否</span><span class="sxs-lookup"><span data-stu-id="56624-128">No</span></span> |
| <span data-ttu-id="56624-129">已啟用</span><span class="sxs-lookup"><span data-stu-id="56624-129">Enabled</span></span> |<span data-ttu-id="56624-130">hello 使用者已註冊 Azure MFA，但尚未註冊。</span><span class="sxs-lookup"><span data-stu-id="56624-130">hello user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="56624-131">會將其下一次登入時提示的 tooregister hello。</span><span class="sxs-lookup"><span data-stu-id="56624-131">They will be prompted tooregister hello next time they sign in.</span></span> |<span data-ttu-id="56624-132">否。</span><span class="sxs-lookup"><span data-stu-id="56624-132">No.</span></span>  <span data-ttu-id="56624-133">Hello 註冊程序完成之前，他們可以繼續 toowork。</span><span class="sxs-lookup"><span data-stu-id="56624-133">They continue toowork until hello registration process is completed.</span></span> |
| <span data-ttu-id="56624-134">已強制</span><span class="sxs-lookup"><span data-stu-id="56624-134">Enforced</span></span> |<span data-ttu-id="56624-135">hello 使用者已註冊且已完成 Azure MFA hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="56624-135">hello user has been enrolled and has completed hello registration process for Azure MFA.</span></span> |<span data-ttu-id="56624-136">是。</span><span class="sxs-lookup"><span data-stu-id="56624-136">Yes.</span></span>  <span data-ttu-id="56624-137">應用程式需要應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="56624-137">Apps require app passwords.</span></span> |

<span data-ttu-id="56624-138">使用者的狀態會反映是否為系統管理員具有它們在註冊 Azure MFA，以及他們是否完成 hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="56624-138">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed hello registration process.</span></span>

<span data-ttu-id="56624-139">所有使用者一開始都是「已停用」狀態。</span><span class="sxs-lookup"><span data-stu-id="56624-139">All users start out *disabled*.</span></span> <span data-ttu-id="56624-140">當您在 Azure MFA 中註冊使用者時，他們的狀態會變更為「已啟用」。</span><span class="sxs-lookup"><span data-stu-id="56624-140">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="56624-141">啟用的使用者登入並完成 hello 註冊程序，其狀態會變更太*強制執行*。</span><span class="sxs-lookup"><span data-stu-id="56624-141">When enabled users sign in and complete hello registration process, their state changes too*enforced*.</span></span>  

### <a name="view-hello-status-for-a-user"></a><span data-ttu-id="56624-142">檢視使用者的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="56624-142">View hello status for a user</span></span>

<span data-ttu-id="56624-143">使用下列步驟 tooaccess hello 頁面供您檢視及管理使用者狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="56624-143">Use hello following steps tooaccess hello page where you can view and manage user states:</span></span>

1. <span data-ttu-id="56624-144">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="56624-144">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="56624-145">跳過**Azure Active Directory** > **使用者和群組** > **所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="56624-145">Go too**Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="56624-146">選取 [多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="56624-146">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="56624-147">![選取 Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="56624-147">![Select Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span></span>
4. <span data-ttu-id="56624-148">新的頁面上，顯示 hello 使用者狀態時，隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="56624-148">A new page, which displays hello user states, opens.</span></span>
   <span data-ttu-id="56624-149">![Multi-Factor Authentication 使用者狀態 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="56624-149">![multi-factor authentication user status - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-hello-status-for-a-user"></a><span data-ttu-id="56624-150">變更使用者的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="56624-150">Change hello status for a user</span></span>

1. <span data-ttu-id="56624-151">使用上述步驟 tooget toohello multi-factor authentication 使用者頁面的 hello。</span><span class="sxs-lookup"><span data-stu-id="56624-151">Use hello preceding steps tooget toohello multi-factor authentication users page.</span></span>
2. <span data-ttu-id="56624-152">您為 Azure MFA 想 tooenable 尋找 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="56624-152">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="56624-153">您可能需要 toochange hello hello 頂端的檢視。</span><span class="sxs-lookup"><span data-stu-id="56624-153">You may need toochange hello view at hello top.</span></span> 
   <span data-ttu-id="56624-154">![尋找使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="56624-154">![Find user - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="56624-155">請檢查 hello 方塊下一步 tootheir 名稱。</span><span class="sxs-lookup"><span data-stu-id="56624-155">Check hello box next tootheir name.</span></span>
4. <span data-ttu-id="56624-156">在 hello 右下快速步驟，選擇**啟用**或**停用**。</span><span class="sxs-lookup"><span data-stu-id="56624-156">On hello right, under quick steps, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="56624-157">![啟用所選的使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="56624-157">![Enable selected user - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>

   >[!TIP]
   ><span data-ttu-id="56624-158">*啟用*使用者自動切換太*強制執行*當他們註冊為 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="56624-158">*Enabled* users automatically switch too*enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="56624-159">您不應手動變更 hello 使用者狀態 tooenforced。</span><span class="sxs-lookup"><span data-stu-id="56624-159">You shouldn't manually change hello user state tooenforced.</span></span> 

5. <span data-ttu-id="56624-160">確認您的選擇會開啟 hello 快顯視窗中。</span><span class="sxs-lookup"><span data-stu-id="56624-160">Confirm your selection in hello pop-up window that opens.</span></span> 

<span data-ttu-id="56624-161">當您啟用使用者之後，應透過電子郵件通知他們。</span><span class="sxs-lookup"><span data-stu-id="56624-161">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="56624-162">告訴他們，則會要求他們 tooregister hello 登入時的下一次。</span><span class="sxs-lookup"><span data-stu-id="56624-162">Tell them that they'll be asked tooregister hello next time they sign in.</span></span> <span data-ttu-id="56624-163">此外，如果您的組織使用不支援新式驗證的非瀏覽器應用程式，其需要 toocreate 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="56624-163">Also, if your organization uses non-browser apps that don't support modern authentication, they'll need toocreate app passwords.</span></span> <span data-ttu-id="56624-164">您也可以包含連結 tooour [Azure MFA 使用者指南](./end-user/multi-factor-authentication-end-user.md)toohelp 它們開始。</span><span class="sxs-lookup"><span data-stu-id="56624-164">You can also include a link tooour [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) toohelp them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="56624-165">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="56624-165">Use PowerShell</span></span>
<span data-ttu-id="56624-166">toochange hello 使用者狀態的狀態使用[Azure AD PowerShell](/powershell/azure/overview)，變更`$st.State`。</span><span class="sxs-lookup"><span data-stu-id="56624-166">toochange hello user status state using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="56624-167">有三個可能的狀態︰</span><span class="sxs-lookup"><span data-stu-id="56624-167">There are three possible states:</span></span>

* <span data-ttu-id="56624-168">已啟用</span><span class="sxs-lookup"><span data-stu-id="56624-168">Enabled</span></span>
* <span data-ttu-id="56624-169">已強制</span><span class="sxs-lookup"><span data-stu-id="56624-169">Enforced</span></span>
* <span data-ttu-id="56624-170">已停用</span><span class="sxs-lookup"><span data-stu-id="56624-170">Disabled</span></span>  

<span data-ttu-id="56624-171">不會移到使用者直接 toohello*強制*狀態。</span><span class="sxs-lookup"><span data-stu-id="56624-171">Don't move users directly toohello *Enforced* state.</span></span> <span data-ttu-id="56624-172">非瀏覽器型應用程式將會停止運作，因為 hello 使用者未通過 MFA 註冊並取得[應用程式密碼](multi-factor-authentication-whats-next.md#app-passwords)。</span><span class="sxs-lookup"><span data-stu-id="56624-172">Non-browser-based apps will stop working because hello user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> 

<span data-ttu-id="56624-173">使用 PowerShell 是一個不錯的選項，當您需要讓使用者 toobulk。</span><span class="sxs-lookup"><span data-stu-id="56624-173">Using PowerShell is a good option when you need toobulk enabling users.</span></span> <span data-ttu-id="56624-174">建立會在使用者清單中循環移動並啟用這些使用者的 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="56624-174">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="56624-175">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="56624-175">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a><span data-ttu-id="56624-176">使用條件式存取原則來啟用 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="56624-176">Enable Azure MFA with a conditional access policy</span></span>

<span data-ttu-id="56624-177">條件式存取是 Azure Active Directory 的付費功能，其具有許多可能的設定選項。</span><span class="sxs-lookup"><span data-stu-id="56624-177">Conditional access is a paid feature of Azure Active Directory, with many possible configuration options.</span></span> <span data-ttu-id="56624-178">這些步驟逐步其中一種方式 toocreate 原則。</span><span class="sxs-lookup"><span data-stu-id="56624-178">These steps walk through one way toocreate a policy.</span></span> <span data-ttu-id="56624-179">如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](../active-directory/active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="56624-179">For more information, read about [Conditional Access in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span></span>

1. <span data-ttu-id="56624-180">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="56624-180">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="56624-181">跳過**Azure Active Directory** > **條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="56624-181">Go too**Azure Active Directory** > **Conditional access**.</span></span>
3. <span data-ttu-id="56624-182">選取 [新增原則]。</span><span class="sxs-lookup"><span data-stu-id="56624-182">Select **New policy**.</span></span>
4. <span data-ttu-id="56624-183">在 [指派] 底下選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="56624-183">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="56624-184">使用 hello **Include**和**排除**toospecify hello 原則將管理哪些使用者和群組的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="56624-184">Use hello **Include** and **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>
5. <span data-ttu-id="56624-185">在 [指派] 底下選取 [雲端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56624-185">Under **Assignments**, select **Cloud apps**.</span></span> <span data-ttu-id="56624-186">選擇 tooinclude**所有雲端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="56624-186">Choose tooinclude **All cloud apps**.</span></span>
6. <span data-ttu-id="56624-187">在 [存取控制] 底下選取 [授與]。</span><span class="sxs-lookup"><span data-stu-id="56624-187">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="56624-188">選擇 [需要多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="56624-188">Choose **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="56624-189">開啟**啟用原則**太**上**，然後選取 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="56624-189">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="56624-190">hello hello 條件式存取原則中的其他選項可讓您 toospecify 應該是必要的雙步驟驗證的確切時間。</span><span class="sxs-lookup"><span data-stu-id="56624-190">hello other options in hello conditional access policy allow you toospecify exactly when two-step verification should be required.</span></span> <span data-ttu-id="56624-191">例如，您可以進行原則，指出： 當約聘人員嘗試 tooaccess 我們採購的應用程式從未加入網域的裝置上不受信任網路時，需要兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="56624-191">For example, you could make a policy that states: when contractors try tooaccess our procurement app from untrusted networks on devices that are not domain-joined, require two-step verification.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="56624-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56624-192">Next steps</span></span>

- <span data-ttu-id="56624-193">取得秘訣 hello[條件式存取的最佳做法](../active-directory/active-directory-conditional-access-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="56624-193">Get tips on hello [Best practices for conditional access](../active-directory/active-directory-conditional-access-best-practices.md)</span></span>

- <span data-ttu-id="56624-194">管理[您的使用者和其裝置](multi-factor-authentication-manage-users-and-devices.md)的 Multi-Factor Authentication 設定</span><span class="sxs-lookup"><span data-stu-id="56624-194">Manage Multi-Factor Authentication settings for [your users and their devices](multi-factor-authentication-manage-users-and-devices.md)</span></span>