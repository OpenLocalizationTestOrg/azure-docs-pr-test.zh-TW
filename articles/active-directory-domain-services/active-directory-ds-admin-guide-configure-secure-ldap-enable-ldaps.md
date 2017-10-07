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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)

## <a name="before-you-begin"></a>開始之前
請確定您已完成[工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。

選擇 toouse hello 預覽 Azure 入口網站體驗或 hello Azure 傳統入口網站 toocomplete 這項工作。
> [!div class="op_single_selector"]
> * **Azure 入口網站 （預覽）**:[啟用安全 LDAP 使用 hello Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Azure 傳統入口網站**:[啟用安全 LDAP 使用 hello 傳統 Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>工作 3-啟用安全 LDAP 的 hello 受管理的網域，使用 hello Azure 入口網站 （預覽）
tooenable 安全 LDAP 資訊，請執行下列組態步驟的 hello:

1. 瀏覽 toohello  **[Azure 入口網站](https://portal.azure.com)**。

2. 搜尋 ' 網域中的服務' hello**搜尋資源**搜尋 方塊。 選取**Azure AD 網域服務**從 hello 搜尋結果。 hello **Azure AD 網域服務**刀鋒視窗會列出受管理的網域。

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. 按一下 hello 受管理網域 (例如，' contoso100.com') toosee hello 名稱 hello 定義域有關的更多詳細資料。

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. 按一下**安全 LDAP** hello 瀏覽窗格中。

    ![Domain Services - 安全 LDAP 刀鋒視窗](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. 根據預設，會停用安全 LDAP 存取 tooyour 受管理的網域。 切換**安全 LDAP**太**啟用**。

    ![啟用安全 LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. 根據預設，安全 LDAP 存取 tooyour 可以透過網際網路已停用的 hello 管理網域。 切換**允許安全 LDAP 存取透過 hello 網際網路**太**啟用**視。 

6. 按一下 hello 資料夾圖示下列**。使用安全 LDAP 的憑證的 PFX 檔案**。 指定安全 LDAP 存取 toohello 受管理的網域的 hello 憑證 hello 路徑 toohello PFX 檔案。

7. 指定 hello**密碼 toodecrypt。PFX 檔案**。 提供 hello 匯出 hello 憑證 toohello PFX 檔案時所使用的相同密碼。

8. 當您完成之後時，按一下 [hello**儲存**] 按鈕。

9. 您會看到通知，通知您正在設定安全 LDAP 的 hello 受管理的網域。 這項作業完成之前，您無法修改 hello 網域的其他設定。

    ![設定安全 LDAP 的 hello 受管理的網域](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> 只需要大約 10 個 too15 分鐘 tooenable 安全 LDAP 的受管理的網域。 如果 hello 提供安全 LDAP 的憑證不符合 hello 所需的準則，您的目錄未啟用安全 LDAP，您看到失敗。 例如，hello 網域名稱不正確，hello 憑證已到期或即將過期。 在此情況下，使用有效憑證重試。
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>工作 4-設定 DNS tooaccess hello 受管理的網域從 hello 網際網路
> [!NOTE]
> **選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。
>
>

在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)。

透過啟用安全 LDAP 存取之後 hello 網際網路的受管理的網域中，您需要 tooupdate DNS，讓用戶端電腦可以找到此受管理的網域。 在工作 3 hello 結尾，外部 IP 位址會顯示在 hello**屬性**刀鋒視窗中的**外部 IP 位址的 LDAPS 存取**。

設定外部的 DNS 提供者，讓該 hello DNS 名稱的 hello 管理網域 (例如，' ldaps.contoso100.com') 點 toothis 外部 IP 位址。 在本例中，我們需要 toocreate hello 下列 DNS 項目：

    ldaps.contoso100.com  -> 52.165.38.113

就這麼簡單： 現在您已經準備就緒 tooconnect toohello 受管理網域使用透過安全 LDAP hello 網際網路。

> [!WARNING]
> 請記住，用戶端電腦必須信任 hello LDAPS 憑證 toobe 無法 tooconnect hello 簽發者成功 toohello 管理使用 LDAPS 網域。 如果您使用公開受信任的憑證授權單位，您不需要 toodo 任何項目因為用戶端電腦會信任這些憑證簽發者。 如果您使用自我簽署的憑證，請到 hello hello 用戶端電腦上的受信任的憑證存放區安裝 hello hello 自我簽署憑證的公開部分。
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>工作 5-鎖定 LDAPS 存取受管理的 tooyour 透過網域 hello 網際網路
> [!NOTE]
> **選擇性的工作**-如果您未啟用 LDAPS 存取 toohello 受管理的網域超過 hello 網際網路、 略過這項組態工作。
>
>

在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)。

透過 hello 公開您透過 LDAPS 存取的受管理的網域網際網路代表安全性威脅。 hello 受管理的網域是從此 hello 連線到網際網路上使用安全 ldap 的 hello 通訊埠 （也就是連接埠 636）。 因此，您可以選擇 toorestrict 存取受管理的 toohello 網域 toospecific 已知的 IP 位址。 為了提升安全性，建立網路安全性群組 (NSG)，並將它與您已在此啟用 Azure AD 網域服務的 hello 子網路產生關聯。

hello 下表說明您可以設定時，NSG toolock hello 透過安全 LDAP 存取範例網際網路。 hello NSG 包含一組規則，允許對內的 LDAPS 存取透過 TCP 連接埠 636 只能從一組指定的 IP 位址。 hello 預設 'DenyAll' 規則套用 tooall 其他輸入的流量的 hello 網際網路。 hello NSG 規則 tooallow LDAPS 存取 hello 透過網際網路從指定的 IP 位址的優先順序高於 hello DenyAll NSG 規則。

![透過範例 NSG toosecure LDAPS 存取 hello 網際網路](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**詳細資訊** - [網路安全性群組](../virtual-network/virtual-networks-nsg.md)。

<br>

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [管理 Azure AD Domain Services 受管理網域上的群組原則](active-directory-ds-admin-guide-administer-group-policy.md)
* [網路安全性群組](../virtual-network/virtual-networks-nsg.md)
* [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
