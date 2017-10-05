---
title: "使用 PowerShell 將 Windows Server 備份至 Azure | Microsoft Docs"
description: "了解如何使用 PowerShell 部署和管理 Azure 備份"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="c690a-103">使用 PowerShell 部署和管理 Windows Server/Windows 用戶端的 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="c690a-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c690a-104">ARM</span><span class="sxs-lookup"><span data-stu-id="c690a-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="c690a-105">傳統</span><span class="sxs-lookup"><span data-stu-id="c690a-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="c690a-106">本文說明如何使用 PowerShell 在 Windows Server 或 Windows 用戶端上設定 Azure 備份，以及管理備份和復原。</span><span class="sxs-lookup"><span data-stu-id="c690a-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="c690a-107">安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c690a-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="c690a-108">本文著重於可讓您在資源群組中使用復原服務保存庫的 Azure Resource Manager (ARM) 和 MS Online Backup PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c690a-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="c690a-109">在 2015 年 10 月，Azure PowerShell 1.0 已發行。</span><span class="sxs-lookup"><span data-stu-id="c690a-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="c690a-110">此版本繼承 0.9.8 版，且帶來一些重要的變更，尤其是 Cmdlet 的命名模式。</span><span class="sxs-lookup"><span data-stu-id="c690a-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="c690a-111">1.0 Cmdlet 遵循命名模式 {動詞}-AzureRm{名詞}；然而，0.9.8 的名稱不包含 **Rm** (例如，New-AzureRmResourceGroup，而不是 New-AzureResourceGroup)。</span><span class="sxs-lookup"><span data-stu-id="c690a-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="c690a-112">在使用 Azure PowerShell 0.9.8 時，您必須先執行 **Switch-AzureMode AzureResourceManager** 命令啟用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="c690a-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="c690a-113">1.0 或更新版本不需要執行此命令。</span><span class="sxs-lookup"><span data-stu-id="c690a-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="c690a-114">如果您想要使用針對 0.9.8 環境所撰寫的指令碼，在 1.0 或更新版本的環境中，您應該先在預先生產環境中小心地更新和測試指令碼，然後才在生產環境中使用它們，以避免產生非預期的影響。</span><span class="sxs-lookup"><span data-stu-id="c690a-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="c690a-115">[下載最新版 PowerShell](https://github.com/Azure/azure-powershell/releases) (所需的最低版本為：1.0.0)</span><span class="sxs-lookup"><span data-stu-id="c690a-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="c690a-116">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="c690a-116">Create a recovery services vault</span></span>
<span data-ttu-id="c690a-117">下列步驟將引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="c690a-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="c690a-118">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="c690a-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="c690a-119">如果您是第一次使用 Azure 備份，您必須使用 **Register-AzureRMResourceProvider** Cmdlet 利用您的訂用帳戶來註冊 Azure 復原服務提供者。</span><span class="sxs-lookup"><span data-stu-id="c690a-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="c690a-120">復原服務保存庫是 ARM 資源，因此您必須將它放在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="c690a-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="c690a-121">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="c690a-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="c690a-122">建立新的資源群組時，請指定資源群組的名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="c690a-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="c690a-123">使用 **New-AzureRmRecoveryServicesVault** Cmdlet 來建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="c690a-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="c690a-124">請務必為保存庫指定與用於資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="c690a-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="c690a-125">指定要使用的儲存體備援類型；您可以使用[本地備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) 或[異地備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="c690a-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="c690a-126">以下範例示範 testVault 設定為 GeoRedundant 的 BackupStorageRedundancy 選項。</span><span class="sxs-lookup"><span data-stu-id="c690a-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="c690a-127">許多 Azure 備份 Cmdlet 都需要將復原服務保存庫物件當做輸入。</span><span class="sxs-lookup"><span data-stu-id="c690a-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="c690a-128">基於這個理由，將備份復原服務保存庫物件儲存在變數中會是方便的做法。</span><span class="sxs-lookup"><span data-stu-id="c690a-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="c690a-129">在訂用帳戶中檢視保存庫</span><span class="sxs-lookup"><span data-stu-id="c690a-129">View the vaults in a subscription</span></span>
<span data-ttu-id="c690a-130">使用 **Get-AzureRmRecoveryServicesVault** 來檢視目前訂用帳戶中所有保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="c690a-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="c690a-131">您可以使用此命令來檢查是否已建立新的保存庫，或查看訂用帳戶中有哪些保存庫可用。</span><span class="sxs-lookup"><span data-stu-id="c690a-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="c690a-132">執行命令時，會列出 **Get-AzureRmRecoveryServicesVault** 以及訂用帳戶中的所有保存庫。</span><span class="sxs-lookup"><span data-stu-id="c690a-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="c690a-133">安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="c690a-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="c690a-134">在安裝 Azure 備份代理程式之前，您必須在 Windows Server 上下載並提供安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c690a-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="c690a-135">您可以從 [Microsoft 下載中心](http://aka.ms/azurebackup_agent) 或從復原服務保存庫的 [儀表板] 頁面取得最新版的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c690a-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="c690a-136">請將安裝程式儲存至容易存取的位置，例如 *C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="c690a-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="c690a-137">或者，使用 PowerShell 來取得下載程式：</span><span class="sxs-lookup"><span data-stu-id="c690a-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="c690a-138">若要安裝代理程式，請在已提升權限的 PowerShell 主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c690a-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="c690a-139">這會以所有預設選項安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="c690a-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="c690a-140">安裝作業會在背景中進行幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="c690a-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="c690a-141">如果您沒有指定 */nu* 選項，則安裝結束時會開啟 **Windows Update** 視窗以檢查是否有任何更新。</span><span class="sxs-lookup"><span data-stu-id="c690a-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="c690a-142">安裝之後，代理程式會顯示在已安裝的程式清單中。</span><span class="sxs-lookup"><span data-stu-id="c690a-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="c690a-143">若要查看已安裝的程式清單，請移至 [控制台] > [程式] > [程式和功能]。</span><span class="sxs-lookup"><span data-stu-id="c690a-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="c690a-145">安裝選項</span><span class="sxs-lookup"><span data-stu-id="c690a-145">Installation options</span></span>
<span data-ttu-id="c690a-146">若要查看所有可透過命令列執行的選項，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c690a-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="c690a-147">可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="c690a-147">The available options include:</span></span>

| <span data-ttu-id="c690a-148">選項</span><span class="sxs-lookup"><span data-stu-id="c690a-148">Option</span></span> | <span data-ttu-id="c690a-149">詳細資料</span><span class="sxs-lookup"><span data-stu-id="c690a-149">Details</span></span> | <span data-ttu-id="c690a-150">預設值</span><span class="sxs-lookup"><span data-stu-id="c690a-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c690a-151">/q</span><span class="sxs-lookup"><span data-stu-id="c690a-151">/q</span></span> |<span data-ttu-id="c690a-152">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="c690a-152">Quiet installation</span></span> |- |
| <span data-ttu-id="c690a-153">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="c690a-153">/p:"location"</span></span> |<span data-ttu-id="c690a-154">Azure 備份代理程式的安裝資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="c690a-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="c690a-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="c690a-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="c690a-156">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="c690a-156">/s:"location"</span></span> |<span data-ttu-id="c690a-157">Azure 備份代理程式的快取資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="c690a-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="c690a-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="c690a-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="c690a-159">/m</span><span class="sxs-lookup"><span data-stu-id="c690a-159">/m</span></span> |<span data-ttu-id="c690a-160">選擇加入 Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="c690a-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="c690a-161">/nu</span><span class="sxs-lookup"><span data-stu-id="c690a-161">/nu</span></span> |<span data-ttu-id="c690a-162">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="c690a-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="c690a-163">/d</span><span class="sxs-lookup"><span data-stu-id="c690a-163">/d</span></span> |<span data-ttu-id="c690a-164">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="c690a-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="c690a-165">/ph</span><span class="sxs-lookup"><span data-stu-id="c690a-165">/ph</span></span> |<span data-ttu-id="c690a-166">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="c690a-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="c690a-167">/po</span><span class="sxs-lookup"><span data-stu-id="c690a-167">/po</span></span> |<span data-ttu-id="c690a-168">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="c690a-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="c690a-169">/pu</span><span class="sxs-lookup"><span data-stu-id="c690a-169">/pu</span></span> |<span data-ttu-id="c690a-170">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="c690a-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="c690a-171">/pw</span><span class="sxs-lookup"><span data-stu-id="c690a-171">/pw</span></span> |<span data-ttu-id="c690a-172">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="c690a-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="c690a-173">向復原服務保存庫註冊 Windows Server 或 Windows 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="c690a-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="c690a-174">建立復原服務保存庫之後，請下載最新版本的代理程式和保存庫認證，並將它們儲存在方便的位置 (如 C:\Downloads)。</span><span class="sxs-lookup"><span data-stu-id="c690a-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="c690a-175">在 Windows Server 或 Windows 用戶端電腦上，執行 [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) Cmdlet 向保存庫註冊電腦。</span><span class="sxs-lookup"><span data-stu-id="c690a-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="c690a-176">此 Cmdlet 和其他用來進行備份的 Cmdlet 皆來自 MSONLINE 模組，Mars AgentInstaller 會在安裝過程中新增此模組。</span><span class="sxs-lookup"><span data-stu-id="c690a-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="c690a-177">AgentInstaller 不會更新 $Env:PSModulePath 變數。</span><span class="sxs-lookup"><span data-stu-id="c690a-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="c690a-178">這表示模組自動載入會失敗。</span><span class="sxs-lookup"><span data-stu-id="c690a-178">This means module auto-load fails.</span></span> <span data-ttu-id="c690a-179">若要解決此問題，您可以執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c690a-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="c690a-180">或者，您可以在指令碼中手動載入模組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c690a-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="c690a-181">在載入 Online Backup Cmdlet 後，您必須註冊保存庫認證：</span><span class="sxs-lookup"><span data-stu-id="c690a-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="c690a-182">請勿使用相對路徑來指定保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="c690a-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="c690a-183">您必須提供絕對路徑做為 Cmdlet 的輸入。</span><span class="sxs-lookup"><span data-stu-id="c690a-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="c690a-184">網路設定</span><span class="sxs-lookup"><span data-stu-id="c690a-184">Networking settings</span></span>
<span data-ttu-id="c690a-185">若 Windows 電腦是透過 Proxy 伺服器連線到網際網路，您也可以提供 Proxy 設定給代理程式。</span><span class="sxs-lookup"><span data-stu-id="c690a-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="c690a-186">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c690a-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="c690a-187">您也可以針對給定的一組當週天數，使用 [```work hour bandwidth```] 和 [```non-work hour bandwidth```] 的選項來控制頻寬使用情形。</span><span class="sxs-lookup"><span data-stu-id="c690a-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="c690a-188">使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) Cmdlet 即可設定 Proxy 和頻寬的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="c690a-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="c690a-189">加密設定</span><span class="sxs-lookup"><span data-stu-id="c690a-189">Encryption settings</span></span>
<span data-ttu-id="c690a-190">傳送至 Azure 備份的備份資料會進行加密來保護資料的機密性。</span><span class="sxs-lookup"><span data-stu-id="c690a-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="c690a-191">加密複雜密碼是在還原時用來解密資料的「密碼」。</span><span class="sxs-lookup"><span data-stu-id="c690a-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="c690a-192">一旦設定，就請保管好此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="c690a-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="c690a-193">若沒有此複雜密碼，您將無法從 Azure 還原資料。</span><span class="sxs-lookup"><span data-stu-id="c690a-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="c690a-194">備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="c690a-194">Back up files and folders</span></span>
<span data-ttu-id="c690a-195">Windows Server 和用戶端的所有 Azure 備份都是由原則來掌管。</span><span class="sxs-lookup"><span data-stu-id="c690a-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="c690a-196">原則包含三個部分：</span><span class="sxs-lookup"><span data-stu-id="c690a-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="c690a-197">**備份排程** ，指定何時進行備份並與服務同步。</span><span class="sxs-lookup"><span data-stu-id="c690a-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="c690a-198">**保留排程** 可指定要在 Azure 中保留復原點多久時間。</span><span class="sxs-lookup"><span data-stu-id="c690a-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="c690a-199">**檔案包含/排除規格** ，指出要備份的項目。</span><span class="sxs-lookup"><span data-stu-id="c690a-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="c690a-200">本文件中要說明如何將備份自動化，因此我們假設還未設定任何選項。</span><span class="sxs-lookup"><span data-stu-id="c690a-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="c690a-201">一開始，請先使用 [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) Cmdlet 建立新的備份原則。</span><span class="sxs-lookup"><span data-stu-id="c690a-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="c690a-202">此時，原則是空的，需要使用其他 Cmdlet 來定義要包含或排除的項目、執行備份的時機，以及儲存備份的位置。</span><span class="sxs-lookup"><span data-stu-id="c690a-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="c690a-203">設定備份排程</span><span class="sxs-lookup"><span data-stu-id="c690a-203">Configuring the backup schedule</span></span>
<span data-ttu-id="c690a-204">原則 3 部分的第 1 個部分是備份排程，請使用 [New-OBSchedule](https://technet.microsoft.com/library/hh770401) Cmdlet 建立。</span><span class="sxs-lookup"><span data-stu-id="c690a-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="c690a-205">備份排程會定義何時需要進行備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="c690a-206">建立排程時，您需要指定 2 個輸入參數：</span><span class="sxs-lookup"><span data-stu-id="c690a-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="c690a-207">**星期幾** 要執行備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="c690a-208">您可以只選一天或選擇一週的每天都執行備份工作，或任意選取要一週的哪幾天。</span><span class="sxs-lookup"><span data-stu-id="c690a-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="c690a-209">**時段** 。</span><span class="sxs-lookup"><span data-stu-id="c690a-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="c690a-210">您可以定義多達一天 3 個不同時段來觸發備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="c690a-211">例如，您可以設定每週六和日下午 4 點執行備份原則。</span><span class="sxs-lookup"><span data-stu-id="c690a-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="c690a-212">備份排程需要與原則建立關聯，您可以使用 [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) Cmdlet 來達成。</span><span class="sxs-lookup"><span data-stu-id="c690a-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="c690a-213">設定保留原則</span><span class="sxs-lookup"><span data-stu-id="c690a-213">Configuring a retention policy</span></span>
<span data-ttu-id="c690a-214">保留原則會定義所建立備份工作的復原點保留時間長度。</span><span class="sxs-lookup"><span data-stu-id="c690a-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="c690a-215">使用 [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) Cmdlet 建立新的保留原則時，您可以使用 Azure 備份來指定需要保留備份復原點的天數。</span><span class="sxs-lookup"><span data-stu-id="c690a-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="c690a-216">下例將保留原則設為 7 天。</span><span class="sxs-lookup"><span data-stu-id="c690a-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="c690a-217">保留原則必須與主要原則建立關聯，方法為使用 Cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405)：</span><span class="sxs-lookup"><span data-stu-id="c690a-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="c690a-218">包含及排除要備份的檔案</span><span class="sxs-lookup"><span data-stu-id="c690a-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="c690a-219">```OBFileSpec``` 物件會定義備份中要包含與排除的檔案。</span><span class="sxs-lookup"><span data-stu-id="c690a-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="c690a-220">此組規則可劃分出電腦上要保護的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="c690a-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="c690a-221">您可以設定所需數量的檔案包含或排除規則，並建立其與原則的關聯。</span><span class="sxs-lookup"><span data-stu-id="c690a-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="c690a-222">建立新的 OBFileSpec 物件時，您可以：</span><span class="sxs-lookup"><span data-stu-id="c690a-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="c690a-223">指定要包含的檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="c690a-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="c690a-224">指定要排除的檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="c690a-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="c690a-225">指定要遞迴備份資料夾中的資料，或是否僅備份指定資料夾中最上層的檔案。</span><span class="sxs-lookup"><span data-stu-id="c690a-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="c690a-226">後者可利用在 New-OBFileSpec 命令中使用 -NonRecursive 旗標來達成。</span><span class="sxs-lookup"><span data-stu-id="c690a-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="c690a-227">在下例中，我們會備份磁碟區 C: 和 D:，並排除 Windows 資料夾和任何暫存資料夾中的作業系統二進位檔。</span><span class="sxs-lookup"><span data-stu-id="c690a-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="c690a-228">若要這樣做，我們將使用 [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) Cmdlet 建立二個檔案規格 - 一個包含和一個排除。</span><span class="sxs-lookup"><span data-stu-id="c690a-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="c690a-229">一旦建立檔案規格之後，再使用 [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) Cmdlet 建立與原則的關聯。</span><span class="sxs-lookup"><span data-stu-id="c690a-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="c690a-230">套用原則</span><span class="sxs-lookup"><span data-stu-id="c690a-230">Applying the policy</span></span>
<span data-ttu-id="c690a-231">現在原則物件已完成，且具有關聯的備份排程、保留原則及包含/排除的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="c690a-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="c690a-232">此原則現在已經過認可，適合用於 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="c690a-233">套用新建立的原則之前，請使用 [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) Cmdlet 確認沒有與伺服器未與現有的備份原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="c690a-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="c690a-234">移除原則時，系統會提示確認。</span><span class="sxs-lookup"><span data-stu-id="c690a-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="c690a-235">若要略過確認，Cmdlet 中請使用 ```-Confirm:$false``` 。</span><span class="sxs-lookup"><span data-stu-id="c690a-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="c690a-236">若要認可原則物件已完成，請使用 [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c690a-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="c690a-237">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="c690a-237">This will also ask for confirmation.</span></span> <span data-ttu-id="c690a-238">若要略過確認，Cmdlet 中請使用 ```-Confirm:$false``` 。</span><span class="sxs-lookup"><span data-stu-id="c690a-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="c690a-239">您可以使用 [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) Cmdlet 來檢視現有備份原則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c690a-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="c690a-240">您可以使用 [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) Cmdlet (適用於備份排程) 和 [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) Cmdlet (適用於保留原則) 進一步向下鑽研</span><span class="sxs-lookup"><span data-stu-id="c690a-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="c690a-241">執行臨機操作備份</span><span class="sxs-lookup"><span data-stu-id="c690a-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="c690a-242">設定備份原則之後，即會根據排程進行備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="c690a-243">您也可以使用 [Start-OBBackup](https://technet.microsoft.com/library/hh770426) Cmdlet 來觸發臨機操作備份：</span><span class="sxs-lookup"><span data-stu-id="c690a-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="c690a-244">從 Azure 備份還原資料</span><span class="sxs-lookup"><span data-stu-id="c690a-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="c690a-245">本節將引導您逐步完成自動化從 Azure 備份復原資料。</span><span class="sxs-lookup"><span data-stu-id="c690a-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="c690a-246">此工作涉及下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c690a-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="c690a-247">挑選來源磁碟區</span><span class="sxs-lookup"><span data-stu-id="c690a-247">Pick the source volume</span></span>
2. <span data-ttu-id="c690a-248">選擇要還原的備份點</span><span class="sxs-lookup"><span data-stu-id="c690a-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="c690a-249">選擇要還原的項目</span><span class="sxs-lookup"><span data-stu-id="c690a-249">Choose an item to restore</span></span>
4. <span data-ttu-id="c690a-250">觸發還原程序</span><span class="sxs-lookup"><span data-stu-id="c690a-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="c690a-251">挑選來源磁碟區</span><span class="sxs-lookup"><span data-stu-id="c690a-251">Picking the source volume</span></span>
<span data-ttu-id="c690a-252">若要從 Azure 備份還原項目，您必須先識別項目的來源。</span><span class="sxs-lookup"><span data-stu-id="c690a-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="c690a-253">我們在 Windows Server 或 Windows 用戶端的內容中執行命令，則已經識別電腦。</span><span class="sxs-lookup"><span data-stu-id="c690a-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="c690a-254">找出來源的下一步是識別包含它的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c690a-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="c690a-255">執行 [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) Cmdlet 可以擷取一份這部電腦所備份磁碟區或來源清單。</span><span class="sxs-lookup"><span data-stu-id="c690a-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="c690a-256">此命令會傳回這部伺服器/用戶端備份的所有來源陣列。</span><span class="sxs-lookup"><span data-stu-id="c690a-256">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="c690a-257">選擇要從中還原的備份點</span><span class="sxs-lookup"><span data-stu-id="c690a-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="c690a-258">您可以執行 [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) Cmdlet 並搭配適當參數來擷取備份點清單。</span><span class="sxs-lookup"><span data-stu-id="c690a-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="c690a-259">範例中，我們會選擇來源磁碟區 *D:* 的最新備份點並加以使用來還原特定檔案。</span><span class="sxs-lookup"><span data-stu-id="c690a-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="c690a-260">物件 ```$rps``` 是備份點陣列。</span><span class="sxs-lookup"><span data-stu-id="c690a-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="c690a-261">第一個元素是最新備份點，且第 N 個元素是最舊的備份點。</span><span class="sxs-lookup"><span data-stu-id="c690a-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="c690a-262">為了選擇最新的備份點，我們使用 ```$rps[0]```。</span><span class="sxs-lookup"><span data-stu-id="c690a-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="c690a-263">選擇要還原的項目</span><span class="sxs-lookup"><span data-stu-id="c690a-263">Choosing an item to restore</span></span>
<span data-ttu-id="c690a-264">為了識別要還原的正確檔案或資料夾，遞迴地使用 [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c690a-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="c690a-265">如此一來，可單獨使用 ```Get-OBRecoverableItem```來瀏覽資料夾的階層。</span><span class="sxs-lookup"><span data-stu-id="c690a-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="c690a-266">在此範例中，如果我們想要還原檔案 *finances.xls*，可以使用物件 ```$filesFolders[1]``` 來參考該檔案。</span><span class="sxs-lookup"><span data-stu-id="c690a-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="c690a-267">您也可以使用 ```Get-OBRecoverableItem``` Cmdlet 來搜尋要還原的項目。</span><span class="sxs-lookup"><span data-stu-id="c690a-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="c690a-268">在範例中，為了搜尋 *finances.xls* ，我們可以執行下列命令來取得該檔案的控制代碼：</span><span class="sxs-lookup"><span data-stu-id="c690a-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="c690a-269">觸發還原程序</span><span class="sxs-lookup"><span data-stu-id="c690a-269">Triggering the restore process</span></span>
<span data-ttu-id="c690a-270">為了觸發還原程序，我們首先需要指定復原選項。</span><span class="sxs-lookup"><span data-stu-id="c690a-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="c690a-271">使用 [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) Cmdlet 可以完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="c690a-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="c690a-272">在此範例中，我們假設要將檔案還原至 *C:\temp*。另外假設要略過已經存在於目的地資料夾 *C:\temp* 中的檔案。為了建立此復原選項，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c690a-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="c690a-273">現在，從 ```Get-OBRecoverableItem``` Cmdlet 的輸出，在選取的 ```$item``` 上使用 [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) 命令來觸發還原程序：</span><span class="sxs-lookup"><span data-stu-id="c690a-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="c690a-274">解除安裝 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="c690a-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="c690a-275">使用下列命令即可解除安裝 Azure 備份代理程式：</span><span class="sxs-lookup"><span data-stu-id="c690a-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="c690a-276">若要從電腦解除安裝代理程式二進位檔，請考量下列後果：</span><span class="sxs-lookup"><span data-stu-id="c690a-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="c690a-277">這會從電腦移除檔案篩選器，並停止追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="c690a-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="c690a-278">會從電腦移除所有原則資訊，但服務中會繼續保存這些原則資訊。</span><span class="sxs-lookup"><span data-stu-id="c690a-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="c690a-279">會移除所有備份排程，且不再進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="c690a-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="c690a-280">不過，Azure 中儲存的資料會留著，根據您所設定的保留原則設定予以保留。</span><span class="sxs-lookup"><span data-stu-id="c690a-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="c690a-281">較舊的時間點會自動過時。</span><span class="sxs-lookup"><span data-stu-id="c690a-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="c690a-282">遠端管理</span><span class="sxs-lookup"><span data-stu-id="c690a-282">Remote management</span></span>
<span data-ttu-id="c690a-283">關於 Azure 備份代理程式、原則和資料來源的所有管理工作，皆可透過 PowerShell 遠端完成。</span><span class="sxs-lookup"><span data-stu-id="c690a-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="c690a-284">要遠端管理的電腦必須經過正確準備。</span><span class="sxs-lookup"><span data-stu-id="c690a-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="c690a-285">依預設，WinRM 服務會設定為手動啟動。</span><span class="sxs-lookup"><span data-stu-id="c690a-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="c690a-286">但您必須將啟動類型設定為 [ *自動* ]，並應該啟動該服務。</span><span class="sxs-lookup"><span data-stu-id="c690a-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="c690a-287">若要驗證 WinRM 服務有在執行，[狀態] 屬性的值應該是 [ *執行中*]。</span><span class="sxs-lookup"><span data-stu-id="c690a-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="c690a-288">應該將 PowerShell 設定為可以遠端執行。</span><span class="sxs-lookup"><span data-stu-id="c690a-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="c690a-289">現在可以遠端管理電腦 - 從代理程式的安裝開始。</span><span class="sxs-lookup"><span data-stu-id="c690a-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="c690a-290">例如，下列指令碼會將代理程式複製到遠端電腦並進行安裝。</span><span class="sxs-lookup"><span data-stu-id="c690a-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="c690a-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c690a-291">Next steps</span></span>
<span data-ttu-id="c690a-292">如需 Windows Server/用戶端的 Azure 備份詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="c690a-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="c690a-293">Azure 備份的簡介</span><span class="sxs-lookup"><span data-stu-id="c690a-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="c690a-294">備份 Windows 伺服器</span><span class="sxs-lookup"><span data-stu-id="c690a-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
