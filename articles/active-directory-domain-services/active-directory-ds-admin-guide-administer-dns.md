---
title: "Azure Active Directory Domain Services：管理受管理網域上的 DNS | Microsoft Docs"
description: "管理 Azure Active Directory Domain Services 受管理網域上的 DNS"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>管理 Azure AD 網域服務受管理網域上的 DNS
Azure Active Directory 網域服務包括提供 hello 受管理的網域的 DNS 解析的 DNS （網域名稱解析） 伺服器。 有時候，您可能需要 tooconfigure hello 受管理網域上的 DNS。 未聯結的 toohello 網域的機器設定負載平衡器虛擬 IP 位址，或設定外部 DNS 轉寄站，您可能需要 toocreate DNS 記錄。 基於這個理由，屬於 toohello ' AAD DC Administrators' 群組的使用者授與 hello 受管理的網域上的 DNS 管理權限。

## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。
4. A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。 如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。
5. 您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister DNS 的受管理的網域中。

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>工作 1-佈建已加入網域的虛擬機器 tooremotely 管理 DNS 的 hello 受管理的網域
可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。 同樣地，可以使用 hello DNS 伺服器管理工具，從遠端管理 hello 受管理的網域的 DNS。

Azure AD 目錄中的系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。 Hello ' AAD DC Administrators' 群組的成員可以管理 DNS 的受管理的網域從遠端使用聯結的 toohello 受管理的網域的 Windows 伺服器/用戶端電腦的 DNS 伺服器工具。 DNS 伺服器工具可以安裝在 Windows Server 上 hello 遠端伺服器管理工具 (RSAT) 選擇性功能的一部分，而且用戶端電腦加入 toohello 受管理網域。

hello 第一項工作是 tooprovision 是聯結的 toohello 受管理的網域 Windows Server 虛擬機器。 如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>工作 2-hello 虛擬機器上安裝 DNS 伺服器工具
執行下列步驟 tooinstall hello DNS 系統管理工具 hello 已加入網域的虛擬機器上的 hello。 如需有關[安裝和使用遠端伺服器管理工具](https://technet.microsoft.com/library/hh831501.aspx)的詳細資訊，請參閱 TechNet。

1. 瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。 選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。 下載完成時，請按一下 hello 檔案。
3. 在 hello 登入提示字元中使用 hello 屬於 toohello ' AAD DC Administrators' 群組的使用者認證。 例如，使用 'bob@domainservicespreview.onmicrosoft.com' 在我們的案例。
4. 從 hello 開始] 畫面開啟**伺服器管理員**。 按一下**新增角色及功能**hello hello 伺服器管理員] 視窗的中央窗格中。

    ![啟動虛擬機器上的伺服器管理員](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. 在 hello**在您開始前**hello 頁面**新增角色及功能精靈**，按一下 [**下一步**。

    ![[開始之前] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. 在 [hello**安裝類型**頁面上，保留 hello**角色型或功能型安裝**檢查的選項，然後按一下**下一步**。

    ![[安裝類型] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. 在 [hello**伺服器選取項目**頁面上，選取 hello 目前虛擬機器從 hello 伺服器集區，然後按一下**下一步**。

    ![[伺服器選擇] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. 在 [hello**伺服器角色**頁面上，按一下**下一步**。 我們請略過此頁面，因為我們 hello 伺服器上未安裝任何角色。
9. 在 [hello**功能**頁面上，按一下 tooexpand hello**遠端伺服器管理工具**節點，然後按一下 [tooexpand hello**角色管理工具**節點。 選取**DNS 伺服器工具**hello 清單中的角色管理工具的功能。

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. 在 [hello**確認**頁面上，按一下**安裝**tooinstall hello DNS 伺服器工具功能 hello 虛擬機器上。 功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>工作 3-啟動 hello DNS 管理主控台 tooadminister DNS
既然 hello DNS 伺服器工具安裝功能 hello 已加入網域的虛擬機器，我們可以使用 hello DNS 工具 tooadminister DNS 受管理的 hello 網域上。

> [!NOTE]
> 您需要 toobe tooadminister hello 受管理的網域上的 DNS hello ' AAD DC Administrators' 群組的成員。
>
>

1. 從 hello 開始畫面上，按一下 [**系統管理工具**。 您應該會看見 hello **DNS** hello 虛擬機器上安裝主控台。

    ![系統管理工具 - DNS 主控台](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. 按一下**DNS** toolaunch hello DNS 管理主控台。
3. 在 hello**連接 tooDNS 伺服器**] 對話方塊中，按一下標題為 hello 選項**hello 下列電腦**，然後輸入 hello DNS 網域名稱的 hello 受管理的網域 (例如，' contoso100.com')。

    ![DNS 主控台-連接 toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. hello DNS 主控台連接 toohello 受管理的網域。

    ![DNS 主控台 - 管理網域](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. 您現在可以使用 hello DNS 主控台 tooadd DNS 項目已啟用 AAD 網域服務的 hello 虛擬網路內的電腦。

> [!WARNING]
> 管理 DNS hello 受管理的網域使用 DNS 系統管理工具時，請格外小心。 請確定您**請勿刪除或修改 hello 內建的 DNS 記錄所使用的 hello 網域中的網域服務**。 內建 DNS 記錄包括網域 DNS 記錄、名稱伺服器記錄和其他用於 DC 位置的記錄。 如果您修改這些記錄，網域服務也會受到干擾 hello 虛擬網路上。
>
>

請參閱 hello [Technet 文章 DNS 工具](https://technet.microsoft.com/library/cc753579.aspx)如需管理 DNS 的詳細資訊。

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [DNS 系統管理工具](https://technet.microsoft.com/library/cc753579.aspx)
