---
title: "aaaConnect 應用程式 tooyour 虛擬網路使用 PowerShell"
description: "說明如何 tooconnect tooand 搭配虛擬網路使用 PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="9362b-103">使用 PowerShell 來連線應用程式 tooyour 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9362b-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="9362b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9362b-104">Overview</span></span>
<span data-ttu-id="9362b-105">在 Azure 應用程式服務，您可以連接您的應用程式 （web、 mobile 或應用程式開發介面） tooan Azure 虛擬網路 (VNet) 您的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="9362b-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="9362b-106">這項功能稱為 VNet 整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="9362b-107">hello VNet 整合功能不應與 hello App Service 環境功能，可讓您 toorun 虛擬網路中的 Azure 應用程式服務執行個體產生混淆。</span><span class="sxs-lookup"><span data-stu-id="9362b-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="9362b-108">hello VNet 整合功能具有使用者介面 (UI) hello 新入口網站中，您可以搭配 toointegrate 使用 hello 傳統部署模型或 hello Azure Resource Manager 部署模型所部署的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="9362b-109">如果您想 toolearn 更多關於 hello 功能，請參閱[整合您的應用程式與 Azure 虛擬網路](web-sites-integrate-with-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="9362b-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="9362b-110">本文是不需 toouse hello UI 的方式，但而有關如何使用 PowerShell tooenable 整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="9362b-111">因為每種部署模型的 hello 命令不同，這份文件會具有每種部署模型區段。</span><span class="sxs-lookup"><span data-stu-id="9362b-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="9362b-112">繼續閱讀本文之前，請確定您有︰</span><span class="sxs-lookup"><span data-stu-id="9362b-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="9362b-113">安裝最新的 Azure PowerShell SDK hello。</span><span class="sxs-lookup"><span data-stu-id="9362b-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="9362b-114">您可以將它安裝以 hello Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="9362b-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="9362b-115">在標準或進階 SKU 執行的 Azure App Service 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="9362b-116">傳統虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9362b-116">Classic virtual networks</span></span>
<span data-ttu-id="9362b-117">本節說明使用 hello 傳統部署模型的虛擬網路的三項工作：</span><span class="sxs-lookup"><span data-stu-id="9362b-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="9362b-118">連接應用程式 tooa 預先存在之虛擬網路閘道，而且已設定點對站連線能力。</span><span class="sxs-lookup"><span data-stu-id="9362b-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="9362b-119">更新應用程式的虛擬網路整合資訊。</span><span class="sxs-lookup"><span data-stu-id="9362b-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="9362b-120">中斷連接您的應用程式與虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="9362b-121">連接應用程式 tooa 傳統的 VNet</span><span class="sxs-lookup"><span data-stu-id="9362b-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="9362b-122">tooconnect 應用程式 tooa 的虛擬網路，請依照下列這三個步驟：</span><span class="sxs-lookup"><span data-stu-id="9362b-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="9362b-123">宣告 toohello web 應用程式，它將會加入特定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="9362b-124">hello 應用程式將會產生憑證，您會獲得 toohello 虛擬網路的點對站連線能力。</span><span class="sxs-lookup"><span data-stu-id="9362b-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="9362b-125">上傳 hello web 應用程式憑證 toohello 虛擬網路，然後再擷取 hello 點對站 VPN 封裝 URI。</span><span class="sxs-lookup"><span data-stu-id="9362b-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="9362b-126">更新 hello web 應用程式的虛擬網路連線與 hello 點對站台封裝 URI。</span><span class="sxs-lookup"><span data-stu-id="9362b-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="9362b-127">hello 第一個和第三個步驟是完全可編寫指令碼，但 hello 第二個步驟需要一次性手動動作透過 hello 入口網站或存取 tooperform**放**或**修補**hello 虛擬網路上的動作Azure 資源管理員端點。</span><span class="sxs-lookup"><span data-stu-id="9362b-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="9362b-128">請連絡 Azure 支援 toohave 啟用。</span><span class="sxs-lookup"><span data-stu-id="9362b-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="9362b-129">開始之前，請確定您的傳統虛擬網路已啟用點對站連接並已部署閘道器。</span><span class="sxs-lookup"><span data-stu-id="9362b-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="9362b-130">toocreate hello 閘道，並啟用點對站連線，您需要 toouse hello 入口網站所述在[建立 VPN 閘道][createvpngateway]。</span><span class="sxs-lookup"><span data-stu-id="9362b-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="9362b-131">hello 傳統虛擬網路需要 toobe hello 相同訂用帳戶您應用程式服務計劃要整合該保存 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="9362b-132">設定 Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="9362b-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="9362b-133">使用下列方式，開啟 PowerShell 視窗，並設定您的 Azure 帳戶和訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="9362b-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="9362b-134">該命令會開啟您的 Azure 認證的提示 tooget。</span><span class="sxs-lookup"><span data-stu-id="9362b-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="9362b-135">登入之後，使用下列命令 tooselect hello 想 toouse 的訂用帳戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="9362b-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="9362b-136">請確定您使用的虛擬網路與應用程式服務方案中的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9362b-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="9362b-137">或</span><span class="sxs-lookup"><span data-stu-id="9362b-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="9362b-138">本文中使用的變數</span><span class="sxs-lookup"><span data-stu-id="9362b-138">Variables used in this article</span></span>
<span data-ttu-id="9362b-139">toosimplify 命令，我們會設定**$Configuration** hello 特定組態 PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="9362b-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="9362b-140">以下列參數的 hello 在 PowerShell 中，如下所示設定變數：</span><span class="sxs-lookup"><span data-stu-id="9362b-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="9362b-141">hello 應用程式位置應該在 hello 位置不包含任何空格。</span><span class="sxs-lookup"><span data-stu-id="9362b-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="9362b-142">例如，美國西部是 westus。</span><span class="sxs-lookup"><span data-stu-id="9362b-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="9362b-143">hello 下一個項目會寫入 hello 憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="9362b-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="9362b-144">它應該是您的本機電腦上的可寫入路徑。</span><span class="sxs-lookup"><span data-stu-id="9362b-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="9362b-145">請確定 tooinclude.cer hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="9362b-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="9362b-146">toosee 您設定為何，型別**$Configuration**。</span><span class="sxs-lookup"><span data-stu-id="9362b-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="9362b-147">hello 本節其餘部分，假設您有建立為上述的變數。</span><span class="sxs-lookup"><span data-stu-id="9362b-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="9362b-148">宣告 hello 虛擬網路 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9362b-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="9362b-149">使用下列命令 tootell hello 應用程式，它會使用這個特定的虛擬網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="9362b-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="9362b-150">這會導致 hello 應用程式 toogenerate 必要的憑證：</span><span class="sxs-lookup"><span data-stu-id="9362b-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="9362b-151">如果此命令成功，**$vnet** 中應該有 **Properties** 變數。</span><span class="sxs-lookup"><span data-stu-id="9362b-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="9362b-152">hello**屬性**變數應該包含這兩個憑證指紋和 hello 憑證資料。</span><span class="sxs-lookup"><span data-stu-id="9362b-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="9362b-153">上傳 hello web 應用程式憑證 toohello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9362b-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="9362b-154">每個訂用帳戶和虛擬網路組合都需要執行手動一次性步驟。</span><span class="sxs-lookup"><span data-stu-id="9362b-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="9362b-155">也就是說，如果您要連接訂閱 A tooVirtual 網路 A 中的應用程式，當您將需要 toodo 這個步驟只不論多少應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="9362b-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="9362b-156">如果您要加入新的應用程式 tooanother 虛擬網路，您將需要 toodo 這一次。</span><span class="sxs-lookup"><span data-stu-id="9362b-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="9362b-157">在訂用帳戶中的層級 Azure 應用程式服務，產生的憑證集，而 hello 組 hello 應用程式將會連接到每個虛擬網路，產生一次 hello 這個錯誤的原因。</span><span class="sxs-lookup"><span data-stu-id="9362b-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="9362b-158">hello 憑證將已經設定如果遵循下列步驟，或如果您以 hello 整合相同虛擬網路使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9362b-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="9362b-159">hello 第一個步驟是 toogenerate hello.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="9362b-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="9362b-160">hello 第二個步驟是 tooupload hello.cer 檔案 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="9362b-161">toogenerate hello.cer 檔案，從在 hello hello API 呼叫先前步驟中，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="9362b-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="9362b-162">hello 憑證將在 hello 位置找到的**$Configuration.GeneratedCertificatePath**指定。</span><span class="sxs-lookup"><span data-stu-id="9362b-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="9362b-163">tooupload hello 憑證手動使用 hello [Azure 入口網站][ azureportal]和**瀏覽的虛擬網路 （傳統）** > **的VPN連線** > **點對站** > **管理憑證**。</span><span class="sxs-lookup"><span data-stu-id="9362b-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="9362b-164">從這裡上傳您的憑證。</span><span class="sxs-lookup"><span data-stu-id="9362b-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="9362b-165">Hello 點對站台的套件</span><span class="sxs-lookup"><span data-stu-id="9362b-165">Get hello point-to-site package</span></span>
<span data-ttu-id="9362b-166">hello 中設定虛擬網路連接 web 應用程式上的下一個步驟是 tooget hello 點對站台的套件，並提供它 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="9362b-167">Hello 儲存下列範本 tooa 檔案稱為 GetNetworkPackageUri.json 某處，例如 C:\Azure\Templates\GetNetworkPackageUri.json 您電腦上。</span><span class="sxs-lookup"><span data-stu-id="9362b-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="9362b-168">設定輸入參數：</span><span class="sxs-lookup"><span data-stu-id="9362b-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="9362b-169">呼叫 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="9362b-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="9362b-170">hello 變數**$output。Outputs.packageUri**現在會包含 hello 封裝 URI toobe 指定 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="9362b-171">上傳 hello 點對站台封裝 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="9362b-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="9362b-172">hello 最後一個步驟是 tooprovide hello 應用程式，此套件。</span><span class="sxs-lookup"><span data-stu-id="9362b-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="9362b-173">只要執行 hello 下一個命令：</span><span class="sxs-lookup"><span data-stu-id="9362b-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="9362b-174">如果訊息要求您 tooconfirm 您要覆寫現有的資源，請確定 tooallow 它。</span><span class="sxs-lookup"><span data-stu-id="9362b-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="9362b-175">此命令執行成功之後，您的應用程式現在應該連接的 toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="9362b-176">tooconfirm 成功移 tooyour 應用程式主控台 中，與 hello 下列輸入：</span><span class="sxs-lookup"><span data-stu-id="9362b-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="9362b-177">如果沒有環境變數呼叫 WEBSITE_VNETNAME 具有符合 hello hello 目標虛擬網路名稱的值，所有組態都成功。</span><span class="sxs-lookup"><span data-stu-id="9362b-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="9362b-178">更新傳統 VNet 整合資訊</span><span class="sxs-lookup"><span data-stu-id="9362b-178">Update classic VNet integration information</span></span>
<span data-ttu-id="9362b-179">tooupdate 或重新同步處理您的資訊，只需重複 hello hello 第一個就地建立 hello 整合時，您會遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="9362b-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="9362b-180">這些步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="9362b-180">Those steps are:</span></span>

1. <span data-ttu-id="9362b-181">定義您的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="9362b-181">Define your configuration information.</span></span>
2. <span data-ttu-id="9362b-182">宣告 hello 虛擬網路 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="9362b-183">取得 hello 點對站台的套件。</span><span class="sxs-lookup"><span data-stu-id="9362b-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="9362b-184">上傳 hello 點對站台封裝 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="9362b-185">中斷連接您的應用程式與傳統 VNet</span><span class="sxs-lookup"><span data-stu-id="9362b-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="9362b-186">toodisconnect hello 應用程式，您需要虛擬網路整合期間所設定的 hello 組態資訊。</span><span class="sxs-lookup"><span data-stu-id="9362b-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="9362b-187">使用該資訊，還有然後一個命令 toodisconnect 應用程式從您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="9362b-188">Resource Manager 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9362b-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="9362b-189">Resource Manager 虛擬網路有 Azure Resource Manager API，可簡化某些處理程序 (相較於傳統虛擬網路)。</span><span class="sxs-lookup"><span data-stu-id="9362b-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="9362b-190">我們有一個指令碼，可協助您完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="9362b-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="9362b-191">建立 Resource Manager 虛擬網路並您的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="9362b-192">建立閘道器，在既存的 Resource Manager 虛擬網路中設定點對站連接，然後與您的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="9362b-193">將您的應用程式與已啟用閘道器和點對站連接的既存 Resource Manager 虛擬網路整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="9362b-194">中斷連接您的應用程式與虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="9362b-195">Resource Manager VNet App Service 整合指令碼</span><span class="sxs-lookup"><span data-stu-id="9362b-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="9362b-196">複製下列指令碼，並將它儲存 tooa 檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="9362b-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="9362b-197">如果您不想 toouse hello 指令碼，則可以從它的免費 toolearn toosee 如何 tooset 進行與資源管理員的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="9362b-198">將儲存一份 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9362b-198">Save a copy of hello script.</span></span> <span data-ttu-id="9362b-199">在本文中，其名稱為 V2VnetAllinOne.ps1，但您可以使用其他名稱。</span><span class="sxs-lookup"><span data-stu-id="9362b-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="9362b-200">此指令碼沒有引數。</span><span class="sxs-lookup"><span data-stu-id="9362b-200">There are no arguments for this script.</span></span> <span data-ttu-id="9362b-201">您只需要執行它。</span><span class="sxs-lookup"><span data-stu-id="9362b-201">You simply run it.</span></span> <span data-ttu-id="9362b-202">hello 首先 hello 指令碼會執行會提示您 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="9362b-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="9362b-203">登入之後，hello 指令碼會取得您的帳戶相關的詳細資料，並傳回訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="9362b-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="9362b-204">不計算 hello 要求您提供認證，執行 hello 初始的指令碼看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="9362b-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="9362b-205">示範訂用帳戶 (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="9362b-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="9362b-206">MS 測試 (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="9362b-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="9362b-207">紫色示範訂用帳戶 (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="9362b-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="9362b-208">選擇選項：3</span><span class="sxs-lookup"><span data-stu-id="9362b-208">Choose an option: 3</span></span>

    <span data-ttu-id="9362b-209">帳戶      : ccompy@microsoft.com 環境      : AzureCloud 訂用帳戶: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d 租用戶       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="9362b-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="9362b-210">請輸入您的應用程式的資源群組 hello: hcdemo rg 請輸入 hello 應用程式名稱： v2vnetpowershell 您該怎麼想 toodo？</span><span class="sxs-lookup"><span data-stu-id="9362b-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="9362b-211">加入新的虛擬網路 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="9362b-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="9362b-212">加入現有的虛擬網路 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="9362b-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="9362b-213">從應用程式移除虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9362b-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="9362b-214">hello 本章節的其餘部分將說明這些三個選項。</span><span class="sxs-lookup"><span data-stu-id="9362b-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="9362b-215">建立 Resource Manager VNet 並與其整合</span><span class="sxs-lookup"><span data-stu-id="9362b-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="9362b-216">新的虛擬網路使用 hello Resource Manager 部署模型，並將其整合應用程式，選取 toocreate **1) 加入應用程式的新的虛擬網路 tooan**。</span><span class="sxs-lookup"><span data-stu-id="9362b-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="9362b-217">這會提示您輸入 hello hello 虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="9362b-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="9362b-218">在這個案例中，如 hello 下列設定，我使用 v2pshell hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9362b-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="9362b-219">hello 指令碼會為 hello hello 正在建立的虛擬網路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9362b-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="9362b-220">如果我想，我可以變更任何 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9362b-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="9362b-221">在此範例執行時，我建立的虛擬網路，具有下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="9362b-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="9362b-222">如果您想要 toochange 任何 hello 值**Y** hello 變更。</span><span class="sxs-lookup"><span data-stu-id="9362b-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="9362b-223">當您滿意 hello 虛擬網路設定時，請輸入**N**或是直接按 Enter，當系統提示您需變更 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="9362b-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="9362b-224">從上到完成為止，hello 指令碼將會告訴您一些決定其 ' i 執行直到它啟動 toocreate hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9362b-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="9362b-225">該步驟可能會佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="9362b-225">That step can take up tooan hour.</span></span> <span data-ttu-id="9362b-226">在這個階段中，沒有任何進度列指示器，但是 hello 指令碼會讓您知道何時建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="9362b-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="9362b-227">Hello 指令碼完成時，它會顯示**已經完成**。</span><span class="sxs-lookup"><span data-stu-id="9362b-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="9362b-228">此時，您將有資源管理員的虛擬網路，hello 名稱與您選取的設定。</span><span class="sxs-lookup"><span data-stu-id="9362b-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="9362b-229">這個新的虛擬網路也會與您的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="9362b-230">將您的應用程式與既存的 Resource Manager VNet 整合</span><span class="sxs-lookup"><span data-stu-id="9362b-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="9362b-231">當您正在整合與預先存在的虛擬網路，如果您提供資源管理員的虛擬網路沒有閘道或點對站連線能力時，hello 指令碼會設定的。</span><span class="sxs-lookup"><span data-stu-id="9362b-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="9362b-232">如果 hello VNET 中已經有設定這些項目，hello 指令碼也會直接 toohello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="9362b-233">toostart 此程序，只需選取**2) 加入現有的虛擬網路 tooan 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9362b-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="9362b-234">此選項只適用於您有預先存在的資源管理員虛擬網路中 hello 與您的應用程式相同的訂閱。</span><span class="sxs-lookup"><span data-stu-id="9362b-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="9362b-235">您選取 hello 選項之後，您會顯示您的資源管理員虛擬網路的清單。</span><span class="sxs-lookup"><span data-stu-id="9362b-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="9362b-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="9362b-236">v2demonetwork</span></span>
    2) <span data-ttu-id="9362b-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="9362b-237">v2pshell</span></span>
    3) <span data-ttu-id="9362b-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="9362b-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="9362b-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="9362b-239">v2asenetwork</span></span>
    5) <span data-ttu-id="9362b-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="9362b-240">v2pshell2</span></span>

    <span data-ttu-id="9362b-241">選擇選項：5</span><span class="sxs-lookup"><span data-stu-id="9362b-241">Choose an option: 5</span></span>

