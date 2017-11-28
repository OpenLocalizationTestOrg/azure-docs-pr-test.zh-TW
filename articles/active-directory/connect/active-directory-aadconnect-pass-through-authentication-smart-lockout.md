---
title: "Azure AD Connect：傳遞驗證 - 智慧鎖定 | Microsoft Docs"
description: "本文章說明 Azure Active Directory (Azure AD) 的傳遞驗證如何在內部部署帳戶防止暴力密碼破解攻擊 hello 雲端中。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="a30ec-104">Azure Active Directory 傳遞驗證：智慧鎖定</span><span class="sxs-lookup"><span data-stu-id="a30ec-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="a30ec-105">概觀</span><span class="sxs-lookup"><span data-stu-id="a30ec-105">Overview</span></span>

<span data-ttu-id="a30ec-106">Azure AD 可防範暴力密碼破解攻擊，並防止正版使用者遭到其 Office 365 和 SaaS 應用程式鎖定而無法使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="a30ec-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="a30ec-107">當您使用傳遞驗證來作為登入方法時，系統便支援這項稱為**智慧鎖定**的功能。</span><span class="sxs-lookup"><span data-stu-id="a30ec-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="a30ec-108">智慧鎖定預設會啟用所有租用戶和要保護所有的 hello 時間; 您的使用者帳戶沒有任何需要 tooturn 其上。</span><span class="sxs-lookup"><span data-stu-id="a30ec-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="a30ec-109">智慧鎖定在運作時，會追蹤失敗的登入嘗試，並在經過一定的**鎖定閾值**後，開始**鎖定期間**。</span><span class="sxs-lookup"><span data-stu-id="a30ec-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="a30ec-110">從 hello 攻擊者在 hello 鎖定持續時間期間的任何登入嘗試會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="a30ec-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="a30ec-111">如果仍繼續 hello 攻擊，hello 後續失敗登入嘗試 hello 鎖定持續時間結束導致較長鎖定持續時間。</span><span class="sxs-lookup"><span data-stu-id="a30ec-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="a30ec-112">hello 預設鎖定閾值為 10 的失敗的嘗試和 hello 預設鎖定持續時間為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="a30ec-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="a30ec-113">智慧鎖定也會區別登入從正版的使用者和攻擊者和出 hello 攻擊者在大部分情況下只鎖定。</span><span class="sxs-lookup"><span data-stu-id="a30ec-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="a30ec-114">這項功能可防止攻擊者惡意地讓使用者遭到鎖定。</span><span class="sxs-lookup"><span data-stu-id="a30ec-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="a30ec-115">我們會使用過去的登入的行為，使用者的裝置和瀏覽器和其他正版的使用者和攻擊者之間的信號 toodistinguish。</span><span class="sxs-lookup"><span data-stu-id="a30ec-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="a30ec-116">我們會持續改善我們的演算法。</span><span class="sxs-lookup"><span data-stu-id="a30ec-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="a30ec-117">傳遞驗證轉送到您在內部部署 Active Directory (AD) 的密碼驗證要求，因為您需要 tooprevent 攻擊者鎖定您的使用者的 AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a30ec-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="a30ec-118">由於您自己的 AD 帳戶鎖定原則 (特別是， [**帳戶鎖定閾值**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx)和[**重設帳戶鎖定計數器後原則** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx))，需要 tooconfigure Azure AD 的鎖定閾值，以及鎖定持續時間值適當地 toofilter 出攻擊 hello 雲端中才能到達您內部部署 AD。</span><span class="sxs-lookup"><span data-stu-id="a30ec-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="a30ec-119">hello 智慧鎖定功能免費而_上_依預設，所有客戶。</span><span class="sxs-lookup"><span data-stu-id="a30ec-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="a30ec-120">不過，修改 Azure AD 的鎖定 」 臨界值和使用 Graph API 的鎖定持續時間值需要您的租用戶 toohave 至少一個 Azure AD Premium P2 授權。</span><span class="sxs-lookup"><span data-stu-id="a30ec-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="a30ec-121">您不需要有 Azure AD Premium P2 授權_每位使用者_tooget hello 智慧鎖定功能，透過通過驗證。</span><span class="sxs-lookup"><span data-stu-id="a30ec-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="a30ec-122">保護 tooensure，您的使用者內部部署 AD 帳戶，您需要 tooensure 的：</span><span class="sxs-lookup"><span data-stu-id="a30ec-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="a30ec-123">Azure AD 的鎖定閾值「小於」AD 的帳戶鎖定閾值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="a30ec-124">我們建議您設定 hello 值，使 AD 的帳戶鎖定閾值是至少兩個或三次 Azure AD 的鎖定 」 臨界值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="a30ec-125">Azure AD 的鎖定期間 (以秒來表示) 比 AD 的下列時間過後重設帳戶鎖定計數器 (以分鐘來表示)「還久」。</span><span class="sxs-lookup"><span data-stu-id="a30ec-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="a30ec-126">驗證 AD 帳戶鎖定原則</span><span class="sxs-lookup"><span data-stu-id="a30ec-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="a30ec-127">使用下列指示 tooverify hello AD 帳戶鎖定原則：</span><span class="sxs-lookup"><span data-stu-id="a30ec-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="a30ec-128">開啟 hello 群組原則管理工具。</span><span class="sxs-lookup"><span data-stu-id="a30ec-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="a30ec-129">編輯 hello 的群組原則是套用的 tooall 使用者，例如 hello 預設網域原則。</span><span class="sxs-lookup"><span data-stu-id="a30ec-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="a30ec-130">瀏覽 tooComputer 原則 \windows 設定 \ 安全性帳戶原則 \ 帳戶鎖定原則。</span><span class="sxs-lookup"><span data-stu-id="a30ec-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="a30ec-131">確認 [帳戶鎖定閾值] 和 [下列時間過後重設帳戶鎖定計數器] 的值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![AD 帳戶鎖定原則](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="a30ec-133">使用您的租用戶智慧鎖定值 hello Graph API toomanage</span><span class="sxs-lookup"><span data-stu-id="a30ec-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="a30ec-134">使用圖形 API 來修改 Azure AD 的鎖定閾值和鎖定期間值是 Azure AD Premium P2 的功能。</span><span class="sxs-lookup"><span data-stu-id="a30ec-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="a30ec-135">它也需要 toobe 上您的租用戶的全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="a30ec-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="a30ec-136">您可以使用[圖表總管](https://developer.microsoft.com/graph/graph-explorer)tooread，設定和更新 Azure AD 的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="a30ec-137">但您也可以透過程式設計的方式進行這些作業。</span><span class="sxs-lookup"><span data-stu-id="a30ec-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="a30ec-138">讀取智慧鎖定值</span><span class="sxs-lookup"><span data-stu-id="a30ec-138">Read Smart Lockout values</span></span>

<span data-ttu-id="a30ec-139">請遵循這些步驟 tooread 租用戶的智慧鎖定值：</span><span class="sxs-lookup"><span data-stu-id="a30ec-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="a30ec-140">以租用戶全域管理員的身分登入 Graph 總管。</span><span class="sxs-lookup"><span data-stu-id="a30ec-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a30ec-141">如果出現提示，hello 授與存取權要求的權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="a30ec-142">按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a30ec-143">設定 hello Graph API 要求，如下所示： Set 版本太"BETA"，要求類型太 「 取得 」 和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`。</span><span class="sxs-lookup"><span data-stu-id="a30ec-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a30ec-144">按一下"執行查詢"toosee 租用戶的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="a30ec-145">如果您之前從未設定過租用戶的值，您會看到空白的設定。</span><span class="sxs-lookup"><span data-stu-id="a30ec-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="a30ec-146">設定智慧鎖定值</span><span class="sxs-lookup"><span data-stu-id="a30ec-146">Set Smart Lockout values</span></span>

<span data-ttu-id="a30ec-147">請遵循這些步驟 tooset （適用於 hello 只有第一次) 的租用戶的智慧鎖定值：</span><span class="sxs-lookup"><span data-stu-id="a30ec-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="a30ec-148">以租用戶全域管理員的身分登入 Graph 總管。</span><span class="sxs-lookup"><span data-stu-id="a30ec-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a30ec-149">如果出現提示，hello 授與存取權要求的權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="a30ec-150">按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a30ec-151">設定 hello Graph API 要求，如下所示： Set 版本太"BETA"，要求類型太"POST"和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`。</span><span class="sxs-lookup"><span data-stu-id="a30ec-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a30ec-152">複製並貼上下列 JSON 要求到 hello 「 要求內文 」 欄位的 hello。</span><span class="sxs-lookup"><span data-stu-id="a30ec-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="a30ec-153">變更為適當的 hello 智慧鎖定值，並使用的隨機 GUID `templateId`。</span><span class="sxs-lookup"><span data-stu-id="a30ec-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="a30ec-154">按一下"執行查詢"tooset 租用戶的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="a30ec-155">如果您不使用它們，您可以將 hello **BannedPasswordList**和**EnableBannedPasswordCheck**值，則為空白 ("") 和"false"分別。</span><span class="sxs-lookup"><span data-stu-id="a30ec-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="a30ec-156">確認您是否已使用[這些步驟](#read-smart-lockout-values)正確地設定租用戶的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="a30ec-157">更新智慧鎖定值</span><span class="sxs-lookup"><span data-stu-id="a30ec-157">Update Smart Lockout values</span></span>

<span data-ttu-id="a30ec-158">遵循這些步驟 tooupdate 租用戶的智慧鎖定值 （如果您已經設定過他們的）：</span><span class="sxs-lookup"><span data-stu-id="a30ec-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="a30ec-159">以租用戶全域管理員的身分登入 Graph 總管。</span><span class="sxs-lookup"><span data-stu-id="a30ec-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a30ec-160">如果出現提示，hello 授與存取權要求的權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="a30ec-161">按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。</span><span class="sxs-lookup"><span data-stu-id="a30ec-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a30ec-162">[您的租用戶智慧鎖定值，請遵循這些步驟 tooread](#read-smart-lockout-values)。</span><span class="sxs-lookup"><span data-stu-id="a30ec-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="a30ec-163">複製 hello `id` "displayName"為"PasswordRuleSettings"hello 項目的數值 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="a30ec-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="a30ec-164">設定 hello Graph API 要求，如下所示： 將版本設定為太"BETA"，太要求類型 「 修補 」 和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>`-使用 hello GUID，如步驟 3 `<id>`。</span><span class="sxs-lookup"><span data-stu-id="a30ec-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="a30ec-165">複製並貼上下列 JSON 要求到 hello 「 要求內文 」 欄位的 hello。</span><span class="sxs-lookup"><span data-stu-id="a30ec-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="a30ec-166">變更為適當的 hello 智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="a30ec-167">按一下"執行查詢"tooupdate 租用戶的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="a30ec-168">確認您是否已使用[這些步驟](#read-smart-lockout-values)正確地更新租用戶的智慧鎖定值。</span><span class="sxs-lookup"><span data-stu-id="a30ec-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a30ec-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a30ec-169">Next steps</span></span>
- <span data-ttu-id="a30ec-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="a30ec-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
