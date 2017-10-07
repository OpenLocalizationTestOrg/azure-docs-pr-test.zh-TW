---
title: "Azure Active Directory Domain Services：管理受管理網域上的群組原則 | Microsoft Docs"
description: "管理 Azure Active Directory Domain Services 受管理網域上的群組原則"
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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>管理 Azure AD Domain Services 受管理網域上的群組原則
Azure Active Directory 網域服務的 hello ' AADDC 使用者 」 和 「 AADDC 電腦 」 容器包含內建群組原則物件 (Gpo)。 您可以自訂這些內建的 Gpo tooconfigure hello 受管理的網域上的群組原則。 此外，hello ' AAD DC Administrators' 群組的成員可以建立自己的自訂 Ou hello 受管理的網域中。 它們也可以建立自訂的 Gpo，並將其連結 toothese 自訂 Ou。 Hello 受管理的網域上的群組原則系統管理特殊權限會授與使用者隸屬 toohello ' AAD DC Administrators' 群組。

## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。
4. A**已加入網域的虛擬機器**從您管理的 hello Azure AD 網域服務受管理的網域。 如果您沒有這類虛擬機器，請遵循所有 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。
5. 您需要 hello 認證**使用者帳戶隸屬 toohello ' AAD DC Administrators' 群組**目錄，tooadminister 群組原則的受管理的網域中。

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>工作 1-佈建已加入網域的虛擬機器 tooremotely hello 受管理的網域的管理群組原則
可以從遠端使用熟悉的 Active Directory 系統管理工具例如 hello Active Directory 管理中心 (ADAC) 或 AD PowerShell 管理 azure AD 網域服務受管理的網域。 同樣地，可以使用 hello 群組原則系統管理工具，從遠端管理的 hello 受管理的網域群組原則。

Azure AD 目錄中的系統管理員沒有 hello 透過遠端桌面的受管理網域的權限 tooconnect toodomain 控制站。 Hello ' AAD DC Administrators' 群組的成員可以管理群組原則的受管理的網域從遠端。 他們可以在 Windows 伺服器/用戶端電腦已加入的 toohello 受管理的網域上使用群組原則工具。 可以安裝 Windows Server 和用戶端電腦上 hello 群組原則管理選擇性功能的一部分加入 toohello 受管理的網域群組原則工具。

hello 第一項工作是 tooprovision 是聯結的 toohello 受管理的網域 Windows Server 虛擬機器。 如需指示，請參閱 toohello 文章 <<c0> [ 加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>工作 2-hello 虛擬機器上安裝群組原則工具
執行下列步驟 tooinstall hello 群組原則系統管理工具 hello 已加入網域的虛擬機器上的 hello。

1. 瀏覽過**虛擬機器**hello Azure 傳統入口網站中的節點。 選取您在工作 1 中建立的 hello 虛擬機器，然後按一下**連接**hello 在 hello hello 視窗底部的命令列上。

    ![TooWindows 虛擬機器連線](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 傳統入口網站會提示您 tooopen 或儲存 '.rdp' 副檔名的檔案，這是使用的 tooconnect toohello 虛擬機器。 下載完成時，請按一下 hello 檔案。
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
9. 在 hello**功能**頁面上，選取 hello**群組原則管理**功能。

    ![[功能] 頁面](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. 在 hello**確認**頁面上，按一下**安裝**hello 虛擬機器上的 tooinstall hello 群組原則管理功能。 功能安裝成功完成時，按一下**關閉**tooexit hello**新增角色及功能**精靈。

    ![確認電子郵件](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>工作 3-啟動 hello 群組原則管理主控台 tooadminister 群組原則
您可以使用 hello 群組原則管理主控台上 hello 已加入網域的虛擬機器 tooadminister hello 受管理的網域上的群組原則。

> [!NOTE]
> 您需要 toobe tooadminister hello 受管理的網域上的群組原則 hello ' AAD DC Administrators' 群組的成員。
>
>

1. 從 hello 開始畫面上，按一下 **系統管理工具**。 您應該會看見 hello**群組原則管理**hello 虛擬機器上安裝主控台。

    ![啟動群組原則管理](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. 按一下**群組原則管理**toolaunch hello 群組原則管理主控台。

    ![群組原則主控台](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>工作 4 - 自訂內建群組原則物件
有兩個內建群組原則物件 (Gpo) 的每個受管理的網域中的 hello 'AADDC 電腦' 和 ' AADDC 使用者 容器。 您可以自訂這些 Gpo tooconfigure 上的群組原則 hello 受管理的網域。

1. 在 hello**群組原則管理**主控台中，按一下 tooexpand hello**樹系： contoso100.com**和**網域**節點 toosee hello 群組原則的受管理的網域。

    ![內建 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. 您可以自訂這些內建的 Gpo tooconfigure 群組原則在受管理的網域上。 Hello GPO 上按一下滑鼠右鍵，然後按一下**編輯...** toocustomize hello 內建 GPO。 hello 群組原則組態編輯器工具可讓您 toocustomize hello GPO。

    ![編輯內建 GPO](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. 您現在可以使用 hello**群組原則管理編輯器**主控台 tooedit hello 內建 GPO。 比方說，下列螢幕擷取畫面的 hello 顯示 toocustomize hello 內建的 「 AADDC 電腦 」 GPO 的方式。

    ![自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>工作 5 - 建立自訂群組原則物件 (GPO)
您可以建立或匯入自己的自訂群組原則物件。 您也可以將連結自訂 Gpo tooa 自訂您受管理的網域中建立的 OU。 如需建立自訂組織單位的詳細資訊，請參閱[在受管理網域上建立自訂 OU](active-directory-ds-admin-guide-create-ou.md)。

> [!NOTE]
> 您需要 toobe tooadminister hello 受管理的網域上的群組原則 hello ' AAD DC Administrators' 群組的成員。
>
>

1. 在 hello**群組原則管理**主控台中，按一下 tooselect 自訂組織單位 (OU)。 Hello OU 上按一下滑鼠右鍵，然後按一下**在這個網域中建立 GPO 並連結到...**.

    ![建立自訂 GPO](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. 指定 hello 新 GPO 的名稱，然後按一下**確定**。

    ![指定 GPO 的名稱](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. 建立新的 GPO，並連結 tooyour 自訂 OU。 Hello GPO 上按一下滑鼠右鍵，然後按一下**編輯...** hello 功能表。

    ![新建立的 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. 您可以自訂 hello 新建立的 GPO，使用 hello**群組原則管理編輯器**。

    ![自訂新 GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


可在 Technet 上取得有關使用[群組原則管理主控台](https://technet.microsoft.com/library/cc753298.aspx)的詳細資訊。

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [群組原則管理主控台](https://technet.microsoft.com/library/cc753298.aspx)
