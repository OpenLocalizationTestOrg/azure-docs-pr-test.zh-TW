---
title: "aaaConnect tooAzure 堆疊時會搭配 CLI |Microsoft 文件"
description: "了解 toouse hello toomanage 跨平台命令列介面 (CLI)，並部署 Azure 堆疊上的資源"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a><span data-ttu-id="ba54c-103">安裝並設定 CLI 以與 Azure Stack 搭配使用</span><span class="sxs-lookup"><span data-stu-id="ba54c-103">Install and configure CLI for use with Azure Stack</span></span>

<span data-ttu-id="ba54c-104">在本文件中，我們引導您完成使用 Azure 命令列介面 (CLI) toomanage Azure 堆疊開發套件資源從 Linux 和 Mac 用戶端的平台的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="ba54c-104">In this document, we guide you through hello process of using Azure Command-line Interface (CLI) toomanage Azure Stack Development Kit resources from Linux and Mac client platforms.</span></span> 

## <a name="export-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="ba54c-105">匯出 hello Azure 堆疊 CA 根憑證</span><span class="sxs-lookup"><span data-stu-id="ba54c-105">Export hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="ba54c-106">如果您從 hello Azure 堆疊開發套件的環境中執行的虛擬機器使用 CLI，hello Azure 堆疊的根憑證已安裝 hello 虛擬機器內，您可以直接擷取。</span><span class="sxs-lookup"><span data-stu-id="ba54c-106">If you are using CLI from a virtual machine that is running within hello Azure Stack Development Kit environment, hello Azure Stack root certificate is already installed within hello virtual machine so you can directly retrieve.</span></span> <span data-ttu-id="ba54c-107">而如果您是使用 CLI 的工作站以外 hello 開發套件，您必須匯出從 hello 開發套件的 hello Azure 堆疊 CA 根憑證，並將它加入 toohello Python 的憑證存放區的開發工作站 （外部 Linux 或 Mac 的平台).</span><span class="sxs-lookup"><span data-stu-id="ba54c-107">Whereas if you are use CLI from a workstation outside hello development kit, you must export hello Azure Stack CA root certificate from hello development kit and add it toohello Python certificate store of your development workstation(external Linux or Mac platform).</span></span> 

<span data-ttu-id="ba54c-108">登入 tooyour 開發套件，然後執行下列指令碼 tooexport hello Azure 堆疊中的根憑證 PEM 格式 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-108">Sign in tooyour development kit and run hello following script tooexport hello Azure Stack root certificate in PEM format:</span></span>

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a><span data-ttu-id="ba54c-109">安裝 CLI</span><span class="sxs-lookup"><span data-stu-id="ba54c-109">Install CLI</span></span>

<span data-ttu-id="ba54c-110">接下來，您應該登入 tooyour 開發工作站，並安裝 CLI。</span><span class="sxs-lookup"><span data-stu-id="ba54c-110">Next you should sign in tooyour development workstation and install CLI.</span></span> <span data-ttu-id="ba54c-111">Azure 堆疊需要 Azure CLI，您可以使用 hello 中所述的 hello 步驟安裝 hello 2.0 版本[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)發行項。</span><span class="sxs-lookup"><span data-stu-id="ba54c-111">Azure Stack requires hello 2.0 version of Azure CLI, which you can install by using hello steps described in hello [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) article.</span></span> <span data-ttu-id="ba54c-112">tooverify 如果 hello 安裝是否成功，開啟終端機或命令提示字元視窗並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-112">tooverify if hello installation was successful, open a terminal or a command prompt window and run hello following command:</span></span>

```azurecli
az --version
```

<span data-ttu-id="ba54c-113">您應該會看到 hello Azure CLI 版本和您的電腦安裝其他相依程式庫。</span><span class="sxs-lookup"><span data-stu-id="ba54c-113">You should see hello version of Azure CLI and other dependent libraries that are installed on your computer.</span></span>

## <a name="trust-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="ba54c-114">信任 hello Azure 堆疊 CA 根憑證</span><span class="sxs-lookup"><span data-stu-id="ba54c-114">Trust hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="ba54c-115">tootrust hello Azure 堆疊 CA 根憑證，您應該將它附加 toohello 現有 python 憑證。</span><span class="sxs-lookup"><span data-stu-id="ba54c-115">tootrust hello Azure Stack CA root certificate, you should append it toohello existing python certificate.</span></span> <span data-ttu-id="ba54c-116">如果您從 Linux 機器建立 hello Azure 堆疊環境中執行 CLI，執行的 hello 下列撞命令：</span><span class="sxs-lookup"><span data-stu-id="ba54c-116">If you are running CLI from a Linux machine that is created within hello Azure Stack environment, run hello following bash command:</span></span>

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

