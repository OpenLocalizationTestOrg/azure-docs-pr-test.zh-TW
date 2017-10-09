---
title: "Azure 備份： DPM 工作負載備份使用 PowerShell tooback |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理 Azure 備份的 Data Protection Manager (DPM) 使用 PowerShell"
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
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="2805b-103">部署和管理備份 tooAzure Data Protection Manager (DPM) 伺服器使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="2805b-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2805b-104">ARM</span><span class="sxs-lookup"><span data-stu-id="2805b-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="2805b-105">傳統</span><span class="sxs-lookup"><span data-stu-id="2805b-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="2805b-106">這篇文章說明如何 toouse PowerShell tooback 及復原 DPM 資料從備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="2805b-107">Microsoft 建議讓大部分的新部署使用復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="2805b-108">如果您是新的 Azure 備份使用者，使用 hello 文章[部署和管理使用 PowerShell 的 Data Protection Manager 資料 tooAzure](backup-dpm-automation.md)，因此您將資料儲存在復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2805b-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2805b-109">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="2805b-110">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2805b-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="2805b-111">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="2805b-112">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="2805b-113">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="2805b-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="2805b-114">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2805b-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="2805b-115">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="2805b-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="2805b-116">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2805b-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="2805b-117">設定 hello PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="2805b-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="2805b-118">您可以使用從 Data Protection Manager tooAzure PowerShell toomanage 備份之前，您必須在 PowerShell 中的 toohave hello 右環境。</span><span class="sxs-lookup"><span data-stu-id="2805b-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="2805b-119">在 hello 開頭 hello PowerShell 工作階段，請確定您執行下列命令 tooimport hello 右模組 hello 和 toocorrectly 參考 hello DPM 指令程式可讓您：</span><span class="sxs-lookup"><span data-stu-id="2805b-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="2805b-120">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="2805b-120">Setup and Registration</span></span>
<span data-ttu-id="2805b-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="2805b-121">toobegin:</span></span>

