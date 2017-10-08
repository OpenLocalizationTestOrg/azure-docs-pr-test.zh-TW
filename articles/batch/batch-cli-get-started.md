---
title: "開始使用 Azure CLI 批次的 aaaGet |Microsoft 文件"
description: "快速介紹 toohello 批次命令中取得 Azure CLI 管理 Azure Batch 服務資源"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="cd22e-103">使用 Azure CLI 管理 Batch 資源</span><span class="sxs-lookup"><span data-stu-id="cd22e-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="cd22e-104">hello Azure CLI 2.0 是 Azure 的新命令列的體驗來管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="cd22e-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="cd22e-105">它可以用於 macOS、Linux 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="cd22e-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="cd22e-106">Azure CLI 2.0 最適合用於與 hello 命令列管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="cd22e-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="cd22e-107">您可以使用 hello Azure CLI toomanage，您的 Azure Batch 帳戶與 toomanage 資源集區、 工作和工作等。</span><span class="sxs-lookup"><span data-stu-id="cd22e-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="cd22e-108">以 hello Azure CLI，您可以編寫指令碼的 hello 許多相同的工作，當您執行與 hello 批次應用程式開發介面、 Azure 入口網站和批次的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cd22e-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="cd22e-109">本文概述如何使用搭配 [Azure CLI 2.0 版](https://docs.microsoft.com/cli/azure/overview) 與 Batch。</span><span class="sxs-lookup"><span data-stu-id="cd22e-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="cd22e-110">請參閱[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)搭配 Azure 使用 hello CLI 的概觀。</span><span class="sxs-lookup"><span data-stu-id="cd22e-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="cd22e-111">Microsoft 建議使用的 hello Azure CLI 2.0 版的 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="cd22e-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="cd22e-112">如需 2.0 版的詳細資訊，請參閱 [Azure Command Line 2.0 現已正式上市](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="cd22e-113">Hello Azure CLI 設定</span><span class="sxs-lookup"><span data-stu-id="cd22e-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="cd22e-114">tooinstall hello Azure CLI，請依照下列所述的 hello 步驟[安裝 hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="cd22e-115">我們建議您更新您的 Azure CLI 安裝經常 tootake 的服務更新和增強功能的優點。</span><span class="sxs-lookup"><span data-stu-id="cd22e-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="cd22e-116">命令說明</span><span class="sxs-lookup"><span data-stu-id="cd22e-116">Command help</span></span>

<span data-ttu-id="cd22e-117">您可以在 hello Azure CLI 中顯示每個命令的說明文字，藉由附加`-h`toohello 命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="cd22e-118">略過任何其他選項。</span><span class="sxs-lookup"><span data-stu-id="cd22e-118">Omit any other options.</span></span> <span data-ttu-id="cd22e-119">例如：</span><span class="sxs-lookup"><span data-stu-id="cd22e-119">For example:</span></span>

* <span data-ttu-id="cd22e-120">hello tooget 說明`az`命令中，輸入：`az -h`</span><span class="sxs-lookup"><span data-stu-id="cd22e-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="cd22e-121">使用 tooget hello CLI 中的所有批次命令的清單：`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="cd22e-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="cd22e-122">tooget 說明建立批次帳戶，請輸入：`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="cd22e-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="cd22e-123">有疑問，請使用 hello`-h`任何 Azure CLI 命令的命令列選項 tooget 說明。</span><span class="sxs-lookup"><span data-stu-id="cd22e-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="cd22e-124">舊版的 hello 使用 Azure CLI `azure` toopreface CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="cd22e-125">在 2.0 版中，所有命令的前面現在都會加上 `az`。</span><span class="sxs-lookup"><span data-stu-id="cd22e-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="cd22e-126">為確定 tooupdate 您指令碼 toouse hello 新語法與 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="cd22e-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="cd22e-127">此外，參考 toohello Azure CLI 參考文件，如需詳細資訊，關於[Azure CLI 命令的批次](https://docs.microsoft.com/cli/azure/batch)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="cd22e-128">登入和驗證</span><span class="sxs-lookup"><span data-stu-id="cd22e-128">Log in and authenticate</span></span>

<span data-ttu-id="cd22e-129">toouse hello Azure CLI 批次，需要在 toolog 和驗證。</span><span class="sxs-lookup"><span data-stu-id="cd22e-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="cd22e-130">有兩個簡單步驟 toofollow:</span><span class="sxs-lookup"><span data-stu-id="cd22e-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="cd22e-131">**登入 Azure。**</span><span class="sxs-lookup"><span data-stu-id="cd22e-131">**Log into Azure.**</span></span> <span data-ttu-id="cd22e-132">登入 Azure 可讓您存取 tooAzure 資源管理員命令，包括[批次管理服務](batch-management-dotnet.md)命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="cd22e-133">**登入您的 Batch 帳戶。**</span><span class="sxs-lookup"><span data-stu-id="cd22e-133">**Log into your Batch account.**</span></span> <span data-ttu-id="cd22e-134">您登入您的批次帳戶可讓存取 tooBatch 服務命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="cd22e-135">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="cd22e-135">Log in tooAzure</span></span>

<span data-ttu-id="cd22e-136">有幾個不同的方式 toolog 至 Azure 中有詳細, 說明[登入 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="cd22e-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="cd22e-137">[以互動方式登入](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="cd22e-138">登入以互動方式執行時 Azure CLI 命令自行從 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="cd22e-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="cd22e-139">[使用服務主體來登入](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="cd22e-140">當您從指令碼或應用程式執行 Azure CLI 命令時，使用服務主體來登入。</span><span class="sxs-lookup"><span data-stu-id="cd22e-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="cd22e-141">Hello 本文的目的，我們會顯示如何 toolog 至 Azure 以互動方式。</span><span class="sxs-lookup"><span data-stu-id="cd22e-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="cd22e-142">型別[az 登入](https://docs.microsoft.com/cli/azure/#login)hello 命令列上：</span><span class="sxs-lookup"><span data-stu-id="cd22e-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="cd22e-143">hello`az login`命令傳回，如下所示，您可以使用 tooauthenticate，語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cd22e-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="cd22e-144">請依照 hello 所提供的指示 tooopen 網頁，並送出 hello 語彙基元 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="cd22e-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![登入 tooAzure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="cd22e-146">列出 hello hello 範例[範例殼層指令碼](#sample-shell-scripts)區段也顯示如何 toostart 您的 Azure CLI 工作階段，以互動方式登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="cd22e-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="cd22e-147">一旦您登入，您可以呼叫命令 toowork 批次管理資源，包括批次帳戶、 金鑰、 應用程式封裝，以及配額。</span><span class="sxs-lookup"><span data-stu-id="cd22e-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="cd22e-148">登入 tooyour 批次帳戶</span><span class="sxs-lookup"><span data-stu-id="cd22e-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="cd22e-149">toouse hello Azure CLI toomanage 批次資源，例如集區、 工作和工作，您需要 toolog 到您的 Batch 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cd22e-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="cd22e-150">toolog toohello 批次服務中的使用 hello [az 批次帳戶登入](https://docs.microsoft.com/cli/azure/batch/account#login)命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="cd22e-151">您有兩個對 Batch 帳戶進行驗證的選項︰</span><span class="sxs-lookup"><span data-stu-id="cd22e-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="cd22e-152">**使用 Azure Active Directory (Azure AD) 驗證。**</span><span class="sxs-lookup"><span data-stu-id="cd22e-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="cd22e-153">向 Azure AD 是 hello 預設值，當您使用 Azure CLI hello 與批次，並在大部分情況下建議使用。</span><span class="sxs-lookup"><span data-stu-id="cd22e-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="cd22e-154">當您登入 tooAzure，以互動方式 hello 上一節中所述時，您的認證會快取，因此 hello Azure CLI 可以讓您登入 tooyour 批次帳戶使用這些相同的認證。</span><span class="sxs-lookup"><span data-stu-id="cd22e-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="cd22e-155">如果您登入使用服務主體的 tooAzure，這些認證也會使用的 toolog tooyour 批次帳戶中。</span><span class="sxs-lookup"><span data-stu-id="cd22e-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="cd22e-156">Azure AD 的優點就是它會提供角色型存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="cd22e-157">使用 RBAC，使用者的存取權視其指派的角色，而不是他們擁有 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd22e-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="cd22e-158">您可以管理 RBAC 角色，並且讓 Azure AD 處理存取和驗證，而不用管理帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd22e-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="cd22e-159">使用 Azure AD 進行驗證時需要您建立您的 Azure 批次帳戶的集區配置模式下設定 too'User 訂用帳戶 '。</span><span class="sxs-lookup"><span data-stu-id="cd22e-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="cd22e-160">toolog tooyour 批次中的使用 Azure AD 的帳戶，請呼叫 hello [az 批次帳戶登入](https://docs.microsoft.com/cli/azure/batch/account#login)命令：</span><span class="sxs-lookup"><span data-stu-id="cd22e-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="cd22e-161">**使用共用金鑰驗證。**</span><span class="sxs-lookup"><span data-stu-id="cd22e-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="cd22e-162">[共用的金鑰驗證](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key)的批次服務會使用您的帳戶存取金鑰 hello tooauthenticate Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="cd22e-163">如果您正在建立 Azure CLI 指令碼 tooautomate 呼叫的批次命令，您可以使用共用金鑰驗證或 Azure AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="cd22e-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="cd22e-164">在某些情況下，使用共用金鑰驗證可能會比建立服務主體簡單。</span><span class="sxs-lookup"><span data-stu-id="cd22e-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="cd22e-165">在使用共用金鑰驗證 toolog 包含 hello `--shared-key-auth` hello 命令列選項：</span><span class="sxs-lookup"><span data-stu-id="cd22e-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="cd22e-166">列出 hello hello 範例[範例殼層指令碼](#sample-shell-scripts)一節說明如何 toolog 到您的 Batch 帳戶與 hello Azure CLI 兩者都使用 Azure AD 和共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd22e-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="cd22e-167">使用 Azure Batch CLI 範本和檔案傳輸 (預覽)</span><span class="sxs-lookup"><span data-stu-id="cd22e-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="cd22e-168">您可以使用 hello Azure CLI toorun 批次作業端對端，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd22e-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="cd22e-169">批次範本檔案支援建立集區、 工作和工作以 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="cd22e-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="cd22e-170">您也可以使用 hello Azure CLI tooupload 作業輸入的檔 toohello hello 與相關聯的 Azure 儲存體帳戶的批次帳戶，並下載作業輸出檔。</span><span class="sxs-lookup"><span data-stu-id="cd22e-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="cd22e-171">如需詳細資訊，請參閱[使用 Azure Batch CLI 範本和檔案傳輸 (預覽)](batch-cli-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="cd22e-172">範例 shell 指令碼</span><span class="sxs-lookup"><span data-stu-id="cd22e-172">Sample shell scripts</span></span>

<span data-ttu-id="cd22e-173">hello 範例指令碼列出下列表格顯示 hello toouse Azure CLI 命令搭配 hello 批次服務和批次管理服務 tooaccomplish 一般工作的方式。</span><span class="sxs-lookup"><span data-stu-id="cd22e-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="cd22e-174">這些範例指令碼，涵蓋許多 hello Azure CLI 批次中可用的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="cd22e-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="cd22e-175">指令碼</span><span class="sxs-lookup"><span data-stu-id="cd22e-175">Script</span></span> | <span data-ttu-id="cd22e-176">注意事項</span><span class="sxs-lookup"><span data-stu-id="cd22e-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cd22e-177">建立 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="cd22e-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="cd22e-178">建立 Batch 帳戶並將它與儲存體帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cd22e-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="cd22e-179">新增應用程式</span><span class="sxs-lookup"><span data-stu-id="cd22e-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="cd22e-180">新增應用程式，並上傳封裝的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="cd22e-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="cd22e-181">管理 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="cd22e-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="cd22e-182">示範建立、調整大小和管理集區。</span><span class="sxs-lookup"><span data-stu-id="cd22e-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="cd22e-183">使用 Batch 執行工作和作業</span><span class="sxs-lookup"><span data-stu-id="cd22e-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="cd22e-184">示範執行工作及新增作業。</span><span class="sxs-lookup"><span data-stu-id="cd22e-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="cd22e-185">用於建立資源的 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="cd22e-185">JSON files for resource creation</span></span>

<span data-ttu-id="cd22e-186">當您建立批次資源，例如集區和工作時，您可以指定包含 hello 新資源的設定，而不是它的參數傳遞做為命令列選項在 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="cd22e-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="cd22e-187">例如：</span><span class="sxs-lookup"><span data-stu-id="cd22e-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="cd22e-188">雖然您可以建立最多使用只有命令列選項的批次資源，某些功能需要您指定 JSON 格式的檔案，其中包含 hello 資源詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cd22e-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="cd22e-189">例如，您必須使用 JSON 檔案，如果您想要啟動工作的 toospecify 資源檔案。</span><span class="sxs-lookup"><span data-stu-id="cd22e-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="cd22e-190">toosee hello JSON 語法需 toocreate 資源，請參閱 toohello[批次 REST API 參考][ rest_api]文件。</span><span class="sxs-lookup"><span data-stu-id="cd22e-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="cd22e-191">每個 「 新增*資源類型*"hello REST API 參考資料中的主題包含範例 JSON 指令碼來建立該資源。</span><span class="sxs-lookup"><span data-stu-id="cd22e-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="cd22e-192">您可以使用這些範例 JSON 指令碼做為範本，如 JSON 檔案 toouse 以 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="cd22e-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="cd22e-193">例如，toosee hello 集區建立的 JSON 語法，請參閱太[加入集區 tooan 帳戶][rest_add_pool]。</span><span class="sxs-lookup"><span data-stu-id="cd22e-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="cd22e-194">如需可指定 JSON 檔案的範例指令碼，請參閱[使用 Batch 執行作業和工作](./scripts/batch-cli-sample-run-job.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cd22e-195">如果當您建立的資源，您會指定 JSON 檔案，則會忽略您在該資源的 hello 命令列指定的任何其他參數。</span><span class="sxs-lookup"><span data-stu-id="cd22e-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="cd22e-196">有效率的 Batch 資源查詢</span><span class="sxs-lookup"><span data-stu-id="cd22e-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="cd22e-197">每個 Batch 資源類型都支援 `list` 命令，已查詢 Batch 帳戶並列出該類型的資源。</span><span class="sxs-lookup"><span data-stu-id="cd22e-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="cd22e-198">例如，您可以列出 hello 集區中您的帳戶和 hello 工作中的工作：</span><span class="sxs-lookup"><span data-stu-id="cd22e-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="cd22e-199">當您查詢與 hello 批次服務`list`作業，您可以指定 OData 子句 toolimit hello 傳回的資料量。</span><span class="sxs-lookup"><span data-stu-id="cd22e-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="cd22e-200">因為所有的篩選發生伺服器端，所以只會 hello 您要求的資料不符合 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="cd22e-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="cd22e-201">使用這些子句 toosave 頻寬 （並因此時間） 當您執行的作業清單。</span><span class="sxs-lookup"><span data-stu-id="cd22e-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="cd22e-202">hello 下表描述支援的 hello 批次服務的 hello OData 子句：</span><span class="sxs-lookup"><span data-stu-id="cd22e-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="cd22e-203">子句</span><span class="sxs-lookup"><span data-stu-id="cd22e-203">Clause</span></span> | <span data-ttu-id="cd22e-204">說明</span><span class="sxs-lookup"><span data-stu-id="cd22e-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="cd22e-205">傳回每個實體的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="cd22e-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="cd22e-206">傳回符合 hello 的唯一實體指定的 OData 運算式。</span><span class="sxs-lookup"><span data-stu-id="cd22e-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="cd22e-207">取得基礎的單一 REST 呼叫中的 hello 實體資訊。</span><span class="sxs-lookup"><span data-stu-id="cd22e-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="cd22e-208">hello expand 的子句目前支援僅 hello`stats`屬性。</span><span class="sxs-lookup"><span data-stu-id="cd22e-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="cd22e-209">如需範例指令碼如何 toouse OData 子句中，請參閱該顯示[與批次執行工作和工作](./scripts/batch-cli-sample-run-job.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="cd22e-210">如需有關如何執行有效率的清單以 OData 子句的查詢的詳細資訊，請參閱[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="cd22e-211">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="cd22e-211">Troubleshooting tips</span></span>

<span data-ttu-id="cd22e-212">hello 下列秘訣可以協助您疑難排解 Azure CLI 問題時：</span><span class="sxs-lookup"><span data-stu-id="cd22e-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="cd22e-213">使用`-h`tooget**說明文字**任何 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="cd22e-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="cd22e-214">使用`-v`和`-vv`toodisplay **verbose**命令輸出。</span><span class="sxs-lookup"><span data-stu-id="cd22e-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="cd22e-215">當 hello`-vv`旗標之後，hello Azure CLI 顯示 hello 實際 REST 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="cd22e-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="cd22e-216">這些參數方便用於顯示完整的錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="cd22e-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="cd22e-217">您可以檢視**命令為 JSON 輸出**以 hello`--json`選項。</span><span class="sxs-lookup"><span data-stu-id="cd22e-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="cd22e-218">例如， `az batch pool show pool001 --json` 會以 JSON 格式顯示 pool001 的屬性。</span><span class="sxs-lookup"><span data-stu-id="cd22e-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="cd22e-219">您可以複製並修改在此輸出 toouse `--json-file` (請參閱[JSON 檔案](#json-files)稍早在本文章)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="cd22e-220">hello [Batch 論壇][ batch_forum]監視的批次小組成員。</span><span class="sxs-lookup"><span data-stu-id="cd22e-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="cd22e-221">如果您遇到問題或需要特定作業的協助，您可以在此張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="cd22e-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd22e-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd22e-222">Next steps</span></span>

* <span data-ttu-id="cd22e-223">如需 hello Azure CLI 的詳細資訊，請參閱 hello [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="cd22e-224">如需 Batch 資源的詳細資訊，請參閱[適用於開發人員的 Azure Batch 概觀](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="cd22e-225">如需使用批次範本 toocreate 集區、 工作和工作，而不需要撰寫程式碼的詳細資訊，請參閱[使用 Azure 批次 CLI 範本和檔案傳輸 （預覽）](batch-cli-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="cd22e-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
