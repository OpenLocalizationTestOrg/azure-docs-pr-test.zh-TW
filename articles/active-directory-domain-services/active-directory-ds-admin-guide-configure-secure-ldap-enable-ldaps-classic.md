---
title: "aaaConfigure 安全 LDAP (LDAPS) 在 Azure AD 網域服務中 |Microsoft 文件"
description: "針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="3d02d-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="3d02d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3d02d-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="3d02d-104">Before you begin</span></span>
<span data-ttu-id="3d02d-105">請確定您已完成[工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。</span><span class="sxs-lookup"><span data-stu-id="3d02d-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="3d02d-106">選擇 toouse hello 預覽 Azure 入口網站體驗或 hello Azure 傳統入口網站 toocomplete 這項工作。</span><span class="sxs-lookup"><span data-stu-id="3d02d-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3d02d-107">**Azure 入口網站 （預覽）**:[啟用安全 LDAP 使用 hello Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="3d02d-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="3d02d-108">**Azure 傳統入口網站**:[啟用安全 LDAP 使用 hello 傳統 Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="3d02d-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="3d02d-109">工作 3-啟用安全 LDAP 的 hello 受管理的網域，使用 hello 傳統 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3d02d-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="3d02d-110">tooenable 安全 LDAP 資訊，請執行下列組態步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3d02d-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="3d02d-111">瀏覽 toohello  **[Azure 傳統入口網站](https://manage.windowsazure.com)**。</span><span class="sxs-lookup"><span data-stu-id="3d02d-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="3d02d-112">選取 hello **Active Directory** hello 左窗格上的節點。</span><span class="sxs-lookup"><span data-stu-id="3d02d-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="3d02d-113">選取 hello Azure AD 目錄 (也參考 tooas 'tenant')，您必須啟用 Azure AD 網域服務。</span><span class="sxs-lookup"><span data-stu-id="3d02d-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="3d02d-115">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3d02d-115">Click hello **Configure** tab.</span></span>

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="3d02d-117">捲動 toohello 節**網域服務**。</span><span class="sxs-lookup"><span data-stu-id="3d02d-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="3d02d-118">您應該會看到標題為選項**安全 LDAP (LDAPS)** hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="3d02d-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![網域服務組態區段](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="3d02d-120">按一下 hello**設定憑證...** hello 向上按鈕 toobring**設定安全 LDAP 的憑證**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3d02d-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![設定安全 LDAP 的憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="3d02d-122">按一下 hello 資料夾圖示下列**使用憑證 PFX 檔案**toospecify hello PFX 檔案，其中包含您想針對安全 LDAP 存取 toohello toouse hello 憑證管理網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="3d02d-123">也請輸入 hello 匯出 hello 憑證 toohello PFX 檔案時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="3d02d-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="3d02d-124">然後，按一下 hello 完成 hello 下方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d02d-124">Then, click hello done button on hello bottom.</span></span>

    ![指定安全 LDAP 的 PFX 檔案和密碼](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="3d02d-126">hello**網域服務**區段 hello**設定**應該取得灰色 索引標籤，並在 hello**暫止...**狀態幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="3d02d-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="3d02d-127">在這段期間，hello LDAPS 憑證會經過驗證的精確度，並設定安全 LDAP 的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="3d02d-129">只需要大約 10 個 too15 分鐘 tooenable 安全 LDAP 的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="3d02d-130">如果 hello 提供安全 LDAP 的憑證不符合 hello 所需的準則，您的目錄未啟用安全 LDAP，您看到失敗。</span><span class="sxs-lookup"><span data-stu-id="3d02d-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="3d02d-131">例如，hello 網域名稱不正確，hello 憑證已到期或即將過期。</span><span class="sxs-lookup"><span data-stu-id="3d02d-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="3d02d-132">當受管理的網域已成功啟用安全 LDAP 時，hello**暫止...**訊息應該就會消失。</span><span class="sxs-lookup"><span data-stu-id="3d02d-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="3d02d-133">您應該會看到 hello 顯示 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="3d02d-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="3d02d-135">工作 4-hello 透過啟用安全 LDAP 存取網際網路</span><span class="sxs-lookup"><span data-stu-id="3d02d-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="3d02d-136">**選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。</span><span class="sxs-lookup"><span data-stu-id="3d02d-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="3d02d-137">在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="3d02d-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="3d02d-138">您應該看到的選項太**啟用安全 LDAP 存取透過 hello 網際網路**在 hello**網域服務**區段 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="3d02d-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="3d02d-139">此選項設定得**否**預設因為管理網際網路存取 toohello 透過安全 LDAP 的網域預設會停用。</span><span class="sxs-lookup"><span data-stu-id="3d02d-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="3d02d-141">切換**啟用安全 LDAP 存取透過 hello 網際網路**太**是**。</span><span class="sxs-lookup"><span data-stu-id="3d02d-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="3d02d-142">按一下 hello**儲存**hello 下方面板上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3d02d-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="3d02d-143">![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="3d02d-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="3d02d-144">hello**網域服務**區段 hello**設定**應該取得灰色 索引標籤，並在 hello**暫止...**狀態幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="3d02d-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="3d02d-145">一段時間後，會啟用透過安全 LDAP 的網際網路存取 tooyour 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="3d02d-147">它需要大約 10 分鐘 tooenable 網際網路存取，透過安全 LDAP 的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="3d02d-148">已成功啟用網際網路的 hello 透過安全 LDAP 存取 tooyour 受管理的網域時, hello**暫止...**訊息應該就會消失。</span><span class="sxs-lookup"><span data-stu-id="3d02d-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="3d02d-149">您應該會看見 hello 外部 IP 位址，可以使用的 tooaccess hello 欄位中利用 ldaps 是您目錄**外部 IP 位址的 LDAPS 存取**。</span><span class="sxs-lookup"><span data-stu-id="3d02d-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="3d02d-151">工作 5-設定 DNS tooaccess hello 受管理的網域從 hello 網際網路</span><span class="sxs-lookup"><span data-stu-id="3d02d-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="3d02d-152">**選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。</span><span class="sxs-lookup"><span data-stu-id="3d02d-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="3d02d-153">在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 4](#task-4---enable-secure-ldap-access-over-the-internet)。</span><span class="sxs-lookup"><span data-stu-id="3d02d-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="3d02d-154">透過啟用安全 LDAP 存取之後 hello 網際網路的受管理的網域中，您需要 tooupdate DNS，讓用戶端電腦可以找到此受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="3d02d-155">在工作 4 hello 結尾，外部 IP 位址會顯示在 hello**設定**索引標籤中**外部 IP 位址的 LDAPS 存取**。</span><span class="sxs-lookup"><span data-stu-id="3d02d-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="3d02d-156">設定外部的 DNS 提供者，讓該 hello DNS 名稱的 hello 管理網域 (例如，' ldaps.contoso100.com') 點 toothis 外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3d02d-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="3d02d-157">在本例中，我們需要 toocreate hello 下列 DNS 項目：</span><span class="sxs-lookup"><span data-stu-id="3d02d-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="3d02d-158">就這麼簡單： 現在您已經準備就緒 tooconnect toohello 受管理網域使用透過安全 LDAP hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="3d02d-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="3d02d-159">請記住，用戶端電腦必須信任 hello LDAPS 憑證 toobe 無法 tooconnect hello 簽發者成功 toohello 管理使用 LDAPS 網域。</span><span class="sxs-lookup"><span data-stu-id="3d02d-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="3d02d-160">如果您使用企業憑證授權單位或公開受信任的憑證授權單位，您不需要 toodo 任何項目因為用戶端電腦會信任這些憑證簽發者。</span><span class="sxs-lookup"><span data-stu-id="3d02d-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="3d02d-161">如果您使用自我簽署的憑證，您需要 tooinstall hello 公開部分的 hello 自我簽署憑證到 hello hello 用戶端電腦上的受信任的憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="3d02d-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="3d02d-162">鎖定 LDAPS 存取 tooyour 受管理的網域 hello 透過網際網路</span><span class="sxs-lookup"><span data-stu-id="3d02d-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="3d02d-163">**選擇性的工作**-如果您未啟用 LDAPS 存取 toohello 受管理的網域超過 hello 網際網路、 略過這項組態工作。</span><span class="sxs-lookup"><span data-stu-id="3d02d-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="3d02d-164">在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 4](#task-4---enable-secure-ldap-access-over-the-internet)。</span><span class="sxs-lookup"><span data-stu-id="3d02d-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="3d02d-165">透過 hello 公開您透過 LDAPS 存取的受管理的網域網際網路代表安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="3d02d-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="3d02d-166">hello 受管理的網域是從此 hello 連線到網際網路上使用安全 ldap 的 hello 通訊埠 （也就是連接埠 636）。</span><span class="sxs-lookup"><span data-stu-id="3d02d-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="3d02d-167">因此，您可以選擇 toorestrict 存取受管理的 toohello 網域 toospecific 已知的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3d02d-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="3d02d-168">為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已在此啟用 Azure AD 網域服務的 hello 子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="3d02d-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="3d02d-169">hello 下表說明您可以設定時，NSG toolock hello 透過安全 LDAP 存取範例網際網路。</span><span class="sxs-lookup"><span data-stu-id="3d02d-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="3d02d-170">hello NSG 包含一組規則，允許對內的 LDAPS 存取透過 TCP 連接埠 636 只能從一組指定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3d02d-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="3d02d-171">hello 預設 'DenyAll' 規則套用 tooall 其他輸入的流量的 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="3d02d-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="3d02d-172">hello NSG 規則 tooallow LDAPS 存取 hello 透過網際網路從指定的 IP 位址的優先順序高於 hello DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="3d02d-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![透過範例 NSG toosecure LDAPS 存取 hello 網際網路](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="3d02d-174">**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="3d02d-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="3d02d-175">相關內容</span><span class="sxs-lookup"><span data-stu-id="3d02d-175">Related content</span></span>
* [<span data-ttu-id="3d02d-176">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="3d02d-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="3d02d-177">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="3d02d-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="3d02d-178">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="3d02d-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="3d02d-179">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="3d02d-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="3d02d-180">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="3d02d-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
