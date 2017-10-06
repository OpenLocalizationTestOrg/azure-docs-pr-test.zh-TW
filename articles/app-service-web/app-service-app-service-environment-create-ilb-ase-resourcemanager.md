---
title: "aaaHow tooCreate ILB ASE 使用 Azure 資源管理員範本 |Microsoft 文件"
description: "了解如何 toocreate 內部負載平衡器 ASE 使用 Azure Resource Manager 範本。"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a><span data-ttu-id="5fcdd-103">如何 tooCreate ILB ASE 使用 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="5fcdd-103">How tooCreate an ILB ASE Using Azure Resource Manager Templates</span></span>

> [!NOTE] 
> <span data-ttu-id="5fcdd-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-104">This article is about hello App Service Environment v1.</span></span> <span data-ttu-id="5fcdd-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-105">There is a newer version of hello App Service Environment that is easier toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="5fcdd-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

## <a name="overview"></a><span data-ttu-id="5fcdd-107">概觀</span><span class="sxs-lookup"><span data-stu-id="5fcdd-107">Overview</span></span>
<span data-ttu-id="5fcdd-108">使用虛擬網路內部位址 (而不是公用 VIP) 可以建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-108">App Service Environments can be created with a virtual network internal address instead of a public VIP.</span></span>  <span data-ttu-id="5fcdd-109">此內部位址是由稱為 hello 內部負載平衡器 (ILB) 的 Azure 元件提供。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-109">This internal address is provided by an Azure component called hello internal load balancer (ILB).</span></span>  <span data-ttu-id="5fcdd-110">ILB ase 中可以使用 hello Azure 入口網站來建立。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-110">An ILB ASE can be created using hello Azure portal.</span></span>  <span data-ttu-id="5fcdd-111">也可以透過 Azure Resource Manager 範本使用自動化建立。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-111">It can also be created using automation by way of Azure Resource Manager templates.</span></span>  <span data-ttu-id="5fcdd-112">這篇文章會逐步 hello 步驟和語法需要 toocreate ILB ase 中使用 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-112">This article walks through hello steps and syntax needed toocreate an ILB ASE with Azure Resource Manager templates.</span></span>

<span data-ttu-id="5fcdd-113">自動建立 ILB ASE 涉及三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="5fcdd-113">There are three steps involved in automating creation of an ILB ASE:</span></span>

