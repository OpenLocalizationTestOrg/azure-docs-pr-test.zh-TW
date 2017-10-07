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
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="1173c-104">將 VMware server tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="1173c-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="1173c-105">本文說明如何 tooconfigure Azure 備份伺服器 toohelp 保護 VMware 伺服器工作負載。</span><span class="sxs-lookup"><span data-stu-id="1173c-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="1173c-106">本文假設您已安裝 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="1173c-107">如果您沒有安裝 Azure 備份伺服器，請參閱[準備使用 Azure 備份伺服器的工作負載備份 tooback](backup-azure-microsoft-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="1173c-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="1173c-108">Azure 備份伺服器可以備份或協助保護 VMware vCenter Server 6.5、6.0 和 5.5 版。</span><span class="sxs-lookup"><span data-stu-id="1173c-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="1173c-109">建立安全連線 toohello vCenter Server</span><span class="sxs-lookup"><span data-stu-id="1173c-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="1173c-110">Azure 備份伺服器預設會透過 HTTPS 通道來與各個 vCenter Server 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1173c-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="1173c-111">tooturn hello 安全通訊，我們建議您在 Azure 備份伺服器上安裝 hello VMware 憑證授權單位 (CA) 憑證。</span><span class="sxs-lookup"><span data-stu-id="1173c-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="1173c-112">如果您不需要安全通訊，並想使用 toodisable hello HTTPS 要求，請參閱[停用安全通訊協定](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)。</span><span class="sxs-lookup"><span data-stu-id="1173c-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="1173c-113">Azure 備份伺服器和 hello vCenter Server 之間的安全連接 toocreate 匯入 hello Azure 備份伺服器上的受信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="1173c-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="1173c-114">一般而言，您可以使用瀏覽器 hello Azure 備份伺服器機器 tooconnect toohello vCenter Server 上透過 hello vSphere Web 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1173c-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="1173c-115">hello 第一次使用 hello Azure 備份伺服器瀏覽器 tooconnect toohello vCenter Server，hello 連接不安全。</span><span class="sxs-lookup"><span data-stu-id="1173c-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="1173c-116">hello 下列影像顯示 hello 不安全的連線。</span><span class="sxs-lookup"><span data-stu-id="1173c-116">hello following image shows hello unsecured connection.</span></span>

![不安全的連線 tooVMware 伺服器的範例](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="1173c-118">toofix 這個問題，並建立安全的連線，請下載 hello 受信任的根 CA 憑證。</span><span class="sxs-lookup"><span data-stu-id="1173c-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="1173c-119">在 Azure 備份伺服器上的 hello 瀏覽器中輸入 hello URL toohello vSphere Web 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1173c-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="1173c-120">hello vSphere Web 用戶端登入頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere Web 用戶端](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="1173c-122">在系統管理員和開發人員的 hello 資訊 hello 下方，找出 hello**下載受信任的根 CA 憑證**連結。</span><span class="sxs-lookup"><span data-stu-id="1173c-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![連結 toodownload hello 受信任的根 CA 憑證](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="1173c-124">如果您沒有看到 hello vSphere Web 用戶端登入頁面，請檢查您的瀏覽器 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="1173c-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="1173c-125">按一下 [下載受信任的根 CA 憑證]。</span><span class="sxs-lookup"><span data-stu-id="1173c-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="1173c-126">hello vCenter 伺服器下載檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="1173c-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="1173c-127">hello 檔案的名稱為**下載**。</span><span class="sxs-lookup"><span data-stu-id="1173c-127">hello file's name is named **download**.</span></span> <span data-ttu-id="1173c-128">根據您的瀏覽器中，您會收到訊息，詢問是否 tooopen 或儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1173c-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![下載憑證後，下載訊息](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="1173c-130">Azure 備份伺服器上儲存 hello 檔案 tooa 位置。</span><span class="sxs-lookup"><span data-stu-id="1173c-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="1173c-131">當您儲存 hello 檔案時，加入 hello.zip 副檔名。</span><span class="sxs-lookup"><span data-stu-id="1173c-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="1173c-132">hello 檔案是.zip 檔案，其中包含 hello hello 憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="1173c-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="1173c-133">Hello.zip 副檔名，您可以使用 hello 擷取工具。</span><span class="sxs-lookup"><span data-stu-id="1173c-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="1173c-134">以滑鼠右鍵按一下**download.zip**，然後選取**全部解壓縮**tooextract hello 內容。</span><span class="sxs-lookup"><span data-stu-id="1173c-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="1173c-135">hello.zip 檔案中擷取名為其內容 tooa 資料夾**憑證**。</span><span class="sxs-lookup"><span data-stu-id="1173c-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="1173c-136">有兩種檔案會出現在 hello 憑證資料夾。</span><span class="sxs-lookup"><span data-stu-id="1173c-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="1173c-137">hello 根憑證檔案具有副檔名，例如.0 和.1 編號序列的開頭。</span><span class="sxs-lookup"><span data-stu-id="1173c-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="1173c-138">hello CRL 檔案具有副檔名，例如.r0 或.r1 序列的開頭。</span><span class="sxs-lookup"><span data-stu-id="1173c-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="1173c-139">與憑證相關聯 hello CRL 檔案。</span><span class="sxs-lookup"><span data-stu-id="1173c-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="1173c-140">download 檔案會在本機解壓縮</span><span class="sxs-lookup"><span data-stu-id="1173c-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="1173c-141">在 hello**憑證**資料夾，hello 根憑證檔案，以滑鼠右鍵按一下，然後按一下**重新命名**。</span><span class="sxs-lookup"><span data-stu-id="1173c-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="1173c-142">將根憑證重新命名</span><span class="sxs-lookup"><span data-stu-id="1173c-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="1173c-143">變更 hello 根憑證的擴充功能 too.crt。</span><span class="sxs-lookup"><span data-stu-id="1173c-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="1173c-144">當詢問您是否確定要 toochange hello 延伸模組，請按一下**是**或**確定**。</span><span class="sxs-lookup"><span data-stu-id="1173c-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="1173c-145">否則，您可以變更 hello 檔案指定的功能。</span><span class="sxs-lookup"><span data-stu-id="1173c-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="1173c-146">hello 圖示 hello 檔案變更 tooan 圖示代表根憑證。</span><span class="sxs-lookup"><span data-stu-id="1173c-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="1173c-147">Hello 根憑證上按一下滑鼠右鍵，然後從 hello 快顯功能表上，選取**安裝憑證**。</span><span class="sxs-lookup"><span data-stu-id="1173c-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="1173c-148">hello**憑證匯入精靈** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="1173c-149">在 hello**憑證匯入精靈**對話方塊中，選取**本機**做為 hello 目的地為 hello 憑證，然後按一下**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1173c-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="1173c-150">憑證存放區目的地選項</span><span class="sxs-lookup"><span data-stu-id="1173c-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="1173c-151">如果您詢問您是否 tooallow 變更 toohello 電腦，按一下**是**或**確定**，tooall hello 變更。</span><span class="sxs-lookup"><span data-stu-id="1173c-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="1173c-152">在 hello**憑證存放區**頁面上，選取**將所有憑證都放入下列存放區的 hello**，然後按一下**瀏覽**toochoose hello 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="1173c-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![將憑證放在特定的儲存位置](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="1173c-154">hello**選取憑證存放區** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![憑證存放區資料夾階層](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="1173c-156">選取**受信任的根憑證授權單位**hello hello 憑證，然後按一下所需的目的地資料夾為**確定**。</span><span class="sxs-lookup"><span data-stu-id="1173c-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![憑證目的資料夾](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="1173c-158">hello**受信任的根憑證授權單位**資料夾確認 hello 憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="1173c-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="1173c-159">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1173c-159">Click **Next**.</span></span>

    ![憑證存放區資料夾](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="1173c-161">在 hello**完成 hello 憑證匯入精靈**頁面上，確認該 hello 憑證位於 hello 所要的資料夾，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="1173c-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![確認憑證位於 hello 適當的資料夾](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="1173c-163">此時會出現一個對話方塊，確認 hello 成功憑證匯入。</span><span class="sxs-lookup"><span data-stu-id="1173c-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="1173c-164">登入 toohello vCenter Server tooconfirm 安全無虞，您的連線。</span><span class="sxs-lookup"><span data-stu-id="1173c-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="1173c-165">如果 hello 憑證匯入不成功，而且您無法建立安全的連線，請參閱 hello VMware vSphere 文件上[取得伺服器憑證](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)。</span><span class="sxs-lookup"><span data-stu-id="1173c-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="1173c-166">如果您組織內的安全界限，而且不想 tooturn hello HTTPS 通訊協定上的，使用下列程序 toodisable hello 安全通訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="1173c-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="1173c-167">停用安全通訊協定</span><span class="sxs-lookup"><span data-stu-id="1173c-167">Disable secure communication protocol</span></span>

<span data-ttu-id="1173c-168">如果您的組織不需要 hello HTTPS 通訊協定，使用下列步驟 toodisable HTTPS hello。</span><span class="sxs-lookup"><span data-stu-id="1173c-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="1173c-169">toodisable hello 預設行為，請建立會忽略 hello 預設行為的登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="1173c-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="1173c-170">複製並貼上下列文字至.txt 檔案的 hello。</span><span class="sxs-lookup"><span data-stu-id="1173c-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="1173c-171">儲存 hello 檔案 tooyour Azure 備份伺服器電腦。</span><span class="sxs-lookup"><span data-stu-id="1173c-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="1173c-172">Hello，檔案名稱使用 DisableSecureAuthentication.reg。</span><span class="sxs-lookup"><span data-stu-id="1173c-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="1173c-173">按兩下 hello 檔案 tooactivate hello 登錄項目。</span><span class="sxs-lookup"><span data-stu-id="1173c-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="1173c-174">Hello vCenter Server 上建立的角色和使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="1173c-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="1173c-175">Hello vCenter Server 上的角色是一組預先定義的權限。</span><span class="sxs-lookup"><span data-stu-id="1173c-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="1173c-176">VCenter Server 系統管理員建立 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="1173c-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="1173c-177">tooassign 權限，hello 管理員組與某個角色的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1173c-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="1173c-178">tooestablish hello 必要的使用者認證 tooback hello vCenter Server 的電腦，建立以特定的權限的角色，然後將 hello 使用者帳戶與 hello 角色產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1173c-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="1173c-179">Azure 備份伺服器會使用使用者名稱和密碼 tooauthenticate hello vcenter 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="1173c-180">Azure 備份伺服器會使用這些認證作為所有備份作業的驗證。</span><span class="sxs-lookup"><span data-stu-id="1173c-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="1173c-181">tooadd vCenter 伺服器角色和其權限的備份系統管理員：</span><span class="sxs-lookup"><span data-stu-id="1173c-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="1173c-182">登入在 toohello vCenter Server，然後在 hello vCenter Server**導覽** 面板中，按一下 **管理**。</span><span class="sxs-lookup"><span data-stu-id="1173c-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![vCenter Server 導覽面板中的管理選項](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="1173c-184">在**管理**選取**角色**，然後在 hello**角色**面板按一下 hello 加入角色圖示 （hello + 符號）。</span><span class="sxs-lookup"><span data-stu-id="1173c-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![新增角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="1173c-186">hello **Create Role**  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-186">hello **Create Role** dialog box appears.</span></span>

    ![建立角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="1173c-188">在 hello **Create Role**對話方塊中的，在 hello**角色名稱**方塊中，輸入*BackupAdminRole*。</span><span class="sxs-lookup"><span data-stu-id="1173c-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="1173c-189">hello 角色名稱可以是任何您喜歡，但它應該是可辨識的 hello 角色的用途。</span><span class="sxs-lookup"><span data-stu-id="1173c-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="1173c-190">選取 hello hello 適當版本的 vCenter 的權限，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1173c-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="1173c-191">下表中的 hello 識別所需的 hello vCenter 6.0 和 vCenter 5.5 的權限。</span><span class="sxs-lookup"><span data-stu-id="1173c-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="1173c-192">當您選取 hello 權限時，請按一下 hello 圖示下一步 toohello 父標籤 tooexpand hello 父系和檢視 hello 子權限。</span><span class="sxs-lookup"><span data-stu-id="1173c-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="1173c-193">tooselect hello VirtualMachine 權限，您需要 toogo hello 到數個層級父子階層。</span><span class="sxs-lookup"><span data-stu-id="1173c-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="1173c-194">您不需要 tooselect 父系權限內的所有子權限。</span><span class="sxs-lookup"><span data-stu-id="1173c-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![父子式權限階層](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="1173c-196">按一下 之後**確定**，hello 新角色會出現在 hello hello 角色面板上的清單。</span><span class="sxs-lookup"><span data-stu-id="1173c-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="1173c-197">Vcenter 6.0 的權限</span><span class="sxs-lookup"><span data-stu-id="1173c-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="1173c-198">Vcenter 5.5 的權限</span><span class="sxs-lookup"><span data-stu-id="1173c-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="1173c-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="1173c-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="1173c-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="1173c-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="1173c-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="1173c-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="1173c-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="1173c-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="1173c-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="1173c-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="1173c-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="1173c-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="1173c-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="1173c-205">Network.Assign</span></span> |
|<span data-ttu-id="1173c-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="1173c-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="1173c-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="1173c-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="1173c-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="1173c-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="1173c-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="1173c-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="1173c-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="1173c-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="1173c-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="1173c-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="1173c-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="1173c-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="1173c-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="1173c-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="1173c-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="1173c-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="1173c-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="1173c-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="1173c-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="1173c-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="1173c-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="1173c-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="1173c-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="1173c-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="1173c-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="1173c-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="1173c-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="1173c-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="1173c-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="1173c-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="1173c-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="1173c-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="1173c-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="1173c-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="1173c-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="1173c-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="1173c-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="1173c-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="1173c-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="1173c-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="1173c-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="1173c-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="1173c-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="1173c-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="1173c-229">建立 vCenter Server 使用者帳戶和權限</span><span class="sxs-lookup"><span data-stu-id="1173c-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="1173c-230">Hello 角色具有權限的設定之後，建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1173c-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="1173c-231">hello 使用者帳戶具有的名稱和密碼，提供用於驗證的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="1173c-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="1173c-232">toocreate hello vCenter Server 中的使用者帳戶，**導覽**] 面板中，按一下 [**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1173c-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![[使用者和群組] 選項](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="1173c-234">hello **vCenter 使用者和群組**面板隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![[vCenter 使用者和群組] 面板](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="1173c-236">在 hello **vCenter 使用者和群組**面板中，選取 hello**使用者**索引標籤，然後再按一下 hello 加入使用者圖示 （hello + 符號）。</span><span class="sxs-lookup"><span data-stu-id="1173c-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="1173c-237">hello**新使用者** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="1173c-238">在 hello**新使用者**對話方塊方塊中，加入 hello 的使用者資訊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1173c-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="1173c-239">在此程序，hello 使用者名稱會是 BackupAdmin。</span><span class="sxs-lookup"><span data-stu-id="1173c-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![[新增使用者] 對話方塊](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="1173c-241">hello 新的使用者帳戶會出現在 [hello] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1173c-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="1173c-242">tooassociate hello 使用者帳戶與 hello 角色，請在 hello**導覽** 面板中，按一下 **全域使用權限**。</span><span class="sxs-lookup"><span data-stu-id="1173c-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="1173c-243">在 hello**全域使用權限**面板中，選取 hello**管理**索引標籤，然後再按一下 hello 加入圖示 （hello + 符號）。</span><span class="sxs-lookup"><span data-stu-id="1173c-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![[通用權限] 面板](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="1173c-245">hello**全域權限根目錄-新增權限** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="1173c-246">在 hello**全域權限根目錄-新增權限**對話方塊中，按一下 **新增**toochoose hello 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="1173c-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![選擇使用者或群組](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="1173c-248">hello**選取使用者/群組** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="1173c-249">在 hello**選取使用者/群組**對話方塊方塊中，選擇**BackupAdmin** ，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1173c-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="1173c-250">在**使用者**，hello *domain\username*格式用於 hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1173c-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="1173c-251">如果您想 toouse 不同的網域，請選擇從 hello**網域**清單。</span><span class="sxs-lookup"><span data-stu-id="1173c-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![新增 BackupAdmin 使用者](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="1173c-253">按一下**確定**tooadd hello 選取使用者 toohello**加入權限** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1173c-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="1173c-254">既然您已經識別 hello 使用者，請將 hello 使用者 toohello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="1173c-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="1173c-255">在**指派角色**，從 hello 下拉式清單中，選取  **BackupAdminRole**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="1173c-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![指派使用者 toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="1173c-257">在 hello**管理** 索引標籤中 hello**全域使用權限**面板、 hello 新的使用者帳戶和相關聯的 hello 角色出現在 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1173c-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="1173c-258">在 Azure 備份伺服器上建立 vCenter Server 認證</span><span class="sxs-lookup"><span data-stu-id="1173c-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="1173c-259">新增 hello VMware server tooAzure 備份伺服器之前，安裝[Update 1 for Azure 備份伺服器](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)。</span><span class="sxs-lookup"><span data-stu-id="1173c-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="1173c-260">tooopen Azure 備份伺服器，按兩下 hello hello Azure 備份伺服器的桌面上的圖示。</span><span class="sxs-lookup"><span data-stu-id="1173c-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Azure 備份伺服器圖示](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="1173c-262">如果在 hello 桌面找不到 hello 圖示，開啟 Azure 備份伺服器從 hello 清單安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="1173c-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="1173c-263">hello Azure 備份伺服器應用程式名稱會呼叫 Microsoft Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="1173c-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="1173c-264">在 hello Azure 備份伺服器主控台中，按一下 **管理**，按一下 **實際執行伺服器**，然後在 hello 工具功能區中，按一下**管理 VMware**。</span><span class="sxs-lookup"><span data-stu-id="1173c-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Azure 備份伺服器主控台](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="1173c-266">hello**管理認證** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="1173c-268">在 [hello**管理認證**對話方塊中，按一下**新增**tooopen hello **Add Credential** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1173c-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="1173c-269">在 hello **Add Credential**對話方塊方塊中，輸入名稱和描述 hello 新認證。</span><span class="sxs-lookup"><span data-stu-id="1173c-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="1173c-270">然後指定 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1173c-270">Then specify hello username and password.</span></span> <span data-ttu-id="1173c-271">hello 名稱*Contoso Vcenter 認證*用 tooidentify hello 下一個程序中的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="1173c-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="1173c-272">使用 hello 相同使用者名稱和密碼用於 hello vCenter Server。</span><span class="sxs-lookup"><span data-stu-id="1173c-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="1173c-273">如果 hello vCenter Server 和 Azure 備份伺服器不在 hello 中相同的網域，**使用者名**，指定 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="1173c-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Azure 備份伺服器的 [新增認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="1173c-275">按一下**新增**tooadd hello 新認證 tooAzure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="1173c-276">hello 新的認證會出現在 hello 清單中 hello**管理認證** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1173c-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="1173c-278">tooclose hello**管理認證**對話方塊方塊中，按一下 hello **X** hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="1173c-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="1173c-279">新增 hello vCenter Server tooAzure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="1173c-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="1173c-280">使用的 tooadd hello vCenter Server tooAzure 備份伺服器實際執行伺服器加入精靈。</span><span class="sxs-lookup"><span data-stu-id="1173c-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="1173c-281">tooopen 實際執行伺服器新增精靈，完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="1173c-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="1173c-282">在 hello Azure 備份伺服器主控台中，按一下 **管理**，按一下**實際執行伺服器**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="1173c-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![開啟「生產伺服器新增精靈」](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="1173c-284">hello**實際執行伺服器加法精靈** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![生產伺服器新增精靈](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="1173c-286">在 hello**選取實際執行伺服器型別**頁面上，選取**VMware Server**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="1173c-287">在**伺服器名稱 /IP 位址**，指定 hello 完整的網域名稱 (FQDN) 或 hello VMware 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1173c-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="1173c-288">如果所有的 hello ESXi 伺服器由 hello 管理相同的 vCenter，您可以使用 hello vCenter 名稱。</span><span class="sxs-lookup"><span data-stu-id="1173c-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![指定 VMware 伺服器的 FQDN 或 IP 位址](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="1173c-290">在**SSL 連接埠**，輸入 hello 是使用的 toocommunicate 與 hello VMware 伺服器的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1173c-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="1173c-291">使用連接埠 443，這種 hello 預設連接埠，除非您知道不同的通訊埠為必要。</span><span class="sxs-lookup"><span data-stu-id="1173c-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="1173c-292">在**指定認證**，選取 hello 您稍早建立的認證。</span><span class="sxs-lookup"><span data-stu-id="1173c-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![指定認證](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="1173c-294">按一下**新增**tooadd hello VMware 伺服器 toohello 清單**新增 VMware Server**，然後按一下**下一步**toomove toohello 下一頁 hello 精靈中的。</span><span class="sxs-lookup"><span data-stu-id="1173c-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![新增 VMWare 伺服器和認證](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="1173c-296">在 hello**摘要**頁面上，按一下**新增**tooadd hello 指定 VMware server tooAzure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![新增 VMware server tooAzure 備份伺服器](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="1173c-298">hello VMware server backup 是無代理程式的備份，並立即新增 hello 新伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="1173c-299">hello**完成**頁面上顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="1173c-299">hello **Finish** page shows you hello results.</span></span>

  ![[完成] 頁面](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="1173c-301">tooadd 本章節的多個執行個體的 vCenter Server tooAzure 備份伺服器，重複 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1173c-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="1173c-302">您將加入 hello vCenter Server tooAzure 備份伺服器之後，hello 下一個步驟是 toocreate 保護群組。</span><span class="sxs-lookup"><span data-stu-id="1173c-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="1173c-303">hello 保護群組指定 hello 短期或長期保留的各種詳細資料，而且它是您定義並套用 hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="1173c-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="1173c-304">備份發生時，和備份的內容的 hello 排程 hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="1173c-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="1173c-305">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="1173c-305">Configure a protection group</span></span>

<span data-ttu-id="1173c-306">如果您不使用 System Center Data Protection Manager 或 Azure 備份伺服器之前，請參閱[規劃磁碟備份](https://technet.microsoft.com/library/hh758026.aspx)tooprepare 硬體環境。</span><span class="sxs-lookup"><span data-stu-id="1173c-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="1173c-307">您可以檢查您有適當的存放裝置之後，使用 hello 建立新保護群組精靈 tooadd VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1173c-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="1173c-308">在 hello Azure 備份伺服器主控台中，按一下 **保護**，然後在 hello 工具功能區中，按一下 **新增**tooopen hello 建立新保護群組精靈。</span><span class="sxs-lookup"><span data-stu-id="1173c-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![開啟 hello 建立新保護群組精靈](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="1173c-310">hello**建立新保護群組**精靈 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![[建立新保護群組] 精靈對話方塊](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="1173c-312">按一下**下一步**tooadvance toohello**選取保護群組類型**頁面。</span><span class="sxs-lookup"><span data-stu-id="1173c-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="1173c-313">在 hello**選取保護群組類型**頁面上，選取**伺服器**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="1173c-314">hello**選取群組成員**頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="1173c-315">在 hello**選取群組成員**頁面、 hello 可用以及 hello 選取成員會出現。</span><span class="sxs-lookup"><span data-stu-id="1173c-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="1173c-316">選取您想 tooprotect，然後再按一下 hello 成員**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="1173c-318">當您選取成員時，如果您選取的資料夾包含其他資料夾或 VM，則您會同時選取這些資料夾和 VM。</span><span class="sxs-lookup"><span data-stu-id="1173c-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="1173c-319">hello 包含 hello 資料夾和 hello 父資料夾中的 Vm 稱為資料夾層級的保護。</span><span class="sxs-lookup"><span data-stu-id="1173c-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="1173c-320">tooremove 資料夾或 VM，清除 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1173c-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="1173c-321">如果 VM 或 VM，其中包含的資料夾已經是受保護的 tooAzure，您無法再次選取該 VM。</span><span class="sxs-lookup"><span data-stu-id="1173c-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="1173c-322">也就是 VM 是受保護的 tooAzure 之後，它無法再次受到保護，這可防止重複的復原點建立一個 vm。</span><span class="sxs-lookup"><span data-stu-id="1173c-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="1173c-323">如果您想 toosee 哪個 Azure 備份伺服器執行個體已經保護成員、 點 toohello 成員 toosee hello 名稱 hello 保護伺服器。</span><span class="sxs-lookup"><span data-stu-id="1173c-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="1173c-324">在 hello**選擇資料保護方式**頁面上，輸入 hello 保護群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="1173c-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="1173c-325">選取短期保護 (toodisk) 和線上保護。</span><span class="sxs-lookup"><span data-stu-id="1173c-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="1173c-326">如果您想 toouse 線上保護 (tooAzure)，您必須使用短期保護 toodisk。</span><span class="sxs-lookup"><span data-stu-id="1173c-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="1173c-327">按一下**下一步**tooproceed toohello 短期保護範圍。</span><span class="sxs-lookup"><span data-stu-id="1173c-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![選擇資料保護方式](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="1173c-329">在 hello**指定短期目標** 頁面上，針對**保留範圍**，指定 hello 天數想 tooretain 復原點是*儲存 toodisk*。</span><span class="sxs-lookup"><span data-stu-id="1173c-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="1173c-330">如果您想 toochange hello 時間與日期當拍攝的復原點時，按一下**修改**。</span><span class="sxs-lookup"><span data-stu-id="1173c-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="1173c-331">hello 短期復原點是完整備份。</span><span class="sxs-lookup"><span data-stu-id="1173c-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="1173c-332">而不是增量備份。</span><span class="sxs-lookup"><span data-stu-id="1173c-332">They are not incremental backups.</span></span> <span data-ttu-id="1173c-333">當您滿意 hello 短期目標，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![指定短期目標](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="1173c-335">在 hello**檢閱磁碟配置**頁面上，檢閱並視需要修改 hello hello Vm 的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="1173c-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="1173c-336">hello 建議磁碟配置根據 hello hello 中指定的保留範圍**指定短期目標** 頁面上，工作負載，hello 類型和 hello hello 大小受保護的資料 （步驟 3 中識別）。</span><span class="sxs-lookup"><span data-stu-id="1173c-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="1173c-337">**資料大小：** hello 保護群組中的 hello 資料的大小。</span><span class="sxs-lookup"><span data-stu-id="1173c-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="1173c-338">**磁碟空間：** hello 建議 hello 保護群組的磁碟空間數量。</span><span class="sxs-lookup"><span data-stu-id="1173c-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="1173c-339">如果您想 toomodify 這項設定時，您應該配置略大於估計每個資料來源成長的 hello 量的總空間。</span><span class="sxs-lookup"><span data-stu-id="1173c-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="1173c-340">**將資料共置：** tooa 單一複本和復原點磁碟區，如果您啟用共置時，可以對應在 hello 保護多個資料來源。</span><span class="sxs-lookup"><span data-stu-id="1173c-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="1173c-341">不支援所有工作負載的共置。</span><span class="sxs-lookup"><span data-stu-id="1173c-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="1173c-342">**自動成長：**如果您開啟此設定，如果 hello 保護群組中的資料成長到超過 hello 初始配置所示，System Center Data Protection Manager 嘗試 tooincrease hello 磁碟大小的 25%。</span><span class="sxs-lookup"><span data-stu-id="1173c-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="1173c-343">**存放集區詳細資料：**顯示 hello hello 存放集區狀態，包括總計和剩餘的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="1173c-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![檢閱磁碟配置](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="1173c-345">當您滿意 hello 空間配置，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="1173c-346">在 hello**選擇複本建立方式**頁面上，指定您想 toogenerate hello 初始複本或複本，Azure 備份伺服器上的 hello 受保護資料的方式。</span><span class="sxs-lookup"><span data-stu-id="1173c-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="1173c-347">hello 預設值是**自動透過網路 hello**和**現在**。</span><span class="sxs-lookup"><span data-stu-id="1173c-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="1173c-348">如果您使用 hello 預設，我們建議您指定離峰時間。</span><span class="sxs-lookup"><span data-stu-id="1173c-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="1173c-349">選擇 [稍後] 並指定日期與時間。</span><span class="sxs-lookup"><span data-stu-id="1173c-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="1173c-350">對於大量資料或較差的網路狀況，請考慮複寫 hello 資料離線使用卸除式媒體。</span><span class="sxs-lookup"><span data-stu-id="1173c-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="1173c-351">做好選擇後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1173c-351">After you have made your choices, click **Next**.</span></span>

    ![選擇複本的建立方式](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="1173c-353">在 hello**一致性檢查選項**頁面上，選取如何及何時 tooautomate hello 一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="1173c-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="1173c-354">當複本資料變得不一致時，或依據設定的排程，您可以執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="1173c-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="1173c-355">如果您不想 tooconfigure 自動一致性檢查，您可以執行手動檢查。</span><span class="sxs-lookup"><span data-stu-id="1173c-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="1173c-356">在 hello 保護區域中的 hello Azure 備份伺服器主控台，以滑鼠右鍵按一下 hello 保護群組，然後選取**執行一致性檢查**。</span><span class="sxs-lookup"><span data-stu-id="1173c-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="1173c-357">按一下**下一步**toomove toohello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="1173c-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="1173c-358">在 hello**指定線上保護資料**頁面上，選取您想 tooprotect 的一或多個資料來源。</span><span class="sxs-lookup"><span data-stu-id="1173c-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="1173c-359">您可以個別選取 hello 成員，或按一下**全選**toochoose 所有成員。</span><span class="sxs-lookup"><span data-stu-id="1173c-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="1173c-360">選擇 hello 成員之後，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-360">After you choose hello members, click **Next**.</span></span>

    ![指定線上保護資料](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="1173c-362">在 hello**指定線上備份排程**頁面上，指定 hello 排程 toogenerate hello 磁碟備份的復原點。</span><span class="sxs-lookup"><span data-stu-id="1173c-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="1173c-363">產生 hello 復原點之後，它是傳送的 toohello Azure 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1173c-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="1173c-364">當您滿意 hello 線上備份排程，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![指定線上備份排程](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="1173c-366">在 hello**指定線上保留原則**頁面上，指出您想在 Azure 中的 tooretain hello 備份資料的時間長度。</span><span class="sxs-lookup"><span data-stu-id="1173c-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="1173c-367">未定義 hello 原則之後，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1173c-367">After hello policy is defined, click **Next**.</span></span>

    ![指定線上保留期原則](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="1173c-369">您可以在 Azure 中保留資料的時間長度沒有限制。</span><span class="sxs-lookup"><span data-stu-id="1173c-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="1173c-370">當您在 Azure 中儲存復原點資料時，hello 只限制是，您不能有超過 9999 的復原點，每個受保護的執行個體。</span><span class="sxs-lookup"><span data-stu-id="1173c-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="1173c-371">在此範例中，hello 受保護的執行個體是 hello VMware server。</span><span class="sxs-lookup"><span data-stu-id="1173c-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="1173c-372">在 hello**摘要**頁面上，檢閱您的保護群組成員和設定，hello 詳細資料，然後按一下**建立群組**。</span><span class="sxs-lookup"><span data-stu-id="1173c-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![保護群組成員和設定的摘要](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="1173c-374">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1173c-374">Next steps</span></span>
<span data-ttu-id="1173c-375">如果您使用 Azure 備份伺服器 tooprotect VMware 工作負載時，您可能會想要使用 Azure 備份伺服器 toohelp 保護[Microsoft Exchange server](./backup-azure-exchange-mabs.md)、 [Microsoft SharePoint 伺服器陣列](./backup-azure-backup-sharepoint-mabs.md)，或[SQL Server 資料庫](./backup-azure-sql-mabs.md)。</span><span class="sxs-lookup"><span data-stu-id="1173c-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="1173c-376">如需註冊 hello 代理程式的問題，設定 hello 保護群組，或備份工作，請參閱[疑難排解 Azure 備份伺服器](./backup-azure-mabs-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="1173c-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
