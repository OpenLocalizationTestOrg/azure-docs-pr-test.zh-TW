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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)

## <a name="before-you-begin"></a>開始之前
請確定您已完成[工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)。

選擇 toouse hello 預覽 Azure 入口網站體驗或 hello Azure 傳統入口網站 toocomplete 這項工作。
> [!div class="op_single_selector"]
> * **Azure 入口網站 （預覽）**:[啟用安全 LDAP 使用 hello Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Azure 傳統入口網站**:[啟用安全 LDAP 使用 hello 傳統 Azure 入口網站](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>工作 3-啟用安全 LDAP 的 hello 受管理的網域，使用 hello 傳統 Azure 入口網站
tooenable 安全 LDAP 資訊，請執行下列組態步驟的 hello:

1. 瀏覽 toohello  **[Azure 傳統入口網站](https://manage.windowsazure.com)**。
2. 選取 hello **Active Directory** hello 左窗格上的節點。
3. 選取 hello Azure AD 目錄 (也參考 tooas 'tenant')，您必須啟用 Azure AD 網域服務。

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. 按一下 hello**設定** 索引標籤。

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. 捲動 toohello 節**網域服務**。 您應該會看到標題為選項**安全 LDAP (LDAPS)** hello 下列螢幕擷取畫面所示：

    ![網域服務組態區段](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. 按一下 hello**設定憑證...** hello 向上按鈕 toobring**設定安全 LDAP 的憑證**對話方塊。

    ![設定安全 LDAP 的憑證](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. 按一下 hello 資料夾圖示下列**使用憑證 PFX 檔案**toospecify hello PFX 檔案，其中包含您想針對安全 LDAP 存取 toohello toouse hello 憑證管理網域。 也請輸入 hello 匯出 hello 憑證 toohello PFX 檔案時所指定的密碼。 然後，按一下 hello 完成 hello 下方的按鈕。

    ![指定安全 LDAP 的 PFX 檔案和密碼](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. hello**網域服務**區段 hello**設定**應該取得灰色 索引標籤，並在 hello**暫止...**狀態幾分鐘的時間。 在這段期間，hello LDAPS 憑證會經過驗證的精確度，並設定安全 LDAP 的受管理的網域。

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > 只需要大約 10 個 too15 分鐘 tooenable 安全 LDAP 的受管理的網域。 如果 hello 提供安全 LDAP 的憑證不符合 hello 所需的準則，您的目錄未啟用安全 LDAP，您看到失敗。 例如，hello 網域名稱不正確，hello 憑證已到期或即將過期。
   >
   >

9. 當受管理的網域已成功啟用安全 LDAP 時，hello**暫止...**訊息應該就會消失。 您應該會看到 hello 顯示 hello 憑證指紋。

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>工作 4-hello 透過啟用安全 LDAP 存取網際網路
**選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。

在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal)。

1. 您應該看到的選項太**啟用安全 LDAP 存取透過 hello 網際網路**在 hello**網域服務**區段 hello**設定**頁面。 此選項設定得**否**預設因為管理網際網路存取 toohello 透過安全 LDAP 的網域預設會停用。

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. 切換**啟用安全 LDAP 存取透過 hello 網際網路**太**是**。 按一下 hello**儲存**hello 下方面板上的按鈕。
    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. hello**網域服務**區段 hello**設定**應該取得灰色 索引標籤，並在 hello**暫止...**狀態幾分鐘的時間。 一段時間後，會啟用透過安全 LDAP 的網際網路存取 tooyour 受管理的網域。

    ![安全 LDAP - 擱置中狀態](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > 它需要大約 10 分鐘 tooenable 網際網路存取，透過安全 LDAP 的受管理的網域。
   >
   >
4. 已成功啟用網際網路的 hello 透過安全 LDAP 存取 tooyour 受管理的網域時, hello**暫止...**訊息應該就會消失。 您應該會看見 hello 外部 IP 位址，可以使用的 tooaccess hello 欄位中利用 ldaps 是您目錄**外部 IP 位址的 LDAPS 存取**。

    ![安全 LDAP 已啟用](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>工作 5-設定 DNS tooaccess hello 受管理的網域從 hello 網際網路
**選擇性的工作**-如果您不打算使用 LDAPS tooaccess hello 受管理的網域超過 hello 網際網路、 略過這項組態工作。

在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 4](#task-4---enable-secure-ldap-access-over-the-internet)。

透過啟用安全 LDAP 存取之後 hello 網際網路的受管理的網域中，您需要 tooupdate DNS，讓用戶端電腦可以找到此受管理的網域。 在工作 4 hello 結尾，外部 IP 位址會顯示在 hello**設定**索引標籤中**外部 IP 位址的 LDAPS 存取**。

設定外部的 DNS 提供者，讓該 hello DNS 名稱的 hello 管理網域 (例如，' ldaps.contoso100.com') 點 toothis 外部 IP 位址。 在本例中，我們需要 toocreate hello 下列 DNS 項目：

    ldaps.contoso100.com  -> 52.165.38.113

就這麼簡單： 現在您已經準備就緒 tooconnect toohello 受管理網域使用透過安全 LDAP hello 網際網路。

> [!WARNING]
> 請記住，用戶端電腦必須信任 hello LDAPS 憑證 toobe 無法 tooconnect hello 簽發者成功 toohello 管理使用 LDAPS 網域。 如果您使用企業憑證授權單位或公開受信任的憑證授權單位，您不需要 toodo 任何項目因為用戶端電腦會信任這些憑證簽發者。 如果您使用自我簽署的憑證，您需要 tooinstall hello 公開部分的 hello 自我簽署憑證到 hello hello 用戶端電腦上的受信任的憑證存放區。
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>鎖定 LDAPS 存取 tooyour 受管理的網域 hello 透過網際網路
> [!NOTE]
> **選擇性的工作**-如果您未啟用 LDAPS 存取 toohello 受管理的網域超過 hello 網際網路、 略過這項組態工作。
>
>

在開始這項工作之前，請確定您已完成 hello 中所述的步驟[工作 4](#task-4---enable-secure-ldap-access-over-the-internet)。

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