1. <span data-ttu-id="5fcdd-114">使用內部負載平衡器位址，而不公用 VIP 的虛擬網路中建立第一個 hello 基底 ASE。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-114">First hello base ASE is created in a virtual network using an internal load balancer address instead of a public VIP.</span></span>  <span data-ttu-id="5fcdd-115">在此步驟中，指派 toohello ILB ASE 根網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-115">As part of this step, a root domain name is assigned toohello ILB ASE.</span></span>
2. <span data-ttu-id="5fcdd-116">Hello 建立 ILB ASE 時，SSL 憑證上傳一次。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-116">Once hello ILB ASE is created, an SSL certificate is uploaded.</span></span>  
3. <span data-ttu-id="5fcdd-117">hello 已上傳的 SSL 憑證明確指派 toohello ILB ASE 做為其 「 預設 」 的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-117">hello uploaded SSL certificate is explicitly assigned toohello ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="5fcdd-118">此 SSL 憑證將用於 SSL 流量 tooapps hello ILB ASE 上時使用一般根指派網域 toohello hello ASE (例如 https://someapp.mycustomrootcomain.com) 定址 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5fcdd-118">This SSL certificate will be used for SSL traffic tooapps on hello ILB ASE when hello apps are addressed using hello common root domain assigned toohello ASE (e.g. https://someapp.mycustomrootcomain.com)</span></span>

## <a name="creating-hello-base-ilb-ase"></a><span data-ttu-id="5fcdd-119">建立 hello 基底 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="5fcdd-119">Creating hello Base ILB ASE</span></span>
<span data-ttu-id="5fcdd-120">在 GitHub 上 ([這裡][quickstartilbasecreate]) 可以取得範例 Azure Resource Manager 範本及其相關聯的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-120">An example Azure Resource Manager template, and its associated parameters file, are available on GitHub [here][quickstartilbasecreate].</span></span>

<span data-ttu-id="5fcdd-121">大部分的 hello 參數在 hello *azuredeploy.parameters.json*檔案是常見的 toocreating 這兩個 ILB ASEs，以及 ASEs 繫結 tooa 公用 VIP。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-121">Most of hello parameters in hello *azuredeploy.parameters.json* file are common toocreating both ILB ASEs, as well as ASEs bound tooa public VIP.</span></span>  <span data-ttu-id="5fcdd-122">out 參數的特殊附註，呼叫 hello 清單或是唯一的當建立 ILB ase 中：</span><span class="sxs-lookup"><span data-stu-id="5fcdd-122">hello list below calls out parameters of special note, or that are unique, when creating an ILB ASE:</span></span>

* <span data-ttu-id="5fcdd-123">*interalLoadBalancingMode*： 在大部分情況下設定此 too3，這表示這兩個連接埠 80/443 上的 HTTP/HTTPS 流量，且 hello 控制項/資料通道連接埠接聽 hello ASE tooby hello FTP 服務，將繫結的 tooan ILB 配置虛擬網路內部位址。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-123">*interalLoadBalancingMode*:  In most cases set this too3, which means both HTTP/HTTPS traffic on ports 80/443, and hello control/data channel ports listened tooby hello FTP service on hello ASE, will be bound tooan ILB allocated virtual network internal address.</span></span>  <span data-ttu-id="5fcdd-124">如果設定此屬性會改為 too2，則只有 hello FTP 服務相關會繫結連接埠 （控制和資料通道） tooan ILB 位址，雖然 hello HTTP/HTTPS 流量將會保留在 hello 公用 VIP。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-124">If this property is instead set too2, then only hello FTP service related ports (both control and data channels) will be bound tooan ILB address, while hello HTTP/HTTPS traffic will remain on hello public VIP.</span></span>
* <span data-ttu-id="5fcdd-125">*dns 尾碼*： 這個參數會定義將會指派 toohello ASE hello 預設根網域。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-125">*dnsSuffix*:  This parameter defines hello default root domain that will be assigned toohello ASE.</span></span>  <span data-ttu-id="5fcdd-126">在 Azure App Service hello 公用種變化，hello 預設根網域的所有 web 應用程式是*.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-126">In hello public variation of Azure App Service, hello default root domain for all web apps is *azurewebsites.net*.</span></span>  <span data-ttu-id="5fcdd-127">不過由於 ILB ASE 內部 tooa 客戶虛擬網路，它不會使意義 toouse hello 公開服務的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-127">However since an ILB ASE is internal tooa customer's virtual network, it doesn't make sense toouse hello public service's default root domain.</span></span>  <span data-ttu-id="5fcdd-128">相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-128">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span>  <span data-ttu-id="5fcdd-129">例如，假設性的 Contoso Corporation 可能會使用預設的根網域的*內部 contoso.com*預定的 tooonly 應用程式是可解析和 Contoso 虛擬網路中存取。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-129">For example, a hypothetical Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended tooonly be resolvable and accessible within Contoso's virtual network.</span></span> 
* <span data-ttu-id="5fcdd-130">*ipSslAddressCount*： 這個參數會自動預設 tooa 中的數值 0 hello *azuredeploy.json*檔案，因為 ILB ASEs 只能有單一的 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-130">*ipSslAddressCount*:  This parameter is automatically defaulted tooa value of 0 in hello *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span>  <span data-ttu-id="5fcdd-131">針對 ILB ase 中，任何明確的 IP SSL 位址，因此 hello ILB ase 中的 IP SSL 位址集區必須設定 toozero，否則將會發生佈建的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-131">There are no explicit IP-SSL addresses for an ILB ASE, and hence hello IP-SSL address pool for an ILB ASE must be set toozero, otherwise a provisioning error will occur.</span></span> 

<span data-ttu-id="5fcdd-132">一次 hello *azuredeploy.parameters.json*為 ILB ase 中，ILB ASE，就可以建立使用下列 Powershell 程式碼片段的 hello hello 檔填入的。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-132">Once hello *azuredeploy.parameters.json* file has been filled in for an ILB ASE, hello ILB ASE can then be created using hello following Powershell code snippet.</span></span>  <span data-ttu-id="5fcdd-133">變更 hello 檔案路徑 toomatch hello Azure 資源管理員範本檔案的位置在電腦。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-133">Change hello file PATHs toomatch where hello Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="5fcdd-134">另請記住 toosupply 您自己的值為 hello Azure Resource Manager 部署的名稱，資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-134">Also remember toosupply your own values for hello Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="5fcdd-135">Hello Azure Resource Manager 範本提交之後會需要幾小時的 hello ILB ASE toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-135">After hello Azure Resource Manager template is submitted it will take a few hours for hello ILB ASE toobe created.</span></span>  <span data-ttu-id="5fcdd-136">Hello 建立完成之後，hello ILB ASE 會顯示在應用程式服務環境的 hello 訂用帳戶觸發 hello 部署的 hello 清單中的 hello 入口網站 UX。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-136">Once hello creation completes, hello ILB ASE will show up in hello portal UX in hello list of App Service Environments for hello subscription that triggered hello deployment.</span></span>

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a><span data-ttu-id="5fcdd-137">上傳和設定 hello"Default"SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="5fcdd-137">Uploading and Configuring hello "Default" SSL Certificate</span></span>
<span data-ttu-id="5fcdd-138">一次建立 ILB ASE hello，SSL 憑證應該是相關聯 hello ASE 當做建立 SSL 連線 tooapps hello 「 預設 」 SSL 憑證的使用。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-138">Once hello ILB ASE is created, an SSL certificate should be associated with hello ASE as hello "default" SSL certificate use for establishing SSL connections tooapps.</span></span>  <span data-ttu-id="5fcdd-139">繼續 hello 假設 Contoso Corporation 範例中，如果 hello ASE 的預設 DNS 尾碼是*內部 contoso.com*，然後連接太*https://some-random-app.internal-contoso.com*需要有效的 SSL 憑證 **.internal contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-139">Continuing with hello hypothetical Contoso Corporation example, if hello ASE's default DNS suffix is *internal-contoso.com*, then a connection too*https://some-random-app.internal-contoso.com* requires an SSL certificate that is valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="5fcdd-140">有各種不同的方式 tooobtain 包括內部 Ca、 購買憑證從外部的簽發者，以及使用自我簽署的憑證的有效 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-140">There are a variety of ways tooobtain a valid SSL certificate including internal CAs, purchasing a certificate from an external issuer, and using a self-signed certificate.</span></span>  <span data-ttu-id="5fcdd-141">Hello hello SSL 憑證的來源，不論 hello 下列憑證的屬性皆需要 toobe 正確設定：</span><span class="sxs-lookup"><span data-stu-id="5fcdd-141">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="5fcdd-142">*主旨*： 此屬性必須設定得 **.your 根網域-here.com*</span><span class="sxs-lookup"><span data-stu-id="5fcdd-142">*Subject*:  This attribute must be set too**.your-root-domain-here.com*</span></span>
* <span data-ttu-id="5fcdd-143">*主體替代名稱*： 此屬性必須包含 **.your 根網域-here.com*，和 **.scm.your-根-網域-here.com*。 hello 原因 hello 第二個項目是將成為使用 hello 表單的位址與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello *your-app-name.scm.your-root-domain-here.com*。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-143">*Subject Alternative Name*:  This attribute must include both **.your-root-domain-here.com*, and **.scm.your-root-domain-here.com*.  hello reason for hello second entry is that SSL connections toohello SCM/Kudu site associated with each app will be made using an address of hello form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="5fcdd-144">備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-144">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span>  <span data-ttu-id="5fcdd-145">hello SSL 憑證必須 toobe 轉換/儲存為.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-145">hello SSL certificate needs toobe converted/saved as a .pfx file.</span></span>  <span data-ttu-id="5fcdd-146">請記住該 hello.pfx 檔案 tooinclude 所有中繼和根憑證，並且也需要 toobe 使用密碼保護。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-146">Remember that hello .pfx file needs tooinclude all intermediate and root certificates, and also needs toobe secured with a password.</span></span>

<span data-ttu-id="5fcdd-147">然後 hello 結果的.pfx 檔案需要 toobe 轉換成 base64 字串因為將使用 Azure Resource Manager 範本上載 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-147">Then hello resultant .pfx file needs toobe converted into a base64 string because hello SSL certificate will be uploaded using an Azure Resource Manager template.</span></span>  <span data-ttu-id="5fcdd-148">Azure Resource Manager 範本是文字檔案，因為需要 toobe 讓它可以包含為 hello 範本的參數轉換成 base64 字串 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-148">Since Azure Resource Manager templates are text files, hello .pfx file needs toobe converted into a base64 string so it can be included as a parameter of hello template.</span></span>

<span data-ttu-id="5fcdd-149">下列的 hello Powershell 程式碼片段顯示產生的自我簽署的憑證的範例，匯出 hello 憑證為.pfx 檔案，將 hello.pfx 檔案轉換成 base64 編碼字串，然後儲存 hello base64 編碼字串 tooa 個別檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-149">hello Powershell code snippet below shows an example of generating a self-signed certificate, exporting hello certificate as a .pfx file, converting hello .pfx file into a base64 encoded string, and then saving hello base64 encoded string tooa separate file.</span></span>  <span data-ttu-id="5fcdd-150">hello Powershell 程式碼的 base64 編碼是改自 hello [Powershell 指令碼的部落格][examplebase64encoding]。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-150">hello Powershell code for base64 encoding was adapted from hello [Powershell Scripts Blog][examplebase64encoding].</span></span>

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="5fcdd-151">已成功產生 hello SSL 憑證，並轉換的 tooa base64 編碼字串，hello 範例如 GitHub 上的 Azure Resource Manager 範本[設定 hello 預設 SSL 憑證][ configuringDefaultSSLCertificate]可用。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-151">Once hello SSL certificate has been successfully generated and converted tooa base64 encoded string, hello example Azure Resource Manager template on GitHub for [configuring hello default SSL certificate][configuringDefaultSSLCertificate] can be used.</span></span>

<span data-ttu-id="5fcdd-152">hello 參數在 hello *azuredeploy.parameters.json*檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="5fcdd-152">hello parameters in hello *azuredeploy.parameters.json* file are listed below:</span></span>

* <span data-ttu-id="5fcdd-153">*appServiceEnvironmentName*: hello 的 hello ILB ASE 正在設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-153">*appServiceEnvironmentName*:  hello name of hello ILB ASE being configured.</span></span>
* <span data-ttu-id="5fcdd-154">*existingAseLocation*： 文字字串，包含 hello hello ILB ASE 部署所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-154">*existingAseLocation*:  Text string containing hello Azure region where hello ILB ASE was deployed.</span></span>  <span data-ttu-id="5fcdd-155">例如 "South Central US"。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-155">For example:  "South Central US".</span></span>
* <span data-ttu-id="5fcdd-156">*pfxBlobString*: hello based64 編碼 hello.pfx 檔案的字串表示。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-156">*pfxBlobString*:  hello based64 encoded string representation of hello .pfx file.</span></span>  <span data-ttu-id="5fcdd-157">使用 hello 稍早所示的程式碼片段，您會複製"exportedcert.pfx.b64 」 中所包含的 hello 字串並貼上做為 hello hello 值*pfxBlobString*屬性。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-157">Using hello code snippet shown earlier, you would copy hello string contained in "exportedcert.pfx.b64" and paste it in as hello value of hello *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="5fcdd-158">*密碼*: hello 用密碼 toosecure hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-158">*password*:  hello password used toosecure hello .pfx file.</span></span>
* <span data-ttu-id="5fcdd-159">*certificateThumbprint*: hello 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-159">*certificateThumbprint*:  hello certificate's thumbprint.</span></span>  <span data-ttu-id="5fcdd-160">如果您從 Powershell 擷取這個值 (例如*$certificate。憑證指紋*hello 從先前程式碼片段)，您可以使用與 hello 值-是。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-160">If you retrieve this value from Powershell (e.g. *$certificate.Thumbprint* from hello earlier code snippet), you can use hello value as-is.</span></span>  <span data-ttu-id="5fcdd-161">但是如果您從 hello Windows 憑證對話方塊複製 hello 值，請記得 toostrip 出 hello 無關的空格。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-161">However if you copy hello value from hello Windows certificate dialog, remember toostrip out hello extraneous spaces.</span></span>  <span data-ttu-id="5fcdd-162">hello *certificateThumbprint*看起來應該像這樣： AF3143EB61D43F6727842115BB7F17BBCECAECAE</span><span class="sxs-lookup"><span data-stu-id="5fcdd-162">hello *certificateThumbprint* should look something like:  AF3143EB61D43F6727842115BB7F17BBCECAECAE</span></span>
* <span data-ttu-id="5fcdd-163">*certificateName*： 自己選擇的好記的字串識別項使用 tooidentity hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-163">*certificateName*:  A friendly string identifier of your own choosing used tooidentity hello certificate.</span></span>  <span data-ttu-id="5fcdd-164">hello 名稱用於一部分 hello 唯一的 Azure 資源管理員識別碼 hello *Microsoft.Web/certificates*代表 hello SSL 憑證的實體。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-164">hello name is used as part of hello unique Azure Resource Manager identifier for hello *Microsoft.Web/certificates* entity representing hello SSL certificate.</span></span>  <span data-ttu-id="5fcdd-165">hello 名稱**必須**結尾 hello 下列尾碼： \_yourASENameHere_InternalLoadBalancingASE。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-165">hello name **must** end with hello following suffix:  \_yourASENameHere_InternalLoadBalancingASE.</span></span>  <span data-ttu-id="5fcdd-166">為指標的 hello 憑證用於保護 ILB 啟用 ase 中 hello 入口網站會使用這個後置詞。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-166">This suffix is used by hello portal as an indicator that hello certificate is used for securing an ILB-enabled ASE.</span></span>

<span data-ttu-id="5fcdd-167">「azuredeploy.parameters.json」  的縮寫範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5fcdd-167">An abbreviated example of *azuredeploy.parameters.json* is shown below:</span></span>

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

<span data-ttu-id="5fcdd-168">一次 hello *azuredeploy.parameters.json*檔案已滿時，可以使用下列 Powershell 程式碼片段的 hello 設定 hello 預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-168">Once hello *azuredeploy.parameters.json* file has been filled in, hello default SSL certificate can be configured using hello following Powershell code snippet.</span></span>  <span data-ttu-id="5fcdd-169">變更 hello 檔案路徑 toomatch hello Azure 資源管理員範本檔案的位置在電腦。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-169">Change hello file PATHs toomatch where hello Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="5fcdd-170">另請記住 toosupply 您自己的值為 hello Azure Resource Manager 部署的名稱，資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-170">Also remember toosupply your own values for hello Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="5fcdd-171">Hello Azure Resource Manager 範本提交之後它需要大約 40 分鐘 ASE 前端 tooapply hello 變更每分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-171">After hello Azure Resource Manager template is submitted it will take roughly forty minutes minutes per ASE front-end tooapply hello change.</span></span>  <span data-ttu-id="5fcdd-172">例如，預設值使用兩個前端，可調整大小 ASE hello 範本需要一小時和 20 分鐘 toocomplete 周圍。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-172">For example, with a default sized ASE using two front-ends, hello template will take around one hour and twenty minutes toocomplete.</span></span>  <span data-ttu-id="5fcdd-173">執行 hello 範本時 hello ASE 將不會無法 tooscaled。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-173">While hello template is running hello ASE will not be able tooscaled.</span></span>  

<span data-ttu-id="5fcdd-174">Hello 範本完成之後，可透過 HTTPS 存取 hello ILB ASE 上的應用程式並 hello 連線將會使用 hello 預設 SSL 憑證保護。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-174">Once hello template completes, apps on hello ILB ASE can be accessed over HTTPS and hello connections will be secured using hello default SSL certificate.</span></span>  <span data-ttu-id="5fcdd-175">hello 預設 SSL 憑證將用於 hello ILB ASE 上的應用程式會解決使用 hello 應用程式名稱加上 hello 預設主機名稱的組合。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-175">hello default SSL certificate will be used when apps on hello ILB ASE are addressed using a combination of hello application name plus hello default hostname.</span></span>  <span data-ttu-id="5fcdd-176">例如*https://mycustomapp.internal-contoso.com*會使用 hello 預設 SSL 憑證的 **.internal contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-176">For example *https://mycustomapp.internal-contoso.com* would use hello default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="5fcdd-177">不過，如同 hello 公用多租用戶的服務上執行的應用程式，開發人員可以也設定個別的應用程式的自訂主機名稱，然後再設定個別的應用程式的唯一 SNI SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-177">However, just like apps running on hello public multi-tenant service, developers can also configure custom host names for individual apps, and then configure unique SNI SSL certificate bindings for individual apps.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="5fcdd-178">開始使用</span><span class="sxs-lookup"><span data-stu-id="5fcdd-178">Getting started</span></span>
<span data-ttu-id="5fcdd-179">tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="5fcdd-179">tooget started with App Service Environments, see [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

<span data-ttu-id="5fcdd-180">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="5fcdd-180">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

