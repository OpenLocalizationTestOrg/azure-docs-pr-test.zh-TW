---
title: " 在 Azure Site Recovery 中管理相應放大處理序伺服器 | Microsoft Doc"
description: "本文說明如何 tooset 及管理 Azure Site Recovery 中的向外延展處理序伺服器。"
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="9a2b1-103">管理相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="9a2b1-104">向外延展處理序伺服器做為協調器 hello 站台復原服務與您在內部部署基礎結構之間資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="9a2b1-105">本文說明如何設定、配置及管理相應放大處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a2b1-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="9a2b1-106">Prerequisites</span></span>
<span data-ttu-id="9a2b1-107">hello 下面是 hello 建議的硬體、 軟體和網路所需設定 tooset 向上擴充處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="9a2b1-108">[容量規劃](site-recovery-capacity-planner.md)是您部署與設定向外延展處理序伺服器 hello 該套件的重要步驟 tooensure 負載需求。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="9a2b1-109">請在[相應放大處理序伺服器的調整特性](#sizing-requirements-for-a-configuration-server)中閱讀更多資訊。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="9a2b1-110">下載 hello 向外延展處理序伺服器軟體</span><span class="sxs-lookup"><span data-stu-id="9a2b1-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="9a2b1-111">登入 toohello Azure 入口網站，並瀏覽 tooyour 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="9a2b1-112">瀏覽過**Site Recovery 基礎結構** > **設定伺服器**（底下的 VMware & 實體機器)。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="9a2b1-113">清單中選取您設定伺服器 toodrill 到 hello 組態伺服器的詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="9a2b1-114">按一下 hello **+ 處理序伺服器** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="9a2b1-115">在 hello**加入處理序伺服器**頁面上，選取**向外延展部署處理序伺服器在內部**選項從 hello**選擇您希望 toodeploy 處理序伺服器**下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![新增伺服器頁面](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="9a2b1-117">按一下 hello**下載 hello Microsoft Azure Site Recovery 統一的安裝**連結 toodownload hello 最新版本的 hello 向外延展處理序伺服器安裝。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="9a2b1-118">hello 向外延展處理伺服器的版本應該相等 tooor 小於 hello 組態伺服器版本，在您的環境中執行。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="9a2b1-119">簡單的方式 tooensure 版本相容性層級是 toouse hello 相同，您最近使用過 tooinstall/更新組態伺服器的安裝程式位元。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="9a2b1-120">從 GUI 安裝並註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="9a2b1-121">如果您有 tooscale 出您的部署超過 200 的來源機器，或總每日變換率超過 2 TB，您會需要額外的處理序伺服器 toohandle hello 流量磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="9a2b1-122">檢查 hello[大小處理序伺服器的建議](#size-recommendations-for-the-process-server)，然後遵循這些指示 tooset，hello 的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="9a2b1-123">設定好 hello 伺服器之後，您將移轉來源機器 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="9a2b1-124">使用命令列安裝並註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="9a2b1-125">範例用法</span><span class="sxs-lookup"><span data-stu-id="9a2b1-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="9a2b1-126">相應放大處理序伺服器安裝程式命令列引數。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="9a2b1-127">建立 Proxy 設定組態檔案</span><span class="sxs-lookup"><span data-stu-id="9a2b1-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="9a2b1-128">ProxySettingsFilePath 參數使用檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="9a2b1-129">使用下列格式，並將它傳遞做為輸入 ProxySettingsFilePath 參數 hello 建立檔案。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="9a2b1-130">修改相應放大處理序伺服器的 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="9a2b1-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="9a2b1-131">登入您的相應放大處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="9a2b1-132">開啟系統管理 PowerShell 命令視窗。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="9a2b1-133">執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="9a2b1-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="9a2b1-134">下一步瀏覽 toohello 目錄**%PROGRAMDATA%\ASR\Agent**和 hello 執行下列命令</span><span class="sxs-lookup"><span data-stu-id="9a2b1-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="9a2b1-135">重新註冊相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="9a2b1-136">接下來，開啟系統管理命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="9a2b1-137">瀏覽 toohello 目錄**%PROGRAMDATA%\ASR\Agent**執行 hello 命令</span><span class="sxs-lookup"><span data-stu-id="9a2b1-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="9a2b1-138">升級相應放大處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="9a2b1-139">將相應放大處理序伺服器解除委任</span><span class="sxs-lookup"><span data-stu-id="9a2b1-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="9a2b1-140">請確定：</span><span class="sxs-lookup"><span data-stu-id="9a2b1-140">Ensure that:</span></span>
  - <span data-ttu-id="9a2b1-141">組態伺服器的連線狀態會顯示成**Connected** hello Azure 入口網站中</span><span class="sxs-lookup"><span data-stu-id="9a2b1-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="9a2b1-142">使用 hello 組態伺服器仍然可以 toocommunicate 為處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="9a2b1-143">系統管理員身分登入 toohello 處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="9a2b1-144">開啟 [控制台] > [程式] > [解除安裝程式]</span><span class="sxs-lookup"><span data-stu-id="9a2b1-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="9a2b1-145">Hello 順序指定下列中的 hello 程式解除安裝：</span><span class="sxs-lookup"><span data-stu-id="9a2b1-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="9a2b1-146">Microsoft Azure Site Recovery 設定伺服器/處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="9a2b1-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="9a2b1-147">Microsoft Azure Site Recovery 設定伺服器相依性</span><span class="sxs-lookup"><span data-stu-id="9a2b1-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="9a2b1-148">Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="9a2b1-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="9a2b1-149">可能需要向上 too15 分鐘 hello 處理序伺服器刪除 tooreflect hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="9a2b1-150">Hello 處理序伺服器是否以 hello 組態伺服器無法 toocommunicate (入口網站中的連接狀態為 Disconnected，) 則需要 toofollow hello 下列步驟 toopurge 它從 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="9a2b1-151">從設定伺服器中將已中斷連線的相應放大處理序伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="9a2b1-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="9a2b1-152">相應放大處理序伺服器的調整大小需求</span><span class="sxs-lookup"><span data-stu-id="9a2b1-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="9a2b1-153">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="9a2b1-153">**Additional process server**</span></span> | <span data-ttu-id="9a2b1-154">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="9a2b1-154">**Cache disk size**</span></span> | <span data-ttu-id="9a2b1-155">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="9a2b1-155">**Data change rate**</span></span> | <span data-ttu-id="9a2b1-156">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="9a2b1-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="9a2b1-157">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a2b1-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="9a2b1-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="9a2b1-158">300 GB</span></span> |<span data-ttu-id="9a2b1-159">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="9a2b1-159">250 GB or less</span></span> |<span data-ttu-id="9a2b1-160">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="9a2b1-161">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a2b1-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="9a2b1-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="9a2b1-162">600 GB</span></span> |<span data-ttu-id="9a2b1-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="9a2b1-163">250 GB too1 TB</span></span> |<span data-ttu-id="9a2b1-164">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="9a2b1-165">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="9a2b1-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="9a2b1-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="9a2b1-166">1 TB</span></span> |<span data-ttu-id="9a2b1-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="9a2b1-167">1 TB too2 TB</span></span> |<span data-ttu-id="9a2b1-168">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="9a2b1-168">Replicate between 150-225 machines.</span></span> |
