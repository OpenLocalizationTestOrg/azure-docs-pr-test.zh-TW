---
title: "Azure 備份 - 使用 PowerShell 備份 DPM 工作負載 | Microsoft Docs"
description: "了解如何使用 PowerShell 部署和管理 Data Protection Manager (DPM) 的 Azure 備份"
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
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="fd8dc-103">使用 PowerShell 部署和管理 Data Protection Manager (DPM) 伺服器的 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="fd8dc-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd8dc-104">ARM</span><span class="sxs-lookup"><span data-stu-id="fd8dc-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="fd8dc-105">傳統</span><span class="sxs-lookup"><span data-stu-id="fd8dc-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="fd8dc-106">本文說明如何使用 PowerShell 來設定 DPM 伺服器上的 Azure 備份以及管理備份和復原。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="fd8dc-107">設定 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="fd8dc-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="fd8dc-108">在可以使用 PowerShell 來管理 Data Protection Manager 的 Azure 備份之前，您必須在 PowerShell 中具備適當的環境。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="fd8dc-109">在 PowerShell 工作階段開始時，請確定您執行下列命令來匯入正確的模組並可讓您正確地參考 DPM Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="fd8dc-110">設定和註冊</span><span class="sxs-lookup"><span data-stu-id="fd8dc-110">Setup and Registration</span></span>
<span data-ttu-id="fd8dc-111">開始：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-111">To begin:</span></span>

