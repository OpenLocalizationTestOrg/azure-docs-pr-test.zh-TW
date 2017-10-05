---
title: "使用 Azure 備份伺服器來備份 VMware 伺服器 | Microsoft Docs"
description: "使用 Azure 備份伺服器，將 VMware vCenter/ESXi 伺服器備份至 Azure 或磁碟。 本文提供備份 (或保護) 您 VMware 工作負載的逐步指示。"
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
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="275fb-104">將 VMware 伺服器備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="275fb-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="275fb-105">本文說明如何設定 Azure 備份伺服器來協助保護 VMware 伺服器工作負載。</span><span class="sxs-lookup"><span data-stu-id="275fb-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="275fb-106">本文假設您已安裝 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="275fb-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="275fb-107">如果您尚未安裝 Azure 備份伺服器，請參閱[使用 Azure 備份伺服器準備將工作負載進行備份](backup-azure-microsoft-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="275fb-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="275fb-108">Azure 備份伺服器可以備份或協助保護 VMware vCenter Server 6.5、6.0 和 5.5 版。</span><span class="sxs-lookup"><span data-stu-id="275fb-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="275fb-109">建立 vCenter Server 的安全連線</span><span class="sxs-lookup"><span data-stu-id="275fb-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="275fb-110">Azure 備份伺服器預設會透過 HTTPS 通道來與各個 vCenter Server 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="275fb-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="275fb-111">若要開啟安全通訊，建議您在 Azure 備份伺服器上安裝 VMware 憑證授權單位 (CA) 憑證。</span><span class="sxs-lookup"><span data-stu-id="275fb-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="275fb-112">如果您不需要安全通訊，而且想要停用 HTTPS 要求，請參閱[停用安全通訊協定](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol)。</span><span class="sxs-lookup"><span data-stu-id="275fb-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="275fb-113">若要建立 Azure 備份伺服器與 vCenter Server 之間的安全連線，請將 Azure 備份伺服器上的受信任憑證匯入。</span><span class="sxs-lookup"><span data-stu-id="275fb-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="275fb-114">通常您會透過 vSphere Web 用戶端，使用 Azure 備份伺服器電腦上的瀏覽器連線到 vCenter Server。</span><span class="sxs-lookup"><span data-stu-id="275fb-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="275fb-115">您第一次使用 Azure 備份伺服器的瀏覽器連線到 vCenter Server 時，連線為不安全。</span><span class="sxs-lookup"><span data-stu-id="275fb-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="275fb-116">下圖顯示不安全的連線。</span><span class="sxs-lookup"><span data-stu-id="275fb-116">The following image shows the unsecured connection.</span></span>

