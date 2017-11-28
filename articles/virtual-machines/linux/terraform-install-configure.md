---
title: "aaaInstall 和在 Azure 中設定 Terraform tooprovision Vm 和其他基礎結構 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定 Terraform toocreate Azure 資源"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="db73a-103">安裝和設定 Terraform tooprovision Vm 和其他基礎結構至 Azure</span><span class="sxs-lookup"><span data-stu-id="db73a-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="db73a-104">本文描述 hello 必要步驟 tooinstall，並將 Terraform tooprovision 資源，例如虛擬機器設定到 Azure。</span><span class="sxs-lookup"><span data-stu-id="db73a-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="db73a-105">您將學習如何 toocreate 與使用 Azure 認證 tooenable Terraform tooprovision 雲端資源以安全的方式。</span><span class="sxs-lookup"><span data-stu-id="db73a-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="db73a-106">HashiCorp Terraform 提供簡單的方式 toodefine，並使用稱為 HashiCorp 設定語言 (HCL) 的自訂範本化語言部署雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="db73a-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="db73a-107">這個自訂的語言是[輕鬆 toowrite 和輕鬆 toounderstand](terraform-create-complete-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="db73a-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="db73a-108">此外，透過 hello`terraform plan`命令時，您在認可之前，您可以視覺化 hello 變更 tooyour 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="db73a-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="db73a-109">請遵循這些步驟 toostart，搭配 Azure 使用 Terraform。</span><span class="sxs-lookup"><span data-stu-id="db73a-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="db73a-110">安裝 Terraform</span><span class="sxs-lookup"><span data-stu-id="db73a-110">Install Terraform</span></span>
<span data-ttu-id="db73a-111">tooinstall Terraform，[下載](https://www.terraform.io/downloads.html)hello 封裝適用於您的作業系統，到個別的安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="db73a-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="db73a-112">hello 下載項目包含單一的可執行檔，您也應該為其定義通用的路徑。</span><span class="sxs-lookup"><span data-stu-id="db73a-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="db73a-113">如需 tooset 如何 hello 路徑在 Linux 和 Mac 上的指示，請移過[此網頁](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux)。</span><span class="sxs-lookup"><span data-stu-id="db73a-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="db73a-114">如需 tooset hello 在 Windows 上，路徑的方式的指示，請移過[此網頁](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)。</span><span class="sxs-lookup"><span data-stu-id="db73a-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="db73a-115">tooverify 您的安裝，請執行 hello`terraform`命令。</span><span class="sxs-lookup"><span data-stu-id="db73a-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="db73a-116">您應該會在輸出看到一份可用的 Terraform 選項清單。</span><span class="sxs-lookup"><span data-stu-id="db73a-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="db73a-117">接下來，您需要 tooallow Terraform 存取 tooyour Azure 訂用帳戶 tooperform 基礎結構佈建。</span><span class="sxs-lookup"><span data-stu-id="db73a-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="db73a-118">設定 Terraform 存取 tooAzure</span><span class="sxs-lookup"><span data-stu-id="db73a-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="db73a-119">tooenable Terraform tooprovision 至 Azure 資源，您需要 toocreate Azure Active Directory (Azure AD) 中的兩個實體： Azure AD 應用程式與 Azure AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="db73a-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="db73a-120">然後，您可以在 Terraform 指令碼中使用這些實體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="db73a-121">服務主體是全域 Azure AD 應用程式的本機執行個體。</span><span class="sxs-lookup"><span data-stu-id="db73a-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="db73a-122">服務主體可讓本機細微的存取控制 tooglobal 資源。</span><span class="sxs-lookup"><span data-stu-id="db73a-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="db73a-123">有數種方式 toocreate Azure AD 應用程式和 Azure AD 服務主體。</span><span class="sxs-lookup"><span data-stu-id="db73a-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="db73a-124">hello 最簡單且最快方式現今是 toouse Azure CLI 2.0 中，其中[您可以下載並安裝在 Windows、 Linux 或 Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="db73a-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="db73a-125">您也可以使用 PowerShell 或 Azure CLI 1.0 toocreate hello 必要的安全性基礎結構。</span><span class="sxs-lookup"><span data-stu-id="db73a-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="db73a-126">接下來的 hello 指示告訴您如何使用這些方法的所有 tooconfigure Terraform azure。</span><span class="sxs-lookup"><span data-stu-id="db73a-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="db73a-127">使用 Azure CLI 2.0 (適用於 Windows、Linux 或 Mac 使用者)</span><span class="sxs-lookup"><span data-stu-id="db73a-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="db73a-128">下載並安裝 hello 之後[Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)，登入 tooadminister 您 Azure 訂用帳戶發出下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="db73a-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="db73a-129">如果您使用 hello 中國、 Azure 德國或 Azure 政府雲端，您需要 toofirst hello Azure CLI toowork 設定與該雲端。</span><span class="sxs-lookup"><span data-stu-id="db73a-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="db73a-130">您可以執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="db73a-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="db73a-131">如果您有多個 Azure 訂用帳戶，其詳細資料會由 hello`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="db73a-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="db73a-132">設定 hello `SUBSCRIPTION_ID` hello 的環境變數 toohold hello 值傳回`id`hello 訂用帳戶的欄位想 toouse。</span><span class="sxs-lookup"><span data-stu-id="db73a-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="db73a-133">設定此工作階段需 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db73a-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="db73a-134">查詢 hello 帳戶 tooget hello 訂用帳戶 ID 和租用戶的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="db73a-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="db73a-135">接下來，為 Terraform 建立不同的認證。</span><span class="sxs-lookup"><span data-stu-id="db73a-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="db73a-136">會傳回您的 appId、密碼、sp_name 和租用戶。</span><span class="sxs-lookup"><span data-stu-id="db73a-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="db73a-137">請記下 hello appId 和密碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="db73a-138">tooconfirm 您的認證 （服務主體），開啟新的殼層並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="db73a-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="db73a-139">傳回值 sp_name、 密碼及租用戶的替代 hello:</span><span class="sxs-lookup"><span data-stu-id="db73a-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="db73a-140">使用 PowerShell (適用於 Windows 使用者)</span><span class="sxs-lookup"><span data-stu-id="db73a-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="db73a-141">toouse Windows 電腦 toowrite 並執行您 Terraform 指令碼和組態工作 toouse PowerShell 設定您的電腦與 hello 權限的 PowerShell 工具。</span><span class="sxs-lookup"><span data-stu-id="db73a-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="db73a-142">中的 hello 步驟來安裝 PowerShell tools[安裝和設定 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="db73a-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="db73a-143">下載並執行 hello [azure setup.ps1 指令碼](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1)從 hello PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="db73a-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="db73a-144">toorun hello azure setup.ps1 指令碼中，下載並執行 hello`./azure-setup.ps1 setup`命令從 hello PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="db73a-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="db73a-145">然後登入 tooyour 具有系統管理權限的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db73a-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="db73a-146">出現提示時，提供應用程式名稱 (任意字串，必填)。</span><span class="sxs-lookup"><span data-stu-id="db73a-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="db73a-147">出現提示時，選擇性提供強式密碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="db73a-148">如果您未提供密碼，則會使用 .NET 安全性程式庫為您產生強式密碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="db73a-149">使用 Azure CLI 1.0 (適用於 Linux 或 Mac 使用者)</span><span class="sxs-lookup"><span data-stu-id="db73a-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="db73a-150">tooget 入門 Terraform Linux 機器上使用 Azure CLI 1.0 的 Mac 電腦上安裝 hello 適當庫。</span><span class="sxs-lookup"><span data-stu-id="db73a-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="db73a-151">中的 hello 步驟來安裝 Azure xPlat CLI 工具[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="db73a-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="db73a-152">下載並安裝 JSON 處理器中的 hello 指示[下載 jq](https://stedolan.github.io/jq/download/)。</span><span class="sxs-lookup"><span data-stu-id="db73a-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="db73a-153">下載並執行 hello [azure setup.sh 指令碼](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh)撞 hello 主控台從指令碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="db73a-154">toorun hello azure setup.sh 指令碼中，下載並執行 hello `./azure-setup setup` hello 主控台命令。</span><span class="sxs-lookup"><span data-stu-id="db73a-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="db73a-155">然後登入 tooyour 具有系統管理權限的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db73a-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="db73a-156">出現提示時，提供應用程式名稱 (任意字串，必填)。</span><span class="sxs-lookup"><span data-stu-id="db73a-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="db73a-157">出現提示時，選擇性提供強式密碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="db73a-158">如果您未提供密碼，則會使用 .NET 安全性程式庫為您產生強式密碼。</span><span class="sxs-lookup"><span data-stu-id="db73a-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="db73a-159">所有的 hello 前一個指令碼建立 Azure AD 應用程式和服務主體。</span><span class="sxs-lookup"><span data-stu-id="db73a-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="db73a-160">hello 服務主體取得 hello 訂用帳戶上的參與者或擁有者層級存取。</span><span class="sxs-lookup"><span data-stu-id="db73a-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="db73a-161">因為 hello 高層級的授與存取權，您應該一律保護 hello 這些指令碼所產生的安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="db73a-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="db73a-162">記下那些指令碼所提供的四個安全性資訊：appId、密碼、subscription_id 和 tenant_id。</span><span class="sxs-lookup"><span data-stu-id="db73a-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="db73a-163">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="db73a-163">Set environment variables</span></span>
<span data-ttu-id="db73a-164">您建立及設定 Azure AD 服務主體之後，您會需要 toolet Terraform 知道 hello 租用戶識別碼、 訂用帳戶 ID、 用戶端識別碼和用戶端秘密 toouse。</span><span class="sxs-lookup"><span data-stu-id="db73a-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="db73a-165">您可以如[使用 Terraform 建立基本基礎結構](terraform-create-complete-vm.md)所述，在 Terraform 指令碼中內嵌這些值來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="db73a-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="db73a-166">或者，您可以設定下列環境變數的 hello （並因此避免不小心簽入，或共用您的認證）：</span><span class="sxs-lookup"><span data-stu-id="db73a-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="db73a-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="db73a-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="db73a-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="db73a-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="db73a-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="db73a-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="db73a-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="db73a-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="db73a-171">您可以使用這個範例的殼層指令碼 tooset 這些變數：</span><span class="sxs-lookup"><span data-stu-id="db73a-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="db73a-172">此外，如果您使用 Terraform 搭配 Azure 在中國或可能是 Azure 政府或德國 Azure 時，您需要 tooset hello 環境變數適當。</span><span class="sxs-lookup"><span data-stu-id="db73a-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db73a-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db73a-173">Next steps</span></span>
<span data-ttu-id="db73a-174">您現在已安裝 Terraform 並設定 Azure 認證，可以開始將基礎結構部署到您的 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="db73a-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="db73a-175">接下來，了解如何太[建立基礎結構與 Terraform](terraform-create-complete-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="db73a-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
