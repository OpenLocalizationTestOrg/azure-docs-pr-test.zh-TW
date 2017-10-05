---
title: " 在 Azure Site Recovery 中管理相應放大處理序伺服器 | Microsoft Doc"
description: "本文說明如何在 Azure Site Recovery 中設定並管理相應放大處理序伺服器。"
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
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="9a94b-103">管理相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="9a94b-104">相應放大處理序伺服器是 Site Recovery 服務和您的內部部署基礎結構之間的資料傳輸協調者。</span><span class="sxs-lookup"><span data-stu-id="9a94b-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="9a94b-105">本文說明如何設定、配置及管理相應放大處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a94b-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="9a94b-106">Prerequisites</span></span>
<span data-ttu-id="9a94b-107">下列為設定相應放大處理序伺服器所需的建議硬體、軟體及網路組態。</span><span class="sxs-lookup"><span data-stu-id="9a94b-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="9a94b-108">[容量計劃](site-recovery-capacity-planner.md)是確保能以符合負載需求的設定部署相應放大處理序伺服器的重要步驟。</span><span class="sxs-lookup"><span data-stu-id="9a94b-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="9a94b-109">請在[相應放大處理序伺服器的調整特性](#sizing-requirements-for-a-configuration-server)中閱讀更多資訊。</span><span class="sxs-lookup"><span data-stu-id="9a94b-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="9a94b-110">下載相應放大處理序伺服器軟體</span><span class="sxs-lookup"><span data-stu-id="9a94b-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="9a94b-111">登入 Azure 入口網站並瀏覽至您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9a94b-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="9a94b-112">瀏覽至 **Site Recovery 基礎結構** > **設定伺服器** \(位於 [適用於 VMware 和實體機器] 底下)。</span><span class="sxs-lookup"><span data-stu-id="9a94b-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="9a94b-113">選取您的設定伺服器以切入設定伺服器的詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="9a94b-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="9a94b-114">按一下 [+ 處理序伺服器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a94b-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="9a94b-115">在 [新增處理序伺服器] 頁面中，選取 [選擇您要部署處理序伺服器的位置] 下拉式清單中的 [於內部部署部署相應放大處理序伺服器] 選項。</span><span class="sxs-lookup"><span data-stu-id="9a94b-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="9a94b-117">按一下 [下載 Microsoft Azure Site Recovery 整合安裝] 連結，以下載相應放大處理序伺服器安裝的最新版本。</span><span class="sxs-lookup"><span data-stu-id="9a94b-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="9a94b-118">您相應放大處理序伺服器的版本，應該要等於或小於您環境中執行的設定伺服器版本。</span><span class="sxs-lookup"><span data-stu-id="9a94b-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="9a94b-119">一個確保版本相容性的簡單方式，便是使用和您最近用來安裝/更新設定伺服器的安裝程式具有相同位元數的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="9a94b-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="9a94b-120">從 GUI 安裝並註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="9a94b-121">如果您必須將您的部署相應放大至超過 200 部來源機器，或是總計超過 2 TB 的每日變換率，您便需要額外的處理序伺服器來處理流量。</span><span class="sxs-lookup"><span data-stu-id="9a94b-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="9a94b-122">檢查[處理伺服器的大小建議](#size-recommendations-for-the-process-server)，然後遵循這些指示來設定處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="9a94b-123">設定伺服器之後，請移轉來源機器以便使用它。</span><span class="sxs-lookup"><span data-stu-id="9a94b-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="9a94b-124">使用命令列安裝並註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="9a94b-125">範例用法</span><span class="sxs-lookup"><span data-stu-id="9a94b-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="9a94b-126">相應放大處理序伺服器安裝程式命令列引數。</span><span class="sxs-lookup"><span data-stu-id="9a94b-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="9a94b-127">建立 Proxy 設定組態檔案</span><span class="sxs-lookup"><span data-stu-id="9a94b-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="9a94b-128">ProxySettingsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="9a94b-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="9a94b-129">使用下列格式建立檔案，並將它以輸入 ProxySettingsFilePath 參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="9a94b-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="9a94b-130">修改相應放大處理序伺服器的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="9a94b-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="9a94b-131">登入您的相應放大處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="9a94b-132">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="9a94b-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="9a94b-133">執行下列命令</span><span class="sxs-lookup"><span data-stu-id="9a94b-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="9a94b-134">接下來，請瀏覽至目錄 **%PROGRAMDATA%\ASR\Agent**，並執行下列命令</span><span class="sxs-lookup"><span data-stu-id="9a94b-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="9a94b-135">重新註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="9a94b-136">接下來，開啟系統管理命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="9a94b-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="9a94b-137">瀏覽至目錄 **%PROGRAMDATA%\ASR\Agent**，並執行命令</span><span class="sxs-lookup"><span data-stu-id="9a94b-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="9a94b-138">升級相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="9a94b-139">將相應放大處理序伺服器解除委任</span><span class="sxs-lookup"><span data-stu-id="9a94b-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="9a94b-140">請確定：</span><span class="sxs-lookup"><span data-stu-id="9a94b-140">Ensure that:</span></span>
  - <span data-ttu-id="9a94b-141">設定伺服器的連線狀態在 Azure 入口網站中顯示為「已連線」</span><span class="sxs-lookup"><span data-stu-id="9a94b-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="9a94b-142">處理序伺服器仍然可以和設定伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="9a94b-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="9a94b-143">以系統管理員身分登入處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="9a94b-144">開啟 [控制台] > [程式] > [解除安裝程式]</span><span class="sxs-lookup"><span data-stu-id="9a94b-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="9a94b-145">以下列順序將程式解除安裝：</span><span class="sxs-lookup"><span data-stu-id="9a94b-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="9a94b-146">Microsoft Azure Site Recovery 設定伺服器/處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a94b-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="9a94b-147">Microsoft Azure Site Recovery 設定伺服器相依性</span><span class="sxs-lookup"><span data-stu-id="9a94b-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="9a94b-148">Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="9a94b-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="9a94b-149">處理序伺服器的刪除可能需要花費 15 分鐘的時間才會顯示於 Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="9a94b-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="9a94b-150">如果處理序伺服器無法與設定伺服器通訊 (入口網站中的 [連線狀態] 為「已中斷連線」)，您必須遵循下列步驟來將它從設定伺服器中清除。</span><span class="sxs-lookup"><span data-stu-id="9a94b-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="9a94b-151">從設定伺服器中將已中斷連線的相應放大處理序伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="9a94b-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="9a94b-152">相應放大處理序伺服器的調整大小需求</span><span class="sxs-lookup"><span data-stu-id="9a94b-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="9a94b-153">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="9a94b-153">**Additional process server**</span></span> | <span data-ttu-id="9a94b-154">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="9a94b-154">**Cache disk size**</span></span> | <span data-ttu-id="9a94b-155">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="9a94b-155">**Data change rate**</span></span> | <span data-ttu-id="9a94b-156">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="9a94b-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="9a94b-157">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a94b-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="9a94b-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="9a94b-158">300 GB</span></span> |<span data-ttu-id="9a94b-159">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="9a94b-159">250 GB or less</span></span> |<span data-ttu-id="9a94b-160">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="9a94b-161">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a94b-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="9a94b-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="9a94b-162">600 GB</span></span> |<span data-ttu-id="9a94b-163">250 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="9a94b-163">250 GB to 1 TB</span></span> |<span data-ttu-id="9a94b-164">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="9a94b-165">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a94b-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="9a94b-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="9a94b-166">1 TB</span></span> |<span data-ttu-id="9a94b-167">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="9a94b-167">1 TB to 2 TB</span></span> |<span data-ttu-id="9a94b-168">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="9a94b-168">Replicate between 150-225 machines.</span></span> |
