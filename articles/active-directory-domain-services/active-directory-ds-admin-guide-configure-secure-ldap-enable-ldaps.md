---
title: "aaaConfigure 安全 LDAP (LDAPS) 在 Azure AD 網域服務中 |Microsoft 文件"
description: "針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="18f83-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="18f83-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="18f83-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="18f83-104">Before you begin</span></span>
<span data-ttu-id="18f83-105">請確定您已完成[工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。</span><span class="sxs-lookup"><span data-stu-id="18f83-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="18f83-106">選擇 toouse hello 預覽 Azure 入口網站體驗或 hello Azure 傳統入口網站 toocomplete 這項工作。</span><span class="sxs-lookup"><span data-stu-id="18f83-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="18f83-107">**Azure 入口網站 （預覽）**:[啟用安全 LDAP 使用 hello Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="18f83-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="18f83-108">**Azure 傳統入口網站**:[啟用安全 LDAP 使用 hello 傳統 Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="18f83-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="18f83-109">工作 3-啟用安全 LDAP 的 hello 受管理的網域，使用 hello Azure 入口網站 （預覽）</span><span class="sxs-lookup"><span data-stu-id="18f83-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="18f83-110">tooenable 安全 LDAP 資訊，請執行下列組態步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18f83-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="18f83-111">瀏覽 toohello  **[Azure 入口網站](https://portal.azure.com)**。</span><span class="sxs-lookup"><span data-stu-id="18f83-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="18f83-112">搜尋 ' 網域中的服務' hello**搜尋資源**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="18f83-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="18f83-113">選取**Azure AD 網域服務**從 hello 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="18f83-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="18f83-114">hello **Azure AD 網域服務**刀鋒視窗會列出受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="18f83-116">按一下 hello 受管理網域 (例如，' contoso100.com') toosee hello 名稱 hello 定義域有關的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="18f83-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="18f83-118">按一下**安全 LDAP** hello 瀏覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="18f83-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services - 安全 LDAP 刀鋒視窗](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="18f83-120">根據預設，會停用安全 LDAP 存取 tooyour 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="18f83-121">切換**安全 LDAP**太**啟用**。</span><span class="sxs-lookup"><span data-stu-id="18f83-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![啟用安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="18f83-123">根據預設，安全 LDAP 存取 tooyour 可以透過網際網路已停用的 hello 管理網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="18f83-124">切換**允許安全 LDAP 存取透過 hello 網際網路**太**啟用**視。</span><span class="sxs-lookup"><span data-stu-id="18f83-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="18f83-125">按一下 hello 資料夾圖示下列**。使用安全 LDAP 的憑證的 PFX 檔案**。</span><span class="sxs-lookup"><span data-stu-id="18f83-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="18f83-126">指定安全 LDAP 存取 toohello 受管理的網域的 hello 憑證 hello 路徑 toohello PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="18f83-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="18f83-127">指定 hello**密碼 toodecrypt。PFX 檔案**。</span><span class="sxs-lookup"><span data-stu-id="18f83-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="18f83-128">提供 hello 匯出 hello 憑證 toohello PFX 檔案時所使用的相同密碼。</span><span class="sxs-lookup"><span data-stu-id="18f83-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="18f83-129">當您完成之後時，按一下 [hello**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18f83-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="18f83-130">您會看到通知，通知您正在設定安全 LDAP 的 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="18f83-131">這項作業完成之前，您無法修改 hello 網域的其他設定。</span><span class="sxs-lookup"><span data-stu-id="18f83-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![設定安全 LDAP 的 hello 受管理的網域](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="18f83-133">只需要大約 10 個 too15 分鐘 tooenable 安全 LDAP 的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="18f83-134">如果 hello 提供安全 LDAP 的憑證不符合 hello 所需的準則，您的目錄未啟用安全 LDAP，您看到失敗。</span><span class="sxs-lookup"><span data-stu-id="18f83-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="18f83-135">例如，hello 網域名稱不正確，hello 憑證已到期或即將過期。</span><span class="sxs-lookup"><span data-stu-id="18f83-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="18f83-136">在此情況下，使用有效憑證重試。</span><span class="sxs-lookup"><span data-stu-id="18f83-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="18f83-137">工作 4-設定 DNS tooaccess hello 受管理的網域從 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="18f83-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="18f83-138">**選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。</span><span class="sxs-lookup"><span data-stu-id="18f83-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="18f83-139">在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)。</span><span class="sxs-lookup"><span data-stu-id="18f83-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="18f83-140">透過啟用安全 LDAP 存取之後 hello 網際網路的受管理的網域中，您需要 tooupdate DNS，讓用戶端電腦可以找到此受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="18f83-141">在工作 3 hello 結尾，外部 IP 位址會顯示在 hello**屬性**刀鋒視窗中的**外部 IP 位址的 LDAPS 存取**。</span><span class="sxs-lookup"><span data-stu-id="18f83-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="18f83-142">設定外部的 DNS 提供者，讓該 hello DNS 名稱的 hello 管理網域 (例如，' ldaps.contoso100.com') 點 toothis 外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18f83-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="18f83-143">在本例中，我們需要 toocreate hello 下列 DNS 項目：</span><span class="sxs-lookup"><span data-stu-id="18f83-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="18f83-144">就這麼簡單： 現在您已經準備就緒 tooconnect toohello 受管理網域使用透過安全 LDAP hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="18f83-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="18f83-145">請記住，用戶端電腦必須信任 hello LDAPS 憑證 toobe 無法 tooconnect hello 簽發者成功 toohello 管理使用 LDAPS 網域。</span><span class="sxs-lookup"><span data-stu-id="18f83-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="18f83-146">如果您使用公開受信任的憑證授權單位，您不需要 toodo 任何項目因為用戶端電腦會信任這些憑證簽發者。</span><span class="sxs-lookup"><span data-stu-id="18f83-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="18f83-147">如果您使用自我簽署的憑證，請到 hello hello 用戶端電腦上的受信任的憑證存放區安裝 hello hello 自我簽署憑證的公開部分。</span><span class="sxs-lookup"><span data-stu-id="18f83-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="18f83-148">工作 5-鎖定 LDAPS 存取受管理的 tooyour 透過網域 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="18f83-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="18f83-149">**選擇性的工作**-如果您未啟用 LDAPS 存取 toohello 受管理的網域超過 hello 網際網路、 略過這項組態工作。</span><span class="sxs-lookup"><span data-stu-id="18f83-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="18f83-150">在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)。</span><span class="sxs-lookup"><span data-stu-id="18f83-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="18f83-151">透過 hello 公開您透過 LDAPS 存取的受管理的網域網際網路代表安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="18f83-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="18f83-152">hello 受管理的網域是從此 hello 連線到網際網路上使用安全 ldap 的 hello 通訊埠 （也就是連接埠 636）。</span><span class="sxs-lookup"><span data-stu-id="18f83-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="18f83-153">因此，您可以選擇 toorestrict 存取受管理的 toohello 網域 toospecific 已知的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18f83-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="18f83-154">為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已在此啟用 Azure AD 網域服務的 hello 子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="18f83-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="18f83-155">hello 下表說明您可以設定時，NSG toolock hello 透過安全 LDAP 存取範例網際網路。</span><span class="sxs-lookup"><span data-stu-id="18f83-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="18f83-156">hello NSG 包含一組規則，允許對內的 LDAPS 存取透過 TCP 連接埠 636 只能從一組指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="18f83-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="18f83-157">hello 預設 'DenyAll' 規則套用 tooall 其他輸入的流量的 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="18f83-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="18f83-158">hello NSG 規則 tooallow LDAPS 存取 hello 透過網際網路從指定的 IP 位址的優先順序高於 hello DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="18f83-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![透過範例 NSG toosecure LDAPS 存取 hello 網際網路](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="18f83-160">**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="18f83-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="18f83-161">相關內容</span><span class="sxs-lookup"><span data-stu-id="18f83-161">Related content</span></span>
* [<span data-ttu-id="18f83-162">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="18f83-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="18f83-163">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="18f83-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="18f83-164">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="18f83-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="18f83-165">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="18f83-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="18f83-166">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="18f83-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
