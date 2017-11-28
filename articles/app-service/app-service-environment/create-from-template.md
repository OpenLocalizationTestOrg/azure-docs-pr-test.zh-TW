---
title: "aaaCreate Azure App Service 環境使用資源管理員範本"
description: "說明如何使用資源管理員範本的外部或 ILB Azure App Service 環境 toocreate"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="6eea6-103">使用 Azure Resource Manager 範本立 ASE</span><span class="sxs-lookup"><span data-stu-id="6eea6-103">Create an ASE by using an Azure Resource Manager template</span></span>

## <a name="overview"></a><span data-ttu-id="6eea6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6eea6-104">Overview</span></span>
<span data-ttu-id="6eea6-105">Azure App Service Environment (ASE) 可以使用網際網路可存取端點，或是 Azure 虛擬網路 (VNet) 中內部位址上的端點來建立。</span><span class="sxs-lookup"><span data-stu-id="6eea6-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span></span> <span data-ttu-id="6eea6-106">使用內部端點建立時，該端點是由稱為內部負載平衡器 (ILB) 的 Azure 元件提供。</span><span class="sxs-lookup"><span data-stu-id="6eea6-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span></span> <span data-ttu-id="6eea6-107">內部 IP 位址上 hello ASE 稱為 ILB ase。</span><span class="sxs-lookup"><span data-stu-id="6eea6-107">hello ASE on an internal IP address is called an ILB ASE.</span></span> <span data-ttu-id="6eea6-108">hello ASE 與公用端點會呼叫外部 ase。</span><span class="sxs-lookup"><span data-stu-id="6eea6-108">hello ASE with a public endpoint is called an External ASE.</span></span> 

<span data-ttu-id="6eea6-109">Ase 中可以建立使用 hello Azure 入口網站或 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6eea6-109">An ASE can be created by using hello Azure portal or an Azure Resource Manager template.</span></span> <span data-ttu-id="6eea6-110">本文逐步解說 hello 步驟和所需的資源管理員範本 toocreate 外部 ASE 或 ILB ASE 語法。</span><span class="sxs-lookup"><span data-stu-id="6eea6-110">This article walks through hello steps and syntax you need toocreate an External ASE or ILB ASE with Resource Manager templates.</span></span> <span data-ttu-id="6eea6-111">toolearn toocreate ASE hello Azure 入口網站中的看到如何[進行外部 ASE] [ MakeExternalASE]或[進行 ILB ASE][MakeILBASE]。</span><span class="sxs-lookup"><span data-stu-id="6eea6-111">toolearn how toocreate an ASE in hello Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="6eea6-112">當您建立 ASE hello Azure 入口網站中時，您可以在相同的時間，或選擇到預先存在的 VNet toodeploy hello 建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="6eea6-112">When you create an ASE in hello Azure portal, you can create your VNet at hello same time or choose a preexisting VNet toodeploy into.</span></span> <span data-ttu-id="6eea6-113">從範本建立 ASE 時，必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="6eea6-113">When you create an ASE from a template, you must start with:</span></span> 

* <span data-ttu-id="6eea6-114">Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="6eea6-114">A Resource Manager VNet.</span></span>
* <span data-ttu-id="6eea6-115">該 VNet 中的子網路。</span><span class="sxs-lookup"><span data-stu-id="6eea6-115">A subnet in that VNet.</span></span> <span data-ttu-id="6eea6-116">我們建議的 ASE 子網路大小`/25`128 位址 tooaccomodate 未來成長使用。</span><span class="sxs-lookup"><span data-stu-id="6eea6-116">We recommend an ASE subnet size of `/25` with 128 addresses tooaccomodate future growth.</span></span> <span data-ttu-id="6eea6-117">建立 hello ASE 之後，您無法變更 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="6eea6-117">After hello ASE is created, you can't change hello size.</span></span>
* <span data-ttu-id="6eea6-118">從您的 VNet hello 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="6eea6-118">hello resource ID from your VNet.</span></span> <span data-ttu-id="6eea6-119">在虛擬網路內容 下，您可以從 hello Azure 入口網站取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="6eea6-119">You can get this information from hello Azure portal under your virtual network properties.</span></span>
* <span data-ttu-id="6eea6-120">您想成 toodeploy 的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6eea6-120">hello subscription you want toodeploy into.</span></span>
* <span data-ttu-id="6eea6-121">您想成 toodeploy hello 位置。</span><span class="sxs-lookup"><span data-stu-id="6eea6-121">hello location you want toodeploy into.</span></span>

