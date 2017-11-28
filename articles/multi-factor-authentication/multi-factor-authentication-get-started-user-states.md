---
title: "Microsoft Azure Multi-Factor Authentication 使用者狀態"
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
ms.openlocfilehash: 1869b7a4ef42536a3cd909ba2983ae0fe97185a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-require-two-step-verification-for-a-user-or-group"></a><span data-ttu-id="5ad65-103">如何要求使用者或群組使用雙步驟驗證</span><span class="sxs-lookup"><span data-stu-id="5ad65-103">How to require two-step verification for a user or group</span></span>

<span data-ttu-id="5ad65-104">可供您要求使用雙步驟驗證的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="5ad65-104">There are two approaches for requiring two-step verification.</span></span> <span data-ttu-id="5ad65-105">第一個選項是為每個使用者啟用 Azure Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-105">The first option is to enable each individual user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="5ad65-106">當您個別地為使用者啟用時，這些使用者永遠會執行雙步驟驗證 (但有一些例外，例如當他們從受信任的 IP 位址登入時，或如果他們開啟已記住的裝置功能)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-106">When users are enabled individually, they always perform two-step verification (with some exceptions, like when they sign in from trusted IP addresses or if the remembered devices feature is turned on).</span></span> <span data-ttu-id="5ad65-107">第二個選項是設定條件式存取原則，以在某些情況下要求使用雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="5ad65-107">The second option is to set up a conditional access policy that requires two-step verification under certain conditions.</span></span>

>[!TIP] 
><span data-ttu-id="5ad65-108">請選擇其中一種方法來要求使用雙步驟驗證，但不要兩種方法都使用。</span><span class="sxs-lookup"><span data-stu-id="5ad65-108">Choose one of these methods to require two-step verification, not both.</span></span> <span data-ttu-id="5ad65-109">為使用者啟用 Azure MFA 的效力會凌駕任何條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ad65-109">Enabling a user for Azure MFA overrides any conditional access policies.</span></span>

## <a name="which-option-is-right-for-you"></a><span data-ttu-id="5ad65-110">您合適的選項</span><span class="sxs-lookup"><span data-stu-id="5ad65-110">Which option is right for you</span></span>

<span data-ttu-id="5ad65-111">**藉由變更使用者狀態來啟用 Azure MFA** 是用來要求使用雙步驟驗證的傳統方法。</span><span class="sxs-lookup"><span data-stu-id="5ad65-111">**Enabling Azure MFA by changing user states** is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="5ad65-112">這種方法適用於雲端 Azure MFA 和 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="5ad65-112">It works for both Azure MFA in the cloud and Azure MFA Server.</span></span> <span data-ttu-id="5ad65-113">您所啟用的所有使用者都會有相同的體驗，也就是每次登入時都要執行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="5ad65-113">All the users that you enable have the same experience, which is to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="5ad65-114">啟用使用者的效力會凌駕任何可能影響該使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ad65-114">Enabling a user overrides any conditional access policies that may affect that user.</span></span> 

