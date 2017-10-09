---
title: "在從 hello CLI tooAzure aaaLog |Microsoft 文件"
description: "從 hello Azure 命令列介面 (Azure CLI) 連接 tooyour Azure 訂用帳戶，如 Mac、 Linux 及 Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a><span data-ttu-id="201b4-103">登入從 hello Azure CLI tooAzure</span><span class="sxs-lookup"><span data-stu-id="201b4-103">Log in tooAzure from hello Azure CLI</span></span>
<span data-ttu-id="201b4-104">hello Azure CLI 是一組的開放原始碼、 跨平台的命令，以使用 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="201b4-104">hello Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="201b4-105">本文說明 hello 不同的方式 tooprovide 您的 Azure 帳戶認證 tooconnect hello Azure CLI tooyour Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="201b4-105">This article describes hello different ways tooprovide your Azure account credentials tooconnect hello Azure CLI tooyour Azure subscription:</span></span>

* <span data-ttu-id="201b4-106">執行 hello `azure login` CLI 命令 tooauthenticate 透過 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="201b4-106">Run hello `azure login` CLI command tooauthenticate through Azure Active Directory.</span></span> <span data-ttu-id="201b4-107">這個方法可讓您存取 tooCLI 命令，在這兩[命令模式](#cli-command-modes)。</span><span class="sxs-lookup"><span data-stu-id="201b4-107">This method gives you access tooCLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="201b4-108">當您執行 hello 命令，而不需要額外的選項，`azure login`會提示您 toocontinue 透過 web 入口網站以互動方式登入。</span><span class="sxs-lookup"><span data-stu-id="201b4-108">When you run hello command without additional options, `azure login` prompts you toocontinue logging in interactively through a web portal.</span></span> <span data-ttu-id="201b4-109">針對其他`azure login`命令選項，請參閱此文件或類型中的 hello 案例`azure login --help`。</span><span class="sxs-lookup"><span data-stu-id="201b4-109">For additional `azure login` command options, see hello scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="201b4-110">如果您只需要 toouse Azure 服務管理模式 CLI 命令 （不建議用於最新的部署），您可以下載並安裝在電腦上的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="201b4-110">If you only need toouse Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="201b4-111">如果您尚未安裝 hello CLI，請參閱[安裝 hello Azure CLI](cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="201b4-111">If you haven't already installed hello CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="201b4-112">如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立 [免費帳戶](http://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="201b4-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="201b4-113">如需不同帳戶身分識別與 Azure 訂用帳戶的背景，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory/active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="201b4-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="201b4-114">案例 1：使用互動式登入方法來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="201b4-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="201b4-115">使用特定的帳戶，hello CLI 需要您 toorun`azure login`然後繼續 hello 登入程序，透過 web 入口網站，稱為程序的網頁瀏覽器*互動式登入*。</span><span class="sxs-lookup"><span data-stu-id="201b4-115">With certain accounts, hello CLI requires you toorun `azure login` and then continue hello login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="201b4-116">常見原因是當您有工作或學校帳戶 (也稱為*組織帳戶*) 設定 toorequire 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="201b4-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up toorequire multifactor authentication.</span></span> <span data-ttu-id="201b4-117">當您想 toouse 資源管理員模式命令時，也使用與您的 Microsoft 帳戶互動式登入。</span><span class="sxs-lookup"><span data-stu-id="201b4-117">Also use interactive login with your Microsoft account, when you want toouse Resource Manager mode commands.</span></span>

<span data-ttu-id="201b4-118">互動式登入是簡單： 型別`azure login`-不使用任何選項-hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="201b4-118">Interactive login is easy: type `azure login` -- without any options -- as shown in hello following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="201b4-119">hello 輸出會顯示 hello 下列類似：</span><span class="sxs-lookup"><span data-stu-id="201b4-119">hello output appears something like hello following:</span></span>

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
<span data-ttu-id="201b4-120">複製 hello 提供 tooyou hello 命令輸出中的程式碼，並開啟瀏覽器 toohttp://aka.ms/devicelogin 或其他頁面，如果指定。</span><span class="sxs-lookup"><span data-stu-id="201b4-120">Copy hello code offered tooyou in hello command output, and open a browser toohttp://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="201b4-121">(您可以開啟瀏覽器上 hello 同一部電腦，或在不同的電腦或裝置上。)輸入 hello 的程式碼，接著便可提示的 tooenter hello 使用者名稱和密碼要 toouse hello 身分識別。</span><span class="sxs-lookup"><span data-stu-id="201b4-121">(You can open a browser on hello same computer, or on a different computer or device.) Enter hello code, and then you are prompted tooenter hello username and password for hello identity you want toouse.</span></span> <span data-ttu-id="201b4-122">在該程序完成，hello 命令殼層時完成 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="201b4-122">When that process completes, hello command shell completes hello login.</span></span> <span data-ttu-id="201b4-123">會出現類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="201b4-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="201b4-124">透過互動式登入，驗證和授權都是使用 Azure Active Directory 來執行。</span><span class="sxs-lookup"><span data-stu-id="201b4-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="201b4-125">如果您使用 Microsoft 帳戶的身分識別，hello 登入程序會存取您的 Azure Active Directory 預設網域。</span><span class="sxs-lookup"><span data-stu-id="201b4-125">If you use a Microsoft account identity, hello login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="201b4-126">(如果您註冊免費 Azure 帳戶，Azure Active Directory 會為您的帳戶自動建立預設網域。)</span><span class="sxs-lookup"><span data-stu-id="201b4-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="201b4-127">案例 2：利用使用者名稱和密碼來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="201b4-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="201b4-128">使用 hello`azure login`命令與 hello 使用者名稱 (`-u`) 參數 tooauthenticate 時想 toouse 工作或學校帳戶，不需要多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="201b4-128">Use hello `azure login` command with hello username (`-u`) parameter tooauthenticate when you want toouse a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="201b4-129">系統會提示您在 hello 密碼的 hello 命令列 (或者，您可以選擇性地傳遞為 hello 的額外參數的 hello 密碼`azure login`命令)。</span><span class="sxs-lookup"><span data-stu-id="201b4-129">You are prompted at hello command line for hello password (or you can optionally pass hello password as an additional parameter of hello `azure login` command).</span></span> <span data-ttu-id="201b4-130">hello 下列範例會將 $ hello 的組織帳戶的使用者名稱：</span><span class="sxs-lookup"><span data-stu-id="201b4-130">hello following example passes hello username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="201b4-131">然後，您會收到提示 tooenter 您的密碼：</span><span class="sxs-lookup"><span data-stu-id="201b4-131">You are then prompted tooenter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="201b4-132">然後完成 hello 登入程序。</span><span class="sxs-lookup"><span data-stu-id="201b4-132">hello login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="201b4-133">如果這是您第一次登入才能執行這些認證時，系統會詢問 tooverify 您希望 toocache 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="201b4-133">If this is your first time logging in with these credentials, you are asked tooverify that you wish toocache an authentication token.</span></span> <span data-ttu-id="201b4-134">如果您先前使用 hello，也會發生此提示`azure logout`命令 （hello 文件中稍後所述）。</span><span class="sxs-lookup"><span data-stu-id="201b4-134">This prompt also occurs if you previously used hello `azure logout` command (described later in hello article).</span></span> <span data-ttu-id="201b4-135">toobypass 自動化案例中，這個提示字元執行`azure login`以 hello`-q`參數。</span><span class="sxs-lookup"><span data-stu-id="201b4-135">toobypass this prompt for automation scenarios, run `azure login` with hello `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="201b4-136">案例 3：使用服務主體來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="201b4-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="201b4-137">如果您建立服務主體的 Active Directory 應用程式，而且 hello 服務主體對您的訂用帳戶的權限，您可以使用 hello`azure login`命令 tooauthenticate hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="201b4-137">If you create a service principal for an Active Directory application, and hello service principal has permissions on your subscription, you can use hello `azure login` command tooauthenticate hello service principal.</span></span> <span data-ttu-id="201b4-138">根據您的案例中，您可以提供 hello hello 服務主體的認證當做明確參數的 hello`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="201b4-138">Depending on your scenario, you could provide hello credentials of hello service principal as explicit parameters of hello `azure login` command.</span></span> <span data-ttu-id="201b4-139">例如，hello 下列命令會將 hello 服務主體名稱和 Active Directory 租用戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="201b4-139">For example, hello following command passes hello service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="201b4-140">您會再提示的 tooprovide hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="201b4-140">You are then prompted tooprovide hello password.</span></span> <span data-ttu-id="201b4-141">您也可以提供 hello 認證透過 CLI 指令碼或應用程式程式碼，或用於自動化案例非互動方式使用憑證 tooauthenticate hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="201b4-141">You can also provide hello credentials through a CLI script or application code, or use a certificate tooauthenticate hello service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="201b4-142">如需詳細資料與範例，請參閱[使用 Azure Resource Manager 驗證服務主體](resource-group-authenticate-service-principal-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="201b4-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="201b4-143">案例 4：使用發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="201b4-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="201b4-144">如果您只需要 toouse hello Azure 服務管理模式 CLI 命令 (例如，toodeploy Azure Vm 中 hello 傳統部署模型)，您可以使用發行設定檔案連接。</span><span class="sxs-lookup"><span data-stu-id="201b4-144">If you only need toouse hello Azure Service Management mode CLI commands (for example, toodeploy Azure VMs in hello classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="201b4-145">這個方法會將憑證安裝在本機電腦，讓您的 tooperform 管理工作，只要 hello 訂用帳戶和 hello 憑證有效。</span><span class="sxs-lookup"><span data-stu-id="201b4-145">This method installs a certificate on your local computer that allows you tooperform management tasks for as long as hello subscription and hello certificate are valid.</span></span>

* <span data-ttu-id="201b4-146">**toodownload hello 的發行設定檔**您的帳戶，請確定 CLI 是服務管理模式中，輸入該 hello `azure config mode asm`。</span><span class="sxs-lookup"><span data-stu-id="201b4-146">**toodownload hello publish settings file** for your account, ensure that hello CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="201b4-147">然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="201b4-147">Then run hello following command:</span></span>

        azure account download

<span data-ttu-id="201b4-148">這會開啟預設的瀏覽器，並提示您在 toohello toosign [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="201b4-148">This opens your default browser and prompts you toosign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="201b4-149">登入後便會下載 `.publishsettings` 檔案。</span><span class="sxs-lookup"><span data-stu-id="201b4-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="201b4-150">請記下此檔案的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="201b4-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="201b4-151">如果您的帳戶與多個 Azure Active Directory 租用戶相關聯，您可能會是哪一種 Active Directory 想 toodownload 發行設定檔案的提示的 tooselect。</span><span class="sxs-lookup"><span data-stu-id="201b4-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted tooselect which Active Directory you wish toodownload a publish settings file for.</span></span>
>
>

<span data-ttu-id="201b4-152">一旦使用 hello 下載頁面上，選取或瀏覽 hello Azure 傳統入口網站，hello 選取 Active Directory 會變成 hello hello 傳統入口網站並下載頁面使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="201b4-152">Once selected using hello download page, or by visiting hello Azure classic portal, hello selected Active Directory becomes hello default used by hello classic portal and download page.</span></span> <span data-ttu-id="201b4-153">一旦建立預設值，您會看到 hello 文字 '**按一下這裡 tooreturn toohello 選取 頁面上**' hello 頁面頂端的 hello 下載。</span><span class="sxs-lookup"><span data-stu-id="201b4-153">Once a default has been established, you see hello text '**click here tooreturn toohello selection page**' at hello top of hello download page.</span></span> <span data-ttu-id="201b4-154">使用 hello 提供連結 tooreturn toohello 選取 頁面。</span><span class="sxs-lookup"><span data-stu-id="201b4-154">Use hello provided link tooreturn toohello selection page.</span></span>

* <span data-ttu-id="201b4-155">**tooimport hello 的發行設定檔**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="201b4-155">**tooimport hello publish settings file**, run hello following command:</span></span>

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="201b4-156">匯入之後您將發行設定，您應該刪除 hello`.publishsettings`檔案。</span><span class="sxs-lookup"><span data-stu-id="201b4-156">After importing your publish settings, you should delete hello `.publishsettings` file.</span></span> <span data-ttu-id="201b4-157">它已不再需要由 hello Azure CLI，並存在安全性風險，因為它可能會使用的 toogain 存取 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="201b4-157">It is no longer required by hello Azure CLI and presents a security risk as it could be used toogain access tooyour subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="201b4-158">CLI 命令模式</span><span class="sxs-lookup"><span data-stu-id="201b4-158">CLI command modes</span></span>
<span data-ttu-id="201b4-159">hello Azure CLI 提供兩種命令模式使用具有不同的命令集的 Azure 資源：</span><span class="sxs-lookup"><span data-stu-id="201b4-159">hello Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="201b4-160">**Resource Manager 模式**： 適用於使用 hello Resource Manager 部署模型中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="201b4-160">**Resource Manager mode** - for working with Azure resources in hello Resource Manager deployment model.</span></span> <span data-ttu-id="201b4-161">tooset 此模式中，執行`azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="201b4-161">tooset this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="201b4-162">**服務管理模式**： 適用於使用 hello 傳統部署模型中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="201b4-162">**Service Management mode** - for working with Azure resources in hello classic deployment model.</span></span> <span data-ttu-id="201b4-163">tooset 此模式中，執行`azure config mode asm`。</span><span class="sxs-lookup"><span data-stu-id="201b4-163">tooset this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="201b4-164">最初安裝時，hello 的 hello CLI 處於 Resource Manager 模式的目前版本。</span><span class="sxs-lookup"><span data-stu-id="201b4-164">When first installed, hello current release of hello CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="201b4-165">hello Resource Manager 模式和服務管理模式互斥。</span><span class="sxs-lookup"><span data-stu-id="201b4-165">hello Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="201b4-166">也就是一種模式中建立的資源無法在此管理 hello 其他模式。</span><span class="sxs-lookup"><span data-stu-id="201b4-166">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="201b4-167">多重訂閱</span><span class="sxs-lookup"><span data-stu-id="201b4-167">Multiple subscriptions</span></span>
<span data-ttu-id="201b4-168">如果您有多個 Azure 訂用帳戶，連接 tooAzure 授與存取您的認證與相關聯的 tooall 訂閱。</span><span class="sxs-lookup"><span data-stu-id="201b4-168">If you have multiple Azure subscriptions, connecting tooAzure grants access tooall subscriptions associated with your credentials.</span></span> <span data-ttu-id="201b4-169">一個訂用帳戶是 hello 預設為選取，而且執行作業時，由 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="201b4-169">One subscription is selected as hello default, and used by hello Azure CLI when performing operations.</span></span> <span data-ttu-id="201b4-170">您可以檢視 hello 訂用帳戶，包括 hello 目前預設訂用帳戶，請使用 hello`azure account list`命令。</span><span class="sxs-lookup"><span data-stu-id="201b4-170">You can view hello subscriptions, including hello current default subscription, using hello `azure account list` command.</span></span> <span data-ttu-id="201b4-171">此命令會傳回類似 toohello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="201b4-171">This command returns information similar toohello following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="201b4-172">在上述清單中的 hello，hello**目前**資料行會指出 hello 目前預設訂用帳戶與 Azure-sub-1。</span><span class="sxs-lookup"><span data-stu-id="201b4-172">In hello preceding list, hello **Current** column indicates hello current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="201b4-173">toochange hello 預設訂用帳戶，使用 hello`azure account set`命令，然後指定您想 toobe hello 預設 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="201b4-173">toochange hello default subscription, use hello `azure account set` command, and specify hello subscription that you wish toobe hello default.</span></span> <span data-ttu-id="201b4-174">例如：</span><span class="sxs-lookup"><span data-stu-id="201b4-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="201b4-175">這樣會變更 hello 預設訂用帳戶 tooAzure-sub-2。</span><span class="sxs-lookup"><span data-stu-id="201b4-175">This changes hello default subscription tooAzure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="201b4-176">變更 hello 預設訂用帳戶會立即生效，以及全域變更;新的 Azure CLI 命令，不管您是從執行 hello 相同命令列執行個體或不同的執行個體，使用 hello 新預設訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="201b4-176">Changing hello default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from hello same command-line instance or a different instance, use hello new default subscription.</span></span>
>
>

<span data-ttu-id="201b4-177">如果您想 toouse hello Azure CLI 的非預設訂用帳戶，但不想 toochange hello 目前的預設值，您可以使用 hello `--subscription` hello 命令選項，然後提供 hello 名稱 hello 訂用帳戶中，您想 toouse hello 作業。</span><span class="sxs-lookup"><span data-stu-id="201b4-177">If you wish toouse a non-default subscription with hello Azure CLI, but don't want toochange hello current default, you can use hello `--subscription` option for hello command and provide hello name of hello subscription you wish toouse for hello operation.</span></span>

<span data-ttu-id="201b4-178">一旦您已連線的 tooyour Azure 訂用帳戶，您可以從開始使用 Azure 資源 hello Azure CLI 命令 toowork。</span><span class="sxs-lookup"><span data-stu-id="201b4-178">Once you are connected tooyour Azure subscription, you can start using hello Azure CLI commands toowork with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="201b4-179">CLI 設定的儲存位置</span><span class="sxs-lookup"><span data-stu-id="201b4-179">Storage of CLI settings</span></span>
<span data-ttu-id="201b4-180">是否登入 hello`azure login`命令或匯入發行設定時，您的 CLI 設定檔和記錄檔儲存在`.azure`目錄位於您`user`目錄。</span><span class="sxs-lookup"><span data-stu-id="201b4-180">Whether you log in with hello `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="201b4-181">`user` 目錄已受到作業系統的保護。</span><span class="sxs-lookup"><span data-stu-id="201b4-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="201b4-182">不過，我們建議您採取其他步驟 tooencrypt 您`user`目錄。</span><span class="sxs-lookup"><span data-stu-id="201b4-182">However, we recommend that you take additional steps tooencrypt your `user` directory.</span></span> <span data-ttu-id="201b4-183">您可以在 hello 下列方法來這樣做：</span><span class="sxs-lookup"><span data-stu-id="201b4-183">You can do so in hello following ways:</span></span>

* <span data-ttu-id="201b4-184">在 Windows 中，修改 hello 目錄屬性，或使用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="201b4-184">On Windows, modify hello directory properties or use BitLocker.</span></span>
* <span data-ttu-id="201b4-185">在 Mac 上，開啟 FileVault hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="201b4-185">On Mac, turn on FileVault for hello directory.</span></span>
* <span data-ttu-id="201b4-186">在 Ubuntu，使用 hello 加密首頁目錄功能。</span><span class="sxs-lookup"><span data-stu-id="201b4-186">On Ubuntu, use hello Encrypted Home directory feature.</span></span> <span data-ttu-id="201b4-187">其他 Linux 散發套件提供類似的功能。</span><span class="sxs-lookup"><span data-stu-id="201b4-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="201b4-188">登出</span><span class="sxs-lookup"><span data-stu-id="201b4-188">Logging out</span></span>
<span data-ttu-id="201b4-189">toolog 出使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="201b4-189">toolog out, use hello following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="201b4-190">如果 hello 訂用帳戶相關聯 hello 帳戶只驗證與 Active Directory，登出 hello 本機設定檔中刪除 hello 訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="201b4-190">If hello subscriptions associated with hello account are only authenticated with Active Directory, logging out deletes hello subscription information from hello local profile.</span></span> <span data-ttu-id="201b4-191">不過，如果 hello 訂用帳戶也已匯入發行設定檔，登出只刪除 Active Directory 相關 hello 本機設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="201b4-191">However, if a publish settings file was also imported for hello subscriptions, logging out only deletes Active Directory related information from hello local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="201b4-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="201b4-192">Next steps</span></span>
* <span data-ttu-id="201b4-193">toouse Azure CLI 命令，請參閱[Resource Manager 模式中的 Azure CLI 命令](virtual-machines/azure-cli-arm-commands.md)和[服務管理模式中的 Azure CLI 命令](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="201b4-193">toouse Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="201b4-194">深入了解 hello Azure CLI toolearn 下載原始程式碼、 報告的問題，或參與 toohello 專案，請瀏覽 hello [hello Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="201b4-194">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="201b4-195">如果您遇到了使用 Azure CLI hello 或 Azure 的問題，請瀏覽 hello [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)。</span><span class="sxs-lookup"><span data-stu-id="201b4-195">If you encounter problems using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