<span data-ttu-id="6eea6-122">tooautomate ASE 建立：</span><span class="sxs-lookup"><span data-stu-id="6eea6-122">tooautomate your ASE creation:</span></span>

1. <span data-ttu-id="6eea6-123">從範本建立 hello ASE。</span><span class="sxs-lookup"><span data-stu-id="6eea6-123">Create hello ASE from a template.</span></span> <span data-ttu-id="6eea6-124">如果是建立外部 ASE，完成此步驟就建立完成。</span><span class="sxs-lookup"><span data-stu-id="6eea6-124">If you create an External ASE, you're finished after this step.</span></span> <span data-ttu-id="6eea6-125">如果您建立 ILB ase 中，有幾個的多個項目 toodo。</span><span class="sxs-lookup"><span data-stu-id="6eea6-125">If you create an ILB ASE, there are a few more things toodo.</span></span>

2. <span data-ttu-id="6eea6-126">建立 ILB ASE 之後，會上傳與您的 ILB ASE 網域相符的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span></span>

3. <span data-ttu-id="6eea6-127">hello 已上傳的 SSL 憑證指派 toohello ILB ASE 做為其 「 預設 」 的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-127">hello uploaded SSL certificate is assigned toohello ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="6eea6-128">此憑證用於 SSL 流量 tooapps hello ILB ASE 上，使用 hello 一般根網域的指派的 toohello ASE (例如，https://someapp.mycustomrootcomain.com) 時。</span><span class="sxs-lookup"><span data-stu-id="6eea6-128">This certificate is used for SSL traffic tooapps on hello ILB ASE when they use hello common root domain that's assigned toohello ASE (for example, https://someapp.mycustomrootcomain.com).</span></span>


## <a name="create-hello-ase"></a><span data-ttu-id="6eea6-129">建立 hello ASE</span><span class="sxs-lookup"><span data-stu-id="6eea6-129">Create hello ASE</span></span>
<span data-ttu-id="6eea6-130">在 GitHub 上的[範例][quickstartasev2create]中有可建立 ASE 的 Resource Manager 範本及其相關聯的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span></span>

<span data-ttu-id="6eea6-131">如果您想 toomake ILB ase 中，使用這些資源管理員範本[範例][quickstartilbasecreate]。</span><span class="sxs-lookup"><span data-stu-id="6eea6-131">If you want toomake an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span></span> <span data-ttu-id="6eea6-132">它們，符合 toothat 使用案例。</span><span class="sxs-lookup"><span data-stu-id="6eea6-132">They cater toothat use case.</span></span> <span data-ttu-id="6eea6-133">大部分的 hello 參數在 hello *azuredeploy.parameters.json*檔案是常見 toohello 建立 ILB ASEs 和外部 ASEs。</span><span class="sxs-lookup"><span data-stu-id="6eea6-133">Most of hello parameters in hello *azuredeploy.parameters.json* file are common toohello creation of ILB ASEs and External ASEs.</span></span> <span data-ttu-id="6eea6-134">hello 表呼叫參數的特殊附註，或獨有的當您建立 ILB ase 中：</span><span class="sxs-lookup"><span data-stu-id="6eea6-134">hello following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span></span>

