---
title: " 在 Azure Site Recovery 中管理組態伺服器 | Microsoft Doc"
description: "本文說明如何 tooset 和管理組態伺服器。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="e6508-103">管理組態伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-103">Manage a Configuration Server</span></span>

<span data-ttu-id="e6508-104">設定伺服器將充當 hello 站台復原服務與您在內部部署基礎結構之間的協調者。</span><span class="sxs-lookup"><span data-stu-id="e6508-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="e6508-105">本文說明如何設定、 設定和管理 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6508-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6508-106">Prerequisites</span></span>
<span data-ttu-id="e6508-107">hello 下面是 hello 最低硬體、 軟體和組態伺服器的網路所需設定 tooset。</span><span class="sxs-lookup"><span data-stu-id="e6508-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e6508-108">[容量規劃](site-recovery-capacity-planner.md)是您部署與設定的組態伺服器 hello 該套件的重要步驟 tooensure 負載需求。</span><span class="sxs-lookup"><span data-stu-id="e6508-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="e6508-109">深入了解[組態伺服器的大小需求](#sizing-requirements-for-a-configuration-server)。</span><span class="sxs-lookup"><span data-stu-id="e6508-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="e6508-110">下載 hello 組態伺服器軟體</span><span class="sxs-lookup"><span data-stu-id="e6508-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="e6508-111">登入 toohello Azure 入口網站，並瀏覽 tooyour 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="e6508-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="e6508-112">瀏覽過**Site Recovery 基礎結構** > **設定伺服器**（底下的 VMware & 實體機器)。</span><span class="sxs-lookup"><span data-stu-id="e6508-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="e6508-114">按一下 hello **+ 伺服器** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6508-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="e6508-115">在 hello**新增伺服器**頁面上，按一下 hello 下載按鈕 toodownload hello 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="e6508-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="e6508-116">您需要此金鑰期間 hello 組態伺服器安裝 tooregister 它與 Azure Site Recovery 服務。</span><span class="sxs-lookup"><span data-stu-id="e6508-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="e6508-117">按一下 hello**下載 hello Microsoft Azure Site Recovery 統一的安裝**連結 toodownload hello 最新版本的 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![下載頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="e6508-119">可以直接從下載最新版本的組態伺服器 hello [Microsoft Download Center 下載頁面](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="e6508-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="e6508-120">從 GUI 安裝和註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="e6508-121">使用命令列安裝和註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="e6508-122">範例用法</span><span class="sxs-lookup"><span data-stu-id="e6508-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="e6508-123">組態伺服器安裝程式命令列引數。</span><span class="sxs-lookup"><span data-stu-id="e6508-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="e6508-124">建立 MySql 認證檔案</span><span class="sxs-lookup"><span data-stu-id="e6508-124">Create a MySql credentials file</span></span>
<span data-ttu-id="e6508-125">MySQLCredsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="e6508-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e6508-126">建立使用下列格式，並將它傳遞做為輸入 MySQLCredsFilePath 參數 hello hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6508-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="e6508-127">建立 Proxy 設定組態檔案</span><span class="sxs-lookup"><span data-stu-id="e6508-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="e6508-128">ProxySettingsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="e6508-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e6508-129">建立使用下列格式，並將它傳遞做為輸入 ProxySettingsFilePath 參數 hello hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e6508-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="e6508-130">修改組態伺服器的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="e6508-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="e6508-131">登入 tooyour 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e6508-132">啟動 hello cspsconfigtool.exe 上使用 hello 快顯程式。</span><span class="sxs-lookup"><span data-stu-id="e6508-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="e6508-133">按一下 hello**保存庫註冊** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6508-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="e6508-134">從 hello 入口網站下載新的保存庫註冊檔，並提供它當做輸入的 toohello 工具。</span><span class="sxs-lookup"><span data-stu-id="e6508-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="e6508-136">提供 hello 新 Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6508-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="e6508-137">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="e6508-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="e6508-138">執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="e6508-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="e6508-139">如果您有向外延展處理伺服器附加 toothis 組態伺服器，您需要[hello 向外延展程序的所有伺服器上，請修正 hello proxy 設定](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server)部署中。</span><span class="sxs-lookup"><span data-stu-id="e6508-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="e6508-140">重新註冊組態伺服器 hello 與相同的復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="e6508-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="e6508-141">登入 tooyour 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="e6508-142">啟動 hello cspsconfigtool.exe 使用 hello 捷徑在桌面上。</span><span class="sxs-lookup"><span data-stu-id="e6508-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="e6508-143">按一下 hello**保存庫註冊** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6508-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="e6508-144">從 hello 入口網站下載新的登錄檔案，並提供它當做輸入的 toohello 工具。</span><span class="sxs-lookup"><span data-stu-id="e6508-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="e6508-145">![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="e6508-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="e6508-146">提供 hello Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6508-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="e6508-147">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="e6508-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="e6508-148">執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="e6508-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="e6508-149">如果您有向外延展處理伺服器附加 toothis 組態伺服器，您需要[重新註冊所有 hello 向外延展處理伺服器](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server)部署中。</span><span class="sxs-lookup"><span data-stu-id="e6508-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="e6508-150">向不同的復原服務保存庫註冊組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="e6508-151">登入 tooyour 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e6508-152">系統管理員命令提示字元中，從執行 hello 命令</span><span class="sxs-lookup"><span data-stu-id="e6508-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="e6508-153">啟動 hello cspsconfigtool.exe 上使用 hello 快顯程式。</span><span class="sxs-lookup"><span data-stu-id="e6508-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="e6508-154">按一下 hello**保存庫註冊** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6508-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="e6508-155">從 hello 入口網站下載新的登錄檔案，並提供它當做輸入的 toohello 工具。</span><span class="sxs-lookup"><span data-stu-id="e6508-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="e6508-157">提供 hello Proxy 伺服器詳細資料，並按一下 hello**註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6508-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="e6508-158">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="e6508-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="e6508-159">執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="e6508-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="e6508-160">解除委任組態伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="e6508-161">在開始解除委任設定伺服器之前，請確定 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="e6508-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="e6508-162">停用保護此組態伺服器下的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e6508-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="e6508-163">取消關聯從 hello 組態伺服器的所有複寫原則。</span><span class="sxs-lookup"><span data-stu-id="e6508-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="e6508-164">刪除所有相關聯的 toohello 組態伺服器的 Vcenter 伺服器 /vsphere 主機。</span><span class="sxs-lookup"><span data-stu-id="e6508-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="e6508-165">從 Azure 入口網站刪除 hello 組態伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="e6508-166">在 Azure 入口網站，瀏覽過**Site Recovery 基礎結構** > **設定伺服器**功能表 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="e6508-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="e6508-167">按一下您想 toodecommission 組態伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="e6508-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="e6508-168">在 hello 組態伺服器的詳細資料頁面上，按一下 hello 刪除 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6508-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="e6508-170">按一下**是**tooconfirm hello hello 伺服器刪除。</span><span class="sxs-lookup"><span data-stu-id="e6508-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="e6508-171">如果您有任何虛擬機器、 複寫原則或 vCenter 伺服器 /vsphere 主機與這個組態伺服器相關聯，您無法刪除 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="e6508-172">您嘗試 toodelete hello 保存庫之前，請刪除這些實體。</span><span class="sxs-lookup"><span data-stu-id="e6508-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="e6508-173">解除安裝 hello 組態伺服器軟體和其相依性</span><span class="sxs-lookup"><span data-stu-id="e6508-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="e6508-174">如果您計劃 tooreuse hello 與 Azure Site Recovery 的組態伺服器一次，然後您可以略過 toostep 4 直接</span><span class="sxs-lookup"><span data-stu-id="e6508-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="e6508-175">系統管理員身分登入 toohello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="e6508-176">開啟 [控制台] > [程式] > [解除安裝程式]</span><span class="sxs-lookup"><span data-stu-id="e6508-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="e6508-177">解除安裝 hello 下列順序中的 hello 程式：</span><span class="sxs-lookup"><span data-stu-id="e6508-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="e6508-178">Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="e6508-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="e6508-179">Microsoft Azure Site Recovery Mobility Service/主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="e6508-180">Microsoft Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="e6508-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="e6508-181">Microsoft Azure Site Recovery 組態伺服器/處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="e6508-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="e6508-182">Microsoft Azure Site Recovery 組態伺服器相依性</span><span class="sxs-lookup"><span data-stu-id="e6508-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="e6508-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="e6508-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="e6508-184">執行下列命令從 hello 和系統管理員命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="e6508-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="e6508-185">更新組態伺服器安全通訊端層 (SSL) 憑證</span><span class="sxs-lookup"><span data-stu-id="e6508-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="e6508-186">設定伺服器 hello 可以協調 hello 活動 hello 行動服務處理序伺服器的內建網頁伺服器與主要目標伺服器連接 toohello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="e6508-187">hello 組態伺服器的網頁伺服器會使用 SSL 憑證 tooauthenticate 其用戶端。</span><span class="sxs-lookup"><span data-stu-id="e6508-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="e6508-188">此憑證有三年後的到期，而且可以使用下列方法 hello 隨時更新：</span><span class="sxs-lookup"><span data-stu-id="e6508-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="e6508-189">只有在 9.4.XXXX.X 或更新版本上才會履行憑證到期日。</span><span class="sxs-lookup"><span data-stu-id="e6508-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="e6508-190">升級所有 hello Azure Site Recovery 元件 （組態伺服器、 處理序伺服器、 主要目標伺服器、 行動服務） 開始 hello 更新憑證的工作流程之前。</span><span class="sxs-lookup"><span data-stu-id="e6508-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="e6508-191">在 hello Azure 入口網站中，瀏覽 tooyour 保存庫 > Site Recovery 基礎結構 > 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="e6508-192">按一下您需要 toorenew hello 組態伺服器 hello 的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="e6508-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="e6508-193">在 hello 設定伺服器健全狀況，您可以看到 hello hello SSL 憑證的到期日。</span><span class="sxs-lookup"><span data-stu-id="e6508-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="e6508-194">依序按一下 hello 更新 hello 憑證**更新憑證**動作 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="e6508-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="e6508-196">安全通訊端層憑證到期警告</span><span class="sxs-lookup"><span data-stu-id="e6508-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="e6508-197">hello 2016 年之前所發生的所有安裝的 SSL 憑證的有效設定 tooone 年。</span><span class="sxs-lookup"><span data-stu-id="e6508-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="e6508-198">您已開始看到 hello Azure 入口網站中顯示的憑證到期通知。</span><span class="sxs-lookup"><span data-stu-id="e6508-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="e6508-199">如果 hello 組態伺服器的 SSL 憑證將會在 hello tooexpire 接下來的兩個月，hello 服務會啟動通知的使用者經由 hello Azure 入口網站 （& s） （您需要訂閱 toobe tooAzure Site Recovery 通知） 的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e6508-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="e6508-200">您會開始在 hello 保存庫資源 頁面上看到通知橫幅。</span><span class="sxs-lookup"><span data-stu-id="e6508-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![憑證通知](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="e6508-202">按一下 hello 憑證到期日的 hello 橫幅 tooget 其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e6508-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![憑證詳細資料](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="e6508-204">如果您不是看到 [立即更新] 按鈕，而是 [立即升級] 按鈕，</span><span class="sxs-lookup"><span data-stu-id="e6508-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="e6508-205">這表示您的環境中尚未升級的 too9.4.xxxx.x 或更高版本的部分元件。</span><span class="sxs-lookup"><span data-stu-id="e6508-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="e6508-206">組態伺服器的大小需求</span><span class="sxs-lookup"><span data-stu-id="e6508-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="e6508-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e6508-207">**CPU**</span></span> | <span data-ttu-id="e6508-208">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="e6508-208">**Memory**</span></span> | <span data-ttu-id="e6508-209">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="e6508-209">**Cache disk size**</span></span> | <span data-ttu-id="e6508-210">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="e6508-210">**Data change rate**</span></span> | <span data-ttu-id="e6508-211">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="e6508-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e6508-212">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e6508-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e6508-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="e6508-213">16 GB</span></span> |<span data-ttu-id="e6508-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="e6508-214">300 GB</span></span> |<span data-ttu-id="e6508-215">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="e6508-215">500 GB or less</span></span> |<span data-ttu-id="e6508-216">複寫少於 100 部電腦。</span><span class="sxs-lookup"><span data-stu-id="e6508-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="e6508-217">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e6508-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e6508-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="e6508-218">18 GB</span></span> |<span data-ttu-id="e6508-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="e6508-219">600 GB</span></span> |<span data-ttu-id="e6508-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="e6508-220">500 GB too1 TB</span></span> |<span data-ttu-id="e6508-221">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="e6508-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="e6508-222">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e6508-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e6508-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="e6508-223">32 GB</span></span> |<span data-ttu-id="e6508-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="e6508-224">1 TB</span></span> |<span data-ttu-id="e6508-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="e6508-225">1 TB too2 TB</span></span> |<span data-ttu-id="e6508-226">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="e6508-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="e6508-227">如果您每日的資料變換量超過 2 TB，或您計劃 tooreplicate 200 個以上的虛擬機器，則建議 toodeploy 額外的處理序伺服器 tooload 平衡 hello 複寫流量。</span><span class="sxs-lookup"><span data-stu-id="e6508-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="e6508-228">深入了解如何 toodeploy 向外延展處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6508-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="e6508-229">常見問題</span><span class="sxs-lookup"><span data-stu-id="e6508-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
