---
title: "VMware 伺服器使用 Azure 備份伺服器 aaaBack |Microsoft 文件"
description: "使用 Azure 備份伺服器 tooback VMware vCenter/ESXi 伺服器 tooAzure 或磁碟。 本文提供備份 (或保護) 您 VMware 工作負載的逐步指示。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a>將 VMware server tooAzure 備份

本文說明如何 tooconfigure Azure 備份伺服器 toohelp 保護 VMware 伺服器工作負載。 本文假設您已安裝 Azure 備份伺服器。 如果您沒有安裝 Azure 備份伺服器，請參閱[準備使用 Azure 備份伺服器的工作負載備份 tooback](backup-azure-microsoft-azure-backup.md)。

Azure 備份伺服器可以備份或協助保護 VMware vCenter Server 6.5、6.0 和 5.5 版。


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>建立安全連線 toohello vCenter Server

Azure 備份伺服器預設會透過 HTTPS 通道來與各個 vCenter Server 進行通訊。 tooturn hello 安全通訊，我們建議您在 Azure 備份伺服器上安裝 hello VMware 憑證授權單位 (CA) 憑證。 如果您不需要安全通訊，並想使用 toodisable hello HTTPS 要求，請參閱[停用安全通訊協定](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)。 Azure 備份伺服器和 hello vCenter Server 之間的安全連接 toocreate 匯入 hello Azure 備份伺服器上的受信任的憑證。

一般而言，您可以使用瀏覽器 hello Azure 備份伺服器機器 tooconnect toohello vCenter Server 上透過 hello vSphere Web 用戶端。 hello 第一次使用 hello Azure 備份伺服器瀏覽器 tooconnect toohello vCenter Server，hello 連接不安全。 hello 下列影像顯示 hello 不安全的連線。

