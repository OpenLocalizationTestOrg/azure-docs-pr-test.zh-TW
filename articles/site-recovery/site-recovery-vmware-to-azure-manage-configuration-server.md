---
title: " 在 Azure Site Recovery 中管理組態伺服器 | Microsoft Doc"
description: "本文說明如何設定和管理組態伺服器。"
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="1d201-103">管理組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-103">Manage a Configuration Server</span></span>

<span data-ttu-id="1d201-104">組態伺服器做為 Site Recovery 服務和您的內部部署基礎結構之間的協調者。</span><span class="sxs-lookup"><span data-stu-id="1d201-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="1d201-105">本文說明如何安裝、設定及管理組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d201-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d201-106">Prerequisites</span></span>
<span data-ttu-id="1d201-107">下列為安裝組態伺服器所需的最基本硬體、軟體及網路設定。</span><span class="sxs-lookup"><span data-stu-id="1d201-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1d201-108">[容量規劃](site-recovery-capacity-planner.md)是確保以符合負載需求的設定來部署組態伺服器的重要步驟。</span><span class="sxs-lookup"><span data-stu-id="1d201-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="1d201-109">深入了解[組態伺服器的大小需求](#sizing-requirements-for-a-configuration-server)。</span><span class="sxs-lookup"><span data-stu-id="1d201-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="1d201-110">下載組態伺服器軟體</span><span class="sxs-lookup"><span data-stu-id="1d201-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="1d201-111">登入 Azure 入口網站並瀏覽至您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1d201-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="1d201-112">瀏覽至 [Site Recovery 基礎結構] > [組態伺服器] \(位於 [適用於 VMware 和實體機器] 底下)。</span><span class="sxs-lookup"><span data-stu-id="1d201-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="1d201-114">按一下 [+伺服器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d201-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="1d201-115">在 [新增伺服器] 頁面上，按一下 [下載] 按鈕，下載註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d201-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="1d201-116">在組態伺服器安裝期間，您需要使用此金鑰向 Azure Site Recovery 服務註冊它。</span><span class="sxs-lookup"><span data-stu-id="1d201-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="1d201-117">按一下 [下載 Microsoft Azure Site Recovery 整合安裝] 連結，以下載最新版本的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![下載頁面](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="1d201-119">您可以直接從 [Microsoft 下載中心下載頁面](http://aka.ms/unifiedsetup)，下載最新版本的組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="1d201-120">從 GUI 安裝和註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="1d201-121">使用命令列安裝和註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="1d201-122">範例用法</span><span class="sxs-lookup"><span data-stu-id="1d201-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="1d201-123">組態伺服器安裝程式命令列引數。</span><span class="sxs-lookup"><span data-stu-id="1d201-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="1d201-124">建立 MySql 認證檔案</span><span class="sxs-lookup"><span data-stu-id="1d201-124">Create a MySql credentials file</span></span>
<span data-ttu-id="1d201-125">MySQLCredsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="1d201-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="1d201-126">使用下列格式建立檔案，並將它以輸入 MySQLCredsFilePath 參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="1d201-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="1d201-127">建立 Proxy 設定組態檔案</span><span class="sxs-lookup"><span data-stu-id="1d201-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="1d201-128">ProxySettingsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="1d201-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="1d201-129">使用下列格式建立檔案，並將它以輸入 ProxySettingsFilePath 參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="1d201-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="1d201-130">修改組態伺服器的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="1d201-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="1d201-131">登入您的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="1d201-132">使用捷徑啟動 cspsconfigtool.exe。</span><span class="sxs-lookup"><span data-stu-id="1d201-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="1d201-133">按一下 [保存庫註冊] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1d201-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="1d201-134">從入口網站下載新的保存庫註冊檔案，並當做輸入提供給工具。</span><span class="sxs-lookup"><span data-stu-id="1d201-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="1d201-136">提供新的 Proxy 伺服器詳細資料，然後按一下 [註冊] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d201-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="1d201-137">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="1d201-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="1d201-138">執行下列命令</span><span class="sxs-lookup"><span data-stu-id="1d201-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="1d201-139">如果您有連結至此組態伺服器的相應放大處理序伺服器，您需要在部署中[修正所有相應放大處理序伺服器上的 Proxy 設定](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server)。</span><span class="sxs-lookup"><span data-stu-id="1d201-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="1d201-140">向相同的復原服務保存庫註冊組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="1d201-141">登入您的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="1d201-142">使用桌面上的捷徑啟動 cspsconfigtool.exe。</span><span class="sxs-lookup"><span data-stu-id="1d201-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="1d201-143">按一下 [保存庫註冊] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1d201-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="1d201-144">從入口網站下載新的註冊檔案，並當做輸入提供給工具。</span><span class="sxs-lookup"><span data-stu-id="1d201-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="1d201-145">![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="1d201-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="1d201-146">提供 Proxy 伺服器詳細資料，然後按一下 [註冊] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d201-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="1d201-147">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="1d201-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="1d201-148">執行下列命令</span><span class="sxs-lookup"><span data-stu-id="1d201-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="1d201-149">如果您有連結至此組態伺服器的相應放大處理序伺服器，您需要在部署中[重新註冊所有相應放大處理序伺服器](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server)。</span><span class="sxs-lookup"><span data-stu-id="1d201-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="1d201-150">向不同的復原服務保存庫註冊組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="1d201-151">登入您的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="1d201-152">從系統管理命令提示字元中，執行命令</span><span class="sxs-lookup"><span data-stu-id="1d201-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="1d201-153">使用捷徑啟動 cspsconfigtool.exe。</span><span class="sxs-lookup"><span data-stu-id="1d201-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="1d201-154">按一下 [保存庫註冊] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1d201-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="1d201-155">從入口網站下載新的註冊檔案，並當做輸入提供給工具。</span><span class="sxs-lookup"><span data-stu-id="1d201-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![註冊組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="1d201-157">提供 Proxy 伺服器詳細資料，然後按一下 [註冊] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d201-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="1d201-158">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="1d201-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="1d201-159">執行下列命令</span><span class="sxs-lookup"><span data-stu-id="1d201-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="1d201-160">解除委任組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="1d201-161">在開始解除委任組態伺服器之前，請確認下列事項。</span><span class="sxs-lookup"><span data-stu-id="1d201-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="1d201-162">停用保護此組態伺服器下的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1d201-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="1d201-163">解除所有複寫原則與組態伺服器的關聯。</span><span class="sxs-lookup"><span data-stu-id="1d201-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="1d201-164">刪除與組態伺服器相關聯的所有 VCenters 伺服器/vSphere 主機。</span><span class="sxs-lookup"><span data-stu-id="1d201-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="1d201-165">從 Azure 入口網站刪除組態伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="1d201-166">在 Azure 入口網站中，從 [保存庫] 功能表瀏覽至 [Site Recovery 基礎結構] > [組態伺服器]。</span><span class="sxs-lookup"><span data-stu-id="1d201-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="1d201-167">按一下您想要解除委任的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="1d201-168">在組態伺服器的詳細資料頁面上，按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d201-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="1d201-170">按一下 [是] 以確認刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="1d201-171">如果您有任何虛擬機器、複寫原則或 vCenter 伺服器/vSphere 主機與此組態伺服器相關聯，則無法刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="1d201-172">嘗試刪除保存庫之前，請先刪除這些實體。</span><span class="sxs-lookup"><span data-stu-id="1d201-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="1d201-173">解除安裝組態伺服器軟體和其相依性</span><span class="sxs-lookup"><span data-stu-id="1d201-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="1d201-174">如果您打算再次搭配 Azure Site Recovery 來重複使用組態伺服器，您可以直接跳至步驟 4</span><span class="sxs-lookup"><span data-stu-id="1d201-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="1d201-175">以系統管理員身分登入組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="1d201-176">開啟 [控制台] > [程式集] > [解除安裝程式]</span><span class="sxs-lookup"><span data-stu-id="1d201-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="1d201-177">依下列順序將程式解除安裝：</span><span class="sxs-lookup"><span data-stu-id="1d201-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="1d201-178">Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="1d201-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="1d201-179">Microsoft Azure Site Recovery Mobility Service/主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="1d201-180">Microsoft Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="1d201-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="1d201-181">Microsoft Azure Site Recovery 組態伺服器/處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="1d201-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="1d201-182">Microsoft Azure Site Recovery 組態伺服器相依性</span><span class="sxs-lookup"><span data-stu-id="1d201-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="1d201-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="1d201-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="1d201-184">從系統管理命令提示字元中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="1d201-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="1d201-185">更新組態伺服器安全通訊端層 (SSL) 憑證</span><span class="sxs-lookup"><span data-stu-id="1d201-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="1d201-186">組態伺服器有內建的 Web 伺服器，可協調連線至組態伺服器的行動服務、處理序伺服器和主要目標伺服器的活動。</span><span class="sxs-lookup"><span data-stu-id="1d201-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="1d201-187">組態伺服器的 Web 伺服器使用 SSL 憑證來驗證其用戶端。</span><span class="sxs-lookup"><span data-stu-id="1d201-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="1d201-188">此憑證三年期滿，可隨時使用下列方法更新︰</span><span class="sxs-lookup"><span data-stu-id="1d201-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="1d201-189">只有在 9.4.XXXX.X 或更新版本上才會履行憑證到期日。</span><span class="sxs-lookup"><span data-stu-id="1d201-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="1d201-190">開始「更新憑證」工作流程之前，請升級所有 Azure Site Recovery 元件 (組態伺服器、處理序伺服器、主要目標伺服器、行動服務)。</span><span class="sxs-lookup"><span data-stu-id="1d201-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="1d201-191">在 Azure 入口網站上，瀏覽至 [保存庫] > [Site Recovery 基礎結構] > [組態伺服器]。</span><span class="sxs-lookup"><span data-stu-id="1d201-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="1d201-192">按一下您需要更新 SSL 憑證的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="1d201-193">在 [組態伺服器健全狀況] 下，您可以看到 SSL 憑證的到期日。</span><span class="sxs-lookup"><span data-stu-id="1d201-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="1d201-194">按一下 [更新憑證] 動作來更新憑證，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="1d201-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![刪除組態伺服器](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="1d201-196">安全通訊端層憑證到期警告</span><span class="sxs-lookup"><span data-stu-id="1d201-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="1d201-197">對於 2016 年 5 月之前完成的所有安裝，SSL 憑證的有效性設定為一年。</span><span class="sxs-lookup"><span data-stu-id="1d201-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="1d201-198">您已開始看到 Azure 入口網站中顯示憑證到期通知。</span><span class="sxs-lookup"><span data-stu-id="1d201-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="1d201-199">如果組態伺服器的 SSL 憑證將於接下來兩個月之內到期，服務會開始透過 Azure 入口網站和電子郵件來通知使用者 (您需要訂閱 Azure Site Recovery 通知)。</span><span class="sxs-lookup"><span data-stu-id="1d201-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="1d201-200">您開始在保存庫的資源頁面上看到通知橫幅。</span><span class="sxs-lookup"><span data-stu-id="1d201-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![憑證通知](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="1d201-202">按一下橫幅，以取得憑證到期日的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1d201-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![憑證詳細資料](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="1d201-204">如果您不是看到 [立即更新] 按鈕，而是 [立即升級] 按鈕，</span><span class="sxs-lookup"><span data-stu-id="1d201-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="1d201-205">這表示您的環境中有些元件尚未升級至 9.4.xxxx.x 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1d201-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="1d201-206">組態伺服器的大小需求</span><span class="sxs-lookup"><span data-stu-id="1d201-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="1d201-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="1d201-207">**CPU**</span></span> | <span data-ttu-id="1d201-208">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="1d201-208">**Memory**</span></span> | <span data-ttu-id="1d201-209">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="1d201-209">**Cache disk size**</span></span> | <span data-ttu-id="1d201-210">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="1d201-210">**Data change rate**</span></span> | <span data-ttu-id="1d201-211">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="1d201-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1d201-212">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="1d201-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="1d201-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="1d201-213">16 GB</span></span> |<span data-ttu-id="1d201-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="1d201-214">300 GB</span></span> |<span data-ttu-id="1d201-215">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="1d201-215">500 GB or less</span></span> |<span data-ttu-id="1d201-216">複寫少於 100 部電腦。</span><span class="sxs-lookup"><span data-stu-id="1d201-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="1d201-217">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="1d201-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="1d201-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="1d201-218">18 GB</span></span> |<span data-ttu-id="1d201-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="1d201-219">600 GB</span></span> |<span data-ttu-id="1d201-220">500 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="1d201-220">500 GB to 1 TB</span></span> |<span data-ttu-id="1d201-221">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="1d201-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="1d201-222">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="1d201-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="1d201-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="1d201-223">32 GB</span></span> |<span data-ttu-id="1d201-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="1d201-224">1 TB</span></span> |<span data-ttu-id="1d201-225">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="1d201-225">1 TB to 2 TB</span></span> |<span data-ttu-id="1d201-226">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="1d201-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="1d201-227">如果您每日資料變換量超過 2 TB，或您打算複寫 200 個以上的虛擬機器，建議部署額外的處理序伺服器，以平衡複寫流量的負載。</span><span class="sxs-lookup"><span data-stu-id="1d201-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="1d201-228">深入了解如何部署相應放大處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d201-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="1d201-229">常見問題</span><span class="sxs-lookup"><span data-stu-id="1d201-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