* <span data-ttu-id="6eea6-135">*interalLoadBalancingMode*： 在大部分情況下，設定此 too3，這表示這兩個連接埠 80/443 上的 HTTP/HTTPS 流量，及 hello 控制項/資料通道連接埠上 hello ASE tooby hello FTP 服務該通訊埠，您將繫結的 tooan ILB 配置的虛擬網路內部位址。</span><span class="sxs-lookup"><span data-stu-id="6eea6-135">*interalLoadBalancingMode*: In most cases, set this too3, which means both HTTP/HTTPS traffic on ports 80/443, and hello control/data channel ports listened tooby hello FTP service on hello ASE, will be bound tooan ILB-allocated virtual network internal address.</span></span> <span data-ttu-id="6eea6-136">如果這個屬性設定 too2，只有 hello FTP 服務的相關連接埠 （控制和資料通道） 是繫結的 tooan ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="6eea6-136">If this property is set too2, only hello FTP service-related ports (both control and data channels) are bound tooan ILB address.</span></span> <span data-ttu-id="6eea6-137">hello HTTP/HTTPS 流量會保留在 hello 公用 VIP。</span><span class="sxs-lookup"><span data-stu-id="6eea6-137">hello HTTP/HTTPS traffic remains on hello public VIP.</span></span>
* <span data-ttu-id="6eea6-138">*dns 尾碼*： 這個參數會定義會指派的 toohello ASE hello 預設根網域。</span><span class="sxs-lookup"><span data-stu-id="6eea6-138">*dnsSuffix*: This parameter defines hello default root domain that's assigned toohello ASE.</span></span> <span data-ttu-id="6eea6-139">在 Azure App Service hello 公用種變化，hello 預設根網域的所有 web 應用程式是*.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="6eea6-139">In hello public variation of Azure App Service, hello default root domain for all web apps is *azurewebsites.net*.</span></span> <span data-ttu-id="6eea6-140">由於 ILB ASE 內部 tooa 客戶虛擬網路，就沒有任何意義 toouse hello 公開服務的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="6eea6-140">Because an ILB ASE is internal tooa customer's virtual network, it doesn't make sense toouse hello public service's default root domain.</span></span> <span data-ttu-id="6eea6-141">相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="6eea6-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span> <span data-ttu-id="6eea6-142">例如，Contoso Corporation 可能會使用預設的根網域的*內部 contoso.com*針對預定的 toobe 解析與只能在 Contoso 虛擬網路中存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eea6-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended toobe resolvable and accessible only within Contoso's virtual network.</span></span> 
* <span data-ttu-id="6eea6-143">*ipSslAddressCount*： 這個參數會自動預設為 tooa 中的數值 0 hello *azuredeploy.json*檔案，因為 ILB ASEs 只能有單一的 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="6eea6-143">*ipSslAddressCount*: This parameter automatically defaults tooa value of 0 in hello *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span> <span data-ttu-id="6eea6-144">ILB ASE 沒有明確的 IP-SSL 位址。</span><span class="sxs-lookup"><span data-stu-id="6eea6-144">There are no explicit IP-SSL addresses for an ILB ASE.</span></span> <span data-ttu-id="6eea6-145">因此，hello ILB ase 中的 IP SSL 位址集區必須設定 toozero。</span><span class="sxs-lookup"><span data-stu-id="6eea6-145">Hence, hello IP-SSL address pool for an ILB ASE must be set toozero.</span></span> <span data-ttu-id="6eea6-146">否則，就會發生佈建錯誤。</span><span class="sxs-lookup"><span data-stu-id="6eea6-146">Otherwise, a provisioning error occurs.</span></span> 

