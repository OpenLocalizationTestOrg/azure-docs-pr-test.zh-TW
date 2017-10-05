---
title: "在 Azure AD Domain Services 中設定安全的 LDAP (LDAPS) | Microsoft Docs"
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
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="9e9ce-103">針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)</span><span class="sxs-lookup"><span data-stu-id="9e9ce-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e9ce-104">開始之前</span><span class="sxs-lookup"><span data-stu-id="9e9ce-104">Before you begin</span></span>
<span data-ttu-id="9e9ce-105">確定您已完成[工作 2 - 將安全的 LDAP 憑證匯出到 .PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="9e9ce-106">選擇要使用預覽 Azure 入口網站體驗或 Azure 傳統入口網站來完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9e9ce-107">**Azure 入口網站 (預覽)**：[使用 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="9e9ce-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="9e9ce-108">**Azure 傳統入口網站**：[使用傳統 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="9e9ce-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="9e9ce-109">工作 3 - 使用 Azure 入口網站 (預覽) 為受管理的網域啟用安全 LDAP</span><span class="sxs-lookup"><span data-stu-id="9e9ce-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="9e9ce-110">若要啟用安全的 LDAP，請執行下列設定步驟：</span><span class="sxs-lookup"><span data-stu-id="9e9ce-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="9e9ce-111">瀏覽至 **Azure 入口網站[](https://portal.azure.com)**。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="9e9ce-112">在 [搜尋資源] 搜尋方塊中搜尋「網域服務」。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="9e9ce-113">從搜尋結果選取 [Azure AD Domain Services]。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="9e9ce-114">[Azure AD Domain Services] 刀鋒視窗會列出受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="9e9ce-116">按一下受管理的網域名稱 (例如，'contoso100.com')，以查看網域的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="9e9ce-118">按一下導覽窗格中的 [安全 LDAP]。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Domain Services - 安全 LDAP 刀鋒視窗](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="9e9ce-120">根據預設，已停用受管理的網域的安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="9e9ce-121">將 [安全 LDAP] 切換至 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![啟用安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="9e9ce-123">根據預設，已停用透過網際網路之受管理的網域的安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="9e9ce-124">視需要將 [在網際網路上允許安全 LDAP 存取] 切換為 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="9e9ce-125">按一下 [.PFX 檔案]\(具備安全 LDAP 的憑證\) 後面的資料夾圖示。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="9e9ce-126">指定具備憑證之 PFX 檔案的路徑，對受管理的網域進行安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="9e9ce-127">指定 [用以解密 PFX 檔案的密碼]。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="9e9ce-128">提供將憑證匯出到 PFX 檔案時所使用的相同密碼。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="9e9ce-129">完成時，請按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="9e9ce-130">您會看到通知，通知您安全 LDAP 已針對受管理的網域進行設定。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="9e9ce-131">這項作業完成之前，您無法修改網域的其他設定。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![為受管理的網域設定安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="9e9ce-133">為受管理的網域啟用安全 LDAP 需要約 10 到 15 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="9e9ce-134">如果提供的安全 LDAP 憑證不符合所需的準則，則不會為您的目錄啟用安全 LDAP，而且您會看到失敗。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="9e9ce-135">例如，網域名稱不正確、憑證已到期或即將到期等。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="9e9ce-136">在此情況下，使用有效憑證重試。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="9e9ce-137">工作 4 - 設定 DNS 以從網際網路存取受管理的網域</span><span class="sxs-lookup"><span data-stu-id="9e9ce-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="9e9ce-138">**選擇性工作** - 如果您不打算使用 LDAPS 來透過網際網路存取受管理的網域，請略過這項設定工作。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="9e9ce-139">開始這項工作之前，請先確定您已完成 [工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="9e9ce-140">為受管理的網域啟用了透過網際網路的安全 LDAP 存取後，您需要更新 DNS 以便用戶端電腦可以找到此受管理網域。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="9e9ce-141">在工作 3 的最後階段，[屬性] 索引標籤的 [LDAPS 存取的外部 IP 位址] 中會顯示外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="9e9ce-142">請設定外部 DNS 提供者，讓受管理網域的 DNS 名稱 (例如 'ldaps.contoso100.com') 指向這個外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="9e9ce-143">在我們的範例中，我們需要建立下列 DNS 項目︰</span><span class="sxs-lookup"><span data-stu-id="9e9ce-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="9e9ce-144">這樣就大功告成了。您現在已準備好可使用安全 LDAP 透過網際網路連線到受管理網域。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="9e9ce-145">請記住，用戶端電腦必須信任 LDAPS 憑證的簽發者，才能成功使用 LDAPS 連線到受管理網域。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="9e9ce-146">如果您使用公開的受信任憑證授權單位，您不需要採取任何動作，因為用戶端電腦會信任這些憑證簽發者。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="9e9ce-147">如果您使用自我簽署憑證，在用戶端電腦的受信任憑證存放區中安裝自我簽署憑證的公開部分。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="9e9ce-148">工作 5 - 鎖定透過網際網路對於受管理網域的安全 LDAP 存取</span><span class="sxs-lookup"><span data-stu-id="9e9ce-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="9e9ce-149">**選擇性工作** - 如果您尚未啟用透過網際網路對於受管理的網域之 LDAPS 存取，請略過這項設定工作。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="9e9ce-150">開始這項工作之前，請先確定您已完成 [工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="9e9ce-151">公開受管理的網域透過網際網路進行 LDAPS 存取，代表著安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="9e9ce-152">受管理的網域可以從用於安全 LDAP 之通訊埠的網際網路 (也就是連接埠 636) 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="9e9ce-153">因此，您可以選擇將受管理的網域存取限制為特定已知 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="9e9ce-154">為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已啟用 Azure AD Domain Services 的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="9e9ce-155">下表說明您可以設定的範例 NSG，以鎖定透過網際網路的安全 LDAP 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="9e9ce-156">NSG 包含一組規則，允許僅從一組指定 IP 位址透過 TCP 連接埠 636 的輸入 LDAPS 存取。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="9e9ce-157">預設 'DenyAll' 規則適用於來自網際網路的所有其他輸入流量。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="9e9ce-158">允許從指定的 IP 位址透過網際網路之 LDAPS 存取的 NSG 規則，其優先順序高於 DenyAll NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![透過網際網路之安全 LDAP 存取的範例 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="9e9ce-160">**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ce-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="9e9ce-161">相關內容</span><span class="sxs-lookup"><span data-stu-id="9e9ce-161">Related content</span></span>
* [<span data-ttu-id="9e9ce-162">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="9e9ce-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="9e9ce-163">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="9e9ce-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="9e9ce-164">管理 Azure AD Domain Services 受管理網域上的群組原則</span><span class="sxs-lookup"><span data-stu-id="9e9ce-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="9e9ce-165">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="9e9ce-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="9e9ce-166">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="9e9ce-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