<span data-ttu-id="9362b-242">只要選取您想要使用 toointegrate hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="9362b-243">如果您已經有具有已啟用點對站連線的閘道，hello 指令碼將會直接與虛擬網路整合您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9362b-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="9362b-244">如果您沒有閘道，您將需要 toospecify hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="9362b-245">您的閘道器子網路必須位於您的虛擬網路位址空間，而且它不能在任何其他子網路中。</span><span class="sxs-lookup"><span data-stu-id="9362b-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="9362b-246">如果您的虛擬網路沒有閘道器且您執行此步驟，則結果如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9362b-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="9362b-247">在此範例中，建立虛擬網路閘道具有 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="9362b-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="9362b-248">如果您想要 toochange 任何這些設定，您可以這樣做。</span><span class="sxs-lookup"><span data-stu-id="9362b-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="9362b-249">否則，請按下 Enter，hello 指令碼將會建立您的閘道，並附加您的應用程式 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="9362b-250">hello 閘道建立時間仍然是一小時，不過，因此請確定您記住。</span><span class="sxs-lookup"><span data-stu-id="9362b-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="9362b-251">當所有項目完成時，會顯示 hello 指令碼**已經完成**。</span><span class="sxs-lookup"><span data-stu-id="9362b-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="9362b-252">中斷連接您的應用程式與 Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="9362b-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="9362b-253">從您的虛擬網路中斷連接您的應用程式不會使 hello 閘道中斷或停用 點對站連線能力。</span><span class="sxs-lookup"><span data-stu-id="9362b-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="9362b-254">畢竟，您可能將它使用於其他項目。</span><span class="sxs-lookup"><span data-stu-id="9362b-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="9362b-255">它也不會中斷它 hello 以外的任何其他應用程式從您提供的其中一個。</span><span class="sxs-lookup"><span data-stu-id="9362b-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="9362b-256">tooperform 此動作，選取**3) 移除應用程式的虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="9362b-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="9362b-257">在您這麼做時，您會看到如下的畫面：</span><span class="sxs-lookup"><span data-stu-id="9362b-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="9362b-258">雖然 hello 指令碼說明刪除，但它不會刪除 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9362b-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="9362b-259">它只移除 hello 整合。</span><span class="sxs-lookup"><span data-stu-id="9362b-259">It’s just removing hello integration.</span></span> <span data-ttu-id="9362b-260">這是您想要確認之後 toodo，hello 命令相當快速地進行處理，並告訴您**True**完成時。</span><span class="sxs-lookup"><span data-stu-id="9362b-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
