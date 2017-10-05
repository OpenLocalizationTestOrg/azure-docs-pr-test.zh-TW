---
title: "Azure 備份：使用 PowerShell 備份 DPM 工作負載 | Microsoft Docs"
description: "了解如何使用 PowerShell 部署和管理 Data Protection Manager (DPM) 的 Azure 備份"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="66413-103">使用 PowerShell 部署和管理 Data Protection Manager (DPM) 伺服器的 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="66413-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66413-104">ARM</span><span class="sxs-lookup"><span data-stu-id="66413-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="66413-105">傳統</span><span class="sxs-lookup"><span data-stu-id="66413-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="66413-106">本文說明如何使用 PowerShell 從備份保存庫備份和還原 DPM 資料。</span><span class="sxs-lookup"><span data-stu-id="66413-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="66413-107">Microsoft 建議讓大部分的新部署使用復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="66413-108">如果您是新的 Azure 備份使用者，請利用[使用 PowerShell 管理 Data Protection Manager 資料並部署到 Azure](backup-dpm-automation.md)一文，因此您將資料儲存在復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="66413-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66413-109">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="66413-110">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="66413-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="66413-111">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="66413-112">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="66413-113">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="66413-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="66413-114">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="66413-115">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="66413-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="66413-116">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="66413-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="66413-117">設定 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="66413-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="66413-118">在可以使用 PowerShell 來管理 Data Protection Manager 的 Azure 備份之前，您必須在 PowerShell 中具備適當的環境。</span><span class="sxs-lookup"><span data-stu-id="66413-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="66413-119">在 PowerShell 工作階段開始時，請確定您執行下列命令來匯入正確的模組並可讓您正確地參考 DPM Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="66413-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="66413-120">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="66413-120">Setup and Registration</span></span>
<span data-ttu-id="66413-121">開始：</span><span class="sxs-lookup"><span data-stu-id="66413-121">To begin:</span></span>

