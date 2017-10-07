---
title: "Azure Active Directory Domain Services：管理指南 | Microsoft Docs"
description: "在 Azure AD 網域服務受管理的網域上建立組織單位 (OU)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>在 Azure AD 網域服務的受管理網域上建立組織單位 (OU)
Azure AD 網域服務的受管理網域包含兩個內建的容器，分別稱為「AADDC 電腦」和「AADDC 使用者」。 hello AADDC 電腦容器有電腦物件的所有電腦的加入 toohello 受管理的網域。 hello ' AADDC 使用者 容器包含使用者和群組 hello Azure AD 租用戶中。 有時候，您可能需要 toocreate hello 受管理網域 toodeploy 工作負載的服務帳戶。 基於此目的，您可以在 hello 受管理的網域上建立自訂組織單位 (OU)，並建立該 OU 中的服務帳戶。 本文章將示範如何在受管理的網域 OU toocreate。

## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。
4. 已加入網域的虛擬機器，您用來管理 hello Azure AD 網域服務受管理網域。 如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。
5. 您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，toocreate 受管理的網域上的自訂 OU 中。

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>在已加入網域的虛擬機器上安裝 AD 系統管理工具進行遠端管理
可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。 租用戶系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。 tooadminister hello 受管理的網域，虛擬機器聯結的 toohello 受管理的網域上安裝 hello AD 系統管理工具功能。 Toohello 文章的標題，請參閱[管理 Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-administer-domain.md)如需相關指示。

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>在 hello 受管理的網域上建立組織單位
既然 hello AD 系統管理工具安裝在 hello 已加入網域的虛擬機器，我們可以使用這些工具 toocreate 組織單位 hello 受管理網域上。 執行下列步驟的 hello:

> [!NOTE]
> 只有 hello ' AAD DC Administrators' 群組的成員有自訂的 OU hello toocreate 必要權限。 請確定您執行下列步驟以使用者所屬群組 toothis hello。
>
>

1. 從 hello 開始畫面上，按一下 **系統管理工具**。 您應該會看到 hello AD hello 虛擬機器上安裝的系統管理工具。

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. 按一下 [Active Directory 管理中心] 。

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello 網域中，按一下 hello hello 左窗格 (例如，' contoso100.com') 中的網域名稱。

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Hello 右側**工作** 窗格中，按一下 **新增**hello 網域名稱 節點下。 此範例中，按一下**新增**hello 右側 hello 'contoso100(local)' 節點下**工作**窗格。

    ![ADAC - 新的 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. 您應該會看到 hello 選項 toocreate 組織單位。 按一下**組織單位**toolaunch hello**建立組織單位**對話方塊。
6. 在 [hello**建立組織單位**] 對話方塊中，指定**名稱**的 hello 新 OU。 提供 hello OU 的簡短描述。 您可能也會設定 hello**管理者**hello OU 的欄位。 toocreate hello 自訂 OU 中，按一下**確定**。

    ![ADAC - 建立 OU 對話方塊](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. 新建立的 OU 的 hello 現在應該會出現在 hello AD 管理中心 (ADAC) 中。

    ![ADAC - OU 已建立](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>新建 OU 的權限/安全性
根據預設，hello （hello ' AAD DC Administrators' 群組的成員） 建立使用者自訂的 OU 會授與系統管理權限 （完全控制） 透過 hello hello OU。 hello 使用者可以繼續進行，並授與權限 tooother 使用者或視需要的 toohello ' AAD DC Administrators' 群組。 Hello 下列螢幕擷取畫面所示，hello 使用者 'bob@domainservicespreview.onmicrosoft.com' 建立的 hello 新 'MyCustomOU' 的組織單位是授與完整控制權。

 ![ADAC - 新的 OU 安全性](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>管理自訂 OU 的注意事項
既然您已建立了自訂 OU，就可以繼續在這個 OU 中建立使用者、群組、電腦和服務帳戶。 您無法從 hello ' AADDC Users' OU toocustom Ou 移動使用者或群組。

> [!WARNING]
> 您在自訂 OU 下建立的使用者帳戶、群組、服務帳戶和電腦物件無法在 Azure AD 租用戶中使用。 換句話說，這些物件不會使用 hello Azure AD Graph API 或 hello Azure AD UI 中顯示。 這些物件只可用於 Azure AD 網域服務受管理的網域中。
>
>

## <a name="related-content"></a>相關內容
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [設定受管理網域的群組原則](active-directory-ds-admin-guide-administer-group-policy.md)
* [Active Directory 管理中心：入門](https://technet.microsoft.com/library/dd560651.aspx)
* [服務帳戶的逐步指南](https://technet.microsoft.com/library/dd548356.aspx)
