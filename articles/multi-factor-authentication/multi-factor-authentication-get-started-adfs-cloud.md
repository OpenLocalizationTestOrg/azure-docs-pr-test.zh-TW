---
title: "使用 Azure MFA 和 AD FS aaaSecure 雲端資源 |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 AD FS hello 雲端中的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="9cc98-103">使用 Azure Multi-Factor Authentication 與 AD FS 保護雲端資源</span><span class="sxs-lookup"><span data-stu-id="9cc98-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="9cc98-104">如果您的組織會與 Azure Active Directory 同盟，使用 Azure Multi-factor Authentication 或 Active Directory Federation Services (AD FS) toosecure 資源存取的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="9cc98-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="9cc98-105">使用下列程序 toosecure Azure Active Directory 資源與 Azure Multi-factor Authentication 或 Active Directory Federation Services 的 hello。</span><span class="sxs-lookup"><span data-stu-id="9cc98-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="9cc98-106">使用 AD FS 保護 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="9cc98-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="9cc98-107">toosecure 您雲端的資源，設定宣告規則，讓使用者執行雙步驟驗證成功時，Active Directory Federation Services 會發出 hello multipleauthn 宣告。</span><span class="sxs-lookup"><span data-stu-id="9cc98-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="9cc98-108">這個宣告會傳遞 tooAzure AD 上。</span><span class="sxs-lookup"><span data-stu-id="9cc98-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="9cc98-109">請遵循此程序 toowalk，透過 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="9cc98-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="9cc98-110">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="9cc98-111">Hello 左側選取**信賴憑證者信任**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="9cc98-112">以滑鼠右鍵按一下 [Microsoft Office 365 身分識別平台]，然後選取 [編輯宣告規則]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="9cc98-114">在 [發佈轉換規則] 上，按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="9cc98-116">在 hello 新增轉換宣告規則精靈中，選取**傳遞或篩選傳入宣告**從 hello 下拉式清單，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="9cc98-118">指定規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cc98-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="9cc98-119">選取**驗證方法參考**為 hello 傳入宣告類型。</span><span class="sxs-lookup"><span data-stu-id="9cc98-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="9cc98-120">選取 [傳遞所有宣告值]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="9cc98-121">![新增轉換宣告規則精靈](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="9cc98-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="9cc98-122">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9cc98-122">Click **Finish**.</span></span> <span data-ttu-id="9cc98-123">關閉 hello AD FS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="9cc98-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="9cc98-124">同盟使用者的可信任 IP</span><span class="sxs-lookup"><span data-stu-id="9cc98-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="9cc98-125">信任的 Ip 可讓系統管理員 tooby 傳遞雙步驟驗證特定的 IP 位址，或具有源自其自己內部網路要求的同盟使用者。</span><span class="sxs-lookup"><span data-stu-id="9cc98-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="9cc98-126">hello 下列各節說明如何 tooconfigure Azure 多重要素驗證信任 Ip 和同盟的使用者，當要求源自同盟的使用者內部網路時略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="9cc98-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="9cc98-127">這是設定來達成的 AD FS toouse 傳遞或篩選內送宣告範本以 hello 公司網路內部的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="9cc98-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="9cc98-128">此範例使用 Office 365 做為信賴憑證者信任。</span><span class="sxs-lookup"><span data-stu-id="9cc98-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="9cc98-129">設定 hello AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="9cc98-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="9cc98-130">我們需要 toodo hello 第一件事是 tooconfigure hello AD FS 宣告。</span><span class="sxs-lookup"><span data-stu-id="9cc98-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="9cc98-131">建立兩個宣告規則，一個用於 hello 公司網路內部宣告類型和另一個，適用於維持使用者登入。</span><span class="sxs-lookup"><span data-stu-id="9cc98-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="9cc98-132">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="9cc98-133">Hello 左側選取**信賴憑證者信任**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="9cc98-134">以滑鼠右鍵按一下**[Microsoft Office 365 身分識別平台]**，然後選取 **[編輯宣告規則...]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="9cc98-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="9cc98-135">在 [發佈轉換規則] 上，按一下 **[新增規則]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="9cc98-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="9cc98-136">在 hello 新增轉換宣告規則精靈中，選取**傳遞或篩選傳入宣告**從 hello 下拉式清單，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="9cc98-137">![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="9cc98-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="9cc98-138">在 [hello] 方塊下一步 tooClaim 規則名稱命名您的規則。</span><span class="sxs-lookup"><span data-stu-id="9cc98-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="9cc98-139">例如：InsideCorpNet。</span><span class="sxs-lookup"><span data-stu-id="9cc98-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="9cc98-140">Hello 下拉式清單中，從 下一步 tooIncoming 宣告類型，則選取**公司網路內部**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="9cc98-141">![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="9cc98-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="9cc98-142">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9cc98-142">Click **Finish**.</span></span>
9. <span data-ttu-id="9cc98-143">在 [發佈轉換規則] 上，按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="9cc98-144">在 hello 新增轉換宣告規則精靈中，選取**使用自訂規則傳送宣告**從 hello 下拉式清單，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="9cc98-145">在 宣告規則名稱底下的 hello 方塊： 輸入*維持使用者登入*。</span><span class="sxs-lookup"><span data-stu-id="9cc98-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="9cc98-146">在 [hello 自訂規則] 方塊中輸入：</span><span class="sxs-lookup"><span data-stu-id="9cc98-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="9cc98-148">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="9cc98-148">Click **Finish**.</span></span>
14. <span data-ttu-id="9cc98-149">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="9cc98-149">Click **Apply**.</span></span>
15. <span data-ttu-id="9cc98-150">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-150">Click **Ok**.</span></span>
16. <span data-ttu-id="9cc98-151">關閉 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="9cc98-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="9cc98-152">搭配同盟使用者設定 Azure Multi-Factor Authentication 信任的 IP</span><span class="sxs-lookup"><span data-stu-id="9cc98-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="9cc98-153">既然 hello 宣告已備妥，我們可以設定信任的 Ip。</span><span class="sxs-lookup"><span data-stu-id="9cc98-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="9cc98-154">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="9cc98-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9cc98-155">Hello 左側，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="9cc98-156">在 [目錄] 選取您要設定信任的 Ip tooset 的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="9cc98-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="9cc98-157">在 hello 您選取的目錄中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="9cc98-158">在 hello 多因素驗證 區段中，按一下 **管理服務設定**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="9cc98-159">在 [hello 服務設定] 頁面上，在受信任 Ip 時，選取**從同盟使用者略過多 multi-factor-authentication 要求，我的內部網路上**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="9cc98-161">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9cc98-161">Click **save**.</span></span>
8. <span data-ttu-id="9cc98-162">一旦套用 hello 更新之後，按一下 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="9cc98-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="9cc98-163">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="9cc98-163">That’s it!</span></span> <span data-ttu-id="9cc98-164">此時，Office 365 同盟的使用者應該只有 toouse MFA 時宣告來自外部的 hello 公司內部網路。</span><span class="sxs-lookup"><span data-stu-id="9cc98-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
