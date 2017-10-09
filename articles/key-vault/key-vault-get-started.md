---
title: "開始使用 Azure 金鑰保存庫的 aaaGet |Microsoft 文件"
description: "使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a><span data-ttu-id="48434-103">開始使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="48434-103">Get started with Azure Key Vault</span></span>
<span data-ttu-id="48434-104">大部分地區均提供 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="48434-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="48434-105">如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="48434-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="48434-106">簡介</span><span class="sxs-lookup"><span data-stu-id="48434-106">Introduction</span></span>
<span data-ttu-id="48434-107">使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器 （保存庫） 在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。</span><span class="sxs-lookup"><span data-stu-id="48434-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="48434-108">它會引導您透過使用 Azure PowerShell toocreate hello 程序包含金鑰或密碼，您可以使用 Azure 應用程式的保存庫。</span><span class="sxs-lookup"><span data-stu-id="48434-108">It walks you through hello process of using Azure PowerShell toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="48434-109">接著，它會說明應用程式可以如何使用該金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="48434-109">It then shows you how an application can use that key or password.</span></span>

<span data-ttu-id="48434-110">**估計時間 toocomplete:** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="48434-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="48434-111">本教學課程不包括如何 toowrite hello Azure hello 步驟的其中一個包含的應用程式，也就是如何 tooauthorize 應用程式 toouse 金鑰或密碼中 hello 金鑰保存庫的指示。</span><span class="sxs-lookup"><span data-stu-id="48434-111">This tutorial does not include instructions for how toowrite hello Azure application that one of hello steps includes, namely how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="48434-112">本教學課程使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="48434-112">This tutorial uses Azure PowerShell.</span></span> <span data-ttu-id="48434-113">如需跨平台命令列介面的指示，請參閱 [這個對等的教學課程](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="48434-113">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
>

