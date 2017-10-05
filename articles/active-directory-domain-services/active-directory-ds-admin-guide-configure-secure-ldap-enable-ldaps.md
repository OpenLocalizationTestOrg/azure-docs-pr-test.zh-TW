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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)

## <a name="before-you-begin"></a>開始之前
確定您已完成[工作 2 - 將安全的 LDAP 憑證匯出到 .PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。

選擇要使用預覽 Azure 入口網站體驗或 Azure 傳統入口網站來完成這項工作。
> [!div class="op_single_selector"]
> * **Azure 入口網站 (預覽)**：[使用 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Azure 傳統入口網站**：[使用傳統 Azure 入口網站啟用安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a>工作 3 - 使用 Azure 入口網站 (預覽) 為受管理的網域啟用安全 LDAP
若要啟用安全的 LDAP，請執行下列設定步驟：

1. 瀏覽至 **Azure 入口網站[](https://portal.azure.com)**。

2. 在 [搜尋資源] 搜尋方塊中搜尋「網域服務」。 從搜尋結果選取 [Azure AD Domain Services]。 [Azure AD Domain Services] 刀鋒視窗會列出受管理的網域。

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. 按一下受管理的網域名稱 (例如，'contoso100.com')，以查看網域的詳細資料。

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. 按一下導覽窗格中的 [安全 LDAP]。

    ![Domain Services - 安全 LDAP 刀鋒視窗](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. 根據預設，已停用受管理的網域的安全 LDAP 存取。 將 [安全 LDAP] 切換至 [啟用]。

    ![啟用安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. 根據預設，已停用透過網際網路之受管理的網域的安全 LDAP 存取。 視需要將 [在網際網路上允許安全 LDAP 存取] 切換為 [啟用]。 

6. 按一下 [.PFX 檔案]\(具備安全 LDAP 的憑證\) 後面的資料夾圖示。 指定具備憑證之 PFX 檔案的路徑，對受管理的網域進行安全 LDAP 存取。

7. 指定 [用以解密 PFX 檔案的密碼]。 提供將憑證匯出到 PFX 檔案時所使用的相同密碼。

8. 完成時，請按一下 [儲存] 按鈕。

9. 您會看到通知，通知您安全 LDAP 已針對受管理的網域進行設定。 這項作業完成之前，您無法修改網域的其他設定。

    ![為受管理的網域設定安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> 為受管理的網域啟用安全 LDAP 需要約 10 到 15 分鐘的時間。 如果提供的安全 LDAP 憑證不符合所需的準則，則不會為您的目錄啟用安全 LDAP，而且您會看到失敗。 例如，網域名稱不正確、憑證已到期或即將到期等。 在此情況下，使用有效憑證重試。
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a>工作 4 - 設定 DNS 以從網際網路存取受管理的網域
> [!NOTE]
> **選擇性工作** - 如果您不打算使用 LDAPS 來透過網際網路存取受管理的網域，請略過這項設定工作。
>
>

開始這項工作之前，請先確定您已完成 [工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)中所述的步驟。

為受管理的網域啟用了透過網際網路的安全 LDAP 存取後，您需要更新 DNS 以便用戶端電腦可以找到此受管理網域。 在工作 3 的最後階段，[屬性] 索引標籤的 [LDAPS 存取的外部 IP 位址] 中會顯示外部 IP 位址。

請設定外部 DNS 提供者，讓受管理網域的 DNS 名稱 (例如 'ldaps.contoso100.com') 指向這個外部 IP 位址。 在我們的範例中，我們需要建立下列 DNS 項目︰

    ldaps.contoso100.com  -> 52.165.38.113

這樣就大功告成了。您現在已準備好可使用安全 LDAP 透過網際網路連線到受管理網域。

> [!WARNING]
> 請記住，用戶端電腦必須信任 LDAPS 憑證的簽發者，才能成功使用 LDAPS 連線到受管理網域。 如果您使用公開的受信任憑證授權單位，您不需要採取任何動作，因為用戶端電腦會信任這些憑證簽發者。 如果您使用自我簽署憑證，在用戶端電腦的受信任憑證存放區中安裝自我簽署憑證的公開部分。
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a>工作 5 - 鎖定透過網際網路對於受管理網域的安全 LDAP 存取
> [!NOTE]
> **選擇性工作** - 如果您尚未啟用透過網際網路對於受管理的網域之 LDAPS 存取，請略過這項設定工作。
>
>

開始這項工作之前，請先確定您已完成 [工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)中所述的步驟。

公開受管理的網域透過網際網路進行 LDAPS 存取，代表著安全性威脅。 受管理的網域可以從用於安全 LDAP 之通訊埠的網際網路 (也就是連接埠 636) 存取。 因此，您可以選擇將受管理的網域存取限制為特定已知 IP 位址。 為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已啟用 Azure AD Domain Services 的子網路產生關聯。

下表說明您可以設定的範例 NSG，以鎖定透過網際網路的安全 LDAP 存取。 NSG 包含一組規則，允許僅從一組指定 IP 位址透過 TCP 連接埠 636 的輸入 LDAPS 存取。 預設 'DenyAll' 規則適用於來自網際網路的所有其他輸入流量。 允許從指定的 IP 位址透過網際網路之 LDAPS 存取的 NSG 規則，其優先順序高於 DenyAll NSG 規則。

![透過網際網路之安全 LDAP 存取的範例 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。

<br>

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [管理 Azure AD Domain Services 受管理網域上的群組原則](active-directory-ds-admin-guide-administer-group-policy.md)
* [網路安全性群組](../virtual-network/virtual-networks-nsg.md)
* [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