<span data-ttu-id="6eea6-147">之後 hello *azuredeploy.parameters.json*檔案填滿，請建立 hello ASE 利用 hello PowerShell 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6eea6-147">After hello *azuredeploy.parameters.json* file is filled in, create hello ASE by using hello PowerShell code snippet.</span></span> <span data-ttu-id="6eea6-148">變更 hello 檔案路徑 toomatch hello 資源管理員範本檔案位置在電腦上。</span><span class="sxs-lookup"><span data-stu-id="6eea6-148">Change hello file paths toomatch hello Resource Manager template-file locations on your machine.</span></span> <span data-ttu-id="6eea6-149">請記住 toosupply 您自己的值為 hello 資源管理員部署名稱和 hello 資源群組名稱：</span><span class="sxs-lookup"><span data-stu-id="6eea6-149">Remember toosupply your own values for hello Resource Manager deployment name and hello resource group name:</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="6eea6-150">它會建立 hello ASE toobe 一小時。</span><span class="sxs-lookup"><span data-stu-id="6eea6-150">It takes about an hour for hello ASE toobe created.</span></span> <span data-ttu-id="6eea6-151">然後 hello ASE 顯示 hello ASEs 觸發 hello 部署的 hello 訂閱 hello 清單中的入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6eea6-151">Then hello ASE shows up in hello portal in hello list of ASEs for hello subscription that triggered hello deployment.</span></span>

## <a name="upload-and-configure-hello-default-ssl-certificate"></a><span data-ttu-id="6eea6-152">上傳和設定 hello 「 預設 」 的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6eea6-152">Upload and configure hello "default" SSL certificate</span></span>
<span data-ttu-id="6eea6-153">會使用的 tooestablish SSL 連線 tooapps hello 「 預設 」 SSL 憑證，必須是與 hello ASE 相關聯的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-153">An SSL certificate must be associated with hello ASE as hello "default" SSL certificate that's used tooestablish SSL connections tooapps.</span></span> <span data-ttu-id="6eea6-154">如果 hello ASE 的預設 DNS 尾碼是*內部 contoso.com*，連線 toohttps://some-random-app.internal-contoso.com 需要有效的 SSL 憑證 **.internal contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="6eea6-154">If hello ASE's default DNS suffix is *internal-contoso.com*, a connection toohttps://some-random-app.internal-contoso.com requires an SSL certificate that's valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="6eea6-155">使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證，取得有效的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span></span> <span data-ttu-id="6eea6-156">不論 hello 來源 hello SSL 憑證，必須適當設定下列憑證屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="6eea6-156">Regardless of hello source of hello SSL certificate, hello following certificate attributes must be configured properly:</span></span>

* <span data-ttu-id="6eea6-157">**主旨**： 此屬性必須設定得 **.your 根網域-here.com*。</span><span class="sxs-lookup"><span data-stu-id="6eea6-157">**Subject**: This attribute must be set too**.your-root-domain-here.com*.</span></span>
* <span data-ttu-id="6eea6-158">**Subject Alternative Name**此屬性必須同時包含 *.your-root-domain-here.com 和 *.scm.your-root-domain-here.com。與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello 使用 hello 表單的位址*your-app-name.scm.your-root-domain-here.com*。</span><span class="sxs-lookup"><span data-stu-id="6eea6-158">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here.com* and **.scm.your-root-domain-here.com*. SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="6eea6-159">備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。</span><span class="sxs-lookup"><span data-stu-id="6eea6-159">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span> <span data-ttu-id="6eea6-160">轉換/儲存為.pfx 檔案 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-160">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="6eea6-161">請記住該 hello.pfx 檔案必須包含所有中繼和根憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-161">Remember that hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="6eea6-162">使用密碼保護其安全。</span><span class="sxs-lookup"><span data-stu-id="6eea6-162">Secure it with a password.</span></span>

<span data-ttu-id="6eea6-163">toobe 轉換成 base64 字串 hello 的 SSL 憑證上傳使用資源管理員範本，因為需要 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-163">hello .pfx file needs toobe converted into a base64 string because hello SSL certificate is uploaded by using a Resource Manager template.</span></span> <span data-ttu-id="6eea6-164">因為資源管理員範本檔案是文字檔，hello.pfx 檔必須轉換成 base64 字串。</span><span class="sxs-lookup"><span data-stu-id="6eea6-164">Because Resource Manager templates are text files, hello .pfx file must be converted into a base64 string.</span></span> <span data-ttu-id="6eea6-165">如此一來，它可以包含為 hello 範本的參數。</span><span class="sxs-lookup"><span data-stu-id="6eea6-165">This way it can be included as a parameter of hello template.</span></span>