![不安全的連線 tooVMware 伺服器的範例](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix 這個問題，並建立安全的連線，請下載 hello 受信任的根 CA 憑證。

1. 在 Azure 備份伺服器上的 hello 瀏覽器中輸入 hello URL toohello vSphere Web 用戶端。 hello vSphere Web 用戶端登入頁面隨即出現。

    ![vSphere Web 用戶端](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    在系統管理員和開發人員的 hello 資訊 hello 下方，找出 hello**下載受信任的根 CA 憑證**連結。

    ![連結 toodownload hello 受信任的根 CA 憑證](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  如果您沒有看到 hello vSphere Web 用戶端登入頁面，請檢查您的瀏覽器 proxy 設定。

2. 按一下 [下載受信任的根 CA 憑證]。

    hello vCenter 伺服器下載檔案 tooyour 本機電腦。 hello 檔案的名稱為**下載**。 根據您的瀏覽器中，您會收到訊息，詢問是否 tooopen 或儲存 hello 檔案。

    ![下載憑證後，下載訊息](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Azure 備份伺服器上儲存 hello 檔案 tooa 位置。 當您儲存 hello 檔案時，加入 hello.zip 副檔名。

    hello 檔案是.zip 檔案，其中包含 hello hello 憑證資訊。 Hello.zip 副檔名，您可以使用 hello 擷取工具。

4. 以滑鼠右鍵按一下**download.zip**，然後選取**全部解壓縮**tooextract hello 內容。

    hello.zip 檔案中擷取名為其內容 tooa 資料夾**憑證**。 有兩種檔案會出現在 hello 憑證資料夾。 hello 根憑證檔案具有副檔名，例如.0 和.1 編號序列的開頭。
    
    hello CRL 檔案具有副檔名，例如.r0 或.r1 序列的開頭。 與憑證相關聯 hello CRL 檔案。

    ![download 檔案會在本機解壓縮 ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. 在 hello**憑證**資料夾，hello 根憑證檔案，以滑鼠右鍵按一下，然後按一下**重新命名**。

    ![將根憑證重新命名 ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    變更 hello 根憑證的擴充功能 too.crt。 當詢問您是否確定要 toochange hello 延伸模組，請按一下**是**或**確定**。 否則，您可以變更 hello 檔案指定的功能。 hello 圖示 hello 檔案變更 tooan 圖示代表根憑證。

6. Hello 根憑證上按一下滑鼠右鍵，然後從 hello 快顯功能表上，選取**安裝憑證**。

    hello**憑證匯入精靈** 對話方塊隨即出現。

7. 在 hello**憑證匯入精靈**對話方塊中，選取**本機**做為 hello 目的地為 hello 憑證，然後按一下**下一步**toocontinue。

    ![憑證存放區目的地選項 ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    如果您詢問您是否 tooallow 變更 toohello 電腦，按一下**是**或**確定**，tooall hello 變更。

8. 在 hello**憑證存放區**頁面上，選取**將所有憑證都放入下列存放區的 hello**，然後按一下**瀏覽**toochoose hello 憑證存放區。

    ![將憑證放在特定的儲存位置](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    hello**選取憑證存放區** 對話方塊隨即出現。

    ![憑證存放區資料夾階層](./media/backup-azure-backup-server-vmware/cert-store.png)

9. 選取**受信任的根憑證授權單位**hello hello 憑證，然後按一下所需的目的地資料夾為**確定**。

    ![憑證目的資料夾](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    hello**受信任的根憑證授權單位**資料夾確認 hello 憑證存放區。 按一下 [下一步] 。

    ![憑證存放區資料夾](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. 在 hello**完成 hello 憑證匯入精靈**頁面上，確認該 hello 憑證位於 hello 所要的資料夾，然後按一下**完成**。

    ![確認憑證位於 hello 適當的資料夾](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    此時會出現一個對話方塊，確認 hello 成功憑證匯入。

11. 登入 toohello vCenter Server tooconfirm 安全無虞，您的連線。

  如果 hello 憑證匯入不成功，而且您無法建立安全的連線，請參閱 hello VMware vSphere 文件上[取得伺服器憑證](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)。

  如果您組織內的安全界限，而且不想 tooturn hello HTTPS 通訊協定上的，使用下列程序 toodisable hello 安全通訊的 hello。

### <a name="disable-secure-communication-protocol"></a>停用安全通訊協定

如果您的組織不需要 hello HTTPS 通訊協定，使用下列步驟 toodisable HTTPS hello。 toodisable hello 預設行為，請建立會忽略 hello 預設行為的登錄機碼。

1. 複製並貼上下列文字至.txt 檔案的 hello。

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. 儲存 hello 檔案 tooyour Azure 備份伺服器電腦。 Hello，檔案名稱使用 DisableSecureAuthentication.reg。

3. 按兩下 hello 檔案 tooactivate hello 登錄項目。


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Hello vCenter Server 上建立的角色和使用者帳戶

Hello vCenter Server 上的角色是一組預先定義的權限。 VCenter Server 系統管理員建立 hello 角色。 tooassign 權限，hello 管理員組與某個角色的使用者帳戶。 tooestablish hello 必要的使用者認證 tooback hello vCenter Server 的電腦，建立以特定的權限的角色，然後將 hello 使用者帳戶與 hello 角色產生關聯。

Azure 備份伺服器會使用使用者名稱和密碼 tooauthenticate hello vcenter 伺服器。 Azure 備份伺服器會使用這些認證作為所有備份作業的驗證。

tooadd vCenter 伺服器角色和其權限的備份系統管理員：

1. 登入在 toohello vCenter Server，然後在 hello vCenter Server**導覽** 面板中，按一下 **管理**。

    ![vCenter Server 導覽面板中的管理選項](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. 在**管理**選取**角色**，然後在 hello**角色**面板按一下 hello 加入角色圖示 （hello + 符號）。

    ![新增角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    hello **Create Role**  對話方塊隨即出現。

    ![建立角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. 在 hello **Create Role**對話方塊中的，在 hello**角色名稱**方塊中，輸入*BackupAdminRole*。 hello 角色名稱可以是任何您喜歡，但它應該是可辨識的 hello 角色的用途。

4. 選取 hello hello 適當版本的 vCenter 的權限，然後按一下**確定**。 下表中的 hello 識別所需的 hello vCenter 6.0 和 vCenter 5.5 的權限。

  當您選取 hello 權限時，請按一下 hello 圖示下一步 toohello 父標籤 tooexpand hello 父系和檢視 hello 子權限。 tooselect hello VirtualMachine 權限，您需要 toogo hello 到數個層級父子階層。 您不需要 tooselect 父系權限內的所有子權限。

  ![父子式權限階層](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  按一下 之後**確定**，hello 新角色會出現在 hello hello 角色面板上的清單。

|Vcenter 6.0 的權限| Vcenter 5.5 的權限|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>建立 vCenter Server 使用者帳戶和權限

Hello 角色具有權限的設定之後，建立使用者帳戶。 hello 使用者帳戶具有的名稱和密碼，提供用於驗證的 hello 認證。

1. toocreate hello vCenter Server 中的使用者帳戶，**導覽**] 面板中，按一下 [**使用者和群組**。

    ![[使用者和群組] 選項](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    hello **vCenter 使用者和群組**面板隨即出現。

    ![[vCenter 使用者和群組] 面板](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. 在 hello **vCenter 使用者和群組**面板中，選取 hello**使用者**索引標籤，然後再按一下 hello 加入使用者圖示 （hello + 符號）。

    hello**新使用者** 對話方塊隨即出現。

3. 在 hello**新使用者**對話方塊方塊中，加入 hello 的使用者資訊，然後按一下**確定**。 在此程序，hello 使用者名稱會是 BackupAdmin。

    ![[新增使用者] 對話方塊](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    hello 新的使用者帳戶會出現在 [hello] 清單中。

4. tooassociate hello 使用者帳戶與 hello 角色，請在 hello**導覽** 面板中，按一下 **全域使用權限**。 在 hello**全域使用權限**面板中，選取 hello**管理**索引標籤，然後再按一下 hello 加入圖示 （hello + 符號）。

    ![[通用權限] 面板](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    hello**全域權限根目錄-新增權限** 對話方塊隨即出現。

5. 在 hello**全域權限根目錄-新增權限**對話方塊中，按一下 **新增**toochoose hello 使用者或群組。

    ![選擇使用者或群組](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    hello**選取使用者/群組** 對話方塊隨即出現。

6. 在 hello**選取使用者/群組**對話方塊方塊中，選擇**BackupAdmin** ，然後按一下**新增**。

    在**使用者**，hello *domain\username*格式用於 hello 使用者帳戶。 如果您想 toouse 不同的網域，請選擇從 hello**網域**清單。

    ![新增 BackupAdmin 使用者](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    按一下**確定**tooadd hello 選取使用者 toohello**加入權限** 對話方塊。

7. 既然您已經識別 hello 使用者，請將 hello 使用者 toohello 角色指派。 在**指派角色**，從 hello 下拉式清單中，選取  **BackupAdminRole**，然後按一下 **確定**。

    ![指派使用者 toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  在 hello**管理** 索引標籤中 hello**全域使用權限**面板、 hello 新的使用者帳戶和相關聯的 hello 角色出現在 hello 清單。


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>在 Azure 備份伺服器上建立 vCenter Server 認證

新增 hello VMware server tooAzure 備份伺服器之前，安裝[Update 1 for Azure 備份伺服器](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)。

1. tooopen Azure 備份伺服器，按兩下 hello hello Azure 備份伺服器的桌面上的圖示。

    ![Azure 備份伺服器圖示](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    如果在 hello 桌面找不到 hello 圖示，開啟 Azure 備份伺服器從 hello 清單安裝應用程式。 hello Azure 備份伺服器應用程式名稱會呼叫 Microsoft Azure 備份。

2. 在 hello Azure 備份伺服器主控台中，按一下 **管理**，按一下 **實際執行伺服器**，然後在 hello 工具功能區中，按一下**管理 VMware**。

    ![Azure 備份伺服器主控台](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    hello**管理認證** 對話方塊隨即出現。

    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. 在 [hello**管理認證**對話方塊中，按一下**新增**tooopen hello **Add Credential** ] 對話方塊。

4. 在 hello **Add Credential**對話方塊方塊中，輸入名稱和描述 hello 新認證。 然後指定 hello 使用者名稱和密碼。 hello 名稱*Contoso Vcenter 認證*用 tooidentify hello 下一個程序中的 hello 認證。 使用 hello 相同使用者名稱和密碼用於 hello vCenter Server。 如果 hello vCenter Server 和 Azure 備份伺服器不在 hello 中相同的網域，**使用者名**，指定 hello 網域。

    ![Azure 備份伺服器的 [新增認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    按一下**新增**tooadd hello 新認證 tooAzure 備份伺服器。 hello 新的認證會出現在 hello 清單中 hello**管理認證** 對話方塊。
    
    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. tooclose hello**管理認證**對話方塊方塊中，按一下 hello **X** hello 右上角。


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>新增 hello vCenter Server tooAzure 備份伺服器

使用的 tooadd hello vCenter Server tooAzure 備份伺服器實際執行伺服器加入精靈。

tooopen 實際執行伺服器新增精靈，完成下列程序的 hello:

1. 在 hello Azure 備份伺服器主控台中，按一下 **管理**，按一下**實際執行伺服器**，然後按一下**新增**。

    ![開啟「生產伺服器新增精靈」](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    hello**實際執行伺服器加法精靈** 對話方塊隨即出現。

    ![生產伺服器新增精靈](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. 在 hello**選取實際執行伺服器型別**頁面上，選取**VMware Server**，然後按一下**下一步**。

3. 在**伺服器名稱 /IP 位址**，指定 hello 完整的網域名稱 (FQDN) 或 hello VMware 伺服器的 IP 位址。 如果所有的 hello ESXi 伺服器由 hello 管理相同的 vCenter，您可以使用 hello vCenter 名稱。

    ![指定 VMware 伺服器的 FQDN 或 IP 位址](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. 在**SSL 連接埠**，輸入 hello 是使用的 toocommunicate 與 hello VMware 伺服器的連接埠。 使用連接埠 443，這種 hello 預設連接埠，除非您知道不同的通訊埠為必要。

5. 在**指定認證**，選取 hello 您稍早建立的認證。

    ![指定認證](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. 按一下**新增**tooadd hello VMware 伺服器 toohello 清單**新增 VMware Server**，然後按一下**下一步**toomove toohello 下一頁 hello 精靈中的。

    ![新增 VMWare 伺服器和認證](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. 在 hello**摘要**頁面上，按一下**新增**tooadd hello 指定 VMware server tooAzure 備份伺服器。

    ![新增 VMware server tooAzure 備份伺服器](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  hello VMware server backup 是無代理程式的備份，並立即新增 hello 新伺服器。 hello**完成**頁面上顯示 hello 結果。

  ![[完成] 頁面](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd 本章節的多個執行個體的 vCenter Server tooAzure 備份伺服器，重複 hello 上一個步驟。

您將加入 hello vCenter Server tooAzure 備份伺服器之後，hello 下一個步驟是 toocreate 保護群組。 hello 保護群組指定 hello 短期或長期保留的各種詳細資料，而且它是您定義並套用 hello 備份原則。 備份發生時，和備份的內容的 hello 排程 hello 備份原則。


## <a name="configure-a-protection-group"></a>設定保護群組

如果您不使用 System Center Data Protection Manager 或 Azure 備份伺服器之前，請參閱[規劃磁碟備份](https://technet.microsoft.com/library/hh758026.aspx)tooprepare 硬體環境。 您可以檢查您有適當的存放裝置之後，使用 hello 建立新保護群組精靈 tooadd VMware 虛擬機器。

1. 在 hello Azure 備份伺服器主控台中，按一下 **保護**，然後在 hello 工具功能區中，按一下 **新增**tooopen hello 建立新保護群組精靈。

    ![開啟 hello 建立新保護群組精靈](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    hello**建立新保護群組**精靈 對話方塊隨即出現。

    ![[建立新保護群組] 精靈對話方塊](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    按一下**下一步**tooadvance toohello**選取保護群組類型**頁面。

2. 在 hello**選取保護群組類型**頁面上，選取**伺服器**，然後按一下**下一步**。 hello**選取群組成員**頁面隨即出現。

3. 在 hello**選取群組成員**頁面、 hello 可用以及 hello 選取成員會出現。 選取您想 tooprotect，然後再按一下 hello 成員**下一步**。

    ![選擇群組成員](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    當您選取成員時，如果您選取的資料夾包含其他資料夾或 VM，則您會同時選取這些資料夾和 VM。 hello 包含 hello 資料夾和 hello 父資料夾中的 Vm 稱為資料夾層級的保護。 tooremove 資料夾或 VM，清除 hello 核取方塊。

    如果 VM 或 VM，其中包含的資料夾已經是受保護的 tooAzure，您無法再次選取該 VM。 也就是 VM 是受保護的 tooAzure 之後，它無法再次受到保護，這可防止重複的復原點建立一個 vm。 如果您想 toosee 哪個 Azure 備份伺服器執行個體已經保護成員、 點 toohello 成員 toosee hello 名稱 hello 保護伺服器。

4. 在 hello**選擇資料保護方式**頁面上，輸入 hello 保護群組的名稱。 選取短期保護 (toodisk) 和線上保護。 如果您想 toouse 線上保護 (tooAzure)，您必須使用短期保護 toodisk。 按一下**下一步**tooproceed toohello 短期保護範圍。

    ![選擇資料保護方式](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. 在 hello**指定短期目標** 頁面上，針對**保留範圍**，指定 hello 天數想 tooretain 復原點是*儲存 toodisk*。 如果您想 toochange hello 時間與日期當拍攝的復原點時，按一下**修改**。 hello 短期復原點是完整備份。 而不是增量備份。 當您滿意 hello 短期目標，請按一下**下一步**。

    ![指定短期目標](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. 在 hello**檢閱磁碟配置**頁面上，檢閱並視需要修改 hello hello Vm 的磁碟空間。 hello 建議磁碟配置根據 hello hello 中指定的保留範圍**指定短期目標** 頁面上，工作負載，hello 類型和 hello hello 大小受保護的資料 （步驟 3 中識別）。  

  - **資料大小：** hello 保護群組中的 hello 資料的大小。
  - **磁碟空間：** hello 建議 hello 保護群組的磁碟空間數量。 如果您想 toomodify 這項設定時，您應該配置略大於估計每個資料來源成長的 hello 量的總空間。
  - **將資料共置：** tooa 單一複本和復原點磁碟區，如果您啟用共置時，可以對應在 hello 保護多個資料來源。 不支援所有工作負載的共置。
  - **自動成長：**如果您開啟此設定，如果 hello 保護群組中的資料成長到超過 hello 初始配置所示，System Center Data Protection Manager 嘗試 tooincrease hello 磁碟大小的 25%。
  - **存放集區詳細資料：**顯示 hello hello 存放集區狀態，包括總計和剩餘的磁碟大小。

    ![檢閱磁碟配置](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    當您滿意 hello 空間配置，請按一下**下一步**。

7. 在 hello**選擇複本建立方式**頁面上，指定您想 toogenerate hello 初始複本或複本，Azure 備份伺服器上的 hello 受保護資料的方式。

    hello 預設值是**自動透過網路 hello**和**現在**。 如果您使用 hello 預設，我們建議您指定離峰時間。 選擇 [稍後] 並指定日期與時間。

    對於大量資料或較差的網路狀況，請考慮複寫 hello 資料離線使用卸除式媒體。

    做好選擇後，請按 [下一步]。

    ![選擇複本的建立方式](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. 在 hello**一致性檢查選項**頁面上，選取如何及何時 tooautomate hello 一致性檢查。 當複本資料變得不一致時，或依據設定的排程，您可以執行一致性檢查。

    如果您不想 tooconfigure 自動一致性檢查，您可以執行手動檢查。 在 hello 保護區域中的 hello Azure 備份伺服器主控台，以滑鼠右鍵按一下 hello 保護群組，然後選取**執行一致性檢查**。

    按一下**下一步**toomove toohello 下一個頁面。

9. 在 hello**指定線上保護資料**頁面上，選取您想 tooprotect 的一或多個資料來源。 您可以個別選取 hello 成員，或按一下**全選**toochoose 所有成員。 選擇 hello 成員之後，請按一下**下一步**。

    ![指定線上保護資料](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. 在 hello**指定線上備份排程**頁面上，指定 hello 排程 toogenerate hello 磁碟備份的復原點。 產生 hello 復原點之後，它是傳送的 toohello Azure 復原服務保存庫。 當您滿意 hello 線上備份排程，請按一下**下一步**。

    ![指定線上備份排程](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. 在 hello**指定線上保留原則**頁面上，指出您想在 Azure 中的 tooretain hello 備份資料的時間長度。 未定義 hello 原則之後，請按一下**下一步**。

    ![指定線上保留期原則](./media/backup-azure-backup-server-vmware/retention-policy.png)

    您可以在 Azure 中保留資料的時間長度沒有限制。 當您在 Azure 中儲存復原點資料時，hello 只限制是，您不能有超過 9999 的復原點，每個受保護的執行個體。 在此範例中，hello 受保護的執行個體是 hello VMware server。

12. 在 hello**摘要**頁面上，檢閱您的保護群組成員和設定，hello 詳細資料，然後按一下**建立群組**。

    ![保護群組成員和設定的摘要](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>後續步驟
如果您使用 Azure 備份伺服器 tooprotect VMware 工作負載時，您可能會想要使用 Azure 備份伺服器 toohelp 保護[Microsoft Exchange server](./backup-azure-exchange-mabs.md)、 [Microsoft SharePoint 伺服器陣列](./backup-azure-backup-sharepoint-mabs.md)，或[SQL Server 資料庫](./backup-azure-sql-mabs.md)。

如需註冊 hello 代理程式的問題，設定 hello 保護群組，或備份工作，請參閱[疑難排解 Azure 備份伺服器](./backup-azure-mabs-troubleshoot.md)。
