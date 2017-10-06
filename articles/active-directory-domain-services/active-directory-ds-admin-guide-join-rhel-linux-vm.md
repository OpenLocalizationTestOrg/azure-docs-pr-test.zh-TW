---
title: "Azure Active Directory 網域服務： 加入 RHEL VM tooa 受管理的網域 |Microsoft 文件"
description: "將 Red Hat Enterprise Linux 虛擬機器加入 tooAzure AD 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>加入 Red Hat Enterprise Linux 7 虛擬機器 tooa 受管理的網域
本文示範 toojoin Red Hat Enterprise Linux (RHEL) 7 虛擬機器 tooan Azure AD 網域服務網域的管理方式。

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>佈建 Red Hat Enterprise Linux 虛擬機器
執行下列步驟使用 hello Azure 入口網站的 tooprovision RHEL 7 虛擬機器的 hello。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

    ![Azure 入口網站儀表板](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. 按一下**新增**在左窗格中，然後輸入 hello **Red Hat** hello 搜尋列中 hello 下列螢幕擷取畫面所示。 Red Hat Enterprise Linux 的項目會出現在 hello 搜尋結果。 按一下 [Red Hat Enterprise Linux 7.2]。

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. hello 搜尋結果中 hello**一切**窗格應該會列出 hello Red Hat Enterprise Linux 7.2 映像。 按一下**Red Hat Enterprise Linux 7.2** tooview hello 虛擬機器映像的詳細資訊。

    ![在結果中選取 RHEL](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. 在 [hello **Red Hat Enterprise Linux 7.2** ] 窗格中，您應該會看到 hello 虛擬機器映像的詳細資訊。 在 [hello**選取部署模型**下拉式清單中，選取**傳統**。 然後按一下 [hello**建立**] 按鈕。

    ![檢視映像的詳細資料](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. 在 [hello**基本概念**hello 頁面**建立虛擬機器**精靈] 中，輸入 hello**主機名稱**hello 新虛擬機器。 也指定本機系統管理員使用者名稱中 hello**使用者名**欄位和**密碼**。 您也可以選擇 toouse SSH 金鑰 tooauthenticate hello 本機系統管理員使用者。 也選取**定價層**hello 虛擬機器。

    ![建立 VM - 基本頁面](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. 在 [hello**大小**頁面 hello**建立虛擬機器**hello 虛擬機器精靈、 選取 hello 大小。

    ![建立 VM - 選取大小](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. 在 [hello**設定**頁面 hello**建立虛擬機器**精靈、 選取 hello hello 虛擬機器的儲存體帳戶。 按一下**虛擬網路**tooselect hello 虛擬網路 toowhich hello Linux VM，必須先部署。 在 [hello**虛擬網路**刀鋒視窗中，選取 hello Azure AD 網域服務可用的虛擬網路。 在此範例中，我們挑選 hello 'MyPreviewVNet' 的虛擬網路。

    ![建立 VM - 選取虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Hello 上**摘要**hello 頁面**建立虛擬機器**精靈、 檢閱，並按一下 hello**確定**] 按鈕。

    ![建立 VM - 選取的虛擬網路](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. 部署的 hello 新的虛擬機器根據 hello RHEL 7.2 映像應該會開始。

    ![建立 VM - 部署開始](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. 請稍候幾分鐘 hello 虛擬機器必須部署成功且可供使用。

    ![建立 VM - 已部署](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>從遠端連線 toohello 新提供的 Linux 虛擬機器
hello RHEL 7.2 虛擬機器已在 Azure 中佈建。 hello 下一個工作是 tooconnect 遠端 toohello 虛擬機器。

**Toohello RHEL 7.2 虛擬機器連線**遵循 hello 文章中的 hello 指示[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

hello 其餘 hello 步驟假設您使用 hello PuTTY SSH 用戶端 tooconnect toohello RHEL 虛擬機器。 如需詳細資訊，請參閱 hello [PuTTY 下載頁面](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。

1. 開啟 hello PuTTY 程式。
2. 輸入 hello**主機名稱**hello 新建 RHEL 虛擬機器。 在此範例中，我們的虛擬機器會具有 hello 主機名稱 'contoso rhel.cloudapp.net'。 如果您不確定您的 VM hello 主機名稱，請參閱 toohello hello Azure 入口網站上的 VM 儀表板。

    ![PuTTY 連線](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. 登入 toohello 使用 hello hello 虛擬機器建立時，您所指定的本機系統管理員認證的虛擬機器。 在此範例中，我們會使用 hello 本機系統管理員帳戶 」 mahesh"。

    ![PuTTY 登入](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Hello Linux 虛擬機器上安裝必要的封裝
連接 toohello 虛擬機器之後, hello 下一個工作是 tooinstall 封裝所需的 hello 虛擬機器上的網域加入。 執行下列步驟的 hello:

1. **安裝 realmd:** hello realmd 封裝用於加入網域。 在您 PuTTY 終端機中，輸入下列命令的 hello:

    sudo yum install realmd

    ![安裝 realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    在幾分鐘後應該取得安裝 hello realmd 套件 hello 虛擬機器上。

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **安裝 sssd:** hello realmd 套件相依於 sssd tooperform 網域加入作業。 在您 PuTTY 終端機中，輸入下列命令的 hello:

    sudo yum install sssd

    ![安裝 sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    在幾分鐘後應該取得安裝 hello sssd 套件 hello 虛擬機器上。

    ![realmd 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **安裝 kerberos:**您 PuTTY 的終端機中輸入下列命令的 hello:

    sudo yum install krb5-workstation krb5-libs

    ![安裝 kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    在幾分鐘後應該取得安裝 hello realmd 套件 hello 虛擬機器上。

    ![Kerberos 已安裝](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>加入 hello Linux 虛擬機器 toohello 受管理的網域
現在，hello Linux 虛擬機器上安裝所需的 hello 封裝，hello 下一項工作就會是 toojoin hello 虛擬機器 toohello 受管理的網域。

1. 探索 hello AAD 網域服務受管理的網域。 在您 PuTTY 終端機中，輸入下列命令的 hello:

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    如果**領域探索**是無法 toofind 您受管理的網域，請確定該 hello 網域可連線從 hello 虛擬機器 (請嘗試 ping)。 此外也請確認該 hello 虛擬機器已確實已部署的 toohello 在哪一個 hello 受管理的網域都位於相同虛擬網路。
2. 初始化 kerberos。 在您 PuTTY 終端機中，輸入下列命令的 hello。 請確認您指定隸屬 toohello ' AAD DC Administrators' 群組的使用者身分。 只有這些使用者可以加入電腦 toohello 受管理的網域。

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    請確定您指定 hello 網域名稱以大寫的字母，且其他 kinit 失敗。
3. 加入 hello 機器 toohello 網域。 在您 PuTTY 終端機中，輸入下列命令的 hello。 指定 hello hello 前面步驟 ('kinit') 中所指定的同一個使用者。

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![加入領域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

您應該會收到訊息 （「 已順利註冊機器領域中 」） hello 機器時已成功的 toohello 受管理的網域。

## <a name="verify-domain-join"></a>確認加入網域
您可以快速驗證 hello 機器是否已成功加入的 toohello 受管理的網域。 連接 toohello 加入 RHEL VM 是否已正確地解決 hello 使用者帳戶使用 SSH 和網域使用者帳戶，然後核取 toosee 新網域。

1. 在您 PuTTY 終端機，下列命令 tooconnect toohello 新類型 hello 中使用 SSH RHEL 虛擬機器加入網域。 使用網域帳戶所屬 toohello 受管理的網域 (例如，'bob@CONTOSO100.COM' 在此情況下。)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. 您 PuTTY 的終端機中輸入下列命令 toosee，如果已正確初始化 hello 主目錄的 hello。

    pwd
3. 您 PuTTY 的終端機中輸入下列命令 toosee，如果正在正確解析 hello 群組成員資格的 hello。

    id

這些命令的輸出範例如下：

![確認加入網域](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>針對加入網域進行疑難排解
請參閱 toohello[疑難排解網域加入](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join)發行項。

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [加入 Windows Server 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [如何 tooa 執行 Linux 的虛擬機器上的 toolog](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* [安裝 Kerberos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows 整合指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
