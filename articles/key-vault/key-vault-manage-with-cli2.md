---
title: "Azure 金鑰保存庫使用 CLI aaaManage |Microsoft 文件"
description: "透過 hello CLI 2.0 使用金鑰保存庫中的這個教學課程 tooautomate 一般工作"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="20fae-103">使用 CLI 2.0 管理 Key Vault</span><span class="sxs-lookup"><span data-stu-id="20fae-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="20fae-104">大部分地區均提供 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="20fae-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="20fae-105">如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="20fae-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="20fae-106">簡介</span><span class="sxs-lookup"><span data-stu-id="20fae-106">Introduction</span></span>
<span data-ttu-id="20fae-107">使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器 （保存庫） 在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。</span><span class="sxs-lookup"><span data-stu-id="20fae-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="20fae-108">它會引導您透過使用 Azure 跨平台命令列介面 toocreate hello 程序包含金鑰或密碼，您可以使用 Azure 應用程式的保存庫。</span><span class="sxs-lookup"><span data-stu-id="20fae-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="20fae-109">接著，它會說明應用程式後續可以如何使用該金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="20fae-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="20fae-110">**估計時間 toocomplete:** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="20fae-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="20fae-111">本教學課程不包括指示 toowrite hello Azure 應用程式的其中一個 hello 步驟包含時，會顯示如何 tooauthorize 應用程式 toouse 索引鍵或 hello 機碼中的密碼保存庫的方式。</span><span class="sxs-lookup"><span data-stu-id="20fae-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="20fae-112">這個教學課程使用 hello 最新的 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="20fae-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="20fae-113">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="20fae-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20fae-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="20fae-114">Prerequisites</span></span>
<span data-ttu-id="20fae-115">toocomplete 本教學課程中，您必須擁有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="20fae-116">訂用帳戶 tooMicrosoft Azure。</span><span class="sxs-lookup"><span data-stu-id="20fae-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="20fae-117">如果您沒有訂用帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="20fae-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="20fae-118">命令列介面 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="20fae-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="20fae-119">tooinstall hello 最新版本，並連接 tooyour Azure 訂用帳戶，請參閱[安裝及設定 Azure 跨平台命令列介面 2.0 hello](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="20fae-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="20fae-120">將會設定的 toouse hello 金鑰或密碼，您在本教學課程中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="20fae-121">範例應用程式是可從 hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343)。</span><span class="sxs-lookup"><span data-stu-id="20fae-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="20fae-122">如需指示，請參閱 hello 隨附的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="20fae-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="20fae-123">取得使用 Azure 跨平台命令列介面的說明</span><span class="sxs-lookup"><span data-stu-id="20fae-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="20fae-124">本教學課程假設您熟悉 hello 命令列介面 （Bash，終端機，命令提示字元）</span><span class="sxs-lookup"><span data-stu-id="20fae-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="20fae-125">hello-說明或-h 參數可以是 tooview 說明用於特定的命令。</span><span class="sxs-lookup"><span data-stu-id="20fae-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="20fae-126">或者，azure 的 hello 說明 [命令] [選項] 格式也可以使用的 tooreturn hello 相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="20fae-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="20fae-127">比方說，hello 下列命令傳回所有 hello 相同的資訊：</span><span class="sxs-lookup"><span data-stu-id="20fae-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="20fae-128">關於 hello 參數所需的命令有疑問，請參閱使用 toohelp-說明、-h 或 az 說明 [命令]。</span><span class="sxs-lookup"><span data-stu-id="20fae-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="20fae-129">您也可以閱讀下列教學課程 tooget 熟悉使用 Azure Resource Manager Azure 跨平台命令列介面中的 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="20fae-130">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20fae-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="20fae-131">開始使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="20fae-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="20fae-132">連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20fae-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="20fae-133">在使用組織帳戶，下列命令使用 hello toolog:</span><span class="sxs-lookup"><span data-stu-id="20fae-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="20fae-134">或如果您希望 toolog 以互動方式輸入</span><span class="sxs-lookup"><span data-stu-id="20fae-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="20fae-135">如果您有多個訂用帳戶，並想 toospecify 特定一個 toouse for Azure Key Vault，輸入下列帳戶 toosee hello 訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="20fae-136">然後，toospecify hello 訂用帳戶 toouse，類型：</span><span class="sxs-lookup"><span data-stu-id="20fae-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="20fae-137">如需設定 Azure 跨平台命令列介面的詳細資訊，請參閱[安裝 Azure CLI](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="20fae-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="20fae-138">建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="20fae-138">Create a new resource group</span></span>
<span data-ttu-id="20fae-139">使用 Azure 資源管理員時，會在資源群組內建立所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="20fae-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="20fae-140">在本教學課程中，我們將建立新的資源群組 'ContosoResourceGroup'。</span><span class="sxs-lookup"><span data-stu-id="20fae-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="20fae-141">hello 第一個參數是資源群組名稱，且 hello 第二個參數是 hello 的位置。</span><span class="sxs-lookup"><span data-stu-id="20fae-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="20fae-142">位置，請使用 hello 命令`az account list-locations`tooidentify 如何 toospecify 替代位置 toohello 其中一個在此範例中。</span><span class="sxs-lookup"><span data-stu-id="20fae-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="20fae-143">如果您需要更多資訊，請輸入：`az account list-locations -h`。</span><span class="sxs-lookup"><span data-stu-id="20fae-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="20fae-144">註冊 hello 金鑰保存庫資源提供者</span><span class="sxs-lookup"><span data-stu-id="20fae-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="20fae-145">請確定已在訂用帳戶中註冊金鑰保存庫資源提供者：</span><span class="sxs-lookup"><span data-stu-id="20fae-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="20fae-146">這個動作只需要執行一次，每個訂閱的 toobe。</span><span class="sxs-lookup"><span data-stu-id="20fae-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="20fae-147">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="20fae-147">Create a key vault</span></span>
<span data-ttu-id="20fae-148">使用 hello`az keyvault create`命令 toocreate 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="20fae-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="20fae-149">此指令碼有三個必要參數： 資源群組名稱、 金鑰保存庫名稱和 hello 地理位置。</span><span class="sxs-lookup"><span data-stu-id="20fae-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="20fae-150">例如，如果您使用 ContosoKeyVault ContosoResourceGroup，hello 資源群組名稱和東亞、 hello 位置 hello 保存庫名稱輸入：</span><span class="sxs-lookup"><span data-stu-id="20fae-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="20fae-151">hello 輸出此命令會顯示您剛才建立的 hello 金鑰保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="20fae-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="20fae-152">hello 兩個最重要的屬性包括：</span><span class="sxs-lookup"><span data-stu-id="20fae-152">hello two most important properties are:</span></span>

* <span data-ttu-id="20fae-153">**名稱**: hello 範例中，這是 ContosoKeyVault。</span><span class="sxs-lookup"><span data-stu-id="20fae-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="20fae-154">您將在其他 Key Vault 命令中使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="20fae-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="20fae-155">**vaultUri**: hello 範例中，這是 https://contosokeyvault.vault.azure.net。</span><span class="sxs-lookup"><span data-stu-id="20fae-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="20fae-156">透過其 REST API 使用保存庫的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="20fae-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="20fae-157">現在已授權的 tooperform 保存庫上此金鑰的任何作業，就會是您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="20fae-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="20fae-158">而且，沒有其他人有此授權。</span><span class="sxs-lookup"><span data-stu-id="20fae-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="20fae-159">新增金鑰或密碼 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="20fae-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="20fae-160">如果您想為您的 Azure 金鑰保存庫 toocreate 受軟體保護的金鑰，請使用 hello`az key create`命令，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="20fae-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="20fae-161">不過，如果您有現有的索引鍵.pem 檔案，以本機檔案儲存在名為 softkey.pem 想 tooupload tooAzure 金鑰保存庫的檔案中，輸入 hello hello 中的下列 tooimport hello 索引鍵。PEM 檔案，它會透過 hello 金鑰保存庫服務中的軟體保護金鑰 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="20fae-162">您現在可以參考 hello 金鑰，您建立或上傳 tooAzure 金鑰保存庫中，使用它的 URI。</span><span class="sxs-lookup"><span data-stu-id="20fae-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="20fae-163">使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways 取得 hello 目前的版本，並使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget 這個特定的版本。</span><span class="sxs-lookup"><span data-stu-id="20fae-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="20fae-164">tooadd 秘密 toohello 保存庫，這是名為 SQLPassword 密碼，並且 hello 值的 Pa$ $w0rd tooAzure 金鑰保存庫中，下列類型 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="20fae-165">您現在可以參考您藉由使用其 URI 新增 tooAzure 金鑰保存庫，此密碼。</span><span class="sxs-lookup"><span data-stu-id="20fae-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="20fae-166">使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways 取得 hello 目前的版本，並使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget 這個特定的版本。</span><span class="sxs-lookup"><span data-stu-id="20fae-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="20fae-167">讓我們來檢視 hello 金鑰或您剛才建立的密碼：</span><span class="sxs-lookup"><span data-stu-id="20fae-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="20fae-168">tooview 您索引鍵，類型：`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="20fae-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="20fae-169">tooview 秘密，型別：`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="20fae-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="20fae-170">向 Azure Active Directory 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="20fae-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="20fae-171">這步驟通常會由開發人員在個別電腦上完成。</span><span class="sxs-lookup"><span data-stu-id="20fae-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="20fae-172">它不是特定 tooAzure 金鑰保存庫，但隨附在這裡，以求完整。</span><span class="sxs-lookup"><span data-stu-id="20fae-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20fae-173">toocomplete hello 教學課程，您的帳戶、 hello 保存庫和您要登錄在此步驟中的 hello 應用程式都必須在 hello 相同的 Azure 目錄。</span><span class="sxs-lookup"><span data-stu-id="20fae-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="20fae-174">使用金鑰保存庫的應用程式必須使用 Azure Active Directory 的權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="20fae-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="20fae-175">toodo，hello hello 應用程式的擁有者必須先註冊他們的 Azure Active Directory 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="20fae-176">在 hello 註冊結尾，hello 應用程式擁有者取得 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="20fae-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="20fae-177">**應用程式識別碼**(也稱為用戶端 ID) 和**驗證金鑰**（也稱為 hello 共用的密碼）。</span><span class="sxs-lookup"><span data-stu-id="20fae-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="20fae-178">hello 應用程式必須提供這兩個這些值 tooAzure Active Directory，tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="20fae-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="20fae-179">Hello 應用程式的方式設定的 toodo 這取決於 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="20fae-180">Hello 金鑰保存庫的範例應用程式，hello 應用程式擁有者，請 hello app.config 檔案中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="20fae-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="20fae-181">在 Azure Active Directory tooregister hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="20fae-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="20fae-182">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="20fae-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="20fae-183">Hello 左側，按一下  **Azure Active Directory**，然後選取您要在其中登錄您的應用程式的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="20fae-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="20fae-184">您必須選取 hello 含有相同目錄 hello 您用來建立金鑰保存庫的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20fae-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="20fae-185">如果您不知道哪個目錄這是，按一下 **設定**，識別 hello 訂閱您用來建立金鑰保存庫，並注意 hello hello 目錄名稱顯示 hello 最後一個資料行。</span><span class="sxs-lookup"><span data-stu-id="20fae-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="20fae-186">按一下 [ **應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="20fae-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="20fae-187">如果沒有任何應用程式已加入 tooyour 目錄，此頁面會顯示只有 hello**新增應用程式**連結。</span><span class="sxs-lookup"><span data-stu-id="20fae-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="20fae-188">按一下 [hello] 連結，或或者，您可以按一下 hello**新增**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="20fae-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="20fae-189">在 hello**新增應用程式**精靈，在 hello**您該怎麼想 toodo？**頁面上，按一下**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="20fae-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="20fae-190">在 hello**告訴我們您的應用程式**頁面上，指定您的應用程式的名稱，然後選取**WEB 應用程式和/或 WEB API** (hello 預設值)。</span><span class="sxs-lookup"><span data-stu-id="20fae-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="20fae-191">按一下 [下一步 hello] 圖示。</span><span class="sxs-lookup"><span data-stu-id="20fae-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="20fae-192">在 hello**應用程式屬性**頁面上，指定 hello**登入 URL**和**應用程式識別碼 URI** web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="20fae-193">如果您的應用程式沒有這些值，您可以在此步驟中虛構這些值 (例如，您可以在這兩個方塊中指定 http://test1.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="20fae-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="20fae-194">並不重要如果存在這些站台。重要的是每個應用程式的 hello 應用程式識別碼 URI 是不同的目錄中的每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="20fae-195">hello 目錄會使用此字串 tooidentify 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fae-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="20fae-196">按一下 hello 完成圖示 toosave hello 精靈中的變更。</span><span class="sxs-lookup"><span data-stu-id="20fae-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="20fae-197">在 hello 快速入門 頁面上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="20fae-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="20fae-198">捲動 toohello**金鑰**區段中選取 hello 持續時間，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="20fae-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="20fae-199">hello 頁面重新整理，而且現在會顯示金鑰值。</span><span class="sxs-lookup"><span data-stu-id="20fae-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="20fae-200">您必須設定您的應用程式具有此機碼值與 hello**用戶端識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="20fae-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="20fae-201">(有關此設定的指示僅適用於特定應用程式。)</span><span class="sxs-lookup"><span data-stu-id="20fae-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="20fae-202">複製此頁面上，您會在您的保存庫使用 hello 下一個步驟 tooset 權限中的 hello 用戶端識別碼值。</span><span class="sxs-lookup"><span data-stu-id="20fae-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="20fae-203">授權 hello 應用程式 toouse hello 金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="20fae-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="20fae-204">tooauthorize hello 應用程式 tooaccess hello 金鑰或密碼在 hello 保存庫使用 hello`az keyvault set-policy`命令。</span><span class="sxs-lookup"><span data-stu-id="20fae-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="20fae-205">例如，如果您想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed，用戶端識別碼，而且您想 tooauthorize hello 應用程式 toodecrypt 並登入具有索引鍵在您的保存庫中的 ContosoKeyVault 和 hello 應用程式保存庫名稱，然後執行 hello下列：</span><span class="sxs-lookup"><span data-stu-id="20fae-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="20fae-206">如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="20fae-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="20fae-207">如果您想 toouse 硬體安全性模組 (HSM)</span><span class="sxs-lookup"><span data-stu-id="20fae-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="20fae-208">為求保險，您可以匯入，或在硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="20fae-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="20fae-209">hello Hsm 是的 FIPS 140-2 Level 2 驗證。</span><span class="sxs-lookup"><span data-stu-id="20fae-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="20fae-210">如果這項需求不適 tooyou，略過本節並移太[刪除 hello 金鑰保存庫及相關聯的金鑰和秘密](#delete-the-key-vault-and-associated-keys-and-secrets)。</span><span class="sxs-lookup"><span data-stu-id="20fae-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="20fae-211">toocreate 這些受 HSM 保護的金鑰，您必須擁有支援 HSM 保護的金鑰保存庫訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20fae-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="20fae-212">當您建立 hello keyvault 時，加入 hello 'sku' 參數：</span><span class="sxs-lookup"><span data-stu-id="20fae-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="20fae-213">您可以將軟體保護的金鑰 （如稍早所示） 和 toothis 受 HSM 保護的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="20fae-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="20fae-214">toocreate HSM 保護的金鑰組 hello 目的地參數 too'HSM':</span><span class="sxs-lookup"><span data-stu-id="20fae-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="20fae-215">您可以使用 hello.pem 檔案，儲存在電腦中的下列命令 tooimport 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="20fae-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="20fae-216">這個命令匯入 hello 金鑰 Hsm hello 金鑰保存庫服務中：</span><span class="sxs-lookup"><span data-stu-id="20fae-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="20fae-217">hello 下一個命令會匯入 「 攜帶您自己的金鑰 」 (BYOK) 封裝。</span><span class="sxs-lookup"><span data-stu-id="20fae-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="20fae-218">這可讓您在您本機的 HSM 中產生您的金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的不需要離開 hello HSM 界限的 hello 金鑰：</span><span class="sxs-lookup"><span data-stu-id="20fae-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="20fae-219">如需詳細說明 toogenerate 這個 BYOK 封裝，請參閱[如何 toouse HSM-Protected 索引鍵，使用 Azure Key Vault](key-vault-hsm-protected-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="20fae-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="20fae-220">刪除 hello 金鑰保存庫及相關聯的金鑰和密碼</span><span class="sxs-lookup"><span data-stu-id="20fae-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="20fae-221">如果您不再需要 hello 金鑰保存庫和 hello 金鑰或密碼，其中的內容，您可以刪除 hello 金鑰保存庫使用 hello`az keyvault delete`命令：</span><span class="sxs-lookup"><span data-stu-id="20fae-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="20fae-222">或者，您可以刪除整個 Azure 資源群組，其中包括 hello 金鑰保存庫和您在該群組中包含的任何其他資源：</span><span class="sxs-lookup"><span data-stu-id="20fae-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="20fae-223">其他 Azure 跨平台命令列介面命令</span><span class="sxs-lookup"><span data-stu-id="20fae-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="20fae-224">可能有助於管理 Azure 金鑰保存庫的其他命令。</span><span class="sxs-lookup"><span data-stu-id="20fae-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="20fae-225">此命令會列出以表格形式顯示的所有金鑰和所選屬性：</span><span class="sxs-lookup"><span data-stu-id="20fae-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="20fae-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="20fae-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="20fae-227">此命令會顯示 hello 指定索引鍵屬性的完整清單：</span><span class="sxs-lookup"><span data-stu-id="20fae-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="20fae-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="20fae-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="20fae-229">此命令會列出以表格形式顯示的所有密碼名稱和所選屬性：</span><span class="sxs-lookup"><span data-stu-id="20fae-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="20fae-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="20fae-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="20fae-231">以下是如何的範例 tooremove 特定索引鍵：</span><span class="sxs-lookup"><span data-stu-id="20fae-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="20fae-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="20fae-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="20fae-233">以下是如何的範例 tooremove 特定密碼：</span><span class="sxs-lookup"><span data-stu-id="20fae-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="20fae-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="20fae-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="20fae-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20fae-235">Next steps</span></span>
<span data-ttu-id="20fae-236">如需金鑰保存庫命令的完整 Azure CLI 參考，請參閱 [Key Vault CLI 參考](/cli/azure/keyvault)。</span><span class="sxs-lookup"><span data-stu-id="20fae-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="20fae-237">程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="20fae-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
