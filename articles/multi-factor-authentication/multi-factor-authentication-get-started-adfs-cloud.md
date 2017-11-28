---
title: "使用 Azure MFA 與 AD FS 保護雲端資源 | Microsoft Docs"
description: "這是說明如何在雲端開始使用 Azure MFA 和 AD FS 的 Azure Multi-Factor Authentication 頁面。"
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
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="324fa-103">使用 Azure Multi-Factor Authentication 與 AD FS 保護雲端資源</span><span class="sxs-lookup"><span data-stu-id="324fa-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="324fa-104">如果您的組織與 Azure Active Directory 同盟，請使用 Azure Multi-factor Authentication 或 Active Directory Federation Services (AD FS) 來保護 Azure AD 存取的資源。</span><span class="sxs-lookup"><span data-stu-id="324fa-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="324fa-105">使用下列程序可利用 Azure Multi-Factor Authentication 或 Active Directory Federation Services 來保護 Azure Active Directory 資源。</span><span class="sxs-lookup"><span data-stu-id="324fa-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="324fa-106">使用 AD FS 保護 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="324fa-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="324fa-107">若要保護雲端資源，請設定宣告規則，以便在使用者成功執行雙步驟驗證時，Active Directory Federation Services 會發出 multipleauthn 宣告。</span><span class="sxs-lookup"><span data-stu-id="324fa-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="324fa-108">此宣告會傳遞至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="324fa-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="324fa-109">遵循此程序來逐步執行各個步驟︰</span><span class="sxs-lookup"><span data-stu-id="324fa-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="324fa-110">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="324fa-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="324fa-111">在左側選取 [信賴憑證者信任]。</span><span class="sxs-lookup"><span data-stu-id="324fa-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="324fa-112">以滑鼠右鍵按一下 [Microsoft Office 365 身分識別平台]，然後選取 [編輯宣告規則]。</span><span class="sxs-lookup"><span data-stu-id="324fa-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="324fa-114">在 [發佈轉換規則] 上，按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="324fa-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="324fa-116">在 [新增轉換宣告規則精靈] 上，從下拉式清單選取 [通過或篩選傳入宣告]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="324fa-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="324fa-118">指定規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="324fa-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="324fa-119">選取 [驗證方法參考] 做為傳入宣告類型。</span><span class="sxs-lookup"><span data-stu-id="324fa-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="324fa-120">選取 [傳遞所有宣告值]。</span><span class="sxs-lookup"><span data-stu-id="324fa-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="324fa-121">![新增轉換宣告規則精靈](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="324fa-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="324fa-122">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="324fa-122">Click **Finish**.</span></span> <span data-ttu-id="324fa-123">關閉 AD FS 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="324fa-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="324fa-124">同盟使用者的可信任 IP</span><span class="sxs-lookup"><span data-stu-id="324fa-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="324fa-125">信任的 IP 可讓系統管理員針對特定的 IP 位址，或針對從他們自己的內部網路發出要求的同盟使用者，略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="324fa-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="324fa-126">下列各節說明當要求是來自同盟使用者的內部網路時，如何設定同盟使用者的 Azure Multi-Factor Authentication 信任的 IP，以及略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="324fa-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="324fa-127">這是藉由設定 AD FS 使用「通過或篩選傳入宣告」範本與「位於公司網路之內」宣告類別來達成。</span><span class="sxs-lookup"><span data-stu-id="324fa-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="324fa-128">此範例使用 Office 365 做為信賴憑證者信任。</span><span class="sxs-lookup"><span data-stu-id="324fa-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="324fa-129">設定 AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="324fa-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="324fa-130">我們要做的第一件事是設定 AD FS 宣告。</span><span class="sxs-lookup"><span data-stu-id="324fa-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="324fa-131">建立兩個宣告規則，一個用於「位於公司網路之內」宣告類型，另一個用於保持使用者登入。</span><span class="sxs-lookup"><span data-stu-id="324fa-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="324fa-132">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="324fa-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="324fa-133">在左側選取 [信賴憑證者信任]。</span><span class="sxs-lookup"><span data-stu-id="324fa-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="324fa-134">以滑鼠右鍵按一下**[Microsoft Office 365 身分識別平台]**，然後選取 **[編輯宣告規則...]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="324fa-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="324fa-135">在 [發佈轉換規則] 上，按一下 **[新增規則]**。
   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="324fa-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="324fa-136">在 [新增轉換宣告規則精靈] 上，從下拉式清單選取 [通過或篩選傳入宣告]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="324fa-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="324fa-137">![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="324fa-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="324fa-138">在 [宣告規則名稱] 旁邊的方塊中，命名您的規則。</span><span class="sxs-lookup"><span data-stu-id="324fa-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="324fa-139">例如：InsideCorpNet。</span><span class="sxs-lookup"><span data-stu-id="324fa-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="324fa-140">從 [連入宣告類型] 旁邊的下拉式清單中，選取 [位於公司網路之內]。</span><span class="sxs-lookup"><span data-stu-id="324fa-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="324fa-141">![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="324fa-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="324fa-142">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="324fa-142">Click **Finish**.</span></span>
9. <span data-ttu-id="324fa-143">在 [發佈轉換規則] 上，按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="324fa-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="324fa-144">在 [新增轉換宣告規則精靈] 上，從下拉式清單選取 [使用自訂規則傳送宣告]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="324fa-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="324fa-145">在 [宣告規則名稱] 下的方塊中：輸入「保持使用者登入」。</span><span class="sxs-lookup"><span data-stu-id="324fa-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="324fa-146">在 [自訂規則] 方塊中輸入：</span><span class="sxs-lookup"><span data-stu-id="324fa-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="324fa-148">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="324fa-148">Click **Finish**.</span></span>
14. <span data-ttu-id="324fa-149">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="324fa-149">Click **Apply**.</span></span>
15. <span data-ttu-id="324fa-150">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="324fa-150">Click **Ok**.</span></span>
16. <span data-ttu-id="324fa-151">關閉 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="324fa-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="324fa-152">搭配同盟使用者設定 Azure Multi-Factor Authentication 信任的 IP</span><span class="sxs-lookup"><span data-stu-id="324fa-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="324fa-153">既然已經有宣告，我們可以開始設定信任的 IP。</span><span class="sxs-lookup"><span data-stu-id="324fa-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="324fa-154">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="324fa-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="324fa-155">在左側按一下 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="324fa-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="324fa-156">在目錄底下，選取您要在其中設定信任之 IP 的目錄。</span><span class="sxs-lookup"><span data-stu-id="324fa-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="324fa-157">在您選取的目錄上，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="324fa-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="324fa-158">在 Multi-Factor Authentication 區段中，按一下 [管理服務設定]。</span><span class="sxs-lookup"><span data-stu-id="324fa-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="324fa-159">在 [服務設定] 頁面的 [信任的 IP] 下，選取 [對於來自內部網路之同盟使用者的要求略過多重要素驗證]。</span><span class="sxs-lookup"><span data-stu-id="324fa-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="324fa-161">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="324fa-161">Click **save**.</span></span>
8. <span data-ttu-id="324fa-162">套用更新之後，請按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="324fa-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="324fa-163">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="324fa-163">That’s it!</span></span> <span data-ttu-id="324fa-164">現在，當宣告來自公司內部網路之外時，Office 365 使用者同盟只需要使用 MFA。</span><span class="sxs-lookup"><span data-stu-id="324fa-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
