---
title: "備份-使用 PowerShell tooback DPM 工作負載備份 aaaAzure |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理 Azure 備份的 Data Protection Manager (DPM) 使用 PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="fb4f1-103">部署和管理備份 tooAzure Data Protection Manager (DPM) 伺服器使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb4f1-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb4f1-104">ARM</span><span class="sxs-lookup"><span data-stu-id="fb4f1-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="fb4f1-105">傳統</span><span class="sxs-lookup"><span data-stu-id="fb4f1-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="fb4f1-106">本文章將示範如何 toouse PowerShell toosetup Azure 備份上的 DPM 伺服器和 toomanage 備份和復原。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="fb4f1-107">設定 hello PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="fb4f1-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="fb4f1-108">您可以使用從 Data Protection Manager tooAzure PowerShell toomanage 備份之前，您必須在 PowerShell 中的 toohave hello 右環境。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="fb4f1-109">在 hello 開頭 hello PowerShell 工作階段，請確定您執行下列命令 tooimport hello 右模組 hello 和 toocorrectly 參考 hello DPM 指令程式可讓您：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="fb4f1-110">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="fb4f1-110">Setup and Registration</span></span>
<span data-ttu-id="fb4f1-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="fb4f1-111">toobegin:</span></span>

1. <span data-ttu-id="fb4f1-112">[下載最新版 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需的基本版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="fb4f1-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="fb4f1-113">啟用 hello Azure 備份指令程式，藉由切換太*AzureResourceManager*模式使用 hello **Switch-azuremode**指令程式：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="fb4f1-114">hello 下列安裝和註冊工作可以自動化使用 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb4f1-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="fb4f1-115">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="fb4f1-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="fb4f1-116">安裝 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="fb4f1-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="fb4f1-117">註冊以 hello Azure 備份服務</span><span class="sxs-lookup"><span data-stu-id="fb4f1-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="fb4f1-118">網路設定</span><span class="sxs-lookup"><span data-stu-id="fb4f1-118">Networking settings</span></span>
* <span data-ttu-id="fb4f1-119">加密設定</span><span class="sxs-lookup"><span data-stu-id="fb4f1-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fb4f1-120">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="fb4f1-120">Create a recovery services vault</span></span>
<span data-ttu-id="fb4f1-121">hello 步驟會引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="fb4f1-122">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="fb4f1-123">如果您使用 Azure Backup hello 第一次，您必須使用 hello**暫存器 AzureRMResourceProvider** cmdlet tooregister hello Azure 復原服務提供者與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="fb4f1-124">hello 復原服務保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="fb4f1-125">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="fb4f1-126">建立新的資源群組時，指定 hello 名稱和位置 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="fb4f1-127">使用 hello**新增 AzureRmRecoveryServicesVault** cmdlet toocreate 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="fb4f1-128">請務必 toospecify hello hello 保存庫相同的位置，所用的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="fb4f1-129">指定儲存體備援 toouse; hello 類型您可以使用[本機備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage)或[地理備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="fb4f1-130">hello 下列範例顯示 hello testVault-BackupStorageRedundancy 選項設定 tooGeoRedundant。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="fb4f1-131">許多 Azure Backup cmdlet 需要 hello 復原服務保存庫的物件做為輸入。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="fb4f1-132">基於這個理由，它是方便 toostore hello 備份復原服務保存庫在變數中。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="fb4f1-133">檢視訂用帳戶中的 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="fb4f1-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="fb4f1-134">使用**Get AzureRmRecoveryServicesVault** tooview hello 份 hello 目前訂用帳戶中所有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="fb4f1-135">您可以使用，則已建立新的保存庫，此命令 toocheck 或 toosee hello 訂用帳戶中有哪些保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="fb4f1-136">執行 hello 命令，取得 AzureRmRecoveryServicesVault，並列出 hello 訂用帳戶中所有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="fb4f1-137">在 DPM 伺服器上安裝 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="fb4f1-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="fb4f1-138">安裝 hello Azure Backup agent 之前，您需要 toohave hello 安裝程式，下載和 hello Windows Server 上也一樣。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="fb4f1-139">收到 hello 的 hello 最新版本的 hello installer [Microsoft Download Center](http://aka.ms/azurebackup_agent)或從 hello 復原服務保存庫的 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="fb4f1-140">儲存 hello installer tooan 更容易存取的位置，例如 * C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="fb4f1-141">tooinstall hello 代理程式，執行下列命令，在提升權限的 PowerShell 主控台中的 hello **hello DPM 伺服器上**:</span><span class="sxs-lookup"><span data-stu-id="fb4f1-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="fb4f1-142">這會 hello 代理程式安裝與所有 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="fb4f1-143">hello 安裝需要幾分鐘 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="fb4f1-144">如果您未指定 hello */nu*選項 hello **Windows Update**視窗隨即開啟的任何更新的 hello 安裝 toocheck hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="fb4f1-145">hello 代理程式會在顯示 hello 的安裝程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="fb4f1-146">toosee hello 列出已安裝的程式，請移過**控制台** > **程式** > **程式和功能**。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="fb4f1-148">安裝選項</span><span class="sxs-lookup"><span data-stu-id="fb4f1-148">Installation options</span></span>
<span data-ttu-id="fb4f1-149">toosee 所有 hello 選項可透過 hello 命令列，使用 hello 下列都命令：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="fb4f1-150">hello 可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-150">hello available options include:</span></span>

| <span data-ttu-id="fb4f1-151">選項</span><span class="sxs-lookup"><span data-stu-id="fb4f1-151">Option</span></span> | <span data-ttu-id="fb4f1-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="fb4f1-152">Details</span></span> | <span data-ttu-id="fb4f1-153">預設值</span><span class="sxs-lookup"><span data-stu-id="fb4f1-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb4f1-154">/q</span><span class="sxs-lookup"><span data-stu-id="fb4f1-154">/q</span></span> |<span data-ttu-id="fb4f1-155">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="fb4f1-155">Quiet installation</span></span> |- |
| <span data-ttu-id="fb4f1-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="fb4f1-156">/p:"location"</span></span> |<span data-ttu-id="fb4f1-157">路徑 toohello hello Azure Backup agent 的安裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="fb4f1-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="fb4f1-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="fb4f1-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="fb4f1-159">/s:"location"</span></span> |<span data-ttu-id="fb4f1-160">路徑 toohello hello Azure 備份代理程式的快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="fb4f1-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="fb4f1-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="fb4f1-162">/m</span><span class="sxs-lookup"><span data-stu-id="fb4f1-162">/m</span></span> |<span data-ttu-id="fb4f1-163">選擇加入 tooMicrosoft 更新</span><span class="sxs-lookup"><span data-stu-id="fb4f1-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="fb4f1-164">/nu</span><span class="sxs-lookup"><span data-stu-id="fb4f1-164">/nu</span></span> |<span data-ttu-id="fb4f1-165">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="fb4f1-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="fb4f1-166">/d</span><span class="sxs-lookup"><span data-stu-id="fb4f1-166">/d</span></span> |<span data-ttu-id="fb4f1-167">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="fb4f1-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="fb4f1-168">/ph</span><span class="sxs-lookup"><span data-stu-id="fb4f1-168">/ph</span></span> |<span data-ttu-id="fb4f1-169">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="fb4f1-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="fb4f1-170">/po</span><span class="sxs-lookup"><span data-stu-id="fb4f1-170">/po</span></span> |<span data-ttu-id="fb4f1-171">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="fb4f1-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="fb4f1-172">/pu</span><span class="sxs-lookup"><span data-stu-id="fb4f1-172">/pu</span></span> |<span data-ttu-id="fb4f1-173">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="fb4f1-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="fb4f1-174">/pw</span><span class="sxs-lookup"><span data-stu-id="fb4f1-174">/pw</span></span> |<span data-ttu-id="fb4f1-175">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="fb4f1-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="fb4f1-176">註冊 DPM tooa 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="fb4f1-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="fb4f1-177">建立 hello 復原服務保存庫之後，請下載 hello 最新的代理程式 」 和 「 hello 保存庫認證，並將它儲存在方便的位置，例如 C:\Downloads。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="fb4f1-178">Hello DPM 伺服器上，執行 hello [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) hello 保存庫 cmdlet tooregister hello 機器。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="fb4f1-179">初始組態設定</span><span class="sxs-lookup"><span data-stu-id="fb4f1-179">Initial configuration settings</span></span>
<span data-ttu-id="fb4f1-180">一旦 hello DPM 伺服器以 hello 註冊復原服務保存庫，開始的預設訂用帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="fb4f1-181">這些訂用帳戶設定包括網路、 加密和 hello 暫存區域。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="fb4f1-182">您需要 toofirst toochange 訂用帳戶設定取得的控制代碼上 hello 現有 （預設值） 的設定使用 hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fb4f1-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="fb4f1-183">所有修改都都本機 PowerShell 物件提出的 toothis ```$setting``` hello 完整物件則不認可的 tooDPM 和 Azure 備份 toosave 它們使用 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="fb4f1-184">您需要 toouse hello ```–Commit``` hello 變更的旗標 tooensure 會保存。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="fb4f1-185">hello 設定將不套用，Azure 備份所使用，除非已認可。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="fb4f1-186">網路</span><span class="sxs-lookup"><span data-stu-id="fb4f1-186">Networking</span></span>
<span data-ttu-id="fb4f1-187">如果 hello DPM 機器 toohello hello 上的 Azure 備份服務的 hello 連線網際網路，透過 proxy 伺服器 hello proxy 伺服器設定應該提供的成功備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="fb4f1-188">這是使用 hello```-ProxyServer```和```-ProxyPort```，```-ProxyUsername```和 hello```ProxyPassword```參數以 hello[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="fb4f1-189">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="fb4f1-190">頻寬使用也可以控制選項的```-WorkHourBandwidth```和```-NonWorkHourBandwidth```一組指定的 hello 一週天數。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="fb4f1-191">本範例未設定任何節流。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="fb4f1-192">設定 hello 臨時區域</span><span class="sxs-lookup"><span data-stu-id="fb4f1-192">Configuring hello staging Area</span></span>
<span data-ttu-id="fb4f1-193">hello DPM 伺服器上執行的 hello Azure 備份代理程式需要暫存位置，還原從 hello 雲端 （本機臨時區域） 的資料。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="fb4f1-194">設定使用 hello hello 臨時區域[組 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet 和 hello```-StagingAreaPath```參數。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="fb4f1-195">Hello 上述範例中，在 hello 臨時區域將太設定*C:\StagingArea* hello PowerShell 物件中```$setting```。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="fb4f1-196">請確定 hello 指定的資料夾已經存在，否則 hello 最終認可的 hello 訂用帳戶設定將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="fb4f1-197">加密設定</span><span class="sxs-lookup"><span data-stu-id="fb4f1-197">Encryption settings</span></span>
<span data-ttu-id="fb4f1-198">hello 傳送備份資料 tooAzure 備份是加密的 tooprotect hello hello 資料機密性。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="fb4f1-199">hello 加密複雜密碼是還原的 hello 「 密碼 」 toodecrypt hello 資料在 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="fb4f1-200">它是重要 tookeep 此資訊安全，而且一旦設定保護。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="fb4f1-201">Hello 下列範例中，在 hello 第一個命令會將轉換字串 hello ```passphrase123456789``` tooa 安全字串，並指派 hello 安全字串 toohello 名為變數```$Passphrase```。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="fb4f1-202">hello 第二個命令設定安全字串的 hello```$Passphrase```當做 hello 密碼加密備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="fb4f1-203">安全及安全一旦設定之後，保留 hello 複雜密碼資訊。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="fb4f1-204">您不會將資料從 Azure 可以 toorestore 沒有此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="fb4f1-205">此時，您應該做所有所需的 hello 變更 toohello```$setting```物件。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="fb4f1-206">請記住 toocommit hello 變更。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="fb4f1-207">保護資料 tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="fb4f1-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="fb4f1-208">在本節中，您將加入實際執行伺服器 tooDPM，然後保護 hello 資料 toolocal DPM 存放裝置，然後 tooAzure 備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="fb4f1-209">在 hello 範例中，我們將示範如何 tooback 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="fb4f1-210">hello 邏輯很容易就能擴充的 toobackup 任何 DPM 支援的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="fb4f1-211">所有 DPM 備份皆受到保護群組 (PG) 所控管，並且由四個部分構成：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="fb4f1-212">**群組成員**是所有的 hello 可保護物件的清單 (也稱為*Datasources*在 DPM 中) 您想在 hello tooprotect 相同的保護群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="fb4f1-213">比方說，您可能想 tooprotect 生產 Vm 一個保護群組與另一個保護群組中的 SQL Server 資料庫中，因為它們可能會有不同的備份需求。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="fb4f1-214">您可以在實際伺服器上備份任何資料來源必須先確定 toomake hello hello 伺服器上安裝 DPM 代理程式，並由 DPM 管理。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="fb4f1-215">請依照下列步驟 hello[安裝 hello DPM 代理程式](https://technet.microsoft.com/library/bb870935.aspx)並將其連結 toohello 適當的 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="fb4f1-216">**資料保護方式**指定 hello 目標備份位置-磁帶、 磁碟和雲端。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="fb4f1-217">在本例中，我們會保護資料 toohello 本機磁碟和 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="fb4f1-218">A**備份排程**，會指定備份時需要採取 toobe hello 資料應該同步處理頻率 hello DPM 伺服器與 hello 實際執行伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="fb4f1-219">A**保留排程**指定 tooretain hello 復原點在 Azure 中的時間長度。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="fb4f1-220">建立保護群組</span><span class="sxs-lookup"><span data-stu-id="fb4f1-220">Creating a protection group</span></span>
<span data-ttu-id="fb4f1-221">開始建立新的保護群組使用 hello[新增 DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="fb4f1-222">hello 以上指令程式會建立名為保護群組*ProtectGroup01*。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="fb4f1-223">現有的保護群組也可以修改更新 tooadd 備份 toohello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="fb4f1-224">不過，toomake 的任何變更 toohello 新保護群組的或現有的-我們需要 tooget 控制代碼上*可修改*物件使用 hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="fb4f1-225">加入群組成員 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="fb4f1-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="fb4f1-226">每個 DPM 代理程式知道 hello hello 其安裝所在的伺服器上的資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="fb4f1-227">tooadd datasource toohello 保護群組，DPM 代理程式需求 toofirst hello 傳送 hello 資料來源後 toohello DPM 伺服器的清單。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="fb4f1-228">一或多個資料來源會選取並加入 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="fb4f1-229">這是的 tooachieve 需要 hello PowerShell 步驟：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="fb4f1-230">擷取由 DPM 管理透過 hello DPM 代理程式的所有伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="fb4f1-231">選擇特定伺服器。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-231">Choose a specific server.</span></span>
3. <span data-ttu-id="fb4f1-232">擷取 hello 伺服器上的所有資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="fb4f1-233">選擇一或多個資料來源，並將其新增 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="fb4f1-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="fb4f1-234">伺服器的 hello DPM 代理程式已安裝且受 DPM 伺服器 hello hello 清單取得以 hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="fb4f1-235">在此範例中，我們將篩選並只設定名稱為 *productionserver01* 的 PS 來進行備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="fb4f1-236">上的 立即擷取的資料來源的 hello 清單```$server```使用 hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="fb4f1-237">在此範例中我們會篩選 hello 磁碟區 * d:\*我們想 tooconfigure 進行備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="fb4f1-238">此資料來源，然後會加入 toohello 保護群組使用 hello[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="fb4f1-239">請記住 toouse hello*可修改*保護群組物件```$MPG```toomake hello 新增項目。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="fb4f1-240">重複此步驟，視需要多次直到您已經新增所有 hello 選擇資料來源 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="fb4f1-241">您也可以只有一個資料來源，以及用於建立 hello 保護群組的完整 hello 工作流程的開頭，並在稍後加入更多的資料來源 toohello 保護群組。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="fb4f1-242">選取 hello 資料保護方式</span><span class="sxs-lookup"><span data-stu-id="fb4f1-242">Selecting hello data protection method</span></span>
<span data-ttu-id="fb4f1-243">一旦 hello 資料來源已加入 toohello 保護群組，hello 下一個步驟是使用 hello toospecify hello 保護方法[組 DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="fb4f1-244">在此範例中，hello 保護群組都已設定本機磁碟和雲端備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="fb4f1-245">您也需要您想使用 hello tooprotect toocloud toospecify hello datasource[新增 DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet 搭配-線上旗標。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="fb4f1-246">設定 hello 保留範圍</span><span class="sxs-lookup"><span data-stu-id="fb4f1-246">Setting hello retention range</span></span>
<span data-ttu-id="fb4f1-247">設定使用 hello hello 備份點 hello 保留[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="fb4f1-248">雖然看起來奇數 tooset hello 保留之前 hello 備份排程已定義，使用 hello```Set-DPMPolicyObjective```指令程式會自動設定預設的備份排程，其可以加以修改。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="fb4f1-249">它永遠是可能 tooset hello 備份排程第一次，並 hello 之後保留原則。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="fb4f1-250">Hello 下列範例中，在 hello cmdlet 會設定 hello 保持參數對於磁碟備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="fb4f1-251">這將會保留備份的 10 天，並同步處理資料之間 hello 實際伺服器與 hello DPM 伺服器每隔 6 小時。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="fb4f1-252">hello```SynchronizationFrequencyMinutes```頻率備份點建立時，如何但不會定義通常資料會複製的 toohello DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="fb4f1-253">此設定可防止備份變得太大。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="fb4f1-254">備份將的 tooAzure （DPM 會參照為線上備份 toothem） hello 的保留範圍可以設定成[長期的保留使用祖父-父親-Son 配置 (GFS)](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="fb4f1-255">也就是說，您可以定義結合的保留原則，包含每日、每週、每月和每年保留原則。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="fb4f1-256">在此範例中，我們建立陣列，表示我們想要的 hello 複雜的保留配置，然後設定使用 hello hello 保留範圍[組 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="fb4f1-257">設定 hello 的備份排程</span><span class="sxs-lookup"><span data-stu-id="fb4f1-257">Set hello backup schedule</span></span>
<span data-ttu-id="fb4f1-258">DPM 預設備份的排程自動設定如果您指定使用 hello hello 保護目標```Set-DPMPolicyObjective```cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="fb4f1-259">toochange hello 預設排程，使用 hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet 加 hello[組 DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="fb4f1-260">在上述範例中，hello```$onlineSch```是四個元素陣列，其中包含 hello 現有的線上保護排程 hello GFS 配置中的 hello 保護群組：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="fb4f1-261">```$onlineSch[0]```包含 hello 每日排程</span><span class="sxs-lookup"><span data-stu-id="fb4f1-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="fb4f1-262">```$onlineSch[1]```包含 hello 每週排程</span><span class="sxs-lookup"><span data-stu-id="fb4f1-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="fb4f1-263">```$onlineSch[2]```包含 hello 每月排程</span><span class="sxs-lookup"><span data-stu-id="fb4f1-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="fb4f1-264">```$onlineSch[3]```包含 hello 每年的排程</span><span class="sxs-lookup"><span data-stu-id="fb4f1-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="fb4f1-265">因此，如果您需要 toomodify hello 每週排程，您需要 toorefer toohello ```$onlineSch[1]```。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="fb4f1-266">初始備份</span><span class="sxs-lookup"><span data-stu-id="fb4f1-266">Initial backup</span></span>
<span data-ttu-id="fb4f1-267">當備份 hello datasource 第一次，DPM 必須建立初始複本的建立 hello datasource toobe 受保護的 DPM 複本磁碟區上的完整複本。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="fb4f1-268">此活動可以特定的時間，排程，或可以觸發以手動方式，使用 hello[組 DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet 搭配 hello 參數```-NOW```。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="fb4f1-269">變更 hello 的 DPM 複本與復原點磁碟區的大小</span><span class="sxs-lookup"><span data-stu-id="fb4f1-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="fb4f1-270">您也可以變更 DPM 複本磁碟區和陰影複製磁碟區使用的 hello 大小[組 DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet，如 hello 下列範例所示： Get-datasourcediskallocation Datasource $DSSet-datasourcediskallocation-Datasource $DS-ProtectionGroup $MPG-手動 ReplicaArea (2 gb) ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="fb4f1-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="fb4f1-271">認可 hello 變更 toohello 保護群組</span><span class="sxs-lookup"><span data-stu-id="fb4f1-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="fb4f1-272">最後，hello 變更需要 toobe 認可 DPM 才會每個新保護群組組態 hello hello 備份。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="fb4f1-273">這可以使用 hello[組 DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="fb4f1-274">檢視 hello 備份點</span><span class="sxs-lookup"><span data-stu-id="fb4f1-274">View hello backup points</span></span>
<span data-ttu-id="fb4f1-275">您可以使用 hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget 一份所有資料來源的復原點。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="fb4f1-276">在此範例中，我們將會：</span><span class="sxs-lookup"><span data-stu-id="fb4f1-276">In this example, we will:</span></span>

* <span data-ttu-id="fb4f1-277">擷取所有 hello PGs hello DPM 伺服器上，並儲存在陣列中```$PG```</span><span class="sxs-lookup"><span data-stu-id="fb4f1-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="fb4f1-278">取得 hello 資料來源對應 toohello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="fb4f1-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="fb4f1-279">取得資料來源中的 hello 的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="fb4f1-280">還原在 Azure 上保護的資料</span><span class="sxs-lookup"><span data-stu-id="fb4f1-280">Restore data protected on Azure</span></span>
<span data-ttu-id="fb4f1-281">還原資料是 ```RecoverableItem``` 物件和 ```RecoveryOption``` 物件的組合。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="fb4f1-282">Hello 前一節中得到 hello 備份點清單的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="fb4f1-283">在 hello 下列範例中，我們示範 toorestore HYPER-V 虛擬機器，從 Azure Backup 以 hello 結合備份點進行復原的目標。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="fb4f1-284">這個範例包含︰</span><span class="sxs-lookup"><span data-stu-id="fb4f1-284">This example includes:</span></span>

* <span data-ttu-id="fb4f1-285">建立的復原選項使用 hello[新增 DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="fb4f1-286">使用 hello 的備份點擷取 hello 陣列```Get-DPMRecoveryPoint```cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="fb4f1-287">選擇從備份點 toorestore。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="fb4f1-288">任何資料來源類型時，可以輕鬆地擴充 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="fb4f1-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb4f1-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb4f1-289">Next steps</span></span>
* <span data-ttu-id="fb4f1-290">如需有關 DPM tooAzure 備份請參閱[簡介 tooDPM 備份](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="fb4f1-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