<span data-ttu-id="6eea6-166">使用下列 PowerShell 程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="6eea6-166">Use hello following PowerShell code snippet to:</span></span>

* <span data-ttu-id="6eea6-167">產生自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-167">Generate a self-signed certificate.</span></span>
* <span data-ttu-id="6eea6-168">Hello 憑證匯出為.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-168">Export hello certificate as a .pfx file.</span></span>
* <span data-ttu-id="6eea6-169">轉換為 base64 編碼的字串中的 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-169">Convert hello .pfx file into a base64-encoded string.</span></span>
* <span data-ttu-id="6eea6-170">儲存 hello base64 編碼字串 tooa 個別檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-170">Save hello base64-encoded string tooa separate file.</span></span> 

<span data-ttu-id="6eea6-171">此為 base64 編碼的 PowerShell 程式碼是來自 hello [PowerShell 指令碼的部落格][examplebase64encoding]:</span><span class="sxs-lookup"><span data-stu-id="6eea6-171">This PowerShell code for base64 encoding was adapted from hello [PowerShell scripts blog][examplebase64encoding]:</span></span>

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="6eea6-172">Hello SSL 憑證已成功產生，並轉換 tooa base64 編碼字串之後，使用 hello 範例 Resource Manager 範本[設定 hello 預設 SSL 憑證][ quickstartconfiguressl] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="6eea6-172">After hello SSL certificate is successfully generated and converted tooa base64-encoded string, use hello example Resource Manager template [Configure hello default SSL certificate][quickstartconfiguressl] on GitHub.</span></span> 

<span data-ttu-id="6eea6-173">hello 參數在 hello *azuredeploy.parameters.json*檔案如下：</span><span class="sxs-lookup"><span data-stu-id="6eea6-173">hello parameters in hello *azuredeploy.parameters.json* file are listed here:</span></span>

* <span data-ttu-id="6eea6-174">*appServiceEnvironmentName*: hello 的 hello ILB ASE 正在設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6eea6-174">*appServiceEnvironmentName*: hello name of hello ILB ASE being configured.</span></span>
* <span data-ttu-id="6eea6-175">*existingAseLocation*： 文字字串，包含 hello hello ILB ASE 部署所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6eea6-175">*existingAseLocation*: Text string containing hello Azure region where hello ILB ASE was deployed.</span></span>  <span data-ttu-id="6eea6-176">例如："South Central US (美國中南部)"。</span><span class="sxs-lookup"><span data-stu-id="6eea6-176">For example: "South Central US".</span></span>
* <span data-ttu-id="6eea6-177">*pfxBlobString*: hello based64 編碼的字串表示法的 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-177">*pfxBlobString*: hello based64-encoded string representation of hello .pfx file.</span></span> <span data-ttu-id="6eea6-178">使用 hello 稍早所示的程式碼片段，並將複製 hello"exportedcert.pfx.b64 」 中所包含的字串。</span><span class="sxs-lookup"><span data-stu-id="6eea6-178">Use hello code snippet shown earlier and copy hello string contained in "exportedcert.pfx.b64".</span></span> <span data-ttu-id="6eea6-179">中貼上做為 hello hello 值*pfxBlobString*屬性。</span><span class="sxs-lookup"><span data-stu-id="6eea6-179">Paste it in as hello value of hello *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="6eea6-180">*密碼*: hello 用密碼 toosecure hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6eea6-180">*password*: hello password used toosecure hello .pfx file.</span></span>
* <span data-ttu-id="6eea6-181">*certificateThumbprint*: hello 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="6eea6-181">*certificateThumbprint*: hello certificate's thumbprint.</span></span> <span data-ttu-id="6eea6-182">如果您從 PowerShell 擷取這個值 (例如， *$certificate。憑證指紋*hello 從先前程式碼片段)，您可以使用 hello 值。</span><span class="sxs-lookup"><span data-stu-id="6eea6-182">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from hello earlier code snippet), you can use hello value as is.</span></span> <span data-ttu-id="6eea6-183">如果您從 Windows 憑證對話方塊 hello 複製 hello 值，請記得 toostrip 出 hello 無關的空格。</span><span class="sxs-lookup"><span data-stu-id="6eea6-183">If you copy hello value from hello Windows certificate dialog box, remember toostrip out hello extraneous spaces.</span></span> <span data-ttu-id="6eea6-184">hello *certificateThumbprint*應看起來像 AF3143EB61D43F6727842115BB7F17BBCECAECAE。</span><span class="sxs-lookup"><span data-stu-id="6eea6-184">hello *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span></span>
* <span data-ttu-id="6eea6-185">*certificateName*： 自己選擇的好記的字串識別項使用 tooidentity hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-185">*certificateName*: A friendly string identifier of your own choosing used tooidentity hello certificate.</span></span> <span data-ttu-id="6eea6-186">hello 名稱用於一部分 hello 唯一的資源管理員識別碼 hello *Microsoft.Web/certificates*代表 hello SSL 憑證的實體。</span><span class="sxs-lookup"><span data-stu-id="6eea6-186">hello name is used as part of hello unique Resource Manager identifier for hello *Microsoft.Web/certificates* entity that represents hello SSL certificate.</span></span> <span data-ttu-id="6eea6-187">hello 名稱*必須*結尾 hello 下列尾碼： \_yourASENameHere_InternalLoadBalancingASE。</span><span class="sxs-lookup"><span data-stu-id="6eea6-187">hello name *must* end with hello following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span></span> <span data-ttu-id="6eea6-188">hello Azure 入口網站會使用這個後置詞，如 hello 憑證指標是使用的 toosecure ILB 啟用 ase。</span><span class="sxs-lookup"><span data-stu-id="6eea6-188">hello Azure portal uses this suffix as an indicator that hello certificate is used toosecure an ILB-enabled ASE.</span></span>

