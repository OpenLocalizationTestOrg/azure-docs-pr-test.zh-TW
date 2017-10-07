---
title: "Azure Active Directory Domain Services：管理受管理的網域 | Microsoft Docs"
description: "管理 Azure Active Directory 網域服務受管理網域"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>管理 Azure Active Directory 網域服務受管理網域
本文示範 tooadminister Azure Active Directory (AD) 網域服務網域的管理方式。

## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。
4. A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。 如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。
5. 您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister 中受管理的網域。

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>可在受管理網域中執行的系統管理工作
Hello 受管理的網域，讓它們 tooperform 工作這類權限會授與 hello ' AAD DC Administrators' 群組的成員：

* 加入機器 toohello 受管理的網域。
* Hello 內建在設定 GPO 的 hello 'AADDC 電腦' 和 ' AADDC 使用者 容器 hello 受管理的網域。
* 管理 hello 受管理的網域上的 DNS。
* 建立及管理自訂組織單位 (Ou) 上 hello 受管理的網域。
* 提升的系統管理存取 toocomputers 聯結 toohello 受管理的網域。

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>未擁有的受管理網域系統管理權限
hello 網域是由 Microsoft，包括活動，例如修補、 監視和備份管理。 因此，hello 網域已鎖定，而且您沒有權限 tooperform 特定系統管理工作 hello 網域上。 您無法執行之工作的部分範例如下。

* 您未獲授予 hello 受管理的網域的網域系統管理員或企業系統管理員權限。
* 您無法擴充 hello hello 受管理的網域結構描述。
* 您無法連接 toodomain hello 使用遠端桌面受管理的網域控制站。
* 您無法加入網域控制站 toohello 受管理的網域。

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>工作 1-佈建已加入網域的 Windows Server 虛擬機器 tooremotely 管理 hello 受管理的網域
可以使用熟悉 Active Directory 系統管理工具，例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。 租用戶系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。 因此，hello ' AAD DC Administrators' 群組可以管理的成員管理的網域從遠端使用 AD 從聯結的 toohello 受管理的網域的 Windows 伺服器/用戶端電腦的系統管理工具。 可以安裝 AD 系統管理工具，因為 Windows Server 和用戶端電腦上 hello 遠端伺服器管理工具 (RSAT) 選擇性功能的一部分加入 toohello 受管理網域。

hello 第一個步驟是 tooset 是聯結的 toohello 受管理網域的 Windows Server 虛擬機器。 如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>從遠端管理 hello 受管理的網域從用戶端電腦 (例如，Windows 10)
在此發行項使用 Windows Server 虛擬機器 tooadminister hello AAD DS hello 指示受管理的網域。 不過，您也可以選擇 toouse Windows 用戶端 (例如，Windows 10) 的虛擬機器 toodo 因此。

您可以[安裝遠端伺服器管理工具 (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx)依照 hello 指示 TechNet 上的 Windows 用戶端虛擬機器上。

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>工作 2-hello 虛擬機器上安裝 Active Directory 管理工具
執行下列步驟 tooinstall hello 的 Active Directory 管理工具 hello 已加入網域的虛擬機器上的 hello。 如需有關[安裝和使用遠端伺服器管理工具的詳細資訊](https://technet.microsoft.com/library/hh831501.aspx)，請參閱 TechNet。

1. 瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。 選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。 下載完成時，請按一下 tooopen hello 檔案。
3. 在 hello 登入提示字元中使用 hello 屬於 toohello ' AAD DC Administrators' 群組的使用者認證。 例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。
4. 從 hello 開始 畫面開啟**伺服器管理員**。 按一下**新增角色及功能**hello hello 伺服器管理員 視窗的中央窗格中。

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. 在 hello**在您開始前**hello 頁面**新增角色及功能精靈**，按一下 **下一步**。

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. 在 hello**安裝類型**頁面上，保留 hello**角色型或功能型安裝**檢查的選項，然後按一下**下一步**。

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. 在 hello**伺服器選取項目**頁面上，選取 hello 目前虛擬機器從 hello 伺服器集區，然後按一下**下一步**。

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. 在 hello**伺服器角色**頁面上，按一下**下一步**。 我們請略過此頁面，因為我們 hello 伺服器上未安裝任何角色。
9. 在 hello**功能**頁面上，按一下 tooexpand hello**遠端伺服器管理工具**節點，然後按一下tooexpand hello**角色管理工具**節點。 選取**AD DS 與 AD LDS 工具**hello 清單中的角色管理工具的功能。

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. 在 hello**確認**頁面上，按一下**安裝**tooinstall hello AD 與 AD LDS 工具功能 hello 虛擬機器上。 功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>工作 3-連接 tooand 瀏覽 hello 受管理的網域
既然 hello AD 系統管理工具安裝在 hello 已加入網域的虛擬機器，我們可以使用這些工具 tooexplore 及管理 hello 受管理的網域。

> [!NOTE]
> 您需要 toobe 成員 hello ' AAD DC Administrators' 群組的 tooadminister hello 管理網域。
>
>

1. 從 hello 開始畫面上，按一下 **系統管理工具**。 您應該會看到 hello AD hello 虛擬機器上安裝的系統管理工具。

    ![安裝在伺服器上的系統管理工具](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. 按一下 [Active Directory 管理中心] 。

    ![Active Directory 管理中心](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooexplore hello 網域中，按一下 hello hello 左窗格 (例如，' contoso100.com') 中的網域名稱。 請注意分別稱為「AADDC 電腦」和「AADDC 使用者」的兩個容器。

    ![ADAC - 檢視網域](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. 按一下稱為 hello 容器**AADDC 使用者**toosee 所有使用者和群組屬於 toohello 受都管理網域。 在此容器中，您應該會看到您的 Azure AD 租用戶中的使用者帳戶和群組顯示出來。 請注意，在此範例中，呼叫 'bob' hello 使用者和呼叫 ' AAD DC Administrators' 群組的使用者帳戶是這個容器中。

    ![ADAC - 網域使用者](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. 按一下稱為 hello 容器**AADDC 電腦**toosee hello 電腦加入 toothis 受管理的網域。 您應該會看到 hello 目前虛擬機器，也就是聯結的 toohello 網域的項目。 所有電腦的電腦帳戶加入 toohello 受管理的網域會儲存在此 「 AADDC 電腦 」 容器的 Azure AD 網域服務。

    ![ADAC - 已加入網域的電腦](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [部署遠端伺服器管理工具](https://technet.microsoft.com/library/hh831501.aspx)