<span data-ttu-id="5ad65-115">**使用條件式存取原則來啟用 Azure MFA** 是用來要求使用雙步驟驗證的更彈性方法。</span><span class="sxs-lookup"><span data-stu-id="5ad65-115">**Enabling Azure MFA with a conditional access policy** is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="5ad65-116">但此方法只適用於雲端 Azure MFA，而且條件式存取是 [Azure Active Directory 的付費功能](https://www.microsoft.com/cloud-platform/azure-active-directory-features)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-116">It only work for Azure MFA in the cloud, though, and conditional access is a [paid feature of Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span> <span data-ttu-id="5ad65-117">您可以建立適用於群組以及個別使用者的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ad65-117">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="5ad65-118">您可以對高風險群組施加比低風險群組更多的限制，或者，也可以只針對高風險雲端應用程式要求雙步驟驗證，至於低風險的雲端應用程式則略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="5ad65-118">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> 

<span data-ttu-id="5ad65-119">當您開啟此要求後，這兩個選項都會提示使用者在第一次登入時註冊 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="5ad65-119">Both of these options prompt users to register for Azure Multi-Factor Authentication the first time that they sign in after the requirements turn on.</span></span> <span data-ttu-id="5ad65-120">這兩個選項也能與可設定的 [Azure Multi-Factor Authentication 設定](multi-factor-authentication-whats-next.md)搭配運作</span><span class="sxs-lookup"><span data-stu-id="5ad65-120">Both options also work with the configurable [Azure Multi-Factor Authentication settings](multi-factor-authentication-whats-next.md)</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="5ad65-121">藉由變更使用者狀態來啟用 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="5ad65-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="5ad65-122">Azure Multi-Factor Authentication 中的使用者帳戶具有下列三種不同狀態：</span><span class="sxs-lookup"><span data-stu-id="5ad65-122">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span></span>

| <span data-ttu-id="5ad65-123">狀態</span><span class="sxs-lookup"><span data-stu-id="5ad65-123">Status</span></span> | <span data-ttu-id="5ad65-124">說明</span><span class="sxs-lookup"><span data-stu-id="5ad65-124">Description</span></span> | <span data-ttu-id="5ad65-125">受影響的非瀏覽器應用程式</span><span class="sxs-lookup"><span data-stu-id="5ad65-125">Non-browser apps affected</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="5ad65-126">已停用</span><span class="sxs-lookup"><span data-stu-id="5ad65-126">Disabled</span></span> |<span data-ttu-id="5ad65-127">未註冊 Azure Multi-Factor Authentication (MFA) 之新使用者的預設狀態。</span><span class="sxs-lookup"><span data-stu-id="5ad65-127">The default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="5ad65-128">否</span><span class="sxs-lookup"><span data-stu-id="5ad65-128">No</span></span> |
| <span data-ttu-id="5ad65-129">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ad65-129">Enabled</span></span> |<span data-ttu-id="5ad65-130">已在 Azure MFA 中註冊使用者，但使用者尚未註冊。</span><span class="sxs-lookup"><span data-stu-id="5ad65-130">The user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="5ad65-131">系統將在他們下一次登入時提示他們註冊。</span><span class="sxs-lookup"><span data-stu-id="5ad65-131">They will be prompted to register the next time they sign in.</span></span> |<span data-ttu-id="5ad65-132">不會。</span><span class="sxs-lookup"><span data-stu-id="5ad65-132">No.</span></span>  <span data-ttu-id="5ad65-133">它們會繼續運作，直到註冊程序完成為止。</span><span class="sxs-lookup"><span data-stu-id="5ad65-133">They continue to work until the registration process is completed.</span></span> |
| <span data-ttu-id="5ad65-134">已強制</span><span class="sxs-lookup"><span data-stu-id="5ad65-134">Enforced</span></span> |<span data-ttu-id="5ad65-135">已註冊使用者，而且使用者已完成 Azure MFA 的註冊程序。</span><span class="sxs-lookup"><span data-stu-id="5ad65-135">The user has been enrolled and has completed the registration process for Azure MFA.</span></span> |<span data-ttu-id="5ad65-136">是。</span><span class="sxs-lookup"><span data-stu-id="5ad65-136">Yes.</span></span>  <span data-ttu-id="5ad65-137">應用程式需要應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="5ad65-137">Apps require app passwords.</span></span> |

<span data-ttu-id="5ad65-138">使用者的狀態會反映系統管理員是否已在 Azure MFA 中註冊他們，以及他們是否已完成註冊程序。</span><span class="sxs-lookup"><span data-stu-id="5ad65-138">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span></span>

<span data-ttu-id="5ad65-139">所有使用者一開始都是「已停用」狀態。</span><span class="sxs-lookup"><span data-stu-id="5ad65-139">All users start out *disabled*.</span></span> <span data-ttu-id="5ad65-140">當您在 Azure MFA 中註冊使用者時，他們的狀態會變更為「已啟用」。</span><span class="sxs-lookup"><span data-stu-id="5ad65-140">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="5ad65-141">當已啟用的使用者登入並完成註冊程序之後，他們的狀態就會變更為「已強制」。</span><span class="sxs-lookup"><span data-stu-id="5ad65-141">When enabled users sign in and complete the registration process, their state changes to *enforced*.</span></span>  

### <a name="view-the-status-for-a-user"></a><span data-ttu-id="5ad65-142">檢視使用者的狀態</span><span class="sxs-lookup"><span data-stu-id="5ad65-142">View the status for a user</span></span>

<span data-ttu-id="5ad65-143">使用下列步驟來存取您可在其中檢視並管理使用者狀態的頁面：</span><span class="sxs-lookup"><span data-stu-id="5ad65-143">Use the following steps to access the page where you can view and manage user states:</span></span>

1. <span data-ttu-id="5ad65-144">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-144">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="5ad65-145">移至 [Azure Active Directory] > [使用者和群組] > [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-145">Go to **Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="5ad65-146">選取 [多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-146">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="5ad65-147">![選取 Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="5ad65-147">![Select Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span></span>
4. <span data-ttu-id="5ad65-148">隨即會開啟新的頁面，以顯示使用者狀態。</span><span class="sxs-lookup"><span data-stu-id="5ad65-148">A new page, which displays the user states, opens.</span></span>
   <span data-ttu-id="5ad65-149">![Multi-Factor Authentication 使用者狀態 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="5ad65-149">![multi-factor authentication user status - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-the-status-for-a-user"></a><span data-ttu-id="5ad65-150">變更使用者的狀態</span><span class="sxs-lookup"><span data-stu-id="5ad65-150">Change the status for a user</span></span>

1. <span data-ttu-id="5ad65-151">使用上述步驟來取得 Multi-Factor Authentication使用者頁面。</span><span class="sxs-lookup"><span data-stu-id="5ad65-151">Use the preceding steps to get to the multi-factor authentication users page.</span></span>
2. <span data-ttu-id="5ad65-152">尋找您想要針對 Azure MFA 啟用的使用者。</span><span class="sxs-lookup"><span data-stu-id="5ad65-152">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="5ad65-153">您可能需要在頂端變更檢視。</span><span class="sxs-lookup"><span data-stu-id="5ad65-153">You may need to change the view at the top.</span></span> 
   <span data-ttu-id="5ad65-154">![尋找使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="5ad65-154">![Find user - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="5ad65-155">勾選其名稱旁的方塊。</span><span class="sxs-lookup"><span data-stu-id="5ad65-155">Check the box next to their name.</span></span>
4. <span data-ttu-id="5ad65-156">在右邊的快速步驟底下，選擇 [啟用] 或 [停用]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-156">On the right, under quick steps, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="5ad65-157">![啟用所選的使用者 - 螢幕擷取畫面](./media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="5ad65-157">![Enable selected user - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>

   >[!TIP]
   ><span data-ttu-id="5ad65-158">「已啟用」的使用者會在註冊 Azure MFA 時自動切換為「已強制」。</span><span class="sxs-lookup"><span data-stu-id="5ad65-158">*Enabled* users automatically switch to *enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="5ad65-159">請勿以手動方式將使用者狀態變更為「已強制」。</span><span class="sxs-lookup"><span data-stu-id="5ad65-159">You shouldn't manually change the user state to enforced.</span></span> 

5. <span data-ttu-id="5ad65-160">在開啟的快顯視窗中確認您的選取項目。</span><span class="sxs-lookup"><span data-stu-id="5ad65-160">Confirm your selection in the pop-up window that opens.</span></span> 

<span data-ttu-id="5ad65-161">當您啟用使用者之後，應透過電子郵件通知他們。</span><span class="sxs-lookup"><span data-stu-id="5ad65-161">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="5ad65-162">告訴他們系統會在他們下一次登入時要求其進行註冊。</span><span class="sxs-lookup"><span data-stu-id="5ad65-162">Tell them that they'll be asked to register the next time they sign in.</span></span> <span data-ttu-id="5ad65-163">此外，如果您的組織使用不支援新式驗證的非瀏覽器應用程式，他們就需要建立應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="5ad65-163">Also, if your organization uses non-browser apps that don't support modern authentication, they'll need to create app passwords.</span></span> <span data-ttu-id="5ad65-164">您也可以包含我們所提供 [Azure MFA 使用者指南](./end-user/multi-factor-authentication-end-user.md)的連結，以協助他們開始使用。</span><span class="sxs-lookup"><span data-stu-id="5ad65-164">You can also include a link to our [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) to help them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="5ad65-165">使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ad65-165">Use PowerShell</span></span>
<span data-ttu-id="5ad65-166">若要使用 [Azure AD PowerShell](/powershell/azure/overview) 來變更使用者狀態，請變更 `$st.State`。</span><span class="sxs-lookup"><span data-stu-id="5ad65-166">To change the user status state using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="5ad65-167">有三個可能的狀態︰</span><span class="sxs-lookup"><span data-stu-id="5ad65-167">There are three possible states:</span></span>

* <span data-ttu-id="5ad65-168">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ad65-168">Enabled</span></span>
* <span data-ttu-id="5ad65-169">已強制</span><span class="sxs-lookup"><span data-stu-id="5ad65-169">Enforced</span></span>
* <span data-ttu-id="5ad65-170">已停用</span><span class="sxs-lookup"><span data-stu-id="5ad65-170">Disabled</span></span>  

<span data-ttu-id="5ad65-171">請勿直接將使用者移至「已強制」狀態。</span><span class="sxs-lookup"><span data-stu-id="5ad65-171">Don't move users directly to the *Enforced* state.</span></span> <span data-ttu-id="5ad65-172">非瀏覽器型應用程式會停止運作，因為使用者未通過 MFA 註冊並取得[應用程式密碼](multi-factor-authentication-whats-next.md#app-passwords)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-172">Non-browser-based apps will stop working because the user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> 

<span data-ttu-id="5ad65-173">當您需要大量啟用使用者時，使用 PowerShell 是一個不錯的選項。</span><span class="sxs-lookup"><span data-stu-id="5ad65-173">Using PowerShell is a good option when you need to bulk enabling users.</span></span> <span data-ttu-id="5ad65-174">建立會在使用者清單中循環移動並啟用這些使用者的 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="5ad65-174">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="5ad65-175">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5ad65-175">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a><span data-ttu-id="5ad65-176">使用條件式存取原則來啟用 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="5ad65-176">Enable Azure MFA with a conditional access policy</span></span>

<span data-ttu-id="5ad65-177">條件式存取是 Azure Active Directory 的付費功能，其具有許多可能的設定選項。</span><span class="sxs-lookup"><span data-stu-id="5ad65-177">Conditional access is a paid feature of Azure Active Directory, with many possible configuration options.</span></span> <span data-ttu-id="5ad65-178">下列步驟會逐步解說一種用來建立原則的方式。</span><span class="sxs-lookup"><span data-stu-id="5ad65-178">These steps walk through one way to create a policy.</span></span> <span data-ttu-id="5ad65-179">如需詳細資訊，請參閱 [Azure Active Directory 中的條件式存取](../active-directory/active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-179">For more information, read about [Conditional Access in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span></span>

1. <span data-ttu-id="5ad65-180">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5ad65-180">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="5ad65-181">移至 [Azure Active Directory] > [條件式存取]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-181">Go to **Azure Active Directory** > **Conditional access**.</span></span>
3. <span data-ttu-id="5ad65-182">選取 [新增原則]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-182">Select **New policy**.</span></span>
4. <span data-ttu-id="5ad65-183">在 [指派] 底下選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-183">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="5ad65-184">使用 [包含] 和 [排除] 索引標籤來指定要由原則管理的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="5ad65-184">Use the **Include** and **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>
5. <span data-ttu-id="5ad65-185">在 [指派] 底下選取 [雲端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-185">Under **Assignments**, select **Cloud apps**.</span></span> <span data-ttu-id="5ad65-186">選擇要包含 [所有雲端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-186">Choose to include **All cloud apps**.</span></span>
6. <span data-ttu-id="5ad65-187">在 [存取控制] 底下選取 [授與]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-187">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="5ad65-188">選擇 [需要多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-188">Choose **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="5ad65-189">將 [啟用原則] 轉為 [開啟]，然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5ad65-189">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="5ad65-190">條件式存取原則中的其他選項可讓您明確指定何時應該要求雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="5ad65-190">The other options in the conditional access policy allow you to specify exactly when two-step verification should be required.</span></span> <span data-ttu-id="5ad65-191">例如，您可以建立規定如下的原則：當承包商嘗試從未加入網域的裝置上不受信任的網路存取我們的採購應用程式時，要求進行雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="5ad65-191">For example, you could make a policy that states: when contractors try to access our procurement app from untrusted networks on devices that are not domain-joined, require two-step verification.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5ad65-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ad65-192">Next steps</span></span>

- <span data-ttu-id="5ad65-193">取得[條件式存取的最佳做法](../active-directory/active-directory-conditional-access-best-practices.md)秘訣</span><span class="sxs-lookup"><span data-stu-id="5ad65-193">Get tips on the [Best practices for conditional access](../active-directory/active-directory-conditional-access-best-practices.md)</span></span>

- <span data-ttu-id="5ad65-194">管理[您的使用者和其裝置](multi-factor-authentication-manage-users-and-devices.md)的 Multi-Factor Authentication 設定</span><span class="sxs-lookup"><span data-stu-id="5ad65-194">Manage Multi-Factor Authentication settings for [your users and their devices](multi-factor-authentication-manage-users-and-devices.md)</span></span>