<span data-ttu-id="48434-114">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="48434-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48434-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="48434-115">Prerequisites</span></span>
<span data-ttu-id="48434-116">toocomplete 本教學課程中，您必須擁有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="48434-116">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="48434-117">訂用帳戶 tooMicrosoft Azure。</span><span class="sxs-lookup"><span data-stu-id="48434-117">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="48434-118">如果您沒有訂用帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="48434-118">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="48434-119">Azure PowerShell， **最低版本為 1.1.0**。</span><span class="sxs-lookup"><span data-stu-id="48434-119">Azure PowerShell, **minimum version of 1.1.0**.</span></span> <span data-ttu-id="48434-120">tooinstall Azure PowerShell，將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="48434-120">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="48434-121">如果您已安裝 Azure PowerShell，並不知道 hello 版本 hello Azure PowerShell 主控台中，輸入`(Get-Module azure -ListAvailable).Version`。</span><span class="sxs-lookup"><span data-stu-id="48434-121">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span> <span data-ttu-id="48434-122">如果您已安裝 Azure PowerShell 版本 0.9.1 至 0.9.8，您仍可使用本教學課程並稍作變更。</span><span class="sxs-lookup"><span data-stu-id="48434-122">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span></span> <span data-ttu-id="48434-123">例如，您必須使用 hello`Switch-AzureMode AzureResourceManager`命令以及某些 hello Azure 金鑰保存庫命令已變更。</span><span class="sxs-lookup"><span data-stu-id="48434-123">For example, you must use hello `Switch-AzureMode AzureResourceManager` command and some of hello Azure Key Vault commands have changed.</span></span> <span data-ttu-id="48434-124">如需 hello 為 0.9.8 透過 0.9.1 版本的金鑰保存庫 cmdlet 的清單，請參閱[Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。</span><span class="sxs-lookup"><span data-stu-id="48434-124">For a list of hello Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>
* <span data-ttu-id="48434-125">將會設定的 toouse hello 金鑰或密碼，您在本教學課程中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-125">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="48434-126">範例應用程式是可從 hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343)。</span><span class="sxs-lookup"><span data-stu-id="48434-126">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span> <span data-ttu-id="48434-127">如需指示，請參閱 hello 隨附的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="48434-127">For instructions, see hello accompanying Readme file.</span></span>

<span data-ttu-id="48434-128">此教學課程的設計為 Azure PowerShell 初學者所設計，但它假設您已了解 hello 基本概念，例如模組、 cmdlet 和工作階段。</span><span class="sxs-lookup"><span data-stu-id="48434-128">This tutorial is designed for Azure PowerShell beginners, but it assumes that you understand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="48434-129">如需詳細資訊，請參閱 [開始使用 Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)。</span><span class="sxs-lookup"><span data-stu-id="48434-129">For more information, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="48434-130">tooget 詳細說明您在此教學課程中，使用 hello 中看到任何 cmdlet **Get-help** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="48434-130">tooget detailed help for any cmdlet that you see in this tutorial, use hello **Get-Help** cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="48434-131">例如，tooget 說明 hello**登入 AzureRmAccount** cmdlet，類型：</span><span class="sxs-lookup"><span data-stu-id="48434-131">For example, tooget help for hello **Login-AzureRmAccount** cmdlet, type:</span></span>

    Get-Help Login-AzureRmAccount -Detailed

<span data-ttu-id="48434-132">您也可以閱讀下列教學課程 tooget 熟悉與 Azure 資源管理員的 Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="48434-132">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure PowerShell:</span></span>

* [<span data-ttu-id="48434-133">如何 tooinstall 和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48434-133">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="48434-134">Azure PowerShell 搭配資源管理員使用</span><span class="sxs-lookup"><span data-stu-id="48434-134">Using Azure PowerShell with Resource Manager</span></span>](../powershell-azure-resource-manager.md)

## <span data-ttu-id="48434-135"><a id="connect"></a>連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="48434-135"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="48434-136">啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="48434-136">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="48434-137">請注意，如果您使用 Azure 中，例如 Azure 政府的特定執行個體使用 hello-使用此命令的環境參數。</span><span class="sxs-lookup"><span data-stu-id="48434-137">Note that if you are using a specific instance of Azure, for example, Azure Government, use hello -Environment parameter with this command.</span></span> <span data-ttu-id="48434-138">例如：`Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span><span class="sxs-lookup"><span data-stu-id="48434-138">For example: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span></span>

<span data-ttu-id="48434-139">在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="48434-139">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="48434-140">Azure PowerShell 取得所有 hello 訂用帳戶相關聯，與此帳戶，而且依預設，會使用 hello 第一個。</span><span class="sxs-lookup"><span data-stu-id="48434-140">Azure PowerShell gets all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="48434-141">如果您有多個訂用帳戶，並想 toospecify 特定一個 toouse for Azure Key Vault，輸入下列帳戶 toosee hello 訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="48434-141">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="48434-142">然後，toospecify hello 訂用帳戶 toouse，類型：</span><span class="sxs-lookup"><span data-stu-id="48434-142">Then, toospecify hello subscription toouse, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

<span data-ttu-id="48434-143">如需有關如何設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="48434-143">For more information about configuring Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="48434-144"><a id="resource"></a>建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="48434-144"><a id="resource"></a>Create a new resource group</span></span>
<span data-ttu-id="48434-145">使用 Azure 資源管理員時，會在資源群組中建立所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="48434-145">When you use Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="48434-146">在本教學課程中，我們將建立名為 **ContosoResourceGroup** 的新資源群組：</span><span class="sxs-lookup"><span data-stu-id="48434-146">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span></span>

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <span data-ttu-id="48434-147"><a id="vault"></a>建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="48434-147"><a id="vault"></a>Create a key vault</span></span>
<span data-ttu-id="48434-148">使用 hello[新增 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="48434-148">Use hello [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate a key vault.</span></span> <span data-ttu-id="48434-149">這個 cmdlet 包含三個必要參數：**資源群組名稱**、**金鑰保存庫名稱**，和 hello**地理位置**。</span><span class="sxs-lookup"><span data-stu-id="48434-149">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and hello **geographic location**.</span></span>

<span data-ttu-id="48434-150">例如，如果您使用保存庫名稱 hello **ContosoKeyVault**，hello 資源群組名稱**ContosoResourceGroup**，和 hello 位置**東亞**，類型：</span><span class="sxs-lookup"><span data-stu-id="48434-150">For example, if you use hello vault name of **ContosoKeyVault**, hello resource group name of **ContosoResourceGroup**, and hello location of **East Asia**, type:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

<span data-ttu-id="48434-151">此 cmdlet 的 hello 輸出會顯示您剛才建立的 hello 金鑰保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="48434-151">hello output of this cmdlet shows properties of hello key vault that you’ve just created.</span></span> <span data-ttu-id="48434-152">hello 兩個最重要的屬性包括：</span><span class="sxs-lookup"><span data-stu-id="48434-152">hello two most important properties are:</span></span>

* <span data-ttu-id="48434-153">**保存庫名稱**: hello 範例中，這是**ContosoKeyVault**。</span><span class="sxs-lookup"><span data-stu-id="48434-153">**Vault Name**: In hello example, this is **ContosoKeyVault**.</span></span> <span data-ttu-id="48434-154">您將在其他金鑰保存庫 Cmdlet 中使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="48434-154">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="48434-155">**保存庫 URI**: hello 範例中，這是 https://contosokeyvault.vault.azure.net/。</span><span class="sxs-lookup"><span data-stu-id="48434-155">**Vault URI**: In hello example, this is https://contosokeyvault.vault.azure.net/.</span></span> <span data-ttu-id="48434-156">透過其 REST API 使用保存庫的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="48434-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="48434-157">現在已授權的 tooperform 保存庫上此金鑰的任何作業，就會是您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="48434-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="48434-158">而且，沒有其他人有此授權。</span><span class="sxs-lookup"><span data-stu-id="48434-158">As yet, nobody else is.</span></span>

> [!NOTE]
> <span data-ttu-id="48434-159">如果您看到 hello 錯誤**hello 訂用帳戶未註冊的 toouse 命名空間 'Microsoft.KeyVault'**當您嘗試 toocreate 新金鑰保存庫，執行`Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"`，然後重新執行新增 AzureRmKeyVault 命令。</span><span class="sxs-lookup"><span data-stu-id="48434-159">If you see hello error **hello subscription is not registered toouse namespace 'Microsoft.KeyVault'** when you try toocreate your new key vault, run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` and then rerun your New-AzureRmKeyVault command.</span></span> <span data-ttu-id="48434-160">如需詳細資訊，請參閱 [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)。</span><span class="sxs-lookup"><span data-stu-id="48434-160">For more information, see [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).</span></span>
>
>

## <span data-ttu-id="48434-161"><a id="add"></a>新增金鑰或密碼 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="48434-161"><a id="add"></a>Add a key or secret toohello key vault</span></span>
<span data-ttu-id="48434-162">如果您想為您的 Azure 金鑰保存庫 toocreate 受軟體保護的金鑰，請使用 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="48434-162">If you want Azure Key Vault toocreate a software-protected key for you, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet, and type hello following:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

<span data-ttu-id="48434-163">不過，如果您在現有受軟體保護金鑰。PFX 檔案儲存 tooyour C:\ 磁碟機中名為您想 tooupload tooAzure 金鑰保存庫，遵循 tooset hello 變數的型別 hello softkey.pfx **securepfxpwd**密碼**123** hello。PFX 檔案：</span><span class="sxs-lookup"><span data-stu-id="48434-163">However, if you have an existing software-protected key in a .PFX file saved tooyour C:\ drive in a file named softkey.pfx that you want tooupload tooAzure Key Vault, type hello following tooset hello variable **securepfxpwd** for a password of **123** for hello .PFX file:</span></span>

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

<span data-ttu-id="48434-164">然後輸入 hello hello 中的下列 tooimport hello 索引鍵。PFX 檔案，它會透過 hello 金鑰保存庫服務中的軟體保護金鑰 hello:</span><span class="sxs-lookup"><span data-stu-id="48434-164">Then type hello following tooimport hello key from hello .PFX file, which protects hello key by software in hello Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


<span data-ttu-id="48434-165">您現在可以參考此機碼，您建立或上傳 tooAzure 金鑰保存庫中，使用它的 URI。</span><span class="sxs-lookup"><span data-stu-id="48434-165">You can now reference this key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="48434-166">使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways 取得 hello 目前的版本，並使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget 這個特定的版本。</span><span class="sxs-lookup"><span data-stu-id="48434-166">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>  

<span data-ttu-id="48434-167">此索引鍵，類型 toodisplay hello URI:</span><span class="sxs-lookup"><span data-stu-id="48434-167">toodisplay hello URI for this key, type:</span></span>

    $Key.key.kid

<span data-ttu-id="48434-168">tooadd 秘密 toohello 保存庫，這是名為 SQLPassword 密碼，且擁有 hello 值 Pa$ $w0rd tooAzure 金鑰保存庫，將第一次 Pa$ $w0rd tooa 安全字串 hello 值輸入 hello 下列轉換：</span><span class="sxs-lookup"><span data-stu-id="48434-168">tooadd a secret toohello vault, which is a password named SQLPassword and has hello value of Pa$$w0rd tooAzure Key Vault, first convert hello value of Pa$$w0rd tooa secure string by typing hello following:</span></span>

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

<span data-ttu-id="48434-169">然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="48434-169">Then, type hello following:</span></span>

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

<span data-ttu-id="48434-170">您現在可以參考您藉由使用其 URI 新增 tooAzure 金鑰保存庫，此密碼。</span><span class="sxs-lookup"><span data-stu-id="48434-170">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="48434-171">使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways 取得 hello 目前的版本，並使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget 這個特定的版本。</span><span class="sxs-lookup"><span data-stu-id="48434-171">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="48434-172">此密碼，類型為 toodisplay hello URI:</span><span class="sxs-lookup"><span data-stu-id="48434-172">toodisplay hello URI for this secret, type:</span></span>

    $secret.Id

<span data-ttu-id="48434-173">讓我們來檢視 hello 金鑰或您剛才建立的密碼：</span><span class="sxs-lookup"><span data-stu-id="48434-173">Let’s view hello key or secret that you just created:</span></span>

* <span data-ttu-id="48434-174">tooview 您索引鍵，類型：`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="48434-174">tooview your key, type: `Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="48434-175">tooview 秘密，型別：`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="48434-175">tooview your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span></span>

<span data-ttu-id="48434-176">現在，您的金鑰保存庫和金鑰或密碼已準備好應用程式 toouse。</span><span class="sxs-lookup"><span data-stu-id="48434-176">Now, your key vault and key or secret is ready for applications toouse.</span></span> <span data-ttu-id="48434-177">您必須授權應用程式 toouse 它們。</span><span class="sxs-lookup"><span data-stu-id="48434-177">You must authorize applications toouse them.</span></span>  

## <span data-ttu-id="48434-178"><a id="register"></a>向 Azure Active Directory 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="48434-178"><a id="register"></a>Register an application with Azure Active Directory</span></span>
<span data-ttu-id="48434-179">這步驟通常會由開發人員在個別電腦上完成。</span><span class="sxs-lookup"><span data-stu-id="48434-179">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="48434-180">它不是特定 tooAzure 金鑰保存庫，但是仍然包含在此處為求完整起見。</span><span class="sxs-lookup"><span data-stu-id="48434-180">It is not specific tooAzure Key Vault, but is included here for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48434-181">toocomplete hello 教學課程，您的帳戶、 hello 保存庫和您要登錄在此步驟中的 hello 應用程式都必須在 hello 相同的 Azure 目錄。</span><span class="sxs-lookup"><span data-stu-id="48434-181">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="48434-182">使用金鑰保存庫的應用程式必須使用 Azure Active Directory 的權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="48434-182">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="48434-183">toodo，hello hello 應用程式的擁有者必須先註冊他們的 Azure Active Directory 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-183">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="48434-184">在 hello 註冊結尾，hello 應用程式擁有者取得 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="48434-184">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="48434-185">**應用程式識別碼**(也稱為用戶端 ID) 和**驗證金鑰**（也稱為 hello 共用的密碼）。</span><span class="sxs-lookup"><span data-stu-id="48434-185">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="48434-186">hello 應用程式必須提供這兩個這些值 tooAzure Active Directory、 tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="48434-186">hello application must present both these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="48434-187">Hello 應用程式的方式設定的 toodo 這取決於 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-187">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="48434-188">Hello 金鑰保存庫的範例應用程式，hello 應用程式擁有者，請 hello app.config 檔案中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="48434-188">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="48434-189">在 Azure Active Directory tooregister hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="48434-189">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="48434-190">登入 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="48434-190">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="48434-191">Hello 左側，按一下  **Active Directory**，然後選取您要在其中登錄您的應用程式的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="48434-191">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> <span data-ttu-id="48434-192">**注意：**您必須選取 hello 含有相同目錄 hello 您用來建立金鑰保存庫的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="48434-192">**Note:** You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="48434-193">如果您不知道哪個目錄這是，按一下 **設定**，識別 hello 訂閱您用來建立金鑰保存庫，並注意 hello hello 目錄名稱顯示 hello 最後一個資料行。</span><span class="sxs-lookup"><span data-stu-id="48434-193">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>
3. <span data-ttu-id="48434-194">按一下 [ **應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="48434-194">Click **APPLICATIONS**.</span></span> <span data-ttu-id="48434-195">如果沒有任何應用程式已加入 tooyour 目錄，此頁面會顯示只有 hello**新增應用程式**連結。</span><span class="sxs-lookup"><span data-stu-id="48434-195">If no apps have been added tooyour directory, this page shows only hello **Add an App** link.</span></span> <span data-ttu-id="48434-196">按一下 [hello] 連結，或或者，您可以按一下**新增**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="48434-196">Click hello link, or alternatively, you can click **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="48434-197">在 hello**新增應用程式**精靈，在 hello**您該怎麼想 toodo？**頁面上，按一下**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="48434-197">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="48434-198">在 hello**告訴我們您的應用程式**頁面上，指定您的應用程式的名稱，然後選取**WEB 應用程式和/或 WEB API** (hello 預設值)。</span><span class="sxs-lookup"><span data-stu-id="48434-198">On hello **Tell us about your application** page, specify a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="48434-199">按一下 hello**下一步**圖示。</span><span class="sxs-lookup"><span data-stu-id="48434-199">Click hello **Next** icon.</span></span>
6. <span data-ttu-id="48434-200">在 hello**應用程式屬性**頁面上，指定 hello**登入 URL**和**應用程式識別碼 URI** web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-200">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="48434-201">如果您的應用程式沒有這些值，您可以在此步驟中虛構這些值 (例如，您可以在這兩個方塊中指定 http://test1.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="48434-201">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="48434-202">這些網站是否存在並不重要。</span><span class="sxs-lookup"><span data-stu-id="48434-202">It does not matter if these sites exist.</span></span> <span data-ttu-id="48434-203">重要的是每個應用程式的 hello 應用程式識別碼 URI 是不同的目錄中的每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-203">What is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="48434-204">hello 目錄會使用此字串 tooidentify 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48434-204">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="48434-205">按一下 hello**完成**圖示 toosave hello 精靈中的變更。</span><span class="sxs-lookup"><span data-stu-id="48434-205">Click hello **Complete** icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="48434-206">在 hello**快速入門**頁面上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="48434-206">On hello **Quick Start** page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="48434-207">捲動 toohello**金鑰**區段中選取 hello 持續時間，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="48434-207">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="48434-208">hello 頁面重新整理，而且現在會顯示金鑰值。</span><span class="sxs-lookup"><span data-stu-id="48434-208">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="48434-209">您必須設定您的應用程式具有此機碼值與 hello**用戶端識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="48434-209">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="48434-210">(有關此設定的指示僅適用於特定應用程式。)</span><span class="sxs-lookup"><span data-stu-id="48434-210">(Instructions for this configuration are application-specific.)</span></span>
10. <span data-ttu-id="48434-211">複製此頁面上，您會在您的保存庫使用 hello 下一個步驟 tooset 權限中的 hello 用戶端識別碼值。</span><span class="sxs-lookup"><span data-stu-id="48434-211">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <span data-ttu-id="48434-212"><a id="authorize"></a>授權 hello 應用程式 toouse hello 金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="48434-212"><a id="authorize"></a>Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="48434-213">tooauthorize hello 應用程式 tooaccess hello hello 保存庫，使用中金鑰或密碼[Set-azurermkeyvaultaccesspolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="48434-213">tooauthorize hello application tooaccess hello key or secret in hello vault, use the [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>

<span data-ttu-id="48434-214">例如，如果您的保存庫名稱是**ContosoKeyVault**和您想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed，用戶端識別碼，而且您想 tooauthorize hello 應用程式 toodecrypt 並登入索引鍵中的 hello 應用程式您的保存庫，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="48434-214">For example, if your vault name is **ContosoKeyVault** and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="48434-215">如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="48434-215">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <span data-ttu-id="48434-216"><a id="HSM"></a>如果您想 toouse 硬體安全性模組 (HSM)</span><span class="sxs-lookup"><span data-stu-id="48434-216"><a id="HSM"></a>If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="48434-217">為求保險，您可以匯入，或在硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="48434-217">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="48434-218">hello Hsm 是的 FIPS 140-2 Level 2 驗證。</span><span class="sxs-lookup"><span data-stu-id="48434-218">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="48434-219">如果這項需求不適 tooyou，略過本節並移太[刪除 hello 金鑰保存庫及相關聯的金鑰和秘密](#delete)。</span><span class="sxs-lookup"><span data-stu-id="48434-219">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete).</span></span>

<span data-ttu-id="48434-220">toocreate 這些受 HSM 保護的金鑰，您必須使用 hello [Azure 金鑰保存庫 Premium 服務層 toosupport 受 HSM 保護金鑰](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="48434-220">toocreate these HSM-protected keys, you must use hello [Azure Key Vault Premium service tier toosupport HSM-protected keys](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="48434-221">此外，請注意此功能不適用於 Azure China。</span><span class="sxs-lookup"><span data-stu-id="48434-221">In addition, note that this functionality is not available for Azure China.</span></span>

<span data-ttu-id="48434-222">當您建立 hello 金鑰保存庫時，新增 hello **-SKU**參數：</span><span class="sxs-lookup"><span data-stu-id="48434-222">When you create hello key vault, add hello **-SKU** parameter:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



<span data-ttu-id="48434-223">您可以將軟體保護金鑰 （如下所示稍早） 和 HSM 保護的金鑰 toothis 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="48434-223">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis key vault.</span></span> <span data-ttu-id="48434-224">toocreate HSM 保護的金鑰組 hello **-目的地**參數 too'HSM':</span><span class="sxs-lookup"><span data-stu-id="48434-224">toocreate an HSM-protected key, set hello **-Destination** parameter too'HSM':</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

<span data-ttu-id="48434-225">您可以使用下列命令 tooimport hello 的金鑰。在您的電腦上的 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="48434-225">You can use hello following command tooimport a key from a .PFX file on your computer.</span></span> <span data-ttu-id="48434-226">這個命令匯入 hello 金鑰 Hsm hello 金鑰保存庫服務中：</span><span class="sxs-lookup"><span data-stu-id="48434-226">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


<span data-ttu-id="48434-227">hello 下一個命令會匯入 「 攜帶您自己的金鑰 」 (BYOK) 封裝。</span><span class="sxs-lookup"><span data-stu-id="48434-227">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="48434-228">此案例可讓您在您本機的 HSM 中產生您的金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的不需要離開 hello HSM 界限的 hello 金鑰：</span><span class="sxs-lookup"><span data-stu-id="48434-228">This scenario lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

<span data-ttu-id="48434-229">如需詳細說明 toogenerate 這個 BYOK 封裝，請參閱[如何為 Azure 金鑰保存庫的 toogenerate 並傳輸受 HSM 保護金鑰](key-vault-hsm-protected-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="48434-229">For more detailed instructions about how toogenerate this BYOK package, see [How toogenerate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <span data-ttu-id="48434-230"><a id="delete"></a>刪除 hello 金鑰保存庫及相關聯的金鑰和密碼</span><span class="sxs-lookup"><span data-stu-id="48434-230"><a id="delete"></a>Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="48434-231">如果您不再需要 hello 金鑰保存庫和 hello 金鑰或密碼，其中的內容，您可以刪除 hello 金鑰保存庫使用 hello[移除 AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="48434-231">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span></span>

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

<span data-ttu-id="48434-232">或者，您可以刪除整個 Azure 資源群組，其中包括 hello 金鑰保存庫和您在該群組中包含的任何其他資源：</span><span class="sxs-lookup"><span data-stu-id="48434-232">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <span data-ttu-id="48434-233"><a id="other"></a>其他 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="48434-233"><a id="other"></a>Other Azure PowerShell Cmdlets</span></span>
<span data-ttu-id="48434-234">可能有助於管理 Azure 金鑰保存庫的其他命令：</span><span class="sxs-lookup"><span data-stu-id="48434-234">Other commands that you might find useful for managing Azure Key Vault:</span></span>

* <span data-ttu-id="48434-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`此命令會取得以表格形式顯示的所有金鑰和所選屬性。</span><span class="sxs-lookup"><span data-stu-id="48434-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span></span>
* <span data-ttu-id="48434-236">`$Keys[0]`： 這個命令會顯示完整的 hello 指定索引鍵的屬性清單</span><span class="sxs-lookup"><span data-stu-id="48434-236">`$Keys[0]`: This command displays a full list of properties for hello specified key</span></span>
* <span data-ttu-id="48434-237">`Get-AzureKeyVaultSecret`此命令會列出以表格形式顯示的所有密碼名稱和所選屬性。</span><span class="sxs-lookup"><span data-stu-id="48434-237">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span></span>
* <span data-ttu-id="48434-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`： 範例如何 tooremove 特定索引鍵。</span><span class="sxs-lookup"><span data-stu-id="48434-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how tooremove a specific key.</span></span>
* <span data-ttu-id="48434-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`： 範例如何 tooremove 特定密碼。</span><span class="sxs-lookup"><span data-stu-id="48434-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how tooremove a specific secret.</span></span>

## <span data-ttu-id="48434-240"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="48434-240"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="48434-241">如需在 Web 應用程式中使用 Azure 金鑰保存庫的後續教學課程，請參閱 [從 Web 應用程式使用 Azure 金鑰保存庫](key-vault-use-from-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="48434-241">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="48434-242">toosee 如何使用金鑰保存庫，請參閱[Azure 金鑰保存庫記錄](key-vault-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="48434-242">toosee how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span></span>

<span data-ttu-id="48434-243">如需 hello Azure 金鑰保存庫的最新版 Azure PowerShell cmdlet 的清單，請參閱[Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。</span><span class="sxs-lookup"><span data-stu-id="48434-243">For a list of hello latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="48434-244">程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="48434-244">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