1. <span data-ttu-id="66413-122">[下載最新的 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需最低版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="66413-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="66413-123">使用 *Switch-AzureMode* Cmdlet 切換至 **AzureResourceManager** 模式，以啟用 Azure 備份 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="66413-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="66413-124">PowerShell 可以自動化下列設定和註冊工作：</span><span class="sxs-lookup"><span data-stu-id="66413-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="66413-125">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="66413-125">Create a backup vault</span></span>
* <span data-ttu-id="66413-126">安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="66413-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="66413-127">向 Azure 備份服務進行註冊</span><span class="sxs-lookup"><span data-stu-id="66413-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="66413-128">網路設定</span><span class="sxs-lookup"><span data-stu-id="66413-128">Networking settings</span></span>
* <span data-ttu-id="66413-129">加密設定</span><span class="sxs-lookup"><span data-stu-id="66413-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="66413-130">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="66413-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="66413-131">對於第一次使用 Azure 備份的客戶，您需要註冊 Azure 備份提供者以搭配您的訂用帳戶使用。</span><span class="sxs-lookup"><span data-stu-id="66413-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="66413-132">這可以透過執行下列命令來完成：Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="66413-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="66413-133">您可以使用 **New-AzureRMBackupVault** Cmdlet 建立新的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="66413-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="66413-134">備份保存庫是 ARM 資源，因此您必須將它放在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="66413-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="66413-135">在提高權限的 Azure PowerShell 主控台中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="66413-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="66413-136">您可以使用 **Get-AzureRMBackupVault** Cmdlet 取得特定訂用帳戶中所有備份保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="66413-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="66413-137">在 DPM 伺服器上安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="66413-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="66413-138">在安裝 Azure 備份代理程式之前，您必須在 Windows Server 上下載並提供安裝程式。</span><span class="sxs-lookup"><span data-stu-id="66413-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="66413-139">您可以從 [Microsoft 下載中心](http://aka.ms/azurebackup_agent) 或從備份保存庫的 [儀表板] 頁面取得最新版的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="66413-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="66413-140">請將安裝程式儲存至容易存取的位置，例如 *C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="66413-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="66413-141">若要安裝代理程式，請在 **DPM 伺服器**上已提升權限的 PowerShell 主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="66413-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="66413-142">這會以所有預設選項安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="66413-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="66413-143">安裝作業會在背景中進行幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="66413-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="66413-144">如果您沒有指定 */nu* 選項，則安裝結束時會開啟 **Windows Update** 視窗以檢查是否有任何更新。</span><span class="sxs-lookup"><span data-stu-id="66413-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="66413-145">代理程式會顯示在已安裝的程式清單中。</span><span class="sxs-lookup"><span data-stu-id="66413-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="66413-146">若要查看已安裝的程式清單，請移至 [控制台] > [程式] > [程式和功能]。</span><span class="sxs-lookup"><span data-stu-id="66413-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="66413-148">安裝選項</span><span class="sxs-lookup"><span data-stu-id="66413-148">Installation options</span></span>
<span data-ttu-id="66413-149">若要查看所有可透過命令列執行的選項，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="66413-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="66413-150">可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="66413-150">The available options include:</span></span>

| <span data-ttu-id="66413-151">選項</span><span class="sxs-lookup"><span data-stu-id="66413-151">Option</span></span> | <span data-ttu-id="66413-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="66413-152">Details</span></span> | <span data-ttu-id="66413-153">預設值</span><span class="sxs-lookup"><span data-stu-id="66413-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66413-154">/q</span><span class="sxs-lookup"><span data-stu-id="66413-154">/q</span></span> |<span data-ttu-id="66413-155">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="66413-155">Quiet installation</span></span> |- |
| <span data-ttu-id="66413-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="66413-156">/p:"location"</span></span> |<span data-ttu-id="66413-157">Azure 備份代理程式的安裝資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="66413-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="66413-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="66413-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="66413-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="66413-159">/s:"location"</span></span> |<span data-ttu-id="66413-160">Azure 備份代理程式的快取資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="66413-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="66413-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="66413-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="66413-162">/m</span><span class="sxs-lookup"><span data-stu-id="66413-162">/m</span></span> |<span data-ttu-id="66413-163">選擇加入 Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="66413-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="66413-164">/nu</span><span class="sxs-lookup"><span data-stu-id="66413-164">/nu</span></span> |<span data-ttu-id="66413-165">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="66413-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="66413-166">/d</span><span class="sxs-lookup"><span data-stu-id="66413-166">/d</span></span> |<span data-ttu-id="66413-167">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="66413-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="66413-168">/ph</span><span class="sxs-lookup"><span data-stu-id="66413-168">/ph</span></span> |<span data-ttu-id="66413-169">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="66413-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="66413-170">/po</span><span class="sxs-lookup"><span data-stu-id="66413-170">/po</span></span> |<span data-ttu-id="66413-171">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="66413-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="66413-172">/pu</span><span class="sxs-lookup"><span data-stu-id="66413-172">/pu</span></span> |<span data-ttu-id="66413-173">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="66413-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="66413-174">/pw</span><span class="sxs-lookup"><span data-stu-id="66413-174">/pw</span></span> |<span data-ttu-id="66413-175">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="66413-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="66413-176">向 Azure 備份服務進行註冊</span><span class="sxs-lookup"><span data-stu-id="66413-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="66413-177">在可註冊 Azure 備份服務之前，您必須確定已符合 [先決條件](backup-azure-dpm-introduction.md) 。</span><span class="sxs-lookup"><span data-stu-id="66413-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="66413-178">您必須：</span><span class="sxs-lookup"><span data-stu-id="66413-178">You must:</span></span>

* <span data-ttu-id="66413-179">具備有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66413-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="66413-180">具備備份保存庫</span><span class="sxs-lookup"><span data-stu-id="66413-180">Have a backup vault</span></span>

<span data-ttu-id="66413-181">若要下載保存庫認證，請在 Azure PowerShell 主控台中執行 **Get-AzureBackupVaultCredentials**，並將其儲存在方便的位置，例如 *C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="66413-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="66413-182">使用 [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) Cmdlet 即可向保存庫註冊電腦：</span><span class="sxs-lookup"><span data-stu-id="66413-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="66413-183">此命令會使用指定的保存庫認證向 Microsoft Azure 保存庫註冊名為 “TestingServer” 的 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="66413-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66413-184">請勿使用相對路徑來指定保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="66413-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="66413-185">您必須提供絕對路徑做為 Cmdlet 的輸入。</span><span class="sxs-lookup"><span data-stu-id="66413-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="66413-186">初始組態設定</span><span class="sxs-lookup"><span data-stu-id="66413-186">Initial configuration settings</span></span>
<span data-ttu-id="66413-187">一旦向 Azure 備份保存庫註冊 DPM 伺服器，就會使用預設的訂用帳戶設定開始。</span><span class="sxs-lookup"><span data-stu-id="66413-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="66413-188">這些訂用帳戶設定包括網路、加密和臨時區域。</span><span class="sxs-lookup"><span data-stu-id="66413-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="66413-189">若要開始變更訂用帳戶設定，您需要先使用 [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) Cmdlet 取得現有 (預設) 設定上的控制代碼：</span><span class="sxs-lookup"><span data-stu-id="66413-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="66413-190">所有修改都會對此本機 PowerShell 物件 ```$setting``` 進行，然後使用 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 將完整物件認可到 DPM 和 Azure 備份以加以儲存。</span><span class="sxs-lookup"><span data-stu-id="66413-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="66413-191">您必須使用 ```–Commit``` 旗標，以確保會保存所做的變更。</span><span class="sxs-lookup"><span data-stu-id="66413-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="66413-192">除非已認可，否則 Azure 備份將不會套用並使用設定。</span><span class="sxs-lookup"><span data-stu-id="66413-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="66413-193">網路</span><span class="sxs-lookup"><span data-stu-id="66413-193">Networking</span></span>
<span data-ttu-id="66413-194">如果 DPM 機器對在網際網路上的 Azure 備份服務的連線是透過 Proxy 伺服器，則應該提供 Proxy 伺服器設定，備份才能成功。</span><span class="sxs-lookup"><span data-stu-id="66413-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="66413-195">這是使用 ```-ProxyServer```、```-ProxyPort```、```-ProxyUsername``` 和 ```ProxyPassword``` 參數搭配 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 完成。</span><span class="sxs-lookup"><span data-stu-id="66413-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="66413-196">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66413-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="66413-197">您也可以針對給定的一組當週天數，使用 ```-WorkHourBandwidth``` 和 ```-NonWorkHourBandwidth``` 的選項來控制頻寬使用情形。</span><span class="sxs-lookup"><span data-stu-id="66413-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="66413-198">本範例未設定任何節流。</span><span class="sxs-lookup"><span data-stu-id="66413-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="66413-199">設定臨時區域</span><span class="sxs-lookup"><span data-stu-id="66413-199">Configuring the staging Area</span></span>
<span data-ttu-id="66413-200">在 DPM 伺服器上執行的 Azure 備份代理程式需要暫存儲存體，以供存放從雲端還原的資料 (本機臨時區域)。</span><span class="sxs-lookup"><span data-stu-id="66413-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="66413-201">使用 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 和 ```-StagingAreaPath``` 參數來設定臨時區域。</span><span class="sxs-lookup"><span data-stu-id="66413-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="66413-202">在上述範例中，臨時區域將在 PowerShell 物件 ```$setting``` 中設定為 *C:\StagingArea*。</span><span class="sxs-lookup"><span data-stu-id="66413-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="66413-203">請確保指定的資料夾已經存在，否則訂用帳戶設定的最終認可將會失敗。</span><span class="sxs-lookup"><span data-stu-id="66413-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="66413-204">加密設定</span><span class="sxs-lookup"><span data-stu-id="66413-204">Encryption settings</span></span>
<span data-ttu-id="66413-205">傳送至 Azure 備份的備份資料會進行加密來保護資料的機密性。</span><span class="sxs-lookup"><span data-stu-id="66413-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="66413-206">加密複雜密碼是在還原時用來解密資料的「密碼」。</span><span class="sxs-lookup"><span data-stu-id="66413-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="66413-207">一旦設定，就請務必保管好這項資訊。</span><span class="sxs-lookup"><span data-stu-id="66413-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="66413-208">在下面的範例中，第一個命令會將字串 ```passphrase123456789``` 轉換為安全字串，並將安全字串指派給名為 ```$Passphrase``` 的變數。</span><span class="sxs-lookup"><span data-stu-id="66413-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="66413-209">第二個命令會將 ```$Passphrase``` 中的安全字串設定為加密備份的密碼。</span><span class="sxs-lookup"><span data-stu-id="66413-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="66413-210">一旦設定，就請保管好此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="66413-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="66413-211">若沒有此複雜密碼，您將無法從 Azure 還原資料。</span><span class="sxs-lookup"><span data-stu-id="66413-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="66413-212">此時，您應該已對 ```$setting``` 物件進行所有必要的變更。</span><span class="sxs-lookup"><span data-stu-id="66413-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="66413-213">記得要認可變更。</span><span class="sxs-lookup"><span data-stu-id="66413-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="66413-214">保護 Azure 備份的資料</span><span class="sxs-lookup"><span data-stu-id="66413-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="66413-215">在本節中，您會將實際執行伺服器加入至 DPM，然後保護資料到本機 DPM 存放區，然後到 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="66413-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="66413-216">在範例中，我們將示範如何備份檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="66413-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="66413-217">您可以輕鬆地運用同樣的觀念，來備份任何 DPM 支援的資料來源。</span><span class="sxs-lookup"><span data-stu-id="66413-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="66413-218">所有 DPM 備份皆受到保護群組 (PG) 所控管，並且由四個部分構成：</span><span class="sxs-lookup"><span data-stu-id="66413-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="66413-219">**群組成員** 是您要在相同的保護群組中保護的所有可保護物件的清單 (在 DPM 中也稱為 *資料來源* )。</span><span class="sxs-lookup"><span data-stu-id="66413-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="66413-220">比方說，您可能想要保護一個保護群組的實際執行 VM 與另一個保護群組中的 SQL Server 資料庫，因為它們可能會有不同的備份需求。</span><span class="sxs-lookup"><span data-stu-id="66413-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="66413-221">在可以備份實際執行伺服器上的資料來源之前，您必須先確定 DPM 代理程式已安裝在伺服器上並受到 DPM 管理。</span><span class="sxs-lookup"><span data-stu-id="66413-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="66413-222">請遵循 [安裝 DPM 代理程式](https://technet.microsoft.com/library/bb870935.aspx) 的步驟，並將其連結至適當的 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="66413-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="66413-223">**資料保護方法** 指定目標備份位置 - 磁帶、磁碟和雲端。</span><span class="sxs-lookup"><span data-stu-id="66413-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="66413-224">在我們的範例中，我們將保護資料至本機磁碟以及雲端。</span><span class="sxs-lookup"><span data-stu-id="66413-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="66413-225">**備份排程** 可指定何時需要進行備份，以及應該在 DPM 伺服器和實際執行伺服器之間同步處理資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="66413-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="66413-226">**保留排程** 可指定要在 Azure 中保留復原點多久時間。</span><span class="sxs-lookup"><span data-stu-id="66413-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="66413-227">建立保護群組</span><span class="sxs-lookup"><span data-stu-id="66413-227">Creating a protection group</span></span>
<span data-ttu-id="66413-228">從使用 [Add-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) Cmdlet 來建立新的保護群組開始。</span><span class="sxs-lookup"><span data-stu-id="66413-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="66413-229">以上 Cmdlet 會建立名為 *ProtectGroup01*的保護群組。</span><span class="sxs-lookup"><span data-stu-id="66413-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="66413-230">也可以修改稍後現有的保護群組，以加入備份至 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="66413-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="66413-231">不過，若要對保護群組 - 新的或現有的- 進行任何變更，我們需要使用 *Get-DPMModifiableProtectionGroup* Cmdlet 來取得 [modifiable](https://technet.microsoft.com/library/hh881713) 物件上的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="66413-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="66413-232">將群組成員加入至保護群組</span><span class="sxs-lookup"><span data-stu-id="66413-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="66413-233">每個 DPM 代理程式會知道它安裝所在伺服器上資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="66413-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="66413-234">若要將資料來源加入至保護群組，DPM 代理程式必須先將資料來源清單傳回到 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="66413-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="66413-235">然後會選取一或多個資料來源，並加入至保護群組。</span><span class="sxs-lookup"><span data-stu-id="66413-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="66413-236">達成此動作所需的 PowerShell 步驟包括：</span><span class="sxs-lookup"><span data-stu-id="66413-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="66413-237">擷取透過 DPM 代理程式由 DPM 管理的所有伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="66413-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="66413-238">選擇特定伺服器。</span><span class="sxs-lookup"><span data-stu-id="66413-238">Choose a specific server.</span></span>
3. <span data-ttu-id="66413-239">擷取伺服器上所有資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="66413-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="66413-240">選擇一或多個資料來源，並將它們加入至保護群組</span><span class="sxs-lookup"><span data-stu-id="66413-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="66413-241">安裝 DPM 代理程式且受 DPM 伺服器管理所在的伺服器清單是使用 [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) Cmdlet 取得。</span><span class="sxs-lookup"><span data-stu-id="66413-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="66413-242">在此範例中，我們將篩選並只設定名稱為 *productionserver01* 的 PS 來進行備份。</span><span class="sxs-lookup"><span data-stu-id="66413-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="66413-243">現在使用 [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) Cmdlet 擷取 ```$server``` 上的資料來源清單。</span><span class="sxs-lookup"><span data-stu-id="66413-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="66413-244">在此範例中，我們會篩選要設定備份的磁碟區 *D:\*。</span><span class="sxs-lookup"><span data-stu-id="66413-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="66413-245">然後此資料來源會使用 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) Cmdlet 新增至保護群組。</span><span class="sxs-lookup"><span data-stu-id="66413-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="66413-246">記得使用「可修改的」保護群組物件 ```$MPG``` 來進行新增。</span><span class="sxs-lookup"><span data-stu-id="66413-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="66413-247">視需要重複此步驟，直到您已加入所有選取的資料來源至保護群組中為止。</span><span class="sxs-lookup"><span data-stu-id="66413-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="66413-248">您也可以從只有一個資料來源開始，並完成建立保護群組的工作流程，然後稍後將更多的資料來源加入至保護群組。</span><span class="sxs-lookup"><span data-stu-id="66413-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="66413-249">選取資料保護方式</span><span class="sxs-lookup"><span data-stu-id="66413-249">Selecting the data protection method</span></span>
<span data-ttu-id="66413-250">資料來源加入至保護群組之後，下一步是使用 [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) Cmdlet 指定保護方法。</span><span class="sxs-lookup"><span data-stu-id="66413-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="66413-251">此範例中，將為本機磁碟和雲端備份設定保護群組。</span><span class="sxs-lookup"><span data-stu-id="66413-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="66413-252">您也必須使用 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) Cmdlet 搭配 -Online 旗標，指定您想要在雲端中保護的資料來源。</span><span class="sxs-lookup"><span data-stu-id="66413-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="66413-253">設定保留範圍</span><span class="sxs-lookup"><span data-stu-id="66413-253">Setting the retention range</span></span>
<span data-ttu-id="66413-254">使用 [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) Cmdlet 設定備份點的保留。</span><span class="sxs-lookup"><span data-stu-id="66413-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="66413-255">雖然在定義備份排程之前設定保留點看起來有點奇怪，使用 ```Set-DPMPolicyObjective``` Cmdlet 會自動設定預設的備份排程，之後便可加以修改。</span><span class="sxs-lookup"><span data-stu-id="66413-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="66413-256">您總是可以先設定備份排程，之後再設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="66413-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="66413-257">在下面的範例中，此 Cmdlet 會設定磁碟備份的保留參數。</span><span class="sxs-lookup"><span data-stu-id="66413-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="66413-258">這將會保留 10 天備份，並每隔 6 小時同步處理實際執行伺服器和 DPM 伺服器之間的資料。</span><span class="sxs-lookup"><span data-stu-id="66413-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="66413-259">```SynchronizationFrequencyMinutes``` 不會定義建立備份點的頻率，只會定有資料複製到 DPM 伺服器的頻率；這可防止備份變得太大。</span><span class="sxs-lookup"><span data-stu-id="66413-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="66413-260">針對移至 Azure 的備份 (DPM 將這些稱為線上備份)，保留範圍可設定為 [使用 Grandfather-Father-Son 配置 (GFS) 的長期保留](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="66413-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="66413-261">也就是說，您可以定義結合的保留原則，包含每日、每週、每月和每年保留原則。</span><span class="sxs-lookup"><span data-stu-id="66413-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="66413-262">在此範例中，我們會建立陣列，表示我們需要的複雜保留配置，然後使用 [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) Cmdlet 設定保留範圍。</span><span class="sxs-lookup"><span data-stu-id="66413-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="66413-263">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="66413-263">Set the backup schedule</span></span>
<span data-ttu-id="66413-264">如果您使用 ```Set-DPMPolicyObjective``` Cmdlet 指定保護目標，DPM 會自動設定預設的備份排程。</span><span class="sxs-lookup"><span data-stu-id="66413-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="66413-265">若要變更預設排程，請依序使用 [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) Cmdlet 和 [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="66413-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="66413-266">在上述範例中， ```$onlineSch``` 是具有四個元素的陣列，其中包含 GFS 配置中保護群組的現有線上保護排程：</span><span class="sxs-lookup"><span data-stu-id="66413-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="66413-267">```$onlineSch[0]``` 將包含每日排程</span><span class="sxs-lookup"><span data-stu-id="66413-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="66413-268">```$onlineSch[1]``` 將包含每週排程</span><span class="sxs-lookup"><span data-stu-id="66413-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="66413-269">```$onlineSch[2]``` 將包含每月排程</span><span class="sxs-lookup"><span data-stu-id="66413-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="66413-270">```$onlineSch[3]``` 將包含每年排程</span><span class="sxs-lookup"><span data-stu-id="66413-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="66413-271">因此，如果您需要修改每週排程，您需要參考 ```$onlineSch[1]```。</span><span class="sxs-lookup"><span data-stu-id="66413-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="66413-272">初始備份</span><span class="sxs-lookup"><span data-stu-id="66413-272">Initial backup</span></span>
<span data-ttu-id="66413-273">第一次備份資料來源時，DPM 就需要建立初始複本，以建立要在 DPM 複本磁碟區上保護的資料來源複本。</span><span class="sxs-lookup"><span data-stu-id="66413-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="66413-274">此活動可以排定在特定的時間，或可以使用 [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) Cmdlet 搭配參數 ```-NOW``` 手動觸發。</span><span class="sxs-lookup"><span data-stu-id="66413-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="66413-275">變更 DPM 複本和復原點磁碟區的大小</span><span class="sxs-lookup"><span data-stu-id="66413-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="66413-276">您也可以變更 DPM 複本磁碟區以及陰影複製磁碟區的大小，方法是使用 [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) Cmdlet，如下列範例所示：Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="66413-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="66413-277">將變更認可到保護群組</span><span class="sxs-lookup"><span data-stu-id="66413-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="66413-278">最後，需要先認可變更，DPM 才可以根據每個新保護群組組態進行備份。</span><span class="sxs-lookup"><span data-stu-id="66413-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="66413-279">這是使用 [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) Cmdlet 來完成。</span><span class="sxs-lookup"><span data-stu-id="66413-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="66413-280">檢視備份點</span><span class="sxs-lookup"><span data-stu-id="66413-280">View the backup points</span></span>
<span data-ttu-id="66413-281">您可以使用 [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) Cmdlet 來取得資料來源所有復原點的清單。</span><span class="sxs-lookup"><span data-stu-id="66413-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="66413-282">在此範例中，我們將會：</span><span class="sxs-lookup"><span data-stu-id="66413-282">In this example, we will:</span></span>

* <span data-ttu-id="66413-283">擷取 DPM 伺服器上將儲存在 ```$PG```</span><span class="sxs-lookup"><span data-stu-id="66413-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="66413-284">取得與 ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="66413-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="66413-285">取得資料來源的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="66413-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="66413-286">還原在 Azure 上保護的資料</span><span class="sxs-lookup"><span data-stu-id="66413-286">Restore data protected on Azure</span></span>
<span data-ttu-id="66413-287">還原資料是 ```RecoverableItem``` 物件和 ```RecoveryOption``` 物件的組合。</span><span class="sxs-lookup"><span data-stu-id="66413-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="66413-288">在上一個節中，我們已取得資料來源的備份點清單。</span><span class="sxs-lookup"><span data-stu-id="66413-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="66413-289">在下列範例中，我們將示範如何透過結合備份點與復原目標從 Azure 備份還原 Hyper-V 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="66413-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="66413-290">其中包括：</span><span class="sxs-lookup"><span data-stu-id="66413-290">This includes:</span></span>

* <span data-ttu-id="66413-291">使用 [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) Cmdlet 建立復原選項。</span><span class="sxs-lookup"><span data-stu-id="66413-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="66413-292">使用 ```Get-DPMRecoveryPoint``` Cmdlet 擷取備份點的陣列。</span><span class="sxs-lookup"><span data-stu-id="66413-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="66413-293">選擇要從中還原的備份點。</span><span class="sxs-lookup"><span data-stu-id="66413-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="66413-294">命令可以很容易地針對任何資料來源類型擴充。</span><span class="sxs-lookup"><span data-stu-id="66413-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66413-295">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66413-295">Next steps</span></span>
* <span data-ttu-id="66413-296">如需 DPM 的 Azure 備份詳細資訊，請參閱 [DPM 備份簡介](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="66413-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
