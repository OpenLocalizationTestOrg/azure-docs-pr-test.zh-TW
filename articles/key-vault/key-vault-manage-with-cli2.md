---
title: "使用 CLI 管理 Azure Key Vault | Microsoft Docs"
description: "透過本教學課程，使用 CLI 2.0 來自動化 Key Vault 中的一般工作"
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
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="15edf-103">使用 CLI 2.0 管理 Key Vault</span><span class="sxs-lookup"><span data-stu-id="15edf-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="15edf-104">大部分地區均提供 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="15edf-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="15edf-105">如需詳細資訊，請參閱 [金鑰保存庫價格頁面](https://azure.microsoft.com/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="15edf-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="15edf-106">簡介</span><span class="sxs-lookup"><span data-stu-id="15edf-106">Introduction</span></span>
<span data-ttu-id="15edf-107">使用本教學課程可協助您開始使用 Azure 金鑰保存庫，進而在 Azure 中建立強化的容器 (保存庫)，以儲存及管理 Azure 中的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="15edf-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="15edf-108">本教學課程將逐步引導您使用 Azure 跨平台命令列介面，來建立一個包含金鑰或密碼的保存庫，而稍後您可以在 Azure 應用程式中使用此金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="15edf-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="15edf-109">接著，它會說明應用程式後續可以如何使用該金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="15edf-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="15edf-110">**預估完成時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="15edf-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="15edf-111">本教學課程沒有說明如何撰寫其中一個步驟所包含的 Azure 應用程式，但會示範如何授權應用程式使用金鑰保存庫中的金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="15edf-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="15edf-112">本教學課程使用最新的 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="15edf-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="15edf-113">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="15edf-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15edf-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="15edf-114">Prerequisites</span></span>
<span data-ttu-id="15edf-115">若要完成本教學課程，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="15edf-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="15edf-116">Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15edf-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="15edf-117">如果您沒有訂用帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial)。</span><span class="sxs-lookup"><span data-stu-id="15edf-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="15edf-118">命令列介面 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="15edf-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="15edf-119">若要安裝最新版本，並連線至 Azure 訂用帳戶，請參閱[安裝與設定 Azure 跨平台命令列介面 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="15edf-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="15edf-120">可設定使用您在本教學課程中所建立之金鑰或密碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="15edf-121">您可以在 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=45343)找到範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="15edf-122">如需相關指示，請參閱隨附的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="15edf-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="15edf-123">取得使用 Azure 跨平台命令列介面的說明</span><span class="sxs-lookup"><span data-stu-id="15edf-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="15edf-124">本教學課程假設您熟悉命令列介面 (Bash、終端機、命令提示字元)</span><span class="sxs-lookup"><span data-stu-id="15edf-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="15edf-125">--help 或 -h 參數可用於檢視特定命令的說明。</span><span class="sxs-lookup"><span data-stu-id="15edf-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="15edf-126">或者，您也可使用 azure help [command] [options] 格式傳回相同資訊。</span><span class="sxs-lookup"><span data-stu-id="15edf-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="15edf-127">例如，以下命令全部都會傳回相同的資訊：</span><span class="sxs-lookup"><span data-stu-id="15edf-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="15edf-128">不確定命令所需的參數時，請使用 --help、-h 或 az help [command] 來查閱說明。</span><span class="sxs-lookup"><span data-stu-id="15edf-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="15edf-129">您也可以閱讀以下教學課程，以熟悉 Azure 跨平台命令列介面中的 Azure 資源管理員：</span><span class="sxs-lookup"><span data-stu-id="15edf-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="15edf-130">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15edf-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="15edf-131">開始使用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="15edf-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="15edf-132">連線到您的訂閱</span><span class="sxs-lookup"><span data-stu-id="15edf-132">Connect to your subscriptions</span></span>
<span data-ttu-id="15edf-133">若要使用組織帳戶登入，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="15edf-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="15edf-134">或者，如果您想要以互動方式輸入來登入</span><span class="sxs-lookup"><span data-stu-id="15edf-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="15edf-135">如果您有多個訂用帳戶，並想要指定其中一個訂用帳戶供 Azure 金鑰保存庫使用，請輸入下列內容以查看您帳戶的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="15edf-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="15edf-136">接著，若要指定要使用的訂用帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="15edf-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="15edf-137">如需設定 Azure 跨平台命令列介面的詳細資訊，請參閱[安裝 Azure CLI](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="15edf-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="15edf-138">建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="15edf-138">Create a new resource group</span></span>
<span data-ttu-id="15edf-139">使用 Azure 資源管理員時，會在資源群組內建立所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="15edf-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="15edf-140">在本教學課程中，我們將建立新的資源群組 'ContosoResourceGroup'。</span><span class="sxs-lookup"><span data-stu-id="15edf-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="15edf-141">第一個參數是資源群組名稱，而第二個參數是位置。</span><span class="sxs-lookup"><span data-stu-id="15edf-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="15edf-142">請針對位置使用 `az account list-locations` 命令，以了解如何指定一個位置替代本範例中的位置。</span><span class="sxs-lookup"><span data-stu-id="15edf-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="15edf-143">如果您需要更多資訊，請輸入：`az account list-locations -h`。</span><span class="sxs-lookup"><span data-stu-id="15edf-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="15edf-144">註冊金鑰保存庫資源提供者</span><span class="sxs-lookup"><span data-stu-id="15edf-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="15edf-145">請確定已在訂用帳戶中註冊金鑰保存庫資源提供者：</span><span class="sxs-lookup"><span data-stu-id="15edf-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="15edf-146">每個訂用帳戶只需要執行這項作業一次。</span><span class="sxs-lookup"><span data-stu-id="15edf-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="15edf-147">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="15edf-147">Create a key vault</span></span>
<span data-ttu-id="15edf-148">使用 `az keyvault create` 命令來建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="15edf-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="15edf-149">這個指令碼包含三個必要參數：資源群組名稱、金鑰保存庫名稱和地理位置。</span><span class="sxs-lookup"><span data-stu-id="15edf-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="15edf-150">例如，如果使用的保存庫名稱為 ContosoKeyVault、資源群組名稱為 ContosoResourceGroup 及位置為東亞，請輸入：</span><span class="sxs-lookup"><span data-stu-id="15edf-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="15edf-151">此命令的輸出會顯示您剛剛建立的金鑰保存庫屬性。</span><span class="sxs-lookup"><span data-stu-id="15edf-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="15edf-152">兩個最重要屬性是：</span><span class="sxs-lookup"><span data-stu-id="15edf-152">The two most important properties are:</span></span>

* <span data-ttu-id="15edf-153">**name**：在此範例中，這是 ContosoKeyVault。</span><span class="sxs-lookup"><span data-stu-id="15edf-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="15edf-154">您將在其他 Key Vault 命令中使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="15edf-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="15edf-155">**vaultUri**：在此範例中，這是 https://contosokeyvault.vault.azure.net。</span><span class="sxs-lookup"><span data-stu-id="15edf-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="15edf-156">透過其 REST API 使用保存庫的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="15edf-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="15edf-157">您的 Azure 帳戶現已取得在此金鑰保存庫上執行任何作業的授權。</span><span class="sxs-lookup"><span data-stu-id="15edf-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="15edf-158">而且，沒有其他人有此授權。</span><span class="sxs-lookup"><span data-stu-id="15edf-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="15edf-159">將金鑰或密碼加入至金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="15edf-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="15edf-160">如果您想讓 Azure 金鑰保存庫為您建立一個軟體防護金鑰，請使用 `az key create` 命令，並輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="15edf-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="15edf-161">不過，如果您在 .pem 檔案中有現有金鑰，而該檔案已另存為本機檔案 (在名為 softkey.pem 的檔案中)，且您想要將該金鑰上傳至 Azure 金鑰保存庫，請輸入下列命令以從 .PEM 檔案匯入金鑰 (這樣便可透過金鑰保存庫服務中的軟體來保護金鑰)：</span><span class="sxs-lookup"><span data-stu-id="15edf-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="15edf-162">您現在可以參照您所建立或上傳至 Azure 金鑰保存庫的金鑰 (藉由使用其 URI)。</span><span class="sxs-lookup"><span data-stu-id="15edf-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="15edf-163">使用 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** 一律可取得目前的版本，而使用 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** 可取得此特定版本。</span><span class="sxs-lookup"><span data-stu-id="15edf-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="15edf-164">若要將名為 SQLPassword 且其 Azure 金鑰保存庫的值為 Pa$$w0rd 的密碼新增至保存庫，請輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="15edf-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="15edf-165">透過使用其 URI，您現在可以參照您新增至 Azure 金鑰保存庫的密碼。</span><span class="sxs-lookup"><span data-stu-id="15edf-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="15edf-166">使用 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** 一律可取得目前的版本，而使用 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** 可取得此特定版本。</span><span class="sxs-lookup"><span data-stu-id="15edf-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="15edf-167">讓我們來檢視剛剛建立的金鑰或密碼：</span><span class="sxs-lookup"><span data-stu-id="15edf-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="15edf-168">若要檢視您的金鑰，請輸入： `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="15edf-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="15edf-169">若要檢視您的祕密，請輸入： `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="15edf-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="15edf-170">向 Azure Active Directory 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="15edf-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="15edf-171">這步驟通常會由開發人員在個別電腦上完成。</span><span class="sxs-lookup"><span data-stu-id="15edf-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="15edf-172">這並非 Azure 金鑰保存庫的特有狀況，在此列出是為了讓程式完整。</span><span class="sxs-lookup"><span data-stu-id="15edf-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15edf-173">若要完成本教學課程，您的帳戶、保存庫及將在本步驟中註冊的應用程式全都必須位於相同的 Azure 目錄中。</span><span class="sxs-lookup"><span data-stu-id="15edf-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="15edf-174">使用金鑰保存庫的應用程式必須使用 Azure Active Directory 的權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="15edf-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="15edf-175">若要達到此目的，應用程式擁有者首先必須在其 Azure Active Directory 中註冊該應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="15edf-176">註冊結束時，應用程式擁有者會取得下列值：</span><span class="sxs-lookup"><span data-stu-id="15edf-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="15edf-177">**應用程式識別碼** (亦稱為用戶端識別碼) 和**驗證金鑰** (亦稱為共用密碼)。</span><span class="sxs-lookup"><span data-stu-id="15edf-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="15edf-178">應用程式必須向 Azure Active Directory 出示這兩個值才能取得權杖。</span><span class="sxs-lookup"><span data-stu-id="15edf-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="15edf-179">如何設定應用程式執行此作業會取決於應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="15edf-180">在金鑰保存庫範例應用程式中，應用程式擁有者會在 app.config 檔案中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="15edf-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="15edf-181">在 Azure Active Directory 中註冊應用程式：</span><span class="sxs-lookup"><span data-stu-id="15edf-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="15edf-182">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="15edf-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="15edf-183">按一下左側的 [Azure Active Directory]，然後選取您將要註冊應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="15edf-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="15edf-184">您必須選取您用來建立金鑰保存庫的 Azure 訂用帳戶所在的同一個目錄。</span><span class="sxs-lookup"><span data-stu-id="15edf-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="15edf-185">如果您不知道是哪個目錄，請按一下 [ **設定**]，找出建立金鑰保存庫所用的訂用帳戶，並記下最後一欄中顯示的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="15edf-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="15edf-186">按一下 [ **應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="15edf-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="15edf-187">如果您的目錄中尚未新增任何應用程式，則此頁面將僅會顯示 [ **新增應用程式** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="15edf-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="15edf-188">按一下此連結，或者您可以按一下命令列上的 [ **新增** ]。</span><span class="sxs-lookup"><span data-stu-id="15edf-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="15edf-189">在 [新增應用程式] 精靈的 [您想做什麼？] 頁面上，按一下 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="15edf-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="15edf-190">在 [告訴我們您的應用程式] 頁面上，指定您的應用程式名稱，並選取 [WEB 應用程式和/或 WEB API] (預設值)。</span><span class="sxs-lookup"><span data-stu-id="15edf-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="15edf-191">按 [下一步] 圖示。</span><span class="sxs-lookup"><span data-stu-id="15edf-191">Click the Next icon.</span></span>
6. <span data-ttu-id="15edf-192">在 [應用程式屬性] 頁面上，為您的 Web 應用程式指定 [登入 URL] 和 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="15edf-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="15edf-193">如果您的應用程式沒有這些值，您可以在此步驟中虛構這些值 (例如，您可以在這兩個方塊中指定 http://test1.contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="15edf-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="15edf-194">這些網站是否存在並沒有影響；重要的是目錄中每個應用程式的應用程式識別碼 URI 都會有所不同。</span><span class="sxs-lookup"><span data-stu-id="15edf-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="15edf-195">目錄會使用此字串來識別您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="15edf-196">按一下 [完成] 圖示以在精靈中儲存變更。</span><span class="sxs-lookup"><span data-stu-id="15edf-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="15edf-197">在 [快速入門] 頁面上，按一下 [ **設定**]。</span><span class="sxs-lookup"><span data-stu-id="15edf-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="15edf-198">捲動到 [金鑰] 區段，選取持續時間，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="15edf-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="15edf-199">頁面會重新整理，並顯示金鑰值。</span><span class="sxs-lookup"><span data-stu-id="15edf-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="15edf-200">您必須使用此金鑰值和 [用戶端識別碼] 值來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="15edf-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="15edf-201">(有關此設定的指示僅適用於特定應用程式。)</span><span class="sxs-lookup"><span data-stu-id="15edf-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="15edf-202">複製此頁面的用戶端識別碼，您將在後續步驟中使用此識別碼來設定保存庫上的權限。</span><span class="sxs-lookup"><span data-stu-id="15edf-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="15edf-203">授權應用程式使用金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="15edf-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="15edf-204">若要授權應用程式存取保存庫中的金鑰或密碼，請使用 `az keyvault set-policy` 命令。</span><span class="sxs-lookup"><span data-stu-id="15edf-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="15edf-205">例如，如果您的保存庫名稱是 ContosoKeyVault，且您要授權的應用程式具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed 的用戶端識別碼，您想要授權應用程式使用保存庫中的金鑰來進行解密並簽署，則請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="15edf-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="15edf-206">如果您想要授權該相同的應用程式讀取您保存庫中的機密資料，請執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="15edf-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="15edf-207">如果想要使用硬體安全模組 (HSM)</span><span class="sxs-lookup"><span data-stu-id="15edf-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="15edf-208">為了加強保證，您可以在硬體安全模組 (HSM) 中匯入或產生無需離開 HSM 界限的金鑰。</span><span class="sxs-lookup"><span data-stu-id="15edf-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="15edf-209">HSM 已通過 FIPS 140-2 Level 2 驗證。</span><span class="sxs-lookup"><span data-stu-id="15edf-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="15edf-210">如果此需求對您不適用，請略過本節並移至 [刪除金鑰保存庫及相關聯的金鑰和密碼](#delete-the-key-vault-and-associated-keys-and-secrets)。</span><span class="sxs-lookup"><span data-stu-id="15edf-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="15edf-211">若要建立這些受 HSM 保護的金鑰，您必須具備支援受 HSM 保護之金鑰的保存庫訂閱。</span><span class="sxs-lookup"><span data-stu-id="15edf-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="15edf-212">建立金鑰保存庫時，請新增 'sku' 參數：</span><span class="sxs-lookup"><span data-stu-id="15edf-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="15edf-213">您可以將軟體防護金鑰 (如稍早所示) 和受 HSM 保護的金鑰新增至此保存庫。</span><span class="sxs-lookup"><span data-stu-id="15edf-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="15edf-214">若要建立受 HSM 保護的金鑰，請將 [目的地] 參數設為 'HSM'：</span><span class="sxs-lookup"><span data-stu-id="15edf-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="15edf-215">您可以使用下列命令，從電腦上的 .pem 檔案匯入金鑰。</span><span class="sxs-lookup"><span data-stu-id="15edf-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="15edf-216">此命令會將金鑰匯入金鑰保存庫服務中的 HSM：</span><span class="sxs-lookup"><span data-stu-id="15edf-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="15edf-217">下一個命令會匯入「自備金鑰」(BYOK) 封包。</span><span class="sxs-lookup"><span data-stu-id="15edf-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="15edf-218">這可讓您在您的本機 HSM 中產生金鑰，且在金鑰無需離開 HSM 界限的情況下，即可將它傳輸到金鑰保存庫服務中的 HSM：</span><span class="sxs-lookup"><span data-stu-id="15edf-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="15edf-219">如需有關如何產生此 BYOK 封包的詳細指示，請參閱 [如何使用 Azure 金鑰保存庫中受 HSM 保護的金鑰](key-vault-hsm-protected-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="15edf-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="15edf-220">刪除金鑰保存庫及相關聯的金鑰和密碼</span><span class="sxs-lookup"><span data-stu-id="15edf-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="15edf-221">如果您不再需要金鑰保存庫及其所包含的金鑰或祕密，可以使用 `az keyvault delete` 命令來刪除金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="15edf-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="15edf-222">或者，您可以刪除整個 Azure 資源群組，其中包括金鑰保存庫和您加入該群組的任何其他資源：</span><span class="sxs-lookup"><span data-stu-id="15edf-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="15edf-223">其他 Azure 跨平台命令列介面命令</span><span class="sxs-lookup"><span data-stu-id="15edf-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="15edf-224">可能有助於管理 Azure 金鑰保存庫的其他命令。</span><span class="sxs-lookup"><span data-stu-id="15edf-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="15edf-225">此命令會列出以表格形式顯示的所有金鑰和所選屬性：</span><span class="sxs-lookup"><span data-stu-id="15edf-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="15edf-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="15edf-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="15edf-227">此命令會顯示指定金鑰的完整屬性清單：</span><span class="sxs-lookup"><span data-stu-id="15edf-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="15edf-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="15edf-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="15edf-229">此命令會列出以表格形式顯示的所有密碼名稱和所選屬性：</span><span class="sxs-lookup"><span data-stu-id="15edf-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="15edf-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="15edf-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="15edf-231">以下是如何移除特定金鑰的範例：</span><span class="sxs-lookup"><span data-stu-id="15edf-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="15edf-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="15edf-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="15edf-233">以下是如何移除特定密碼的範例：</span><span class="sxs-lookup"><span data-stu-id="15edf-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="15edf-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="15edf-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="15edf-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15edf-235">Next steps</span></span>
<span data-ttu-id="15edf-236">如需金鑰保存庫命令的完整 Azure CLI 參考，請參閱 [Key Vault CLI 參考](/cli/azure/keyvault)。</span><span class="sxs-lookup"><span data-stu-id="15edf-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="15edf-237">如需程式設計參考，請參閱 [Azure 金鑰保存庫開發人員指南](key-vault-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="15edf-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
