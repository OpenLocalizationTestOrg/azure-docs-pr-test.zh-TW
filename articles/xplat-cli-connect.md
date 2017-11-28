---
title: "從 CLI 登入 Azure | Microsoft Docs"
description: "從適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI) 連接到您的 Azure 訂用帳戶"
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
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="66c4c-103">從 Azure CLI 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="66c4c-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="66c4c-104">Azure CLI 是一組開放原始碼的跨平台命令，可供您運用在 Azure 資源上。</span><span class="sxs-lookup"><span data-stu-id="66c4c-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="66c4c-105">本文描述提供 Azure 帳戶認證以將 Azure CLI 連線至 Azure 訂用帳戶的不同方式：</span><span class="sxs-lookup"><span data-stu-id="66c4c-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="66c4c-106">透過 Azure Active Directory 執行 `azure login` CLI 命令以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="66c4c-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="66c4c-107">這個方法可讓您在兩個[命令模式](#cli-command-modes)中存取 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="66c4c-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="66c4c-108">當您執行命令時若沒有其他選項，`azure login` 會提示您透過 Web 入口網站以互動方式繼續登入。</span><span class="sxs-lookup"><span data-stu-id="66c4c-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="66c4c-109">如需其他 `azure login` 命令選項，請參閱本文中的案例，或輸入 `azure login --help`。</span><span class="sxs-lookup"><span data-stu-id="66c4c-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="66c4c-110">如果您只需要使用 Azure 服務管理模式 CLI 命令 (不建議用於大部分的新部署)，您可以在您的電腦上下載並安裝發佈設定檔。</span><span class="sxs-lookup"><span data-stu-id="66c4c-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="66c4c-111">如果您尚未安裝 CLI，請參閱 [安裝 Azure CLI](cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="66c4c-112">如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立 [免費帳戶](http://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="66c4c-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="66c4c-113">如需不同帳戶身分識別與 Azure 訂用帳戶的背景，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory/active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="66c4c-114">案例 1：使用互動式登入方法來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="66c4c-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="66c4c-115">使用特定帳戶，CLI 會要求您執行 `azure login`，然後透過 Web 入口網站使用 Web 瀏覽器繼續進行登入程序，此程序稱為*互動式登入*。</span><span class="sxs-lookup"><span data-stu-id="66c4c-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="66c4c-116">常見的原因是您有工作或學校帳戶 (也稱為*組織帳戶*) 設定為需要多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="66c4c-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="66c4c-117">當您想要使用 Resource Manager 模式命令時，也會使用互動方式登入您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c4c-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="66c4c-118">互動式登入很簡單︰輸入 `azure login` 即可，不需要任何選項，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="66c4c-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="66c4c-119">輸出畫面如下所示：</span><span class="sxs-lookup"><span data-stu-id="66c4c-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="66c4c-120">複製命令輸出中提供的程式碼，並開啟瀏覽器至 http://aka.ms/devicelogin，或其他頁面 (若已指定)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="66c4c-121">(您可以在同一台電腦上，或在不同電腦或裝置上開啟瀏覽器。)輸入程式碼後，系統會提示您針對您要使用之身分識別輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="66c4c-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="66c4c-122">完成此程序之後，命令殼層便完成登入。</span><span class="sxs-lookup"><span data-stu-id="66c4c-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="66c4c-123">會出現類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="66c4c-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="66c4c-124">透過互動式登入，驗證和授權都是使用 Azure Active Directory 來執行。</span><span class="sxs-lookup"><span data-stu-id="66c4c-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="66c4c-125">如果您使用 Microsoft 帳戶身分識別，登入程序就會存取您的 Azure Active Directory 預設網域。</span><span class="sxs-lookup"><span data-stu-id="66c4c-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="66c4c-126">(如果您註冊免費 Azure 帳戶，Azure Active Directory 會為您的帳戶自動建立預設網域。)</span><span class="sxs-lookup"><span data-stu-id="66c4c-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="66c4c-127">案例 2：利用使用者名稱和密碼來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="66c4c-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="66c4c-128">當您想要使用不需要多重要素驗證的工作或學校帳戶時，可以使用 `azure login` 命令搭配使用者名稱 (`-u`) 參數以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="66c4c-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="66c4c-129">系統會提示您在命令列中的密碼 (或者可以選擇性地傳遞密碼做為 `azure login` 命令的其他參數)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="66c4c-130">下列範例會傳遞組織帳戶的使用者名稱︰</span><span class="sxs-lookup"><span data-stu-id="66c4c-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="66c4c-131">系統會提示您輸入密碼：</span><span class="sxs-lookup"><span data-stu-id="66c4c-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="66c4c-132">然後完成登入程序。</span><span class="sxs-lookup"><span data-stu-id="66c4c-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="66c4c-133">如果這是您第一次使用這些認證來登入，系統會要求您確認是否要快取驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="66c4c-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="66c4c-134">如果您先前已使用 (如本文稍後所述的) `azure logout` 命令，也會出現此提示。</span><span class="sxs-lookup"><span data-stu-id="66c4c-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="66c4c-135">如果要在自動化作業中略過此提示，請使用 `azure login` 參數執行 `-q`。</span><span class="sxs-lookup"><span data-stu-id="66c4c-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="66c4c-136">案例 3：使用服務主體來登入 Azure</span><span class="sxs-lookup"><span data-stu-id="66c4c-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="66c4c-137">如果您已建立 Active Directory 應用程式的服務主體，而且服務主體擁有訂用帳戶的權限，您就可以使用 `azure login` 命令來驗證服務主體。</span><span class="sxs-lookup"><span data-stu-id="66c4c-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="66c4c-138">根據您的案例，您可以提供服務主體的認證做為 `azure login` 命令的明確參數。</span><span class="sxs-lookup"><span data-stu-id="66c4c-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="66c4c-139">例如，下列命令會傳遞服務主體名稱與 Active Directory 租用戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="66c4c-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="66c4c-140">接著，系統會提示您提供密碼。</span><span class="sxs-lookup"><span data-stu-id="66c4c-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="66c4c-141">您也可以透過 CLI 指令碼或應用程式程式碼提供認證，或針對自動化案例使用憑證以非互動的方式驗證服務主體。</span><span class="sxs-lookup"><span data-stu-id="66c4c-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="66c4c-142">如需詳細資料與範例，請參閱[使用 Azure Resource Manager 驗證服務主體](resource-group-authenticate-service-principal-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="66c4c-143">案例 4：使用發佈設定檔</span><span class="sxs-lookup"><span data-stu-id="66c4c-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="66c4c-144">如果您只需要使用 Azure 服務管理模式 CLI 命令 (例如，在傳統部署模型中部署 Azure VM)，您可以使用發佈設定檔連線。</span><span class="sxs-lookup"><span data-stu-id="66c4c-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="66c4c-145">此方法會在您的本機電腦上安裝憑證，只要訂用帳戶和憑證有效，該憑證便可讓您執行管理工作。</span><span class="sxs-lookup"><span data-stu-id="66c4c-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="66c4c-146">**若要下載您帳戶的發佈設定檔**，請輸入 `azure config mode asm` 以確保 CLI 是在服務管理模式中。</span><span class="sxs-lookup"><span data-stu-id="66c4c-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="66c4c-147">然後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="66c4c-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="66c4c-148">這會開啟您的預設瀏覽器，提示您登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="66c4c-149">登入後便會下載 `.publishsettings` 檔案。</span><span class="sxs-lookup"><span data-stu-id="66c4c-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="66c4c-150">請記下此檔案的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="66c4c-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="66c4c-151">如果您的帳戶與多個 Azure Active Directory 租用戶相關聯，則可能會提示您選取要在其中下載發行設定檔的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="66c4c-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="66c4c-152">在使用下載頁面或是造訪 Azure 傳統入口網站選定之後，所選的 Active Directory 會成為傳統入口網站與下載頁面使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="66c4c-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="66c4c-153">建立好預設值之後，您會在下載頁面上方看到 [click here to return to the selection page]。</span><span class="sxs-lookup"><span data-stu-id="66c4c-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="66c4c-154">請使用提供的連結，返回選取頁面。</span><span class="sxs-lookup"><span data-stu-id="66c4c-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="66c4c-155">**若要匯入發佈設定檔案**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="66c4c-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="66c4c-156">匯入發佈設定之後，請刪除 `.publishsettings` 檔案。</span><span class="sxs-lookup"><span data-stu-id="66c4c-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="66c4c-157">Azure CLI 已不再需要它，而且它可用於存取您的訂用帳戶，因此造成安全風險。</span><span class="sxs-lookup"><span data-stu-id="66c4c-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="66c4c-158">CLI 命令模式</span><span class="sxs-lookup"><span data-stu-id="66c4c-158">CLI command modes</span></span>
<span data-ttu-id="66c4c-159">Azure CLI 提供兩種命令模式來使用具備不同命令集的 Azure 資源︰</span><span class="sxs-lookup"><span data-stu-id="66c4c-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="66c4c-160">**Resource Manager 模式** - 適用於以 Resource Manager 部署模型使用 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="66c4c-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="66c4c-161">若要設定此模式，請執行 `azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="66c4c-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="66c4c-162">**服務管理模式** - 適用於以傳統部署模型使用 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="66c4c-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="66c4c-163">若要設定此模式，請執行 `azure config mode asm`。</span><span class="sxs-lookup"><span data-stu-id="66c4c-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="66c4c-164">初次安裝時，最新版本的 CLI 是在 Resource Manager 模式中。</span><span class="sxs-lookup"><span data-stu-id="66c4c-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="66c4c-165">Resource Manager 模式與服務管理模式是互斥的。</span><span class="sxs-lookup"><span data-stu-id="66c4c-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="66c4c-166">亦即，任一模式所建立的資源，將無法由另一種模式來管理。</span><span class="sxs-lookup"><span data-stu-id="66c4c-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="66c4c-167">多重訂閱</span><span class="sxs-lookup"><span data-stu-id="66c4c-167">Multiple subscriptions</span></span>
<span data-ttu-id="66c4c-168">如果您擁有多個 Azure 訂用帳戶，連接到 Azure 會針對與您的認證相關聯的所有訂用帳戶授予存取權限。</span><span class="sxs-lookup"><span data-stu-id="66c4c-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="66c4c-169">系統會選取一個訂用帳戶做為預設值，以供 Azure CLI 用來執行作業。</span><span class="sxs-lookup"><span data-stu-id="66c4c-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="66c4c-170">您可以使用 `azure account list` 命令檢視訂用帳戶，包括目前的預設訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c4c-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="66c4c-171">此命令會傳回類似以下的資訊：</span><span class="sxs-lookup"><span data-stu-id="66c4c-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="66c4c-172">在上述清單中，[目前] 欄會指出目前的預設訂用帳戶為 Azure-sub-1。</span><span class="sxs-lookup"><span data-stu-id="66c4c-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="66c4c-173">若要變更預設訂用帳戶，請使用 `azure account set` 命令，並指定您想要設為預設值的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c4c-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="66c4c-174">例如：</span><span class="sxs-lookup"><span data-stu-id="66c4c-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="66c4c-175">此動作會將預設訂用帳戶變更為 Azure-sub-2。</span><span class="sxs-lookup"><span data-stu-id="66c4c-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="66c4c-176">變更預設的訂用帳戶會立即生效，而且是全域變更；無論您是從相同的命令列執行個體或不同的執行個體執行新的 Azure CLI 命令，它們都會使用新的預設訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66c4c-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="66c4c-177">如果您要 Azure CLI 使用非預設的訂用帳戶，但又不想變更目前的預設值，可以使用適用於該命令的 `--subscription` 選項，並提供希望該作業使用的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="66c4c-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="66c4c-178">一旦您連接到 Azure 訂用帳戶之後，就可以開始搭配使用 Azure CLI 命令和 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="66c4c-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="66c4c-179">CLI 設定的儲存位置</span><span class="sxs-lookup"><span data-stu-id="66c4c-179">Storage of CLI settings</span></span>
<span data-ttu-id="66c4c-180">無論您是使用 `azure login` 命令登入或是匯入發佈設定，CLI 設定檔和記錄檔都會儲存在您 `user` 目錄中的 `.azure` 目錄內。</span><span class="sxs-lookup"><span data-stu-id="66c4c-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="66c4c-181">`user` 目錄已受到作業系統的保護。</span><span class="sxs-lookup"><span data-stu-id="66c4c-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="66c4c-182">不過，建議您採取額外的步驟來加密 `user` 目錄。</span><span class="sxs-lookup"><span data-stu-id="66c4c-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="66c4c-183">做法如下：</span><span class="sxs-lookup"><span data-stu-id="66c4c-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="66c4c-184">在 Windows 中，修改目錄屬性或使用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="66c4c-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="66c4c-185">在 Mac 中，開啟目錄的 FileVault。</span><span class="sxs-lookup"><span data-stu-id="66c4c-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="66c4c-186">在 Ubuntu 中，使用「加密主目錄」功能。</span><span class="sxs-lookup"><span data-stu-id="66c4c-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="66c4c-187">其他 Linux 散發套件提供類似的功能。</span><span class="sxs-lookup"><span data-stu-id="66c4c-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="66c4c-188">登出</span><span class="sxs-lookup"><span data-stu-id="66c4c-188">Logging out</span></span>
<span data-ttu-id="66c4c-189">若要登出，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="66c4c-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="66c4c-190">如果與帳戶關聯的訂用帳戶僅能對 Active Directory 驗證，進行登出時就會從本機設定檔中刪除訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="66c4c-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="66c4c-191">不過，如果也已匯入訂用帳戶的發佈設定檔，則進行登出時只會從本機設定檔中刪除 Active Directory 相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="66c4c-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66c4c-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66c4c-192">Next steps</span></span>
* <span data-ttu-id="66c4c-193">若要使用 Azure CLI 命令，請參閱 [Resource Manager 模式中的 Azure CLI 命令](virtual-machines/azure-cli-arm-commands.md)和[服務管理模式中的 Azure CLI 命令](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="66c4c-194">若要深入了解 Azure CLI、下載來源程式碼、回報問題，或是參與專案，請造訪 [Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="66c4c-195">如果您在使用 Azure CLI 或 Azure 方面遇到問題，請造訪 [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)(英文)。</span><span class="sxs-lookup"><span data-stu-id="66c4c-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