<span data-ttu-id="ba54c-117">如果您從 hello Azure Sack 環境外機器中執行 CLI，您必須先設定[VPN 連線能力 tooAzure 堆疊](azure-stack-connect-azure-stack.md)。</span><span class="sxs-lookup"><span data-stu-id="ba54c-117">If you are running CLI from a machine outside hello Azure Sack environment, you must first set up [VPN connectivity tooAzure Stack](azure-stack-connect-azure-stack.md).</span></span> <span data-ttu-id="ba54c-118">立即複製到您在開發工作站上稍早匯出的 hello PEM 憑證，並執行下列命令，根據您在開發工作站的 OS hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-118">Now copy hello PEM certificate that you exported earlier onto your development workstation and run hello following commands depending on your development workstation's OS,:</span></span>

### <a name="linux"></a><span data-ttu-id="ba54c-119">Linux</span><span class="sxs-lookup"><span data-stu-id="ba54c-119">Linux</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a><span data-ttu-id="ba54c-120">macOS</span><span class="sxs-lookup"><span data-stu-id="ba54c-120">macOS</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a><span data-ttu-id="ba54c-121">Windows</span><span class="sxs-lookup"><span data-stu-id="ba54c-121">Windows</span></span>

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a><span data-ttu-id="ba54c-122">設定 hello 虛擬機器別名端點</span><span class="sxs-lookup"><span data-stu-id="ba54c-122">Set up hello virtual machine aliases endpoint</span></span>

<span data-ttu-id="ba54c-123">使用者可使用 CLI 建立虛擬機器之前，hello 雲端系統管理員應該設定可公開存取的端點，其中包含虛擬機器映像的別名，並使用 hello 雲端登錄這個端點。</span><span class="sxs-lookup"><span data-stu-id="ba54c-123">Before users can create virtual machines by using CLI, hello cloud administrator should set up a publicly accessible endpoint that contains virtual machine image aliases and register this endpoint with hello cloud.</span></span> <span data-ttu-id="ba54c-124">hello`endpoint-vm-image-alias-doc`中 hello 參數`az cloud register`命令用於此目的。</span><span class="sxs-lookup"><span data-stu-id="ba54c-124">hello `endpoint-vm-image-alias-doc` parameter in hello `az cloud register` command is used for this purpose.</span></span> <span data-ttu-id="ba54c-125">這些新增 tooimage 別名端點之前，雲端系統管理員必須下載 hello 映像 toohello 堆疊 Azure marketplace。</span><span class="sxs-lookup"><span data-stu-id="ba54c-125">Cloud administrators must download hello image toohello Azure Stack marketplace before they add it tooimage aliases endpoint.</span></span>
   
<span data-ttu-id="ba54c-126">例如，Azure 包含使用以下 URI：https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json。</span><span class="sxs-lookup"><span data-stu-id="ba54c-126">For example, Azure contains uses following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span></span> <span data-ttu-id="ba54c-127">hello 雲端系統管理員應該設定類似的端點針對 Azure 堆疊與 hello hello Azure 堆疊 marketplace 中提供的映像。</span><span class="sxs-lookup"><span data-stu-id="ba54c-127">hello cloud administrator should set up a similar endpoint for Azure Stack with hello images that are available in hello Azure Stack marketplace.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="ba54c-128">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="ba54c-128">Connect tooAzure Stack</span></span>

<span data-ttu-id="ba54c-129">使用下列步驟 tooconnect tooAzure 堆疊 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-129">Use hello following steps tooconnect tooAzure Stack:</span></span>