<span data-ttu-id="6eea6-189">以下是 azuredeploy.parameters.json  的縮簡範例︰</span><span class="sxs-lookup"><span data-stu-id="6eea6-189">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span></span>

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

<span data-ttu-id="6eea6-190">之後 hello *azuredeploy.parameters.json*檔案填滿、 使用 hello PowerShell 程式碼片段設定 hello 預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-190">After hello *azuredeploy.parameters.json* file is filled in, configure hello default SSL certificate by using hello PowerShell code snippet.</span></span> <span data-ttu-id="6eea6-191">變更 hello 檔案路徑 toomatch hello 資源管理員範本檔案的位置在電腦。</span><span class="sxs-lookup"><span data-stu-id="6eea6-191">Change hello file paths toomatch where hello Resource Manager template files are located on your machine.</span></span> <span data-ttu-id="6eea6-192">請記住 toosupply 您自己的值為 hello 資源管理員部署名稱和 hello 資源群組名稱：</span><span class="sxs-lookup"><span data-stu-id="6eea6-192">Remember toosupply your own values for hello Resource Manager deployment name and hello resource group name:</span></span>

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="6eea6-193">花大約 40 分鐘每項 ASE 前端 tooapply hello 變更。</span><span class="sxs-lookup"><span data-stu-id="6eea6-193">It takes roughly 40 minutes per ASE front end tooapply hello change.</span></span> <span data-ttu-id="6eea6-194">例如，對於預設大小的 ASE 使用兩個前端，hello 範本所花費一小時和 20 分鐘 toocomplete 周圍。</span><span class="sxs-lookup"><span data-stu-id="6eea6-194">For example, for a default-sized ASE that uses two front ends, hello template takes around one hour and 20 minutes toocomplete.</span></span> <span data-ttu-id="6eea6-195">當執行 hello 範本時，無法擴充 hello ASE。</span><span class="sxs-lookup"><span data-stu-id="6eea6-195">While hello template is running, hello ASE can't scale.</span></span>  