1. <span data-ttu-id="2805b-122">[下載最新的 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需最低版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="2805b-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="2805b-123">啟用 hello Azure 備份指令程式，藉由切換太*AzureResourceManager*模式使用 hello **Switch-azuremode**指令程式：</span><span class="sxs-lookup"><span data-stu-id="2805b-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="2805b-124">hello 下列安裝和註冊工作可以自動化使用 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2805b-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="2805b-125">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="2805b-125">Create a backup vault</span></span>
* <span data-ttu-id="2805b-126">安裝 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="2805b-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="2805b-127">註冊以 hello Azure 備份服務</span><span class="sxs-lookup"><span data-stu-id="2805b-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="2805b-128">網路設定</span><span class="sxs-lookup"><span data-stu-id="2805b-128">Networking settings</span></span>
* <span data-ttu-id="2805b-129">加密設定</span><span class="sxs-lookup"><span data-stu-id="2805b-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="2805b-130">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="2805b-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="2805b-131">Hello 第一次使用 Azure Backup 的客戶，您需要 tooregister hello Azure 備份提供者 toobe 搭配您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2805b-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="2805b-132">這可藉由執行下列命令的 hello： 暫存器 AzureProvider ProviderNamespace"Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="2805b-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="2805b-133">您可以建立新的備份保存庫使用 hello**新增 AzureRMBackupVault**指令程式。</span><span class="sxs-lookup"><span data-stu-id="2805b-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="2805b-134">hello 備份保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。</span><span class="sxs-lookup"><span data-stu-id="2805b-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="2805b-135">在提升權限的 Azure PowerShell 主控台中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2805b-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="2805b-136">您可以取得一份所有 hello 備份保存庫中指定的訂用帳戶使用 hello **Get AzureRMBackupVault**指令程式。</span><span class="sxs-lookup"><span data-stu-id="2805b-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="2805b-137">在 DPM 伺服器上安裝 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="2805b-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="2805b-138">安裝 hello Azure Backup agent 之前，您需要 toohave hello 安裝程式，下載和 hello Windows Server 上也一樣。</span><span class="sxs-lookup"><span data-stu-id="2805b-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="2805b-139">收到 hello 的 hello 最新版本的 hello installer [Microsoft Download Center](http://aka.ms/azurebackup_agent)或從 hello 備份保存庫的 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="2805b-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="2805b-140">儲存 hello installer tooan 更容易存取的位置，例如 * C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="2805b-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="2805b-141">tooinstall hello 代理程式，執行下列命令，在提升權限的 PowerShell 主控台中的 hello **hello DPM 伺服器上**:</span><span class="sxs-lookup"><span data-stu-id="2805b-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="2805b-142">這會 hello 代理程式安裝與所有 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="2805b-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="2805b-143">hello 安裝需要幾分鐘 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="2805b-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="2805b-144">如果您未指定 hello */nu*選項 hello **Windows Update**視窗隨即開啟的任何更新的 hello 安裝 toocheck hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="2805b-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="2805b-145">hello 代理程式會顯示 hello 的安裝程式的清單中。</span><span class="sxs-lookup"><span data-stu-id="2805b-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="2805b-146">toosee hello 列出已安裝的程式，請移過**控制台** > **程式** > **程式和功能**。</span><span class="sxs-lookup"><span data-stu-id="2805b-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="2805b-148">安裝選項</span><span class="sxs-lookup"><span data-stu-id="2805b-148">Installation options</span></span>
<span data-ttu-id="2805b-149">toosee 所有 hello 選項可透過使用 hello 命令列，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2805b-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="2805b-150">hello 可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="2805b-150">hello available options include:</span></span>

| <span data-ttu-id="2805b-151">選項</span><span class="sxs-lookup"><span data-stu-id="2805b-151">Option</span></span> | <span data-ttu-id="2805b-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="2805b-152">Details</span></span> | <span data-ttu-id="2805b-153">預設值</span><span class="sxs-lookup"><span data-stu-id="2805b-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2805b-154">/q</span><span class="sxs-lookup"><span data-stu-id="2805b-154">/q</span></span> |<span data-ttu-id="2805b-155">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="2805b-155">Quiet installation</span></span> |- |
| <span data-ttu-id="2805b-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="2805b-156">/p:"location"</span></span> |<span data-ttu-id="2805b-157">路徑 toohello hello Azure Backup agent 的安裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="2805b-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="2805b-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="2805b-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="2805b-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="2805b-159">/s:"location"</span></span> |<span data-ttu-id="2805b-160">路徑 toohello hello Azure 備份代理程式的快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="2805b-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="2805b-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="2805b-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="2805b-162">/m</span><span class="sxs-lookup"><span data-stu-id="2805b-162">/m</span></span> |<span data-ttu-id="2805b-163">選擇加入 tooMicrosoft 更新</span><span class="sxs-lookup"><span data-stu-id="2805b-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="2805b-164">/nu</span><span class="sxs-lookup"><span data-stu-id="2805b-164">/nu</span></span> |<span data-ttu-id="2805b-165">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="2805b-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="2805b-166">/d</span><span class="sxs-lookup"><span data-stu-id="2805b-166">/d</span></span> |<span data-ttu-id="2805b-167">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="2805b-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="2805b-168">/ph</span><span class="sxs-lookup"><span data-stu-id="2805b-168">/ph</span></span> |<span data-ttu-id="2805b-169">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="2805b-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="2805b-170">/po</span><span class="sxs-lookup"><span data-stu-id="2805b-170">/po</span></span> |<span data-ttu-id="2805b-171">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="2805b-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="2805b-172">/pu</span><span class="sxs-lookup"><span data-stu-id="2805b-172">/pu</span></span> |<span data-ttu-id="2805b-173">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="2805b-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="2805b-174">/pw</span><span class="sxs-lookup"><span data-stu-id="2805b-174">/pw</span></span> |<span data-ttu-id="2805b-175">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="2805b-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="2805b-176">註冊以 hello Azure 備份服務</span><span class="sxs-lookup"><span data-stu-id="2805b-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="2805b-177">您可以向 hello Azure 備份服務之前，您需要 tooensure 該 hello[必要條件](backup-azure-dpm-introduction.md)符合。</span><span class="sxs-lookup"><span data-stu-id="2805b-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="2805b-178">您必須：</span><span class="sxs-lookup"><span data-stu-id="2805b-178">You must:</span></span>

* <span data-ttu-id="2805b-179">具備有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2805b-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="2805b-180">具備備份保存庫</span><span class="sxs-lookup"><span data-stu-id="2805b-180">Have a backup vault</span></span>

<span data-ttu-id="2805b-181">toodownload hello 保存庫認證，執行 hello **Get AzureBackupVaultCredentials** cmdlet，它在方便的位置類似 Azure PowerShell 主控台和存放區中 * C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="2805b-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="2805b-182">Hello 保存庫註冊 hello 機器是使用 hello[開始 DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2805b-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="2805b-183">這會向 Microsoft Azure 保存庫，使用指定的 hello hello DPM 伺服器名為"TestingServer 」 保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="2805b-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2805b-184">請勿使用相對路徑 toospecify hello 保存庫認證檔案。</span><span class="sxs-lookup"><span data-stu-id="2805b-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="2805b-185">您必須提供絕對路徑做為輸入的 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="2805b-186">初始組態設定</span><span class="sxs-lookup"><span data-stu-id="2805b-186">Initial configuration settings</span></span>
<span data-ttu-id="2805b-187">一旦 hello DPM 伺服器已向 hello Azure 備份保存庫，就會開始使用預設訂用帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="2805b-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="2805b-188">這些訂用帳戶設定包括網路、 加密和 hello 暫存區域。</span><span class="sxs-lookup"><span data-stu-id="2805b-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="2805b-189">toobegin 變更 hello 訂用帳戶設定需要 toofirst 取得的控制代碼上 hello 現有 （預設值） 的設定使用 hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2805b-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="2805b-190">所有修改都都本機 PowerShell 物件提出的 toothis ```$setting``` hello 完整物件則不認可的 tooDPM 和 Azure 備份 toosave 它們使用 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="2805b-191">您需要 toouse hello ```–Commit``` hello 變更的旗標 tooensure 會保存。</span><span class="sxs-lookup"><span data-stu-id="2805b-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="2805b-192">hello 設定將不套用，Azure 備份所使用，除非已認可。</span><span class="sxs-lookup"><span data-stu-id="2805b-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="2805b-193">網路</span><span class="sxs-lookup"><span data-stu-id="2805b-193">Networking</span></span>
<span data-ttu-id="2805b-194">如果 hello DPM 機器 toohello hello 上的 Azure 備份服務的 hello 連線網際網路，透過 proxy 伺服器 hello proxy 伺服器設定應該提供的備份 toosucceed。</span><span class="sxs-lookup"><span data-stu-id="2805b-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="2805b-195">這是使用 hello ```-ProxyServer```， ```-ProxyPort```，```-ProxyUsername```和 hello```ProxyPassword```參數以 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="2805b-196">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2805b-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="2805b-197">頻寬使用也可以控制選項的```-WorkHourBandwidth```和```-NonWorkHourBandwidth```一組指定的 hello 一週天數。</span><span class="sxs-lookup"><span data-stu-id="2805b-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="2805b-198">本範例未設定任何節流。</span><span class="sxs-lookup"><span data-stu-id="2805b-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="2805b-199">設定 hello 臨時區域</span><span class="sxs-lookup"><span data-stu-id="2805b-199">Configuring hello staging Area</span></span>
<span data-ttu-id="2805b-200">hello DPM 伺服器上執行的 hello Azure 備份代理程式需要暫存位置，還原從 hello 雲端 （本機臨時區域） 的資料。</span><span class="sxs-lookup"><span data-stu-id="2805b-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="2805b-201">設定使用 hello hello 臨時區域[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet 和 hello```-StagingAreaPath```參數。</span><span class="sxs-lookup"><span data-stu-id="2805b-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="2805b-202">Hello 上述範例中，在 hello 臨時區域將太設定*C:\StagingArea* hello PowerShell 物件中```$setting```。</span><span class="sxs-lookup"><span data-stu-id="2805b-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="2805b-203">請確定 hello 指定的資料夾已經存在，否則 hello 最終認可的 hello 訂用帳戶設定將會失敗。</span><span class="sxs-lookup"><span data-stu-id="2805b-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="2805b-204">加密設定</span><span class="sxs-lookup"><span data-stu-id="2805b-204">Encryption settings</span></span>
<span data-ttu-id="2805b-205">hello 傳送備份資料 tooAzure 備份是加密的 tooprotect hello hello 資料機密性。</span><span class="sxs-lookup"><span data-stu-id="2805b-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="2805b-206">hello 加密複雜密碼是還原的 hello 「 密碼 」 toodecrypt hello 資料在 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="2805b-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="2805b-207">它是重要 tookeep 此資訊安全，而且一旦設定保護。</span><span class="sxs-lookup"><span data-stu-id="2805b-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="2805b-208">Hello 下列範例中，在 hello 第一個命令會將轉換字串 hello ```passphrase123456789``` tooa 安全字串，並指派 hello 安全字串 toohello 名為變數```$Passphrase```。</span><span class="sxs-lookup"><span data-stu-id="2805b-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="2805b-209">hello 第二個命令設定安全字串的 hello```$Passphrase```當做 hello 密碼加密備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="2805b-210">安全及安全一旦設定之後，保留 hello 複雜密碼資訊。</span><span class="sxs-lookup"><span data-stu-id="2805b-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="2805b-211">您不會將資料從 Azure 可以 toorestore 沒有此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="2805b-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="2805b-212">此時，您應該做所有所需的 hello 變更 toohello```$setting```物件。</span><span class="sxs-lookup"><span data-stu-id="2805b-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="2805b-213">請記住 toocommit hello 變更。</span><span class="sxs-lookup"><span data-stu-id="2805b-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="2805b-214">保護資料 tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="2805b-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="2805b-215">在本節中，您將加入實際執行伺服器 tooDPM，然後保護 hello 資料 toolocal DPM 存放裝置，然後 tooAzure 備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="2805b-216">Hello 範例中，我們將示範如何 tooback 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="2805b-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="2805b-217">hello 邏輯很容易就能擴充的 toobackup 任何 DPM 支援的資料來源。</span><span class="sxs-lookup"><span data-stu-id="2805b-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="2805b-218">所有 DPM 備份皆受到保護群組 (PG) 所控管，並且由四個部分構成：</span><span class="sxs-lookup"><span data-stu-id="2805b-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="2805b-219">**群組成員**是所有的 hello 可保護物件的清單 (也稱為*Datasources*在 DPM 中) 您想在 hello tooprotect 相同的保護群組。</span><span class="sxs-lookup"><span data-stu-id="2805b-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="2805b-220">比方說，您可能想 tooprotect 生產 Vm 一個保護群組與另一個保護群組中的 SQL Server 資料庫中，因為它們可能會有不同的備份需求。</span><span class="sxs-lookup"><span data-stu-id="2805b-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="2805b-221">您可以在實際伺服器上備份任何資料來源必須先確定 toomake hello hello 伺服器上安裝 DPM 代理程式，並由 DPM 管理。</span><span class="sxs-lookup"><span data-stu-id="2805b-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="2805b-222">請依照下列步驟 hello[安裝 hello DPM 代理程式](https://technet.microsoft.com/library/bb870935.aspx)並將其連結 toohello 適當的 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2805b-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="2805b-223">**資料保護方式**指定 hello 目標備份位置-磁帶、 磁碟和雲端。</span><span class="sxs-lookup"><span data-stu-id="2805b-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="2805b-224">在本例中，我們會保護資料 toohello 本機磁碟和 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="2805b-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="2805b-225">A**備份排程**，會指定備份時需要採取 toobe hello 資料應該同步處理頻率 hello DPM 伺服器與 hello 實際執行伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="2805b-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="2805b-226">A**保留排程**指定 tooretain hello 復原點在 Azure 中的時間長度。</span><span class="sxs-lookup"><span data-stu-id="2805b-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="2805b-227">建立保護群組</span><span class="sxs-lookup"><span data-stu-id="2805b-227">Creating a protection group</span></span>
<span data-ttu-id="2805b-228">開始建立新的保護群組使用 hello[新增 DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="2805b-229">hello 以上指令程式會建立名為保護群組*ProtectGroup01*。</span><span class="sxs-lookup"><span data-stu-id="2805b-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="2805b-230">現有的保護群組也可以修改更新 tooadd 備份 toohello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="2805b-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="2805b-231">不過，toomake 的任何變更 toohello 新保護群組的或現有的-我們需要 tooget 控制代碼上*可修改*物件使用 hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="2805b-232">加入群組成員 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="2805b-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="2805b-233">每個 DPM 代理程式知道 hello hello 其安裝所在的伺服器上的資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="2805b-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="2805b-234">tooadd datasource toohello 保護群組，DPM 代理程式需求 toofirst hello 傳送 hello 資料來源後 toohello DPM 伺服器的清單。</span><span class="sxs-lookup"><span data-stu-id="2805b-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="2805b-235">一或多個資料來源會選取並加入 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="2805b-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="2805b-236">hello PowerShell 所需的步驟 tooget 來達成此：</span><span class="sxs-lookup"><span data-stu-id="2805b-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="2805b-237">擷取由 DPM 管理透過 hello DPM 代理程式的所有伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="2805b-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="2805b-238">選擇特定伺服器。</span><span class="sxs-lookup"><span data-stu-id="2805b-238">Choose a specific server.</span></span>
3. <span data-ttu-id="2805b-239">擷取 hello 伺服器上的所有資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="2805b-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="2805b-240">選擇一或多個資料來源，並將其新增 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="2805b-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="2805b-241">伺服器的 hello DPM 代理程式已安裝且受 DPM 伺服器 hello hello 清單取得以 hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="2805b-242">在此範例中，我們將篩選並只設定名稱為 *productionserver01* 的 PS 來進行備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="2805b-243">上的 立即擷取的資料來源的 hello 清單```$server```使用 hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="2805b-244">在此範例中我們會篩選 hello 磁碟區 * d:\*我們想要備份的 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="2805b-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="2805b-245">此資料來源，然後會加入 toohello 保護群組使用 hello[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="2805b-246">請記住 toouse hello *modifable*保護群組物件```$MPG```toomake hello 新增項目。</span><span class="sxs-lookup"><span data-stu-id="2805b-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="2805b-247">重複此步驟，視需要多次直到您已經新增所有 hello 選擇資料來源 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="2805b-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="2805b-248">您也可以只有一個資料來源，以及用於建立 hello 保護群組的完整 hello 工作流程的開頭，並在稍後加入更多的資料來源 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="2805b-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="2805b-249">選取 hello 資料保護方式</span><span class="sxs-lookup"><span data-stu-id="2805b-249">Selecting hello data protection method</span></span>
<span data-ttu-id="2805b-250">一旦 hello 資料來源已加入 toohello 保護群組，hello 下一個步驟是使用 hello toospecify hello 保護方法[組 DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="2805b-251">在此範例中，hello 保護群組將會安裝本機磁碟和雲端備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="2805b-252">您也需要您想使用 hello tooprotect toocloud toospecify hello datasource[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet 搭配-線上旗標。</span><span class="sxs-lookup"><span data-stu-id="2805b-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="2805b-253">設定 hello 保留範圍</span><span class="sxs-lookup"><span data-stu-id="2805b-253">Setting hello retention range</span></span>
<span data-ttu-id="2805b-254">設定使用 hello hello 備份點 hello 保留[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="2805b-255">雖然看起來奇數 tooset hello 保留之前 hello 備份排程已定義，使用 hello```Set-DPMPolicyObjective```指令程式會自動設定預設的備份排程，其可以加以修改。</span><span class="sxs-lookup"><span data-stu-id="2805b-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="2805b-256">它永遠是可能 tooset hello 備份排程第一次，並 hello 之後保留原則。</span><span class="sxs-lookup"><span data-stu-id="2805b-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="2805b-257">Hello 下列範例中，在 hello cmdlet 會設定 hello 保持參數對於磁碟備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="2805b-258">這將會保留備份的 10 天，並同步處理資料之間 hello 實際伺服器與 hello DPM 伺服器每隔 6 小時。</span><span class="sxs-lookup"><span data-stu-id="2805b-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="2805b-259">hello```SynchronizationFrequencyMinutes```頻率備份點建立時，如何但不會定義通常資料會複製的 toohello DPM 伺服器，如此可防止備份變得太大。</span><span class="sxs-lookup"><span data-stu-id="2805b-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="2805b-260">備份將的 tooAzure （DPM 會參照為線上備份 toothese） hello 的保留範圍可以設定成[長期的保留使用祖父-父親-Son 配置 (GFS)](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="2805b-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="2805b-261">也就是說，您可以定義結合的保留原則，包含每日、每週、每月和每年保留原則。</span><span class="sxs-lookup"><span data-stu-id="2805b-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="2805b-262">在此範例中，我們建立陣列，表示我們想要的 hello 複雜的保留配置，然後設定使用 hello hello 保留範圍[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="2805b-263">設定 hello 的備份排程</span><span class="sxs-lookup"><span data-stu-id="2805b-263">Set hello backup schedule</span></span>
<span data-ttu-id="2805b-264">DPM 預設備份的排程自動設定如果您指定使用 hello hello 保護目標```Set-DPMPolicyObjective```cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="2805b-265">toochange hello 預設排程，使用 hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet 加 hello[組 DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="2805b-266">在 hello 上述範例中，```$onlineSch```是四個元素陣列，其中包含 hello 現有的線上保護排程 hello GFS 配置中的 hello 保護群組：</span><span class="sxs-lookup"><span data-stu-id="2805b-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="2805b-267">```$onlineSch[0]```將包含 hello 每日排程</span><span class="sxs-lookup"><span data-stu-id="2805b-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="2805b-268">```$onlineSch[1]```將包含 hello 每週排程</span><span class="sxs-lookup"><span data-stu-id="2805b-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="2805b-269">```$onlineSch[2]```將包含 hello 每月排程</span><span class="sxs-lookup"><span data-stu-id="2805b-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="2805b-270">```$onlineSch[3]```將包含 hello 每年的排程</span><span class="sxs-lookup"><span data-stu-id="2805b-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="2805b-271">因此，如果您需要 toomodify hello 每週排程，您需要 toorefer toohello ```$onlineSch[1]```。</span><span class="sxs-lookup"><span data-stu-id="2805b-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="2805b-272">初始備份</span><span class="sxs-lookup"><span data-stu-id="2805b-272">Initial backup</span></span>
<span data-ttu-id="2805b-273">當第一次備份 hello 的資料來源，DPM 需要 toocreate 這將會建立一份 hello datasource toobe 受保護的 DPM 複本磁碟區上的初始複本。</span><span class="sxs-lookup"><span data-stu-id="2805b-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="2805b-274">此活動可以特定的時間，排程，或可以觸發以手動方式，使用 hello[組 DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet 搭配 hello 參數```-NOW```。</span><span class="sxs-lookup"><span data-stu-id="2805b-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="2805b-275">變更 hello 的 DPM 複本與復原點磁碟區的大小</span><span class="sxs-lookup"><span data-stu-id="2805b-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="2805b-276">您也可以變更的 DPM 複本磁碟區，以及陰影複製磁碟區使用的 hello 大小[組 DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet，如下列範例中的 hello 所示： Get-datasourcediskallocation Datasource $DSSet-datasourcediskallocation-Datasource $DS-ProtectionGroup $MPG-手動 ReplicaArea (2 gb) ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="2805b-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="2805b-277">認可 hello 變更 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="2805b-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="2805b-278">最後，hello 變更需要 toobe 認可 DPM 才會每個新保護群組組態 hello hello 備份。</span><span class="sxs-lookup"><span data-stu-id="2805b-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="2805b-279">這是使用 hello[組 DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="2805b-280">檢視 hello 備份點</span><span class="sxs-lookup"><span data-stu-id="2805b-280">View hello backup points</span></span>
<span data-ttu-id="2805b-281">您可以使用 hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget 一份所有資料來源的復原點。</span><span class="sxs-lookup"><span data-stu-id="2805b-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="2805b-282">在此範例中，我們將會：</span><span class="sxs-lookup"><span data-stu-id="2805b-282">In this example, we will:</span></span>

* <span data-ttu-id="2805b-283">擷取所有的 hello PGs hello DPM 伺服器會儲存在陣列上```$PG```</span><span class="sxs-lookup"><span data-stu-id="2805b-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="2805b-284">取得 hello 資料來源對應 toohello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="2805b-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="2805b-285">取得資料來源中的 hello 的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="2805b-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="2805b-286">還原在 Azure 上保護的資料</span><span class="sxs-lookup"><span data-stu-id="2805b-286">Restore data protected on Azure</span></span>
<span data-ttu-id="2805b-287">還原資料是 ```RecoverableItem``` 物件和 ```RecoveryOption``` 物件的組合。</span><span class="sxs-lookup"><span data-stu-id="2805b-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="2805b-288">Hello 前一節中得到 hello 備份點清單的資料來源。</span><span class="sxs-lookup"><span data-stu-id="2805b-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="2805b-289">在 hello 下列範例中，我們示範 toorestore HYPER-V 虛擬機器，從 Azure Backup 以 hello 結合備份點進行復原的目標。</span><span class="sxs-lookup"><span data-stu-id="2805b-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="2805b-290">其中包括：</span><span class="sxs-lookup"><span data-stu-id="2805b-290">This includes:</span></span>

* <span data-ttu-id="2805b-291">建立的復原選項使用 hello[新增 DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="2805b-292">使用 hello 的備份點擷取 hello 陣列```Get-DPMRecoveryPoint```cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2805b-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="2805b-293">選擇從備份點 toorestore。</span><span class="sxs-lookup"><span data-stu-id="2805b-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="2805b-294">任何資料來源類型時，可以輕鬆地擴充 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="2805b-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2805b-295">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2805b-295">Next steps</span></span>
* <span data-ttu-id="2805b-296">如需 Azure 備份的 DPM，請參閱[簡介 tooDPM 備份](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2805b-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