1. <span data-ttu-id="ba54c-130">執行 hello az 雲端註冊命令，以註冊 Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="ba54c-130">Register your Azure Stack environment by running hello az cloud register command.</span></span>
   
   <span data-ttu-id="ba54c-131">a.</span><span class="sxs-lookup"><span data-stu-id="ba54c-131">a.</span></span> <span data-ttu-id="ba54c-132">tooregister hello**雲端管理**環境中，使用：</span><span class="sxs-lookup"><span data-stu-id="ba54c-132">tooregister hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   <span data-ttu-id="ba54c-133">b.</span><span class="sxs-lookup"><span data-stu-id="ba54c-133">b.</span></span> <span data-ttu-id="ba54c-134">tooregister hello**使用者**環境中，使用：</span><span class="sxs-lookup"><span data-stu-id="ba54c-134">tooregister hello **user** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. <span data-ttu-id="ba54c-135">使用下列命令的 hello 設定使用中環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-135">Set hello active environment by using hello following commands:</span></span>

   <span data-ttu-id="ba54c-136">a.</span><span class="sxs-lookup"><span data-stu-id="ba54c-136">a.</span></span> <span data-ttu-id="ba54c-137">Hello**雲端管理**環境中，使用：</span><span class="sxs-lookup"><span data-stu-id="ba54c-137">For hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   <span data-ttu-id="ba54c-138">b.</span><span class="sxs-lookup"><span data-stu-id="ba54c-138">b.</span></span> <span data-ttu-id="ba54c-139">Hello**使用者**環境中，使用：</span><span class="sxs-lookup"><span data-stu-id="ba54c-139">For hello **user** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. <span data-ttu-id="ba54c-140">更新您的環境設定 toouse hello Azure 堆疊特定應用程式開發介面版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="ba54c-140">Update your environment configuration toouse hello Azure Stack specific API version profile.</span></span> <span data-ttu-id="ba54c-141">tooupdate hello 組態，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-141">tooupdate hello configuration, run hello following command:</span></span>

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. <span data-ttu-id="ba54c-142">使用 hello 登入 tooyour Azure 堆疊環境**az 登入**命令。</span><span class="sxs-lookup"><span data-stu-id="ba54c-142">Sign in tooyour Azure Stack environment by using hello **az login** command.</span></span> <span data-ttu-id="ba54c-143">您可以為使用者或做為登入 toohello Azure 堆疊環境[服務主體](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects)。</span><span class="sxs-lookup"><span data-stu-id="ba54c-143">You can sign in toohello Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span></span> 

   * <span data-ttu-id="ba54c-144">以登入**使用者**： 您可以指定 hello 使用者名稱和密碼直接在 hello az 登入的命令，或使用瀏覽器進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ba54c-144">Sign in as a **user**: You can either specify hello username and password directly within hello az login command or authenticate using a browser.</span></span> <span data-ttu-id="ba54c-145">您必須 toodo hello 後者，如果您的帳戶已啟用多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="ba54c-145">You would have toodo hello latter, if your account has multi-factor authentication enabled.</span></span>

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > <span data-ttu-id="ba54c-146">如果您的使用者帳戶啟用多重要素驗證，您可以使用 hello az 登入的命令，而不需提供 hello-u 參數。</span><span class="sxs-lookup"><span data-stu-id="ba54c-146">If your user account has Multi factor authentication enabled, you can use hello az login command without providing hello -u parameter.</span></span> <span data-ttu-id="ba54c-147">執行 hello 命令可讓您 URL，您必須使用 tooauthenticate 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba54c-147">Running hello command gives you a URL and a code that you must use tooauthenticate.</span></span>
   
   * <span data-ttu-id="ba54c-148">以登入**服務主體**： 登入，才能[建立服務主體 hello Azure 入口網站透過](azure-stack-create-service-principals.md)或 CLI 並將其指派角色。</span><span class="sxs-lookup"><span data-stu-id="ba54c-148">Sign in as a **service principal**: Before you sign in, [Create a service principal through hello Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span></span> <span data-ttu-id="ba54c-149">現在，可以使用下列命令的 hello 登入：</span><span class="sxs-lookup"><span data-stu-id="ba54c-149">Now, log in by using hello following command:</span></span>

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="ba54c-150">測試 hello 連線</span><span class="sxs-lookup"><span data-stu-id="ba54c-150">Test hello connectivity</span></span>

<span data-ttu-id="ba54c-151">既然我們的所有項目有安裝程式，讓我們使用 Azure 堆疊內的 CLI toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="ba54c-151">Now that we've got everything setup, let's use CLI toocreate resources within Azure Stack.</span></span> <span data-ttu-id="ba54c-152">例如，您可以建立應用程式的資源群組，並新增虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ba54c-152">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="ba54c-153">使用下列命令 toocreate 資源群組的 hello 名為"MyResourceGroup 」:</span><span class="sxs-lookup"><span data-stu-id="ba54c-153">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```azurecli
az group create \
  -n MyResourceGroup -l local
```

<span data-ttu-id="ba54c-154">如果成功建立 hello 資源群組，就 hello 前一個命令會輸出下列 hello 新建立之資源屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba54c-154">If hello resource group is created successfully, hello previous command outputs hello following properties of hello newly created resource:</span></span>

![資源群組建立輸出](media/azure-stack-connect-cli/image1.png)

<span data-ttu-id="ba54c-156">有一些已知的問題 Azure 堆疊 toolearn 有關這些問題中使用 CLI 2.0 時，請參閱 hello [Azure 堆疊 CLI 中的已知問題](azure-stack-troubleshooting.md#cli)主題。</span><span class="sxs-lookup"><span data-stu-id="ba54c-156">There are some known issues when using CLI 2.0 in Azure Stack, toolearn about these issues, see hello [Known issues in Azure Stack CLI](azure-stack-troubleshooting.md#cli) topic.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ba54c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba54c-157">Next steps</span></span>

[<span data-ttu-id="ba54c-158">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="ba54c-158">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="ba54c-159">使用 PowerShell 連線</span><span class="sxs-lookup"><span data-stu-id="ba54c-159">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

[<span data-ttu-id="ba54c-160">管理使用者權限</span><span class="sxs-lookup"><span data-stu-id="ba54c-160">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