<span data-ttu-id="6eea6-196">Hello 範本完成之後，可以透過 HTTPS 存取 hello ILB ASE 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eea6-196">After hello template finishes, apps on hello ILB ASE can be accessed over HTTPS.</span></span> <span data-ttu-id="6eea6-197">hello 連線使用 hello 預設 SSL 憑證來進行保護。</span><span class="sxs-lookup"><span data-stu-id="6eea6-197">hello connections are secured by using hello default SSL certificate.</span></span> <span data-ttu-id="6eea6-198">hello ILB ASE 上的應用程式會使用 hello 應用程式名稱加上 hello 預設主機名稱的組合來進行定址時，會使用 hello 預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="6eea6-198">hello default SSL certificate is used when apps on hello ILB ASE are addressed by using a combination of hello application name plus hello default host name.</span></span> <span data-ttu-id="6eea6-199">例如，https://mycustomapp.internal-contoso.com 使用 hello 預設 SSL 憑證的 **.internal contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="6eea6-199">For example, https://mycustomapp.internal-contoso.com uses hello default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="6eea6-200">不過，如同 hello 的多租用戶公用服務執行的應用程式，開發人員可以設定個別的應用程式的自訂主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6eea6-200">However, just like apps that run on hello public multitenant service, developers can configure custom host names for individual apps.</span></span> <span data-ttu-id="6eea6-201">他們也可以為個別的應用程式設定唯一 SNI SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="6eea6-201">They also can configure unique SNI SSL certificate bindings for individual apps.</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="6eea6-202">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="6eea6-202">App Service Environment v1</span></span> ##
<span data-ttu-id="6eea6-203">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="6eea6-203">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="6eea6-204">hello 上述資訊為基礎 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="6eea6-204">hello preceding information was based on ASEv2.</span></span> <span data-ttu-id="6eea6-205">此區段會顯示 hello ASEv2 ASEv1 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="6eea6-205">This section shows you hello differences between ASEv1 and ASEv2.</span></span>

<span data-ttu-id="6eea6-206">ASEv1，在您的所有資源 hello 手動管理。</span><span class="sxs-lookup"><span data-stu-id="6eea6-206">In ASEv1, you manage all of hello resources manually.</span></span> <span data-ttu-id="6eea6-207">含有 hello 前端、 背景工作，與用於 IP SSL 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6eea6-207">That includes hello front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="6eea6-208">您可以調整您的應用程式服務計劃之前，您必須向外延展 hello 背景工作集區的 toohost 它。</span><span class="sxs-lookup"><span data-stu-id="6eea6-208">Before you can scale out your App Service plan, you must scale out hello worker pool that you want toohost it.</span></span>

<span data-ttu-id="6eea6-209">ASEv1 使用與 ASEv2 不同的定價模式。</span><span class="sxs-lookup"><span data-stu-id="6eea6-209">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="6eea6-210">在 ASEv1 中，要支付每個配置的核心，</span><span class="sxs-lookup"><span data-stu-id="6eea6-210">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="6eea6-211">包括用於前端或未裝載任何工作負載之背景工作角色的核心。</span><span class="sxs-lookup"><span data-stu-id="6eea6-211">That includes cores that are used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="6eea6-212">ASEv1，在 ase 中的 hello 預設最大標尺大小會是 55 主機總計。</span><span class="sxs-lookup"><span data-stu-id="6eea6-212">In ASEv1, hello default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="6eea6-213">包括背景工作角色與前端。</span><span class="sxs-lookup"><span data-stu-id="6eea6-213">That includes workers and front ends.</span></span> <span data-ttu-id="6eea6-214">一個利用 tooASEv1 是它可以部署在傳統的虛擬網路和資源管理員的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="6eea6-214">One advantage tooASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="6eea6-215">toolearn 深入了解 ASEv1，請參閱[App Service 環境 v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="6eea6-215">toolearn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<span data-ttu-id="6eea6-216">toocreate ASEv1 使用資源管理員範本，請參閱[使用資源管理員範本建立 ILB ASE v1][ILBASEv1Template]。</span><span class="sxs-lookup"><span data-stu-id="6eea6-216">toocreate an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span></span>


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