1. <span data-ttu-id="fd8dc-112">[下載最新版 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需的基本版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="fd8dc-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="fd8dc-113">使用 *Switch-AzureMode* Cmdlet 切換至 **AzureResourceManager** 模式，以啟用 Azure 備份 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="fd8dc-114">PowerShell 可以自動化下列設定和註冊工作：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="fd8dc-115">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="fd8dc-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="fd8dc-116">安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="fd8dc-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="fd8dc-117">向 Azure 備份服務進行註冊</span><span class="sxs-lookup"><span data-stu-id="fd8dc-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="fd8dc-118">網路設定</span><span class="sxs-lookup"><span data-stu-id="fd8dc-118">Networking settings</span></span>
* <span data-ttu-id="fd8dc-119">加密設定</span><span class="sxs-lookup"><span data-stu-id="fd8dc-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fd8dc-120">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="fd8dc-120">Create a recovery services vault</span></span>
<span data-ttu-id="fd8dc-121">下列步驟將引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="fd8dc-122">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="fd8dc-123">如果您是第一次使用 Azure 備份，您必須使用 **Register-AzureRMResourceProvider** Cmdlet 利用您的訂用帳戶來註冊 Azure 復原服務提供者。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="fd8dc-124">復原服務保存庫是 ARM 資源，因此您必須將它放在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="fd8dc-125">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="fd8dc-126">建立新的資源群組時，請指定資源群組的名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="fd8dc-127">使用 **New-AzureRmRecoveryServicesVault** Cmdlet 來建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="fd8dc-128">請務必為保存庫指定與用於資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="fd8dc-129">指定要使用的儲存體備援類型；您可以使用[本地備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) 或[異地備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="fd8dc-130">以下範例示範 testVault 設定為 GeoRedundant 的 BackupStorageRedundancy 選項。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="fd8dc-131">許多 Azure 備份 Cmdlet 都需要將復原服務保存庫物件當做輸入。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="fd8dc-132">基於這個理由，將備份復原服務保存庫物件儲存在變數中會是方便的做法。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="fd8dc-133">在訂用帳戶中檢視保存庫</span><span class="sxs-lookup"><span data-stu-id="fd8dc-133">View the vaults in a subscription</span></span>
<span data-ttu-id="fd8dc-134">使用 **Get-AzureRmRecoveryServicesVault** 來檢視目前訂用帳戶中所有保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="fd8dc-135">您可以使用此命令來檢查是否已建立新的保存庫，或查看訂用帳戶中有哪些保存庫可用。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="fd8dc-136">執行命令時，會列出 Get-AzureRmRecoveryServicesVault 以及訂用帳戶中的所有保存庫。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="fd8dc-137">在 DPM 伺服器上安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="fd8dc-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="fd8dc-138">在安裝 Azure 備份代理程式之前，您必須在 Windows Server 上下載並提供安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="fd8dc-139">您可以從 [Microsoft 下載中心](http://aka.ms/azurebackup_agent) 或從復原服務保存庫的 [儀表板] 頁面取得最新版的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="fd8dc-140">請將安裝程式儲存至容易存取的位置，例如 *C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="fd8dc-141">若要安裝代理程式，請在 **DPM 伺服器**上已提升權限的 PowerShell 主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="fd8dc-142">這會以所有預設選項安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="fd8dc-143">安裝作業會在背景中進行幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="fd8dc-144">如果您沒有指定 */nu* 選項，則安裝結束時會開啟 **Windows Update** 視窗以檢查是否有任何更新。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="fd8dc-145">代理程式會顯示在已安裝的程式清單中。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="fd8dc-146">若要查看已安裝的程式清單，請移至 [控制台] > [程式] > [程式和功能]。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="fd8dc-148">安裝選項</span><span class="sxs-lookup"><span data-stu-id="fd8dc-148">Installation options</span></span>
<span data-ttu-id="fd8dc-149">若要查看所有可透過命令列執行的選項，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="fd8dc-150">可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-150">The available options include:</span></span>

| <span data-ttu-id="fd8dc-151">選項</span><span class="sxs-lookup"><span data-stu-id="fd8dc-151">Option</span></span> | <span data-ttu-id="fd8dc-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="fd8dc-152">Details</span></span> | <span data-ttu-id="fd8dc-153">預設值</span><span class="sxs-lookup"><span data-stu-id="fd8dc-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd8dc-154">/q</span><span class="sxs-lookup"><span data-stu-id="fd8dc-154">/q</span></span> |<span data-ttu-id="fd8dc-155">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="fd8dc-155">Quiet installation</span></span> |- |
| <span data-ttu-id="fd8dc-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="fd8dc-156">/p:"location"</span></span> |<span data-ttu-id="fd8dc-157">Azure 備份代理程式的安裝資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="fd8dc-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="fd8dc-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="fd8dc-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="fd8dc-159">/s:"location"</span></span> |<span data-ttu-id="fd8dc-160">Azure 備份代理程式的快取資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="fd8dc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="fd8dc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="fd8dc-162">/m</span><span class="sxs-lookup"><span data-stu-id="fd8dc-162">/m</span></span> |<span data-ttu-id="fd8dc-163">選擇加入 Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="fd8dc-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="fd8dc-164">/nu</span><span class="sxs-lookup"><span data-stu-id="fd8dc-164">/nu</span></span> |<span data-ttu-id="fd8dc-165">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="fd8dc-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="fd8dc-166">/d</span><span class="sxs-lookup"><span data-stu-id="fd8dc-166">/d</span></span> |<span data-ttu-id="fd8dc-167">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="fd8dc-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="fd8dc-168">/ph</span><span class="sxs-lookup"><span data-stu-id="fd8dc-168">/ph</span></span> |<span data-ttu-id="fd8dc-169">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="fd8dc-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="fd8dc-170">/po</span><span class="sxs-lookup"><span data-stu-id="fd8dc-170">/po</span></span> |<span data-ttu-id="fd8dc-171">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="fd8dc-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="fd8dc-172">/pu</span><span class="sxs-lookup"><span data-stu-id="fd8dc-172">/pu</span></span> |<span data-ttu-id="fd8dc-173">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="fd8dc-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="fd8dc-174">/pw</span><span class="sxs-lookup"><span data-stu-id="fd8dc-174">/pw</span></span> |<span data-ttu-id="fd8dc-175">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="fd8dc-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="fd8dc-176">向復原服務保存庫註冊 DPM</span><span class="sxs-lookup"><span data-stu-id="fd8dc-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="fd8dc-177">建立復原服務保存庫之後，請下載最新版本的代理程式和保存庫認證，並將它們儲存在方便的位置 (如 C:\Downloads)。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="fd8dc-178">在 DPM 伺服器上，執行 [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) Cmdlet 以向保存庫註冊電腦。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="fd8dc-179">初始組態設定</span><span class="sxs-lookup"><span data-stu-id="fd8dc-179">Initial configuration settings</span></span>
<span data-ttu-id="fd8dc-180">一旦向復原服務保存庫註冊 DPM 伺服器，就會使用預設的訂用帳戶設定開始。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="fd8dc-181">這些訂用帳戶設定包括網路、加密和臨時區域。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="fd8dc-182">若要變更訂用帳戶設定，您需要先使用 [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) Cmdlet 取得現有 (預設) 設定上的控制代碼：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="fd8dc-183">所有修改都會對此本機 PowerShell 物件 ```$setting``` 進行，然後使用 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 將完整物件認可到 DPM 和 Azure 備份以加以儲存。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="fd8dc-184">您必須使用 ```–Commit``` 旗標，以確保會保存所做的變更。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="fd8dc-185">除非已認可，否則 Azure 備份將不會套用並使用設定。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="fd8dc-186">網路</span><span class="sxs-lookup"><span data-stu-id="fd8dc-186">Networking</span></span>
<span data-ttu-id="fd8dc-187">如果 DPM 機器對在網際網路上的 Azure 備份服務的連線是透過 Proxy 伺服器，則應該提供 Proxy 伺服器設定，備份才能成功。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="fd8dc-188">這是使用 ```-ProxyServer```、```-ProxyPort```、```-ProxyUsername``` 及 ```ProxyPassword``` 參數搭配 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 來完成。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="fd8dc-189">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="fd8dc-190">您也可以針對給定的一組當週天數，使用 ```-WorkHourBandwidth``` 和 ```-NonWorkHourBandwidth``` 的選項來控制頻寬使用情形。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="fd8dc-191">本範例未設定任何節流。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="fd8dc-192">設定臨時區域</span><span class="sxs-lookup"><span data-stu-id="fd8dc-192">Configuring the staging Area</span></span>
<span data-ttu-id="fd8dc-193">在 DPM 伺服器上執行的 Azure 備份代理程式需要暫存儲存體，以供存放從雲端還原的資料 (本機臨時區域)。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="fd8dc-194">使用 [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) Cmdlet 和 ```-StagingAreaPath``` 參數來設定臨時區域。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="fd8dc-195">在上述範例中，臨時區域將在 PowerShell 物件 ```$setting``` 中設定為 *C:\StagingArea*。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="fd8dc-196">請確保指定的資料夾已經存在，否則訂用帳戶設定的最終認可將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="fd8dc-197">加密設定</span><span class="sxs-lookup"><span data-stu-id="fd8dc-197">Encryption settings</span></span>
<span data-ttu-id="fd8dc-198">傳送至 Azure 備份的備份資料會進行加密來保護資料的機密性。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="fd8dc-199">加密複雜密碼是在還原時用來解密資料的「密碼」。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="fd8dc-200">一旦設定，就請務必保管好這項資訊。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="fd8dc-201">在下面的範例中，第一個命令會將字串 ```passphrase123456789``` 轉換為安全字串，並將安全字串指派給名為 ```$Passphrase``` 的變數。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="fd8dc-202">第二個命令會將 ```$Passphrase``` 中的安全字串設定為加密備份的密碼。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="fd8dc-203">一旦設定，就請保管好此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="fd8dc-204">若沒有此複雜密碼，您將無法從 Azure 還原資料。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="fd8dc-205">此時，您應該已對 ```$setting``` 物件進行所有必要的變更。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="fd8dc-206">記得要認可變更。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="fd8dc-207">保護 Azure 備份的資料</span><span class="sxs-lookup"><span data-stu-id="fd8dc-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="fd8dc-208">在本節中，您會將實際執行伺服器加入至 DPM，然後保護資料到本機 DPM 存放區，然後到 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="fd8dc-209">在範例中，我們將示範如何備份檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="fd8dc-210">您可以輕鬆地運用同樣的觀念，來備份任何 DPM 支援的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="fd8dc-211">所有 DPM 備份皆受到保護群組 (PG) 所控管，並且由四個部分構成：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="fd8dc-212">**群組成員** 是您要在相同的保護群組中保護的所有可保護物件的清單 (在 DPM 中也稱為 *資料來源* )。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="fd8dc-213">比方說，您可能想要保護一個保護群組的實際執行 VM 與另一個保護群組中的 SQL Server 資料庫，因為它們可能會有不同的備份需求。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="fd8dc-214">在可以備份實際執行伺服器上的資料來源之前，您必須先確定 DPM 代理程式已安裝在伺服器上並受到 DPM 管理。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="fd8dc-215">請遵循 [安裝 DPM 代理程式](https://technet.microsoft.com/library/bb870935.aspx) 的步驟，並將其連結至適當的 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="fd8dc-216">**資料保護方法** 指定目標備份位置 - 磁帶、磁碟和雲端。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="fd8dc-217">在我們的範例中，我們將保護資料至本機磁碟以及雲端。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="fd8dc-218">**備份排程** 可指定何時需要進行備份，以及應該在 DPM 伺服器和實際執行伺服器之間同步處理資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="fd8dc-219">**保留排程** 可指定要在 Azure 中保留復原點多久時間。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="fd8dc-220">建立保護群組</span><span class="sxs-lookup"><span data-stu-id="fd8dc-220">Creating a protection group</span></span>
<span data-ttu-id="fd8dc-221">從使用 [Add-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) Cmdlet 來建立新的保護群組開始。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="fd8dc-222">以上 Cmdlet 會建立名為 *ProtectGroup01*的保護群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="fd8dc-223">也可以修改稍後現有的保護群組，以加入備份至 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="fd8dc-224">不過，若要對保護群組 - 新的或現有的- 進行任何變更，我們需要使用 *Get-DPMModifiableProtectionGroup* Cmdlet 來取得 [modifiable](https://technet.microsoft.com/library/hh881713) 物件上的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="fd8dc-225">將群組成員加入至保護群組</span><span class="sxs-lookup"><span data-stu-id="fd8dc-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="fd8dc-226">每個 DPM 代理程式會知道它安裝所在伺服器上資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="fd8dc-227">若要將資料來源加入至保護群組，DPM 代理程式必須先將資料來源清單傳回到 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="fd8dc-228">然後會選取一或多個資料來源，並加入至保護群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="fd8dc-229">達成此動作所需的 PowerShell 步驟包括：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="fd8dc-230">擷取透過 DPM 代理程式由 DPM 管理的所有伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="fd8dc-231">選擇特定伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-231">Choose a specific server.</span></span>
3. <span data-ttu-id="fd8dc-232">擷取伺服器上所有資料來源的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="fd8dc-233">選擇一或多個資料來源，並將它們加入至保護群組</span><span class="sxs-lookup"><span data-stu-id="fd8dc-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="fd8dc-234">安裝 DPM 代理程式且受 DPM 伺服器管理所在的伺服器清單是使用 [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) Cmdlet 取得。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="fd8dc-235">在此範例中，我們將篩選並只設定名稱為 *productionserver01* 的 PS 來進行備份。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="fd8dc-236">現在使用 [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) Cmdlet 擷取 ```$server``` 上的資料來源清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="fd8dc-237">在此範例中，我們會篩選要設定備份的磁碟區 *D:\*。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="fd8dc-238">然後此資料來源會使用 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) Cmdlet 新增至保護群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="fd8dc-239">記得使用「可修改的」保護群組物件 ```$MPG``` 來進行新增。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="fd8dc-240">視需要重複此步驟，直到您已加入所有選取的資料來源至保護群組中為止。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="fd8dc-241">您也可以從只有一個資料來源開始，並完成建立保護群組的工作流程，然後稍後將更多的資料來源加入至保護群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="fd8dc-242">選取資料保護方式</span><span class="sxs-lookup"><span data-stu-id="fd8dc-242">Selecting the data protection method</span></span>
<span data-ttu-id="fd8dc-243">資料來源加入至保護群組之後，下一步是使用 [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) Cmdlet 指定保護方法。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="fd8dc-244">此範例中，將為本機磁碟和雲端備份設定保護群組。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="fd8dc-245">您也必須使用 [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) Cmdlet 搭配 -Online 旗標，指定您想要在雲端中保護的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="fd8dc-246">設定保留範圍</span><span class="sxs-lookup"><span data-stu-id="fd8dc-246">Setting the retention range</span></span>
<span data-ttu-id="fd8dc-247">使用 [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) Cmdlet 設定備份點的保留。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="fd8dc-248">雖然在定義備份排程之前設定保留點看起來有點奇怪，使用 ```Set-DPMPolicyObjective``` Cmdlet 會自動設定預設的備份排程，之後便可加以修改。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="fd8dc-249">您總是可以先設定備份排程，之後再設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="fd8dc-250">在下面的範例中，此 Cmdlet 會設定磁碟備份的保留參數。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="fd8dc-251">這將會保留 10 天備份，並每隔 6 小時同步處理實際執行伺服器和 DPM 伺服器之間的資料。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="fd8dc-252">```SynchronizationFrequencyMinutes``` 不會定義建立備份點的頻率，只會定有資料複製到 DPM 伺服器的頻率。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="fd8dc-253">此設定可防止備份變得太大。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="fd8dc-254">針對移至 Azure 的備份 (DPM 將這些稱為線上備份)，保留範圍可設定為 [使用 Grandfather-Father-Son 配置 (GFS) 的長期保留](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="fd8dc-255">也就是說，您可以定義結合的保留原則，包含每日、每週、每月和每年保留原則。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="fd8dc-256">在此範例中，我們會建立陣列，表示我們需要的複雜保留配置，然後使用 [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) Cmdlet 設定保留範圍。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="fd8dc-257">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="fd8dc-257">Set the backup schedule</span></span>
<span data-ttu-id="fd8dc-258">如果您使用 ```Set-DPMPolicyObjective``` Cmdlet 指定保護目標，DPM 會自動設定預設的備份排程。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="fd8dc-259">若要變更預設排程，請依序使用 [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) Cmdlet 和 [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="fd8dc-260">在上述範例中， ```$onlineSch``` 是具有四個元素的陣列，其中包含 GFS 配置中保護群組的現有線上保護排程：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="fd8dc-261">```$onlineSch[0]``` 包含每日排程</span><span class="sxs-lookup"><span data-stu-id="fd8dc-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="fd8dc-262">```$onlineSch[1]``` 包含每週排程</span><span class="sxs-lookup"><span data-stu-id="fd8dc-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="fd8dc-263">```$onlineSch[2]``` 包含每月排程</span><span class="sxs-lookup"><span data-stu-id="fd8dc-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="fd8dc-264">```$onlineSch[3]``` 包含每年排程</span><span class="sxs-lookup"><span data-stu-id="fd8dc-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="fd8dc-265">因此，如果您需要修改每週排程，您需要參考 ```$onlineSch[1]```。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="fd8dc-266">初始備份</span><span class="sxs-lookup"><span data-stu-id="fd8dc-266">Initial backup</span></span>
<span data-ttu-id="fd8dc-267">第一次備份資料來源時，DPM 需要建立初始複本，以建立要在 DPM 複本磁碟區上保護的資料來源完整複本。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="fd8dc-268">此活動可以排定在特定的時間，或可以使用 [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) Cmdlet 搭配參數 ```-NOW``` 手動觸發。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="fd8dc-269">變更 DPM 複本和復原點磁碟區的大小</span><span class="sxs-lookup"><span data-stu-id="fd8dc-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="fd8dc-270">您也可以變更 DPM 複本磁碟區和陰影複製磁碟區的大小，方法是使用 [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) Cmdlet，如下列範例所示：Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="fd8dc-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="fd8dc-271">將變更認可到保護群組</span><span class="sxs-lookup"><span data-stu-id="fd8dc-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="fd8dc-272">最後，需要先認可變更，DPM 才可以根據每個新保護群組組態進行備份。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="fd8dc-273">這可以使用 [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) Cmdlet 來達成。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="fd8dc-274">檢視備份點</span><span class="sxs-lookup"><span data-stu-id="fd8dc-274">View the backup points</span></span>
<span data-ttu-id="fd8dc-275">您可以使用 [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) Cmdlet 來取得資料來源所有復原點的清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="fd8dc-276">在此範例中，我們將會：</span><span class="sxs-lookup"><span data-stu-id="fd8dc-276">In this example, we will:</span></span>

* <span data-ttu-id="fd8dc-277">擷取 DPM 伺服器上以及儲存在 ```$PG```</span><span class="sxs-lookup"><span data-stu-id="fd8dc-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="fd8dc-278">取得與 ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="fd8dc-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="fd8dc-279">取得資料來源的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="fd8dc-280">還原在 Azure 上保護的資料</span><span class="sxs-lookup"><span data-stu-id="fd8dc-280">Restore data protected on Azure</span></span>
<span data-ttu-id="fd8dc-281">還原資料是 ```RecoverableItem``` 物件和 ```RecoveryOption``` 物件的組合。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="fd8dc-282">在上一個節中，我們已取得資料來源的備份點清單。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="fd8dc-283">在下列範例中，我們將示範如何透過結合備份點與復原目標從 Azure 備份還原 Hyper-V 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="fd8dc-284">這個範例包含︰</span><span class="sxs-lookup"><span data-stu-id="fd8dc-284">This example includes:</span></span>

* <span data-ttu-id="fd8dc-285">使用 [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) Cmdlet 建立復原選項。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="fd8dc-286">使用 ```Get-DPMRecoveryPoint``` Cmdlet 擷取備份點的陣列。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="fd8dc-287">選擇要從中還原的備份點。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="fd8dc-288">命令可以很容易地針對任何資料來源類型擴充。</span><span class="sxs-lookup"><span data-stu-id="fd8dc-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd8dc-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd8dc-289">Next steps</span></span>
* <span data-ttu-id="fd8dc-290">如需 DPM 至 Azure 備份的詳細資訊，請參閱 [DPM 備份簡介](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="fd8dc-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
