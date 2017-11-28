---
title: "設定 Windows Server tooAzure aaaUse PowerShell tooback |Microsoft 文件"
description: "深入了解如何 toodeploy 和管理使用 PowerShell 的 Azure 備份"
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
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="785e8-103">部署和管理備份 tooAzure 使用 PowerShell 的 Windows 伺服器/Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="785e8-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="785e8-104">ARM</span><span class="sxs-lookup"><span data-stu-id="785e8-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="785e8-105">傳統</span><span class="sxs-lookup"><span data-stu-id="785e8-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="785e8-106">本文章將示範如何 toouse PowerShell for Azure 備份 Windows Server 或 Windows 用戶端上所設定和管理備份和復原。</span><span class="sxs-lookup"><span data-stu-id="785e8-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="785e8-107">安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="785e8-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="785e8-108">本文著重在 hello Azure 資源管理員 (ARM) 和 hello MS 線上備份的 PowerShell cmdlet 可讓您 toouse 復原服務保存庫的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="785e8-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="785e8-109">在 2015 年 10 月，Azure PowerShell 1.0 已發行。</span><span class="sxs-lookup"><span data-stu-id="785e8-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="785e8-110">此版本中成功 hello 為 0.9.8 版，並讓它們回到相關的某些重要的變更，尤其是在 hello hello 指令程式的命名模式。</span><span class="sxs-lookup"><span data-stu-id="785e8-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="785e8-111">1.0 cmdlet 後續 hello 命名模式 {動詞}-AzureRm {名詞};而 hello 為 0.9.8 名稱不包含**Rm** (例如，而不是新增 AzureResourceGroup 的新增-AzureRmResourceGroup)。</span><span class="sxs-lookup"><span data-stu-id="785e8-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="785e8-112">使用 Azure PowerShell 為 0.9.8 時，您必須先啟用 hello Resource Manager 模式執行 hello **Switch-azuremode AzureResourceManager**命令。</span><span class="sxs-lookup"><span data-stu-id="785e8-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="785e8-113">1.0 或更新版本不需要執行此命令。</span><span class="sxs-lookup"><span data-stu-id="785e8-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="785e8-114">如果您想 toouse 您撰寫的 hello 1.0 或更新版本的環境中的 hello 為 0.9.8 環境的指令碼應該仔細更新及預先生產環境中測試 hello 指令碼，然後才使用生產 tooavoid 中預期的影響。</span><span class="sxs-lookup"><span data-stu-id="785e8-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="785e8-115">[下載最新 PowerShell 版本 hello](https://github.com/Azure/azure-powershell/releases) (所需的最低版本是： 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="785e8-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="785e8-116">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="785e8-116">Create a recovery services vault</span></span>
<span data-ttu-id="785e8-117">hello 步驟會引導您完成建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="785e8-118">復原服務保存庫不同於備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="785e8-119">如果您使用 Azure Backup hello 第一次，您必須使用 hello**暫存器 AzureRMResourceProvider** cmdlet tooregister hello Azure 復原服務提供者與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="785e8-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="785e8-120">hello 復原服務保存庫是 ARM 資源，因此您需要 tooplace 它資源群組內。</span><span class="sxs-lookup"><span data-stu-id="785e8-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="785e8-121">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="785e8-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="785e8-122">建立新的資源群組時，指定 hello 名稱和位置 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="785e8-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="785e8-123">使用 hello**新增 AzureRmRecoveryServicesVault** cmdlet toocreate hello 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="785e8-124">請務必 toospecify hello hello 保存庫相同的位置，所用的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="785e8-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="785e8-125">指定儲存體備援 toouse; hello 類型您可以使用[本機備援儲存體 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage)或[地理備援儲存體 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="785e8-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="785e8-126">hello 下列範例顯示 hello testVault-BackupStorageRedundancy 選項設定 tooGeoRedundant。</span><span class="sxs-lookup"><span data-stu-id="785e8-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="785e8-127">許多 Azure Backup cmdlet 需要 hello 復原服務保存庫的物件做為輸入。</span><span class="sxs-lookup"><span data-stu-id="785e8-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="785e8-128">基於這個理由，它是方便 toostore hello 備份復原服務保存庫在變數中。</span><span class="sxs-lookup"><span data-stu-id="785e8-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="785e8-129">檢視訂用帳戶中的 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="785e8-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="785e8-130">使用**Get AzureRmRecoveryServicesVault** tooview hello 份 hello 目前訂用帳戶中所有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="785e8-131">您可以使用，則已建立新的保存庫，此命令 toocheck 或 toosee hello 訂用帳戶中有哪些保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="785e8-132">執行 hello 命令**Get AzureRmRecoveryServicesVault**，並列出 hello 訂用帳戶中所有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="785e8-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="785e8-133">安裝 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="785e8-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="785e8-134">安裝 hello Azure Backup agent 之前，您需要 toohave hello 安裝程式，下載和 hello Windows Server 上也一樣。</span><span class="sxs-lookup"><span data-stu-id="785e8-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="785e8-135">收到 hello 的 hello 最新版本的 hello installer [Microsoft Download Center](http://aka.ms/azurebackup_agent)或從 hello 復原服務保存庫的 [儀表板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="785e8-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="785e8-136">儲存 hello installer tooan 更容易存取的位置，例如 * C:\Downloads\*。</span><span class="sxs-lookup"><span data-stu-id="785e8-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="785e8-137">或者，使用 PowerShell tooget hello 程式下載程式：</span><span class="sxs-lookup"><span data-stu-id="785e8-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="785e8-138">tooinstall hello 代理程式，執行下列命令，在提升權限的 PowerShell 主控台中的 hello:</span><span class="sxs-lookup"><span data-stu-id="785e8-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="785e8-139">這會 hello 代理程式安裝與所有 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="785e8-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="785e8-140">hello 安裝需要幾分鐘 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="785e8-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="785e8-141">如果您未指定 hello */nu*選項則 hello **Windows Update**視窗隨即開啟的任何更新的 hello 安裝 toocheck hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="785e8-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="785e8-142">安裝之後，安裝程式的 hello 清單會顯示 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="785e8-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="785e8-143">toosee hello 列出已安裝的程式，請移過**控制台** > **程式** > **程式和功能**。</span><span class="sxs-lookup"><span data-stu-id="785e8-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![已安裝代理程式](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="785e8-145">安裝選項</span><span class="sxs-lookup"><span data-stu-id="785e8-145">Installation options</span></span>
<span data-ttu-id="785e8-146">toosee 所有 hello 選項可透過使用 hello 命令列，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="785e8-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="785e8-147">hello 可用的選項包括：</span><span class="sxs-lookup"><span data-stu-id="785e8-147">hello available options include:</span></span>

| <span data-ttu-id="785e8-148">選項</span><span class="sxs-lookup"><span data-stu-id="785e8-148">Option</span></span> | <span data-ttu-id="785e8-149">詳細資料</span><span class="sxs-lookup"><span data-stu-id="785e8-149">Details</span></span> | <span data-ttu-id="785e8-150">預設值</span><span class="sxs-lookup"><span data-stu-id="785e8-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="785e8-151">/q</span><span class="sxs-lookup"><span data-stu-id="785e8-151">/q</span></span> |<span data-ttu-id="785e8-152">無訊息安裝</span><span class="sxs-lookup"><span data-stu-id="785e8-152">Quiet installation</span></span> |- |
| <span data-ttu-id="785e8-153">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="785e8-153">/p:"location"</span></span> |<span data-ttu-id="785e8-154">路徑 toohello hello Azure Backup agent 的安裝資料夾。</span><span class="sxs-lookup"><span data-stu-id="785e8-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="785e8-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="785e8-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="785e8-156">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="785e8-156">/s:"location"</span></span> |<span data-ttu-id="785e8-157">路徑 toohello hello Azure 備份代理程式的快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="785e8-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="785e8-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="785e8-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="785e8-159">/m</span><span class="sxs-lookup"><span data-stu-id="785e8-159">/m</span></span> |<span data-ttu-id="785e8-160">選擇加入 tooMicrosoft 更新</span><span class="sxs-lookup"><span data-stu-id="785e8-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="785e8-161">/nu</span><span class="sxs-lookup"><span data-stu-id="785e8-161">/nu</span></span> |<span data-ttu-id="785e8-162">安裝完成後不要檢查更新</span><span class="sxs-lookup"><span data-stu-id="785e8-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="785e8-163">/d</span><span class="sxs-lookup"><span data-stu-id="785e8-163">/d</span></span> |<span data-ttu-id="785e8-164">解除安裝 Microsoft Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="785e8-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="785e8-165">/ph</span><span class="sxs-lookup"><span data-stu-id="785e8-165">/ph</span></span> |<span data-ttu-id="785e8-166">Proxy 主機位址</span><span class="sxs-lookup"><span data-stu-id="785e8-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="785e8-167">/po</span><span class="sxs-lookup"><span data-stu-id="785e8-167">/po</span></span> |<span data-ttu-id="785e8-168">Proxy 主機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="785e8-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="785e8-169">/pu</span><span class="sxs-lookup"><span data-stu-id="785e8-169">/pu</span></span> |<span data-ttu-id="785e8-170">Proxy 主機使用者名稱</span><span class="sxs-lookup"><span data-stu-id="785e8-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="785e8-171">/pw</span><span class="sxs-lookup"><span data-stu-id="785e8-171">/pw</span></span> |<span data-ttu-id="785e8-172">Proxy 密碼</span><span class="sxs-lookup"><span data-stu-id="785e8-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="785e8-173">註冊 Windows Server 或 Windows 用戶端機器 tooa 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="785e8-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="785e8-174">建立 hello 復原服務保存庫之後，請下載 hello 最新的代理程式 」 和 「 hello 保存庫認證，並將它儲存在方便的位置，例如 C:\Downloads。</span><span class="sxs-lookup"><span data-stu-id="785e8-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="785e8-175">在 hello Windows Server 或 Windows 用戶端電腦上，執行 hello [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) hello 保存庫 cmdlet tooregister hello 機器。</span><span class="sxs-lookup"><span data-stu-id="785e8-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="785e8-176">這個及其他指令程式使用的備份，會從 hello MSONLINE 模組 hello 安裝程序的一部分加入的 Mars AgentInstaller 哪些 hello。</span><span class="sxs-lookup"><span data-stu-id="785e8-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="785e8-177">hello 代理程式安裝程式不會更新 hello $Env: PSModulePath 變數。</span><span class="sxs-lookup"><span data-stu-id="785e8-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="785e8-178">這表示模組自動載入會失敗。</span><span class="sxs-lookup"><span data-stu-id="785e8-178">This means module auto-load fails.</span></span> <span data-ttu-id="785e8-179">tooresolve 這樣，您可以 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="785e8-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="785e8-180">或者，您可以手動載入 hello 模組在您的指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="785e8-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="785e8-181">一旦您載入 hello Online Backup cmdlet，您會註冊 hello 保存庫認證：</span><span class="sxs-lookup"><span data-stu-id="785e8-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


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
> <span data-ttu-id="785e8-182">請勿使用相對路徑 toospecify hello 保存庫認證檔案。</span><span class="sxs-lookup"><span data-stu-id="785e8-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="785e8-183">您必須提供絕對路徑做為輸入的 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="785e8-184">網路設定</span><span class="sxs-lookup"><span data-stu-id="785e8-184">Networking settings</span></span>
<span data-ttu-id="785e8-185">Hello 連線 hello 的 Windows 電腦的 toohello 網際網路是透過 proxy 伺服器，當 hello proxy 設定也可以提供 toohello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="785e8-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="785e8-186">本範例未使用 Proxy 伺服器，因此會明確地清除任何 Proxy 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="785e8-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="785e8-187">頻寬使用也可以控制與 hello 選項```work hour bandwidth```和```non-work hour bandwidth```一組指定的 hello 一週天數。</span><span class="sxs-lookup"><span data-stu-id="785e8-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="785e8-188">設定 hello proxy 和頻寬詳細資料是使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="785e8-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="785e8-189">加密設定</span><span class="sxs-lookup"><span data-stu-id="785e8-189">Encryption settings</span></span>
<span data-ttu-id="785e8-190">hello 傳送備份資料 tooAzure 備份是加密的 tooprotect hello hello 資料機密性。</span><span class="sxs-lookup"><span data-stu-id="785e8-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="785e8-191">hello 加密複雜密碼是還原的 hello 「 密碼 」 toodecrypt hello 資料在 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="785e8-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="785e8-192">安全及安全一旦設定之後，保留 hello 複雜密碼資訊。</span><span class="sxs-lookup"><span data-stu-id="785e8-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="785e8-193">您無法將資料從 Azure 可以 toorestore 沒有此複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="785e8-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="785e8-194">備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="785e8-194">Back up files and folders</span></span>
<span data-ttu-id="785e8-195">從 Windows 伺服器和用戶端 tooAzure 備份的所有備份都受到原則。</span><span class="sxs-lookup"><span data-stu-id="785e8-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="785e8-196">hello 原則包含三個部分：</span><span class="sxs-lookup"><span data-stu-id="785e8-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="785e8-197">A**備份排程**，指定當備份需要 toobe 採取和與 hello 服務同步處理。</span><span class="sxs-lookup"><span data-stu-id="785e8-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="785e8-198">A**保留排程**指定 tooretain hello 復原點在 Azure 中的時間長度。</span><span class="sxs-lookup"><span data-stu-id="785e8-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="785e8-199">**檔案包含/排除規格** ，指出要備份的項目。</span><span class="sxs-lookup"><span data-stu-id="785e8-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="785e8-200">本文件中要說明如何將備份自動化，因此我們假設還未設定任何選項。</span><span class="sxs-lookup"><span data-stu-id="785e8-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="785e8-201">一開始我們先建立新的備份原則使用 hello [New-obpolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="785e8-202">在此時間 hello 原則是空的其他指令程式會需要的 toodefine、 哪些項目會包含或排除備份會執行，且其中 hello 時將儲存備份。</span><span class="sxs-lookup"><span data-stu-id="785e8-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="785e8-203">設定 hello 備份排程</span><span class="sxs-lookup"><span data-stu-id="785e8-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="785e8-204">第一次 hello hello 原則的 3 組件是 hello 備份排程，會建立使用 hello[新增 OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="785e8-205">hello 備份排程會定義當備份需要採取 toobe。</span><span class="sxs-lookup"><span data-stu-id="785e8-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="785e8-206">建立排程時您會需要 toospecify 2 輸入的參數：</span><span class="sxs-lookup"><span data-stu-id="785e8-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="785e8-207">**Hello 一周天數**該 hello 應該執行備份。</span><span class="sxs-lookup"><span data-stu-id="785e8-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="785e8-208">您可以執行 hello 上只要一天的備份作業或 hello 週中的每日兩者之間的任何組合。</span><span class="sxs-lookup"><span data-stu-id="785e8-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="785e8-209">**Hello 每天時間**hello 備份何時應執行。</span><span class="sxs-lookup"><span data-stu-id="785e8-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="785e8-210">您可以定義總 too3 hello 備份將會觸發時機的 hello 每天不同時間。</span><span class="sxs-lookup"><span data-stu-id="785e8-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="785e8-211">例如，您可以設定每週六和日下午 4 點執行備份原則。</span><span class="sxs-lookup"><span data-stu-id="785e8-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="785e8-212">hello 備份排程必須 toobe 與原則相關聯，而且這可藉由使用 hello [Set-obschedule](https://technet.microsoft.com/library/hh770407) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="785e8-213">設定保留原則</span><span class="sxs-lookup"><span data-stu-id="785e8-213">Configuring a retention policy</span></span>
<span data-ttu-id="785e8-214">hello 保留原則定義多久的復原點建立的備份作業都會保留下來。</span><span class="sxs-lookup"><span data-stu-id="785e8-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="785e8-215">當建立新的保留原則，使用 hello[新增 OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet，您可以指定 hello 的天數 hello 備份復原點需要使用 Azure 備份保留 toobe。</span><span class="sxs-lookup"><span data-stu-id="785e8-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="785e8-216">下列的 hello 範例設定為 7 天的保留原則。</span><span class="sxs-lookup"><span data-stu-id="785e8-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="785e8-217">hello 保留原則必須關聯與 hello 主要原則使用 hello cmdlet[組 OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="785e8-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="785e8-218">包含和排除檔案 toobe 備份</span><span class="sxs-lookup"><span data-stu-id="785e8-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="785e8-219">```OBFileSpec```物件會定義 hello 檔案 toobe 包含和排除在備份中。</span><span class="sxs-lookup"><span data-stu-id="785e8-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="785e8-220">這是一組規則範圍出 hello 保護檔案和電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="785e8-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="785e8-221">您可以設定所需數量的檔案包含或排除規則，並建立其與原則的關聯。</span><span class="sxs-lookup"><span data-stu-id="785e8-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="785e8-222">建立新的 OBFileSpec 物件時，您可以：</span><span class="sxs-lookup"><span data-stu-id="785e8-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="785e8-223">指定包含 hello 檔案和資料夾 toobe</span><span class="sxs-lookup"><span data-stu-id="785e8-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="785e8-224">指定排除 hello 檔案和資料夾 toobe</span><span class="sxs-lookup"><span data-stu-id="785e8-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="785e8-225">指定最多的遞迴備份的資料夾 （或） 中是否只 hello 最上層資料夾中的檔案 hello 指定應該要備份的資料。</span><span class="sxs-lookup"><span data-stu-id="785e8-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="785e8-226">hello 後者是利用 hello New-obfilespec 命令 hello-非遞迴旗標來達成。</span><span class="sxs-lookup"><span data-stu-id="785e8-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="785e8-227">在 hello 下列範例中，我們將備份磁碟區 c： 和 d:，並排除 hello hello Windows 資料夾和任何暫存資料夾中的 OS 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="785e8-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="785e8-228">讓我們將建立兩個檔案規格使用 hello toodo [New-obfilespec](https://technet.microsoft.com/library/hh770408) cmdlet-包含和排除。</span><span class="sxs-lookup"><span data-stu-id="785e8-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="785e8-229">一旦已建立 hello 檔案規格，它們相關聯 hello 原則使用 hello [Add-obfilespec](https://technet.microsoft.com/library/hh770424) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="785e8-230">套用 hello 原則</span><span class="sxs-lookup"><span data-stu-id="785e8-230">Applying hello policy</span></span>
<span data-ttu-id="785e8-231">現在 hello 原則物件已完成，並具有相關聯的備份排程、 保留原則，以及檔案的包含/排除清單。</span><span class="sxs-lookup"><span data-stu-id="785e8-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="785e8-232">此原則現在可以針對 Azure Backup toouse 認可。</span><span class="sxs-lookup"><span data-stu-id="785e8-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="785e8-233">原則在套用新建立的 hello 之前請確認沒有任何現有的備份原則，使用 hello 與 hello 伺服器相關聯[移除 OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="785e8-234">移除 hello 原則將會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="785e8-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="785e8-235">tooskip hello 確認使用 hello```-Confirm:$false```與 hello 指令的旗標。</span><span class="sxs-lookup"><span data-stu-id="785e8-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="785e8-236">調配 hello 原則物件是使用 hello [Set-obpolicy](https://technet.microsoft.com/library/hh770421) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="785e8-237">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="785e8-237">This will also ask for confirmation.</span></span> <span data-ttu-id="785e8-238">tooskip hello 確認使用 hello```-Confirm:$false```與 hello 指令的旗標。</span><span class="sxs-lookup"><span data-stu-id="785e8-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="785e8-239">您可以檢視 hello 詳細資料的 hello 現有的備份原則使用 hello [Get-obpolicy](https://technet.microsoft.com/library/hh770406) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="785e8-240">您可以向下鑽研進一步使用 hello [Get OBSchedule](https://technet.microsoft.com/library/hh770423) hello 備份排程和 hello cmdlet [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello 保留原則的 cmdlet</span><span class="sxs-lookup"><span data-stu-id="785e8-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="785e8-241">執行臨機操作備份</span><span class="sxs-lookup"><span data-stu-id="785e8-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="785e8-242">一旦已設定備份原則 hello 備份會依 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="785e8-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="785e8-243">觸發臨機操作備份，您也可以使用 hello[開始 OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="785e8-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="785e8-244">從 Azure 備份還原資料</span><span class="sxs-lookup"><span data-stu-id="785e8-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="785e8-245">本節將引導您 hello 步驟自動化從 Azure 備份復原資料。</span><span class="sxs-lookup"><span data-stu-id="785e8-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="785e8-246">其中涉及 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="785e8-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="785e8-247">挑選 hello 來源磁碟區</span><span class="sxs-lookup"><span data-stu-id="785e8-247">Pick hello source volume</span></span>
2. <span data-ttu-id="785e8-248">選擇備份的點 toorestore</span><span class="sxs-lookup"><span data-stu-id="785e8-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="785e8-249">選擇項目 toorestore</span><span class="sxs-lookup"><span data-stu-id="785e8-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="785e8-250">觸發程序 hello 還原程序</span><span class="sxs-lookup"><span data-stu-id="785e8-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="785e8-251">挑選 hello 來源磁碟區</span><span class="sxs-lookup"><span data-stu-id="785e8-251">Picking hello source volume</span></span>
<span data-ttu-id="785e8-252">在訂單 toorestore Azure Backup 中的項目，您必須先 tooidentify hello hello 項目的來源。</span><span class="sxs-lookup"><span data-stu-id="785e8-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="785e8-253">我們正在 Windows Server 或 Windows 用戶端 hello 內容中執行 hello 命令，因為已經識別 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="785e8-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="785e8-254">hello 下一個步驟來識別 hello 來源是包含它的 tooidentify hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="785e8-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="785e8-255">一份磁碟區或來源備份從這部電腦可以擷取執行 hello [Get-obrecoverablesource](https://technet.microsoft.com/library/hh770410) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="785e8-256">此命令會傳回所有 hello 來源備份來源伺服器/用戶端的陣列。</span><span class="sxs-lookup"><span data-stu-id="785e8-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="785e8-257">選擇備份點從哪些 toorestore</span><span class="sxs-lookup"><span data-stu-id="785e8-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="785e8-258">擷取一份備份時間點執行 hello [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet 搭配適當的參數。</span><span class="sxs-lookup"><span data-stu-id="785e8-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="785e8-259">在本例中，我們將選擇 hello 最新備份點 hello 來源磁碟區*d:* ，並用 toorecover 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="785e8-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="785e8-260">hello 物件```$rps```是備份的點陣列。</span><span class="sxs-lookup"><span data-stu-id="785e8-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="785e8-261">hello 第一個元素是 hello 最新的點而 hello 第 n 個項目是 hello 最舊的點。</span><span class="sxs-lookup"><span data-stu-id="785e8-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="785e8-262">toochoose hello 最新的點，我們將使用```$rps[0]```。</span><span class="sxs-lookup"><span data-stu-id="785e8-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="785e8-263">選擇項目 toorestore</span><span class="sxs-lookup"><span data-stu-id="785e8-263">Choosing an item toorestore</span></span>
<span data-ttu-id="785e8-264">以遞迴方式 tooidentify hello 確實的檔案或資料夾 toorestore，使用 hello [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="785e8-265">該方式 hello 資料夾階層可瀏覽單獨使用 hello ```Get-OBRecoverableItem```。</span><span class="sxs-lookup"><span data-stu-id="785e8-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="785e8-266">在此範例中，如果我們想要 toorestore hello 檔*finances.xls*我們可以參考使用 hello 物件```$filesFolders[1]```。</span><span class="sxs-lookup"><span data-stu-id="785e8-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="785e8-267">您也可以搜尋項目 toorestore 使用 hello ```Get-OBRecoverableItem``` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="785e8-268">在本例中，針對 toosearch *finances.xls*我們無法取得的控制代碼 hello 檔案上執行此命令：</span><span class="sxs-lookup"><span data-stu-id="785e8-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="785e8-269">觸發 hello 還原程序</span><span class="sxs-lookup"><span data-stu-id="785e8-269">Triggering hello restore process</span></span>
<span data-ttu-id="785e8-270">tootrigger hello 還原程序，我們必須先 toospecify hello 復原選項。</span><span class="sxs-lookup"><span data-stu-id="785e8-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="785e8-271">這可以經由使用 hello[新增 OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="785e8-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="785e8-272">例如，假設我們想 toorestore hello 檔案太*C:\temp*。我們也假設我們想要在 hello 目的地資料夾已存在 tooskip 檔案*C:\temp*。 toocreate 這類復原選項，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="785e8-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="785e8-273">現在使用 hello 觸發 hello 還原程序[Start-obrecovery](https://technet.microsoft.com/library/hh770402.aspx) hello 選取命令```$item```hello hello 輸出```Get-OBRecoverableItem```cmdlet:</span><span class="sxs-lookup"><span data-stu-id="785e8-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="785e8-274">解除安裝 hello Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="785e8-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="785e8-275">解除安裝 hello Azure 備份代理程式可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="785e8-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="785e8-276">Hello 機器上解除安裝 hello 代理程式二進位檔有某些後果 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="785e8-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="785e8-277">移除 hello 機器 hello 檔案篩選器，並會停止追蹤的變更。</span><span class="sxs-lookup"><span data-stu-id="785e8-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="785e8-278">從 hello 機器，移除所有原則資訊，但仍繼續 toobe 儲存在 hello 服務中的 hello 原則資訊。</span><span class="sxs-lookup"><span data-stu-id="785e8-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="785e8-279">會移除所有備份排程，且不再進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="785e8-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="785e8-280">不過，hello 會維持為 Azure 中儲存的資料，而且您根據 hello 保留原則設定會保留。</span><span class="sxs-lookup"><span data-stu-id="785e8-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="785e8-281">較舊的時間點會自動過時。</span><span class="sxs-lookup"><span data-stu-id="785e8-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="785e8-282">遠端管理</span><span class="sxs-lookup"><span data-stu-id="785e8-282">Remote management</span></span>
<span data-ttu-id="785e8-283">可以透過 PowerShell 遠端執行所有 hello 管理周圍 hello Azure 備份代理程式、 原則和資料來源。</span><span class="sxs-lookup"><span data-stu-id="785e8-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="785e8-284">需要 toobe 備妥正確的 hello 機器將從遠端管理。</span><span class="sxs-lookup"><span data-stu-id="785e8-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="785e8-285">根據預設，hello WinRM 服務設定為手動啟動。</span><span class="sxs-lookup"><span data-stu-id="785e8-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="785e8-286">hello 啟動類型必須設定得*自動*和 hello 服務應該啟動。</span><span class="sxs-lookup"><span data-stu-id="785e8-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="785e8-287">tooverify 的 hello WinRM 服務正在執行，hello hello Status 屬性值應該是*執行*。</span><span class="sxs-lookup"><span data-stu-id="785e8-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="785e8-288">應該將 PowerShell 設定為可以遠端執行。</span><span class="sxs-lookup"><span data-stu-id="785e8-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="785e8-289">hello 電腦現在可以管理遠端-從 hello hello 代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="785e8-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="785e8-290">例如，下列指令碼的 hello 複製 hello 代理程式 toohello 遠端電腦，並將它安裝。</span><span class="sxs-lookup"><span data-stu-id="785e8-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="785e8-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="785e8-291">Next steps</span></span>
<span data-ttu-id="785e8-292">如需 Windows Server/用戶端的 Azure 備份詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="785e8-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="785e8-293">簡介 tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="785e8-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="785e8-294">備份 Windows 伺服器</span><span class="sxs-lookup"><span data-stu-id="785e8-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
