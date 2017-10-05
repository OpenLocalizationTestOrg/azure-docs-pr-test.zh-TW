---
title: "在 Azure AD Domain Services 中設定安全的 LDAP (LDAPS) | Microsoft Docs"
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
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="498fb-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="498fb-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="498fb-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="498fb-104">Before you begin</span></span>
<span data-ttu-id="498fb-105">確定您已完成[工作 2 - 將安全的 LDAP 憑證匯出到 .PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。</span><span class="sxs-lookup"><span data-stu-id="498fb-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="498fb-106">選擇要使用預覽 Azure 入口網站體驗或 Azure 傳統入口網站來完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="498fb-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="498fb-107">**Azure 入口網站 (預覽)**：[使用 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="498fb-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="498fb-108">**Azure 傳統入口網站**：[使用傳統 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="498fb-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="498fb-109">工作 3 - 使用傳統 Azure 入口網站為受管理的網域啟用安全 LDAP</span><span class="sxs-lookup"><span data-stu-id="498fb-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="498fb-110">若要啟用安全的 LDAP，請執行下列設定步驟：</span><span class="sxs-lookup"><span data-stu-id="498fb-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="498fb-111">瀏覽至 **[Azure 傳統入口網站](https://manage.windowsazure.com)**。</span><span class="sxs-lookup"><span data-stu-id="498fb-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="498fb-112">在左窗格中，選取 [Active Directory]  節點。</span><span class="sxs-lookup"><span data-stu-id="498fb-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="498fb-113">選取已啟用 Azure AD 網域服務的 Azure AD 目錄 (也稱為「租用戶」)。</span><span class="sxs-lookup"><span data-stu-id="498fb-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="498fb-115">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="498fb-115">Click the **Configure** tab.</span></span>

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="498fb-117">向下捲動到標題為 [網域服務] 的區段。</span><span class="sxs-lookup"><span data-stu-id="498fb-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="498fb-118">您應該會看到標題為 [安全 LDAP (LDAPS)]  的選項，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="498fb-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![網域服務組態區段](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="498fb-120">按一下 [設定憑證...] 按鈕以顯示 [設定安全 LDAP 的憑證] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="498fb-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![設定安全 LDAP 的憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="498fb-122">按一下 [含有憑證的 PFX 檔案] 後面的資料夾圖示，指定要用於對受管理網域進行安全 LDAP 存取之憑證所在的 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="498fb-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="498fb-123">此外，也請輸入將憑證匯出到 PFX 檔案時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="498fb-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="498fb-124">然後，按一下底部的完成按鈕。</span><span class="sxs-lookup"><span data-stu-id="498fb-124">Then, click the done button on the bottom.</span></span>

    ![指定安全 LDAP 的 PFX 檔案和密碼](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="498fb-126">[設定] 索引標籤的 [網域服務] 區段應該會變成灰色，而且有幾分鐘的時間處在 [擱置...] 狀態。</span><span class="sxs-lookup"><span data-stu-id="498fb-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="498fb-127">在此期間，LDAPS 憑證會進行驗證以確認是否正確，並為受管理的網域設定安全 LDAP。</span><span class="sxs-lookup"><span data-stu-id="498fb-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="498fb-129">為受管理的網域啟用安全 LDAP 需要約 10 到 15 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="498fb-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="498fb-130">如果提供的安全 LDAP 憑證不符合所需的準則，則不會為您的目錄啟用安全 LDAP，而且您會看到失敗。</span><span class="sxs-lookup"><span data-stu-id="498fb-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="498fb-131">例如，網域名稱不正確、憑證已到期或即將到期等。</span><span class="sxs-lookup"><span data-stu-id="498fb-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="498fb-132">在為受管理的網域成功啟用安全 LDAP 後，[擱置...]  訊息應該會消失。</span><span class="sxs-lookup"><span data-stu-id="498fb-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="498fb-133">您應該會看到已顯示憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="498fb-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="498fb-135">工作 4 - 透過網際網路啟用安全 LDAP 存取</span><span class="sxs-lookup"><span data-stu-id="498fb-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="498fb-136">**選擇性工作** - 如果您不打算使用 LDAPS 來透過網際網路存取受管理的網域，請略過這項設定工作。</span><span class="sxs-lookup"><span data-stu-id="498fb-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="498fb-137">開始這項工作之前，請先確定您已完成 [工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="498fb-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="498fb-138">您應該會在 [設定] 頁面的 [網域服務] 區段中看到 [透過網際網路啟用安全 LDAP 存取] 的選項。</span><span class="sxs-lookup"><span data-stu-id="498fb-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="498fb-139">此選項會設定為 [否]  ，因為依預設會停用透過安全 LDAP 對受管理網域的網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="498fb-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="498fb-141">將 [透過網際網路啟用安全 LDAP 存取] 切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="498fb-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="498fb-142">按一下底部面板上的 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="498fb-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="498fb-143">![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="498fb-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="498fb-144">[設定] 索引標籤的 [網域服務] 區段應該會變成灰色，而且有幾分鐘的時間處在 [擱置...] 狀態。</span><span class="sxs-lookup"><span data-stu-id="498fb-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="498fb-145">稍後會啟用透過安全 LDAP 對受管理網域的網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="498fb-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="498fb-147">為受管理網域啟用透過安全 LDAP 的網際網路存取需要約 10 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="498fb-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="498fb-148">在成功啟用透過網際網路對受管理網域進行安全 LDAP 存取後，[擱置...]  訊息應該會消失。</span><span class="sxs-lookup"><span data-stu-id="498fb-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="498fb-149">您應該會在 [LDAPS 存取的外部 IP 位址] 欄位中，看到可用來透過 LDAPS 存取您目錄的外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="498fb-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="498fb-151">工作 5 - 設定 DNS 以從網際網路存取受管理的網域</span><span class="sxs-lookup"><span data-stu-id="498fb-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="498fb-152">**選擇性工作** - 如果您不打算使用 LDAPS 來透過網際網路存取受管理的網域，請略過這項設定工作。</span><span class="sxs-lookup"><span data-stu-id="498fb-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="498fb-153">開始這項工作之前，請先確定您已完成 [工作 4](#task-4---enable-secure-ldap-access-over-the-internet)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="498fb-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="498fb-154">為受管理的網域啟用了透過網際網路的安全 LDAP 存取後，您需要更新 DNS 以便用戶端電腦可以找到此受管理網域。</span><span class="sxs-lookup"><span data-stu-id="498fb-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="498fb-155">在工作 4 的最後階段，[設定] 索引標籤的 [LDAPS 存取的外部 IP 位址] 中會顯示外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="498fb-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="498fb-156">請設定外部 DNS 提供者，讓受管理網域的 DNS 名稱 (例如 'ldaps.contoso100.com') 指向這個外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="498fb-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="498fb-157">在我們的範例中，我們需要建立下列 DNS 項目︰</span><span class="sxs-lookup"><span data-stu-id="498fb-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="498fb-158">這樣就大功告成了。您現在已準備好可使用安全 LDAP 透過網際網路連線到受管理網域。</span><span class="sxs-lookup"><span data-stu-id="498fb-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="498fb-159">請記住，用戶端電腦必須信任 LDAPS 憑證的簽發者，才能成功使用 LDAPS 連線到受管理網域。</span><span class="sxs-lookup"><span data-stu-id="498fb-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="498fb-160">如果您使用企業憑證授權單位或公開的受信任憑證授權單位，您不需要採取任何動作，因為用戶端電腦會信任這些憑證簽發者。</span><span class="sxs-lookup"><span data-stu-id="498fb-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="498fb-161">如果您使用自我簽署憑證，則必須在用戶端電腦的受信任憑證存放區中安裝自我簽署憑證的公開部分。</span><span class="sxs-lookup"><span data-stu-id="498fb-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="498fb-162">鎖定透過網際網路對於受管理網域的安全 LDAP 存取</span><span class="sxs-lookup"><span data-stu-id="498fb-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="498fb-163">**選擇性工作** - 如果您尚未啟用透過網際網路對於受管理的網域之 LDAPS 存取，請略過這項設定工作。</span><span class="sxs-lookup"><span data-stu-id="498fb-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="498fb-164">開始這項工作之前，請先確定您已完成 [工作 4](#task-4---enable-secure-ldap-access-over-the-internet)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="498fb-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="498fb-165">公開受管理的網域透過網際網路進行 LDAPS 存取，代表著安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="498fb-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="498fb-166">受管理的網域可以從用於安全 LDAP 之通訊埠的網際網路 (也就是連接埠 636) 存取。</span><span class="sxs-lookup"><span data-stu-id="498fb-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="498fb-167">因此，您可以選擇將受管理的網域存取限制為特定已知 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="498fb-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="498fb-168">為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已啟用 Azure AD Domain Services 的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="498fb-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="498fb-169">下表說明您可以設定的範例 NSG，以鎖定透過網際網路的安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="498fb-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="498fb-170">NSG 包含一組規則，允許僅從一組指定 IP 位址透過 TCP 連接埠 636 的輸入 LDAPS 存取。</span><span class="sxs-lookup"><span data-stu-id="498fb-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="498fb-171">預設 'DenyAll' 規則適用於來自網際網路的所有其他輸入流量。</span><span class="sxs-lookup"><span data-stu-id="498fb-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="498fb-172">允許從指定的 IP 位址透過網際網路之 LDAPS 存取的 NSG 規則，其優先順序高於 DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="498fb-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![透過網際網路之安全 LDAP 存取的範例 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="498fb-174">**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="498fb-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="498fb-175">相關內容</span><span class="sxs-lookup"><span data-stu-id="498fb-175">Related content</span></span>
* [<span data-ttu-id="498fb-176">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="498fb-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="498fb-177">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="498fb-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="498fb-178">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="498fb-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="498fb-179">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="498fb-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="498fb-180">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="498fb-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