![VMware 伺服器的不安全連線範例](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="275fb-118">若要修正此問題，並建立安全連線，請下載受信任的根 CA 憑證。</span><span class="sxs-lookup"><span data-stu-id="275fb-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="275fb-119">在 Azure 備份伺服器上的瀏覽器中，輸入 vSphere Web 用戶端的 URL。</span><span class="sxs-lookup"><span data-stu-id="275fb-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="275fb-120">vSphere Web 用戶端登入頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-120">The vSphere Web Client login page appears.</span></span>

    ![vSphere Web 用戶端](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="275fb-122">在系統管理員和開發人員的資訊底部找到 [下載受信任根 CA 憑證] 連結。</span><span class="sxs-lookup"><span data-stu-id="275fb-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![用來下載受信任根 CA 憑證的連結](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="275fb-124">如果您沒有看到 vSphere Web 用戶端登入頁面，請檢查您瀏覽器的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="275fb-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="275fb-125">按一下 [下載受信任的根 CA 憑證]。</span><span class="sxs-lookup"><span data-stu-id="275fb-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="275fb-126">vCenter Server 會將檔案下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="275fb-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="275fb-127">檔案名稱為 **download**。</span><span class="sxs-lookup"><span data-stu-id="275fb-127">The file's name is named **download**.</span></span> <span data-ttu-id="275fb-128">依您的瀏覽器而定，您會收到詢問您要開啟還是儲存檔案的訊息。</span><span class="sxs-lookup"><span data-stu-id="275fb-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![下載憑證後，下載訊息](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="275fb-130">將檔案儲存至 Azure 備份伺服器上的位置。</span><span class="sxs-lookup"><span data-stu-id="275fb-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="275fb-131">當您儲存檔案時，請新增 .zip 副檔名。</span><span class="sxs-lookup"><span data-stu-id="275fb-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="275fb-132">檔案是包含憑證相關資訊的 .zip 檔。</span><span class="sxs-lookup"><span data-stu-id="275fb-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="275fb-133">使用 .zip 副檔名，您就可以使用解壓縮工具。</span><span class="sxs-lookup"><span data-stu-id="275fb-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="275fb-134">以滑鼠右鍵按一下 **download.zip**，然後選取 [解壓縮全部]，將內容解壓縮。</span><span class="sxs-lookup"><span data-stu-id="275fb-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="275fb-135">.zip 檔案會將其內容解壓縮到名為 **certs** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="275fb-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="275fb-136">certs 資料夾中會出現兩種檔案類型。</span><span class="sxs-lookup"><span data-stu-id="275fb-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="275fb-137">根憑證檔案，其副檔名的開頭是編號序列，例如 .0 和 .1。</span><span class="sxs-lookup"><span data-stu-id="275fb-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="275fb-138">CRL 檔案，其副檔名的開頭是序列，例如 .r0 和 .r1。</span><span class="sxs-lookup"><span data-stu-id="275fb-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="275fb-139">與憑證相關聯的 CRL 檔案。</span><span class="sxs-lookup"><span data-stu-id="275fb-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="275fb-140">download 檔案會在本機解壓縮</span><span class="sxs-lookup"><span data-stu-id="275fb-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="275fb-141">在 **certs** 資料夾中，以滑鼠右鍵按一下根憑證檔案，然後按一下 [重新命名]。</span><span class="sxs-lookup"><span data-stu-id="275fb-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="275fb-142">將根憑證重新命名</span><span class="sxs-lookup"><span data-stu-id="275fb-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="275fb-143">將根憑證的副檔名變更為 .crt。</span><span class="sxs-lookup"><span data-stu-id="275fb-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="275fb-144">當系統詢問您是否確定要變更副檔名時，請按一下 [是] 或 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="275fb-145">否則，請變更檔案的預定功能。</span><span class="sxs-lookup"><span data-stu-id="275fb-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="275fb-146">檔案的圖示會變更為代表根憑證的圖示。</span><span class="sxs-lookup"><span data-stu-id="275fb-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="275fb-147">以滑鼠右鍵按一下根憑證，然後從快顯功能表中選取 [安裝憑證]。</span><span class="sxs-lookup"><span data-stu-id="275fb-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="275fb-148">[憑證匯入精靈] 對話方塊會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="275fb-149">在 [憑證匯入精靈] 對話方塊中，選取 [本機電腦] 作為憑證目的地，然後按 [下一步] 繼續執行。</span><span class="sxs-lookup"><span data-stu-id="275fb-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="275fb-150">憑證存放區目的地選項</span><span class="sxs-lookup"><span data-stu-id="275fb-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="275fb-151">如果系統詢問您是否要允許對電腦進行變更，請對所有變更按一下 [是] 或 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="275fb-152">在 [憑證存放區] 頁面上，選取 [將所有憑證放入以下的存放區]，然後按一下 [瀏覽] 來選擇憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="275fb-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![將憑證放在特定的儲存位置](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="275fb-154">[選取憑證存放區] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![憑證存放區資料夾階層](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="275fb-156">選取 [受信任的根憑證授權單位] 作為憑證的目的地資料夾，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![憑證目的資料夾](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="275fb-158">系統會確認將 [受信任的根憑證授權單位] 資料夾作為憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="275fb-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="275fb-159">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="275fb-159">Click **Next**.</span></span>

    ![憑證存放區資料夾](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="275fb-161">在 [完成憑證匯入精靈] 頁面上，確認憑證是否位於所要的資料夾中，然後按一下 [完成] 以完成精靈。</span><span class="sxs-lookup"><span data-stu-id="275fb-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![確認憑證位於適當的資料夾](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="275fb-163">此時會出現一個對話方塊，向您確認已成功匯入憑證。</span><span class="sxs-lookup"><span data-stu-id="275fb-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="275fb-164">請登入 vCenter Server 以確認您的連線是否安全。</span><span class="sxs-lookup"><span data-stu-id="275fb-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="275fb-165">如果系統未成功匯入憑證，而且您也無法建立安全的連線，請參閱有關[取得伺服器憑證](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html)的 VMware vSphere 文件。</span><span class="sxs-lookup"><span data-stu-id="275fb-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="275fb-166">如果您的組織設有安全界限，而且不想開啟 HTTPS 通訊協定，請使用下列程序來停用安全通訊。</span><span class="sxs-lookup"><span data-stu-id="275fb-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="275fb-167">停用安全通訊協定</span><span class="sxs-lookup"><span data-stu-id="275fb-167">Disable secure communication protocol</span></span>

<span data-ttu-id="275fb-168">如果您的組織不需要 HTTPS 通訊協定，請使用下列步驟來停用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="275fb-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="275fb-169">若要停用預設行為，請建立會忽略預設行為的登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="275fb-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="275fb-170">複製以下文字並貼到 .txt 檔案中。</span><span class="sxs-lookup"><span data-stu-id="275fb-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="275fb-171">將檔案儲存到 Azure 備份伺服器電腦。</span><span class="sxs-lookup"><span data-stu-id="275fb-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="275fb-172">至於檔案名稱，請使用 DisableSecureAuthentication.reg。</span><span class="sxs-lookup"><span data-stu-id="275fb-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="275fb-173">按兩下檔案以啟動登錄項目。</span><span class="sxs-lookup"><span data-stu-id="275fb-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="275fb-174">在 vCenter Server 上建立角色和使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="275fb-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="275fb-175">在 vCenter Server 上，角色是一組預先定義的權限。</span><span class="sxs-lookup"><span data-stu-id="275fb-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="275fb-176">vCenter Server 系統管理員會建立角色。</span><span class="sxs-lookup"><span data-stu-id="275fb-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="275fb-177">為了指派權限，系統管理員會將使用者帳戶與某個角色進行配對。</span><span class="sxs-lookup"><span data-stu-id="275fb-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="275fb-178">若要建立所需的使用者認證以便備份 vCenter Server 電腦，請建立具有特定權限的角色，並讓使用者帳戶與該角色產生關聯。</span><span class="sxs-lookup"><span data-stu-id="275fb-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="275fb-179">Azure 備份伺服器會使用使用者名稱和密碼來驗證 vCenter Server。</span><span class="sxs-lookup"><span data-stu-id="275fb-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="275fb-180">Azure 備份伺服器會使用這些認證作為所有備份作業的驗證。</span><span class="sxs-lookup"><span data-stu-id="275fb-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="275fb-181">若要為備份管理員新增 vCenter Server 角色和其權限︰</span><span class="sxs-lookup"><span data-stu-id="275fb-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="275fb-182">登入 vCenter Server，然後在 vCenter Server 的 [導覽] 面板中，按一下 [管理]。</span><span class="sxs-lookup"><span data-stu-id="275fb-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![vCenter Server 導覽面板中的管理選項](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="275fb-184">在 [管理] 中選取 [角色]，然後在 [角色] 面板中按一下 [新增角色] 圖示(+ 符號)。</span><span class="sxs-lookup"><span data-stu-id="275fb-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![新增角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="275fb-186">[建立角色] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-186">The **Create Role** dialog box appears.</span></span>

    ![建立角色](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="275fb-188">在 [建立角色] 對話方塊的 [角色名稱] 方塊中，輸入「BackupAdminRole」。</span><span class="sxs-lookup"><span data-stu-id="275fb-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="275fb-189">角色名稱可以是您喜歡的名稱，但它應該是可辨識該角色的用途。</span><span class="sxs-lookup"><span data-stu-id="275fb-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="275fb-190">選取適當 vCenter 版本的權限，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="275fb-191">下表指出 vCenter 6.0 和 vCenter 5.5 所需的權限。</span><span class="sxs-lookup"><span data-stu-id="275fb-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="275fb-192">選取權限時，請按一下父標籤旁的圖示，以展開父權限並檢視子權限。</span><span class="sxs-lookup"><span data-stu-id="275fb-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="275fb-193">若要選取 VirtualMachine 權限，您必須深入父子式階層中的好幾層。</span><span class="sxs-lookup"><span data-stu-id="275fb-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="275fb-194">您不需要選取父代權限內的所有子權限。</span><span class="sxs-lookup"><span data-stu-id="275fb-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![父子式權限階層](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="275fb-196">在按一下 [確定] 後，[角色] 面板上的清單中就會出現新的角色。</span><span class="sxs-lookup"><span data-stu-id="275fb-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="275fb-197">Vcenter 6.0 的權限</span><span class="sxs-lookup"><span data-stu-id="275fb-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="275fb-198">Vcenter 5.5 的權限</span><span class="sxs-lookup"><span data-stu-id="275fb-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="275fb-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="275fb-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="275fb-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="275fb-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="275fb-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="275fb-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="275fb-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="275fb-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="275fb-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="275fb-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="275fb-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="275fb-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="275fb-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="275fb-205">Network.Assign</span></span> |
|<span data-ttu-id="275fb-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="275fb-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="275fb-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="275fb-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="275fb-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="275fb-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="275fb-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="275fb-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="275fb-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="275fb-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="275fb-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="275fb-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="275fb-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="275fb-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="275fb-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="275fb-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="275fb-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="275fb-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="275fb-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="275fb-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="275fb-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="275fb-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="275fb-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="275fb-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="275fb-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="275fb-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="275fb-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="275fb-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="275fb-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="275fb-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="275fb-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="275fb-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="275fb-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="275fb-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="275fb-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="275fb-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="275fb-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="275fb-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="275fb-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="275fb-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="275fb-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="275fb-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="275fb-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="275fb-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="275fb-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="275fb-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="275fb-229">建立 vCenter Server 使用者帳戶和權限</span><span class="sxs-lookup"><span data-stu-id="275fb-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="275fb-230">在設定了具有權限的角色後，請建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="275fb-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="275fb-231">使用者帳戶具有名稱和密碼，可提供用於驗證的認證。</span><span class="sxs-lookup"><span data-stu-id="275fb-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="275fb-232">若要建立使用者帳戶，請在 vCenter Server 的 [導覽] 面板中按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="275fb-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![[使用者和群組] 選項](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="275fb-234">[vCenter 使用者和群組] 面板隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![[vCenter 使用者和群組] 面板](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="275fb-236">在 [vCenter 使用者和群組] 面板中，選取 [使用者] 索引標籤，然後按一下 [新增使用者] 圖示 (+ 符號)。</span><span class="sxs-lookup"><span data-stu-id="275fb-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="275fb-237">[新增使用者] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="275fb-238">在 [新增使用者] 對話方塊中新增使用者的資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="275fb-239">在此程序中，使用者名稱是 BackupAdmin。</span><span class="sxs-lookup"><span data-stu-id="275fb-239">In this procedure, the username is BackupAdmin.</span></span>

    ![[新增使用者] 對話方塊](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="275fb-241">新的使用者帳戶會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="275fb-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="275fb-242">若要讓使用者帳戶與角色產生關聯，請在 [導覽] 面板中按一下 [通用權限]。</span><span class="sxs-lookup"><span data-stu-id="275fb-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="275fb-243">在 [通用權限] 面板中，選取 [管理] 索引標籤，然後按一下 [新增] 圖示 (+ 符號)。</span><span class="sxs-lookup"><span data-stu-id="275fb-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![[通用權限] 面板](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="275fb-245">[通用權限根目錄 - 新增權限] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="275fb-246">在 [通用權限根目錄 - 新增權限] 對話方塊中，按一下 [新增] 來選擇使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="275fb-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![選擇使用者或群組](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="275fb-248">[選取使用者/群組] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="275fb-249">在 [選取使用者/群組] 對話方塊中，選擇 [BackupAdmin]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="275fb-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="275fb-250">在 [使用者] 中，使用者帳戶會使用「網域\使用者名稱」格式。</span><span class="sxs-lookup"><span data-stu-id="275fb-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="275fb-251">如果您想要使用不同的網域，請從 [網域] 清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="275fb-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![新增 BackupAdmin 使用者](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="275fb-253">按一下 [確定] 將選取的使用者新增至 [新增權限] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="275fb-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="275fb-254">您現在已找出使用者，請將使用者指派給角色。</span><span class="sxs-lookup"><span data-stu-id="275fb-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="275fb-255">在 [指派的角色] 中，從下拉式清單中選取 [BackupAdminRole]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="275fb-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![將使用者指派給角色](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="275fb-257">在 [通用權限] 面板的 [管理] 索引標籤上，新的使用者帳戶和相關聯的角色便會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="275fb-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="275fb-258">在 Azure 備份伺服器上建立 vCenter Server 認證</span><span class="sxs-lookup"><span data-stu-id="275fb-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="275fb-259">在將 VMware 伺服器新增至 Azure 備份伺服器之前，請先安裝 [Azure 備份伺服器的更新 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server)。</span><span class="sxs-lookup"><span data-stu-id="275fb-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="275fb-260">若要開啟 Azure 備份伺服器，請按兩下 Azure 備份伺服器桌面上的圖示。</span><span class="sxs-lookup"><span data-stu-id="275fb-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Azure 備份伺服器圖示](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="275fb-262">如果您在桌面上找不到此圖示，請從已安裝的應用程式清單開啟 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="275fb-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="275fb-263">Azure 備份伺服器應用程式名稱是「Microsoft Azure 備份」。</span><span class="sxs-lookup"><span data-stu-id="275fb-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="275fb-264">在 Azure 備份伺服器主控台中按一下 [管理]，按一下 [生產伺服器]，然後在工具功能區中按一下 [管理 VMware]。</span><span class="sxs-lookup"><span data-stu-id="275fb-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Azure 備份伺服器主控台](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="275fb-266">[管理認證] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="275fb-268">在 [管理認證] 對話方塊中，按一下 [新增] 以開啟 [新增認證] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="275fb-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="275fb-269">在 [新增認證] 對話方塊中，輸入新認證的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="275fb-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="275fb-270">然後，指定使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="275fb-270">Then specify the username and password.</span></span> <span data-ttu-id="275fb-271">我們會使用「Contoso Vcenter 認證」這個名稱來識別下一個程序中的認證。</span><span class="sxs-lookup"><span data-stu-id="275fb-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="275fb-272">所使用的使用者名稱和密碼請與 vCenter Server 所使用的相同。</span><span class="sxs-lookup"><span data-stu-id="275fb-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="275fb-273">如果 vCenter Server 和 Azure 備份伺服器不在相同網域中，請在 [使用者名稱] 中指定網域。</span><span class="sxs-lookup"><span data-stu-id="275fb-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Azure 備份伺服器的 [新增認證] 對話方塊](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="275fb-275">按一下 [新增] 將新的認證新增至 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="275fb-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="275fb-276">[管理認證] 對話方塊的清單中便會出現新的認證。</span><span class="sxs-lookup"><span data-stu-id="275fb-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Azure 備份伺服器的 [管理認證] 對話方塊](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="275fb-278">若要關閉 [管理認證] 對話方塊，請按一下右上角的 **X**。</span><span class="sxs-lookup"><span data-stu-id="275fb-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="275fb-279">將 vCenter Server 新增至 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="275fb-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="275fb-280">我們會使用「生產伺服器新增精靈」來對 Azure 備份伺服器新增 vCenter Server。</span><span class="sxs-lookup"><span data-stu-id="275fb-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="275fb-281">若要開啟「生產伺服器新增精靈」，請完成下列程序：</span><span class="sxs-lookup"><span data-stu-id="275fb-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="275fb-282">在 Azure 備份伺服器主控台中，依序按一下 [管理]、[生產伺服器] 及 [新增]。</span><span class="sxs-lookup"><span data-stu-id="275fb-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![開啟「生產伺服器新增精靈」](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="275fb-284">[生產伺服器新增精靈] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![生產伺服器新增精靈](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="275fb-286">在 [選取生產伺服器類型] 頁面上選取 [VMware 伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="275fb-287">在 [伺服器名稱/IP 位址] 中，指定 VMware 伺服器的完整網域名稱 (FQDN) 或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="275fb-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="275fb-288">如果所有 ESXi 伺服器均由相同的 vCenter 管理，您可以使用 vCenter 名稱。</span><span class="sxs-lookup"><span data-stu-id="275fb-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![指定 VMware 伺服器的 FQDN 或 IP 位址](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="275fb-290">在 [SSL 連接埠] 中，輸入用來與 VMware 伺服器通訊的連接埠。</span><span class="sxs-lookup"><span data-stu-id="275fb-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="275fb-291">使用連接埠 443，這是預設連接埠，除非您知道需要不同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="275fb-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="275fb-292">在 [指定認證] 中，選取您稍早建立的認證。</span><span class="sxs-lookup"><span data-stu-id="275fb-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![指定認證](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="275fb-294">按一下 [新增] 將 VMware 伺服器新增至 [已新增的 VMware 伺服器] 清單，然後按 [下一步] 移至精靈的下一頁。</span><span class="sxs-lookup"><span data-stu-id="275fb-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![新增 VMWare 伺服器和認證](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="275fb-296">在 [摘要] 頁面中，按一下 [新增] 將指定的 VMware 伺服器新增至 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="275fb-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![將 VMware 伺服器新增至 Azure 備份伺服器](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="275fb-298">VMware 伺服器備份是無代理程式的備份，因此新的伺服器立即就能完成新增。</span><span class="sxs-lookup"><span data-stu-id="275fb-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="275fb-299">[完成] 頁面會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="275fb-299">The **Finish** page shows you the results.</span></span>

  ![[完成] 頁面](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="275fb-301">若要將多個 vCenter Server 執行個體新增至 Azure 備份伺服器，請重複本節的先前步驟。</span><span class="sxs-lookup"><span data-stu-id="275fb-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="275fb-302">在將 vCenter Server 新增到 Azure 備份伺服器後，下一個步驟是建立保護群組。</span><span class="sxs-lookup"><span data-stu-id="275fb-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="275fb-303">保護群組可指定短期或長期保留的各種詳細資料，而且這是您定義及套用備份原則的地方。</span><span class="sxs-lookup"><span data-stu-id="275fb-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="275fb-304">備份原則包含執行備份的排程以及備份的內容。</span><span class="sxs-lookup"><span data-stu-id="275fb-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="275fb-305">設定保護群組</span><span class="sxs-lookup"><span data-stu-id="275fb-305">Configure a protection group</span></span>

<span data-ttu-id="275fb-306">如果您未曾使用 System Center Data Protection Manager 或 Azure 備份伺服器，請參閱[規劃磁碟備份](https://technet.microsoft.com/library/hh758026.aspx)，以準備您的硬體環境。</span><span class="sxs-lookup"><span data-stu-id="275fb-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="275fb-307">在您檢查過您有適當的儲存體後，請使用 [建立新保護群組] 精靈來新增 VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="275fb-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="275fb-308">在 Azure 備份伺服器主控台中，按一下 [保護]，然後按一下工具功能區中的 [新增]，以開啟 [建立新保護群組] 精靈。</span><span class="sxs-lookup"><span data-stu-id="275fb-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![開啟「建立新保護群組」精靈](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="275fb-310">[建立新保護群組] 精靈對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![[建立新保護群組] 精靈對話方塊](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="275fb-312">按 [下一步] 前往 [選取保護群組類型] 頁面。</span><span class="sxs-lookup"><span data-stu-id="275fb-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="275fb-313">在 [選取保護群組類型] 頁面上，選取 [伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="275fb-314">[選取群組成員] 頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="275fb-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="275fb-315">[選取群組成員] 頁面上會出現可用的成員和已選取的成員。</span><span class="sxs-lookup"><span data-stu-id="275fb-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="275fb-316">選取您想要保護的成員，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![選擇群組成員](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="275fb-318">當您選取成員時，如果您選取的資料夾包含其他資料夾或 VM，則您會同時選取這些資料夾和 VM。</span><span class="sxs-lookup"><span data-stu-id="275fb-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="275fb-319">在父資料夾中包含資料夾和 VM 稱為資料夾層級保護。</span><span class="sxs-lookup"><span data-stu-id="275fb-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="275fb-320">若要移除資料夾或 VM，請清除核取方塊。</span><span class="sxs-lookup"><span data-stu-id="275fb-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="275fb-321">如果 VM 或包含 VM 的資料夾已受到 Azure 保護，您就無法再次選取該 VM。</span><span class="sxs-lookup"><span data-stu-id="275fb-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="275fb-322">也就是說，VM 在受到 Azure 保護後就無法再次受到保護，這可防止針對一部 VM 建立重複的復原點。</span><span class="sxs-lookup"><span data-stu-id="275fb-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="275fb-323">如果您想要查看哪個 Azure 備份伺服器執行個體已經保護成員，請指向該成員以查看保護伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="275fb-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="275fb-324">在 [選取資料保護方式] 頁面上，輸入保護群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="275fb-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="275fb-325">選取短期保護 (磁碟) 和線上保護。</span><span class="sxs-lookup"><span data-stu-id="275fb-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="275fb-326">如果您想要使用線上保護 (Azure)，必須使用磁碟的短期保護。</span><span class="sxs-lookup"><span data-stu-id="275fb-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="275fb-327">按 [下一步] 以繼續進行短期保護範圍。</span><span class="sxs-lookup"><span data-stu-id="275fb-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![選擇資料保護方式](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="275fb-329">在 [指定短期目標] 頁面上，針對 [保留範圍]，指定您想要保留復原點「儲存到磁碟」的天數。</span><span class="sxs-lookup"><span data-stu-id="275fb-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="275fb-330">如果您想要變更取得復原點的時間和天數，請按一下 [修改]。</span><span class="sxs-lookup"><span data-stu-id="275fb-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="275fb-331">短期復原點是完整備份。</span><span class="sxs-lookup"><span data-stu-id="275fb-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="275fb-332">而不是增量備份。</span><span class="sxs-lookup"><span data-stu-id="275fb-332">They are not incremental backups.</span></span> <span data-ttu-id="275fb-333">當您滿意短期目標時，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![指定短期目標](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="275fb-335">在 [檢閱磁碟配置] 頁面上，檢閱並視需要修改 VM 的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="275fb-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="275fb-336">建議的磁碟配置是以 [指定短期目標] 頁面中指定的保留範圍、工作負載類型及受保護的資料大小 (可在步驟 3 中找到) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="275fb-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="275fb-337">**資料大小：**保護群組中的資料大小。</span><span class="sxs-lookup"><span data-stu-id="275fb-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="275fb-338">**磁碟空間：**保護群組的建議磁碟空間數量。</span><span class="sxs-lookup"><span data-stu-id="275fb-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="275fb-339">如果您想要修改此設定，您配置的總空間應該稍微大於您預估每個資料來源將成長的數量。</span><span class="sxs-lookup"><span data-stu-id="275fb-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="275fb-340">**共置資料：**如果您開啟共置功能，受保護的多個資料來源可以對應至單一複本和復原點磁碟區。</span><span class="sxs-lookup"><span data-stu-id="275fb-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="275fb-341">不支援所有工作負載的共置。</span><span class="sxs-lookup"><span data-stu-id="275fb-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="275fb-342">**自動成長：**如果您開啟此設定，而且受保護群組中的資料成長超過初始配置，則 System Center Data Protection Manager 會嘗試增加 25% 的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="275fb-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="275fb-343">**儲存集區詳細資料：**顯示儲存體集區的狀態，包括總計和剩餘的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="275fb-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![檢閱磁碟配置](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="275fb-345">當您滿意空間配置時，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="275fb-346">在 [選擇複本的建立方式] 頁面上，指定您要在 Azure 備份伺服器上產生受保護資料之初始副本或複本的方式。</span><span class="sxs-lookup"><span data-stu-id="275fb-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="275fb-347">預設值是 [自動透過網路] 和 [立即]。</span><span class="sxs-lookup"><span data-stu-id="275fb-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="275fb-348">如果您使用預設值，建議您指定離峰時間。</span><span class="sxs-lookup"><span data-stu-id="275fb-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="275fb-349">選擇 [稍後] 並指定日期與時間。</span><span class="sxs-lookup"><span data-stu-id="275fb-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="275fb-350">對於大量資料或較差的網路狀況，請考慮使用卸除式媒體來離線複寫資料。</span><span class="sxs-lookup"><span data-stu-id="275fb-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="275fb-351">做好選擇後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-351">After you have made your choices, click **Next**.</span></span>

    ![選擇複本的建立方式](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="275fb-353">在 [一致性檢查選項] 頁面上，選取如何及何時自動執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="275fb-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="275fb-354">當複本資料變得不一致時，或依據設定的排程，您可以執行一致性檢查。</span><span class="sxs-lookup"><span data-stu-id="275fb-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="275fb-355">如果您不想設定自動一致性檢查，可以執行手動檢查。</span><span class="sxs-lookup"><span data-stu-id="275fb-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="275fb-356">在 Azure 備份伺服器主控台的 [保護] 區域，以滑鼠右鍵按一下保護群組，然後選取 [執行一致性檢查]。</span><span class="sxs-lookup"><span data-stu-id="275fb-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="275fb-357">按 [下一步] 移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="275fb-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="275fb-358">在 [指定線上保護資料] 頁面上，選取您想要保護的一或多個資料來源。</span><span class="sxs-lookup"><span data-stu-id="275fb-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="275fb-359">您可以個別地選取成員，或按一下 [全選] 來選擇所有成員。</span><span class="sxs-lookup"><span data-stu-id="275fb-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="275fb-360">在選擇成員後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-360">After you choose the members, click **Next**.</span></span>

    ![指定線上保護資料](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="275fb-362">在 [指定線上備份排程] 頁面上，指定用來從磁碟備份產生復原點的排程。</span><span class="sxs-lookup"><span data-stu-id="275fb-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="275fb-363">復原點在產生後會傳輸至 Azure 中的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="275fb-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="275fb-364">當您滿意線上備份排程時，請 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![指定線上備份排程](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="275fb-366">在 [指定線上保留原則] 頁面上，指出您要在 Azure 中保留備份資料的時間長度。</span><span class="sxs-lookup"><span data-stu-id="275fb-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="275fb-367">在定義原則之後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="275fb-367">After the policy is defined, click **Next**.</span></span>

    ![指定線上保留期原則](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="275fb-369">您可以在 Azure 中保留資料的時間長度沒有限制。</span><span class="sxs-lookup"><span data-stu-id="275fb-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="275fb-370">當您在 Azure 中儲存復原點資料時，唯一的限制是每個受保護的執行個體不能有超過 9999 個復原點。</span><span class="sxs-lookup"><span data-stu-id="275fb-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="275fb-371">在此範例中，受保護的執行個體是 VMware 伺服器。</span><span class="sxs-lookup"><span data-stu-id="275fb-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="275fb-372">在 [摘要] 頁面上檢閱保護群組成員和設定的詳細資料，然後按一下 [建立群組]。</span><span class="sxs-lookup"><span data-stu-id="275fb-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![保護群組成員和設定的摘要](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="275fb-374">後續步驟</span><span class="sxs-lookup"><span data-stu-id="275fb-374">Next steps</span></span>
<span data-ttu-id="275fb-375">如果您使用 Azure 備份伺服器來保護 VMware 工作負載，對於要如何使用 Azure 備份伺服器來協助保護 [Microsoft Exchange Server](./backup-azure-exchange-mabs.md)、[Microsoft SharePoint 伺服器陣列](./backup-azure-backup-sharepoint-mabs.md)或 [SQL Server 資料庫](./backup-azure-sql-mabs.md)，想必您會感到興趣。</span><span class="sxs-lookup"><span data-stu-id="275fb-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="275fb-376">如需註冊代理程式、設定保護群組或備份作業等問題的相關資訊，請參閱[針對 Azure 備份伺服器進行疑難排解](./backup-azure-mabs-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="275fb-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
