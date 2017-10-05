---
title: "如何使用 Azure Resource Manager 範本建立 ILB ASE | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 範本建立內部負載平衡器 ASE"
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
ms.openlocfilehash: 147ab76d38c8bbbf34d35ed6c2a194d97fe711ab
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-an-ilb-ase-using-azure-resource-manager-templates"></a><span data-ttu-id="128bd-103">如何使用 Azure Resource Manager 範本建立 ILB ASE範本建立 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="128bd-103">How To Create an ILB ASE Using Azure Resource Manager Templates</span></span>

> [!NOTE] 
> <span data-ttu-id="128bd-104">這篇文章是關於 App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="128bd-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="128bd-105">有較新版本的 App Service 環境，更易於使用，並且可以在功能更強大的基礎結構上執行。</span><span class="sxs-lookup"><span data-stu-id="128bd-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="128bd-106">若要深入了解新版本，請從 [App Service 環境簡介](../app-service/app-service-environment/intro.md)開始。</span><span class="sxs-lookup"><span data-stu-id="128bd-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
>

## <a name="overview"></a><span data-ttu-id="128bd-107">概觀</span><span class="sxs-lookup"><span data-stu-id="128bd-107">Overview</span></span>
<span data-ttu-id="128bd-108">使用虛擬網路內部位址 (而不是公用 VIP) 可以建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="128bd-108">App Service Environments can be created with a virtual network internal address instead of a public VIP.</span></span>  <span data-ttu-id="128bd-109">此內部位址是由稱為內部負載平衡器 (ILB) 的 Azure 元件提供。</span><span class="sxs-lookup"><span data-stu-id="128bd-109">This internal address is provided by an Azure component called the internal load balancer (ILB).</span></span>  <span data-ttu-id="128bd-110">使用 Azure 入口網站可以建立 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-110">An ILB ASE can be created using the Azure portal.</span></span>  <span data-ttu-id="128bd-111">也可以透過 Azure Resource Manager 範本使用自動化建立。</span><span class="sxs-lookup"><span data-stu-id="128bd-111">It can also be created using automation by way of Azure Resource Manager templates.</span></span>  <span data-ttu-id="128bd-112">本文逐步解說使用 Azure Resource Manager 範本建立 ILB ASE 所需的步驟和語法。</span><span class="sxs-lookup"><span data-stu-id="128bd-112">This article walks through the steps and syntax needed to create an ILB ASE with Azure Resource Manager templates.</span></span>

<span data-ttu-id="128bd-113">自動建立 ILB ASE 涉及三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="128bd-113">There are three steps involved in automating creation of an ILB ASE:</span></span>

1. <span data-ttu-id="128bd-114">首先會使用內部負載平衡器位址 (而不是公用 VIP)，在虛擬網路中建立基底 ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-114">First the base ASE is created in a virtual network using an internal load balancer address instead of a public VIP.</span></span>  <span data-ttu-id="128bd-115">在此步驟中，根網域名稱會指派給 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-115">As part of this step, a root domain name is assigned to the ILB ASE.</span></span>
2. <span data-ttu-id="128bd-116">一旦建立 ILB ASE，就會上傳 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-116">Once the ILB ASE is created, an SSL certificate is uploaded.</span></span>  
3. <span data-ttu-id="128bd-117">上傳的 SSL 憑證會明確指派給 ILB ASE 做為其「預設」SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-117">The uploaded SSL certificate is explicitly assigned to the ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="128bd-118">如果應用程式是使用指派給 ASE 的一般根網域 (例如 https://someapp.mycustomrootcomain.com) 來定址，此 SSL 憑證將使用於 ILB ASE 上應用程式的 SSL 流量</span><span class="sxs-lookup"><span data-stu-id="128bd-118">This SSL certificate will be used for SSL traffic to apps on the ILB ASE when the apps are addressed using the common root domain assigned to the ASE (e.g. https://someapp.mycustomrootcomain.com)</span></span>

## <a name="creating-the-base-ilb-ase"></a><span data-ttu-id="128bd-119">建立基底 ILB ASE</span><span class="sxs-lookup"><span data-stu-id="128bd-119">Creating the Base ILB ASE</span></span>
<span data-ttu-id="128bd-120">在 GitHub 上 ([這裡][quickstartilbasecreate]) 可以取得範例 Azure Resource Manager 範本及其相關聯的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="128bd-120">An example Azure Resource Manager template, and its associated parameters file, are available on GitHub [here][quickstartilbasecreate].</span></span>

<span data-ttu-id="128bd-121">「azuredeploy.parameters.json」  檔案中的大部分參數通用於建立 ILB ASE 以及繫結至公用 VIP 的 ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-121">Most of the parameters in the *azuredeploy.parameters.json* file are common to creating both ILB ASEs, as well as ASEs bound to a public VIP.</span></span>  <span data-ttu-id="128bd-122">建立 ILB ASE 時，以下清單會呼叫特殊附註或唯一的參數︰</span><span class="sxs-lookup"><span data-stu-id="128bd-122">The list below calls out parameters of special note, or that are unique, when creating an ILB ASE:</span></span>

* <span data-ttu-id="128bd-123">interalLoadBalancingMode︰在大多數情況下，此屬性設定為 3，這表示連接埠 80/443 上的 HTTP/HTTPS 流量，以及 ASE 上的 FTP 服務所接聽的控制項/資料通道連接埠將會繫結至 ILB 配置的虛擬網路內部位址。</span><span class="sxs-lookup"><span data-stu-id="128bd-123">*interalLoadBalancingMode*:  In most cases set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB allocated virtual network internal address.</span></span>  <span data-ttu-id="128bd-124">如果此屬性改為設定為 2，則只有 FTP 服務相關的連接埠 (控制和資料通道) 會繫結至 ILB 位址，而 HTTP/HTTPS 流量將保留在公用 VIP 上。</span><span class="sxs-lookup"><span data-stu-id="128bd-124">If this property is instead set to 2, then only the FTP service related ports (both control and data channels) will be bound to an ILB address, while the HTTP/HTTPS traffic will remain on the public VIP.</span></span>
* <span data-ttu-id="128bd-125">dnsSuffix︰這個參數會定義要指派給 ASE 的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="128bd-125">*dnsSuffix*:  This parameter defines the default root domain that will be assigned to the ASE.</span></span>  <span data-ttu-id="128bd-126">在 Azure App Service 的公用種變化中，所有 Web 應用程式的預設根網域皆為 azurewebsites.net 。</span><span class="sxs-lookup"><span data-stu-id="128bd-126">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span></span>  <span data-ttu-id="128bd-127">不過，由於 ILB ASE 位於客戶虛擬網路的內部，所以不適合使用公用服務的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="128bd-127">However since an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span></span>  <span data-ttu-id="128bd-128">相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="128bd-128">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span>  <span data-ttu-id="128bd-129">例如，假定的 Contoso Corporation 可能會將 internal-contoso.com  的預設根網域用於只能在 Contoso 虛擬網路內解析和存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="128bd-129">For example, a hypothetical Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to only be resolvable and accessible within Contoso's virtual network.</span></span> 
* <span data-ttu-id="128bd-130">ipSslAddressCount︰在 *azuredeploy.json* 檔案中，這個參數的值會自動預設為 0，因為 ILB ASE 只有單一 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="128bd-130">*ipSslAddressCount*:  This parameter is automatically defaulted to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span>  <span data-ttu-id="128bd-131">ILB ASE 沒有明確的 IP-SSL 位址，因此 ILB ASE 的 IP-SSL 位址集區必須設為零，否則會發生佈建錯誤。</span><span class="sxs-lookup"><span data-stu-id="128bd-131">There are no explicit IP-SSL addresses for an ILB ASE, and hence the IP-SSL address pool for an ILB ASE must be set to zero, otherwise a provisioning error will occur.</span></span> 

<span data-ttu-id="128bd-132">一旦針對 ILB ASE 填入 azuredeploy.parameters.json  檔案，就可以使用下列 Powershell 程式碼片段建立 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-132">Once the *azuredeploy.parameters.json* file has been filled in for an ILB ASE, the ILB ASE can then be created using the following Powershell code snippet.</span></span>  <span data-ttu-id="128bd-133">變更檔案 PATH，以符合 Azure Resource Manager 範本檔案位於您電腦上的位置。</span><span class="sxs-lookup"><span data-stu-id="128bd-133">Change the file PATHs to match where the Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="128bd-134">也請記得提供您自己的 Azure Resource Manager 部署名稱和資源群組名稱的值。</span><span class="sxs-lookup"><span data-stu-id="128bd-134">Also remember to supply your own values for the Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="128bd-135">提交 Azure Resource Manager 範本之後，需要數小時的時間才能建立 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-135">After the Azure Resource Manager template is submitted it will take a few hours for the ILB ASE to be created.</span></span>  <span data-ttu-id="128bd-136">建立完成後，ILB ASE 會顯示在觸發部署之訂用帳戶的 App Service 環境清單的入口網站 UX 中。</span><span class="sxs-lookup"><span data-stu-id="128bd-136">Once the creation completes, the ILB ASE will show up in the portal UX in the list of App Service Environments for the subscription that triggered the deployment.</span></span>

## <a name="uploading-and-configuring-the-default-ssl-certificate"></a><span data-ttu-id="128bd-137">上傳和設定「預設」SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="128bd-137">Uploading and Configuring the "Default" SSL Certificate</span></span>
<span data-ttu-id="128bd-138">建立 ILB ASE 後， SSL 憑證應與 ASE 相關聯，做為用來建立應用程式的 SSL 連線的「預設」SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-138">Once the ILB ASE is created, an SSL certificate should be associated with the ASE as the "default" SSL certificate use for establishing SSL connections to apps.</span></span>  <span data-ttu-id="128bd-139">繼續討論假定的 Contoso Corporation 範例，如果 ASE 的預設 DNS 尾碼是 internal-contoso.com，則連接到 https://some-random-app.internal-contoso.com 需要有對 *.internal contoso.com 有效的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-139">Continuing with the hypothetical Contoso Corporation example, if the ASE's default DNS suffix is *internal-contoso.com*, then a connection to *https://some-random-app.internal-contoso.com* requires an SSL certificate that is valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="128bd-140">有各種不同的方式可取得有效的 SSL 憑證，包括內部 CA、向外部簽發者購買憑證，以及使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-140">There are a variety of ways to obtain a valid SSL certificate including internal CAs, purchasing a certificate from an external issuer, and using a self-signed certificate.</span></span>  <span data-ttu-id="128bd-141">無論 SSL 憑證的來源，都需要正確設定下列憑證屬性︰</span><span class="sxs-lookup"><span data-stu-id="128bd-141">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="128bd-142">主體︰此屬性必須設為 *.your-root-domain-here.com</span><span class="sxs-lookup"><span data-stu-id="128bd-142">*Subject*:  This attribute must be set to **.your-root-domain-here.com*</span></span>
* <span data-ttu-id="128bd-143">主體替代名稱︰此屬性必須同時包含 *.your-root-domain-here.com 和 *.scm.your-root-domain-here.com。</span><span class="sxs-lookup"><span data-stu-id="128bd-143">*Subject Alternative Name*:  This attribute must include both **.your-root-domain-here.com*, and **.scm.your-root-domain-here.com*.</span></span>  <span data-ttu-id="128bd-144">第二個項目的原因是將使用 your-app-name.scm.your-root-domain-here.com 形式的位址，進行與每個應用程式相關聯的 SCM/Kudu 網站的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="128bd-144">The reason for the second entry is that SSL connections to the SCM/Kudu site associated with each app will be made using an address of the form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="128bd-145">備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。</span><span class="sxs-lookup"><span data-stu-id="128bd-145">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span>  <span data-ttu-id="128bd-146">SSL 憑證必須能夠轉換/另存為 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="128bd-146">The SSL certificate needs to be converted/saved as a .pfx file.</span></span>  <span data-ttu-id="128bd-147">請記住，.pfx 檔案必須包含所有中繼和根憑證，而且也必須使用密碼保護。</span><span class="sxs-lookup"><span data-stu-id="128bd-147">Remember that the .pfx file needs to include all intermediate and root certificates, and also needs to be secured with a password.</span></span>

<span data-ttu-id="128bd-148">然後必須將結果產生的.pfx 檔案轉換成 base64 字串，因為會使用 Azure Resource Manager 範本上載 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-148">Then the resultant .pfx file needs to be converted into a base64 string because the SSL certificate will be uploaded using an Azure Resource Manager template.</span></span>  <span data-ttu-id="128bd-149">因為 Azure Resource Manager 範本是文字檔案，所以必須將 .pfx 檔案轉換成 base64 字串，才能納入為範本的參數。</span><span class="sxs-lookup"><span data-stu-id="128bd-149">Since Azure Resource Manager templates are text files, the .pfx file needs to be converted into a base64 string so it can be included as a parameter of the template.</span></span>

<span data-ttu-id="128bd-150">下列 Powershell 程式碼片段顯示產生自我簽署憑證、將憑證匯出為 .pfx 檔案、將 .pfx 檔案轉換成 base64 編碼的字串，然後將 base64 編碼字串儲存至個別檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="128bd-150">The Powershell code snippet below shows an example of generating a self-signed certificate, exporting the certificate as a .pfx file, converting the .pfx file into a base64 encoded string, and then saving the base64 encoded string to a separate file.</span></span>  <span data-ttu-id="128bd-151">Base64 編碼的 Powershell 程式碼改寫自 [Powershell 指令碼部落格][examplebase64encoding]。</span><span class="sxs-lookup"><span data-stu-id="128bd-151">The Powershell code for base64 encoding was adapted from the [Powershell Scripts Blog][examplebase64encoding].</span></span>

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="128bd-152">成功產生 SSL 憑證並轉換成 base64 編碼字串後，GitHub 上的範例 Azure Resource Manager 範本即可用於[設定預設 SSL 憑證][configuringDefaultSSLCertificate]。</span><span class="sxs-lookup"><span data-stu-id="128bd-152">Once the SSL certificate has been successfully generated and converted to a base64 encoded string, the example Azure Resource Manager template on GitHub for [configuring the default SSL certificate][configuringDefaultSSLCertificate] can be used.</span></span>

<span data-ttu-id="128bd-153">「azuredeploy.parameters.json」  檔案中的參數如下所列︰</span><span class="sxs-lookup"><span data-stu-id="128bd-153">The parameters in the *azuredeploy.parameters.json* file are listed below:</span></span>

* <span data-ttu-id="128bd-154">appServiceEnvironmentName︰要設定之 ILB ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="128bd-154">*appServiceEnvironmentName*:  The name of the ILB ASE being configured.</span></span>
* <span data-ttu-id="128bd-155">existingAseLocation︰包含 ILB ASE 部署所在的 Azure 區域的文字字串。</span><span class="sxs-lookup"><span data-stu-id="128bd-155">*existingAseLocation*:  Text string containing the Azure region where the ILB ASE was deployed.</span></span>  <span data-ttu-id="128bd-156">例如 "South Central US"。</span><span class="sxs-lookup"><span data-stu-id="128bd-156">For example:  "South Central US".</span></span>
* <span data-ttu-id="128bd-157">pfxBlobString：.pfx 檔案的 based64 編碼字串表示法。</span><span class="sxs-lookup"><span data-stu-id="128bd-157">*pfxBlobString*:  The based64 encoded string representation of the .pfx file.</span></span>  <span data-ttu-id="128bd-158">使用稍早所示的程式碼片段，您會複製 "exportedcert.pfx.b64" 中包含的字串並貼入做為 pfxBlobString 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="128bd-158">Using the code snippet shown earlier, you would copy the string contained in "exportedcert.pfx.b64" and paste it in as the value of the *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="128bd-159">password：用來保護 .pfx 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="128bd-159">*password*:  The password used to secure the .pfx file.</span></span>
* <span data-ttu-id="128bd-160">certificateThumbprint︰憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="128bd-160">*certificateThumbprint*:  The certificate's thumbprint.</span></span>  <span data-ttu-id="128bd-161">如果您從 Powershell 擷取此值 (例如先前程式碼片段中的 $certificate.Thumbprint  )，您可以使用現況值。</span><span class="sxs-lookup"><span data-stu-id="128bd-161">If you retrieve this value from Powershell (e.g. *$certificate.Thumbprint* from the earlier code snippet), you can use the value as-is.</span></span>  <span data-ttu-id="128bd-162">不過，如果您從 Windows 憑證對話方塊複製此值，請記得去除多餘的空格。</span><span class="sxs-lookup"><span data-stu-id="128bd-162">However if you copy the value from the Windows certificate dialog, remember to strip out the extraneous spaces.</span></span>  <span data-ttu-id="128bd-163">CertificateThumbprint 應如下所示︰AF3143EB61D43F6727842115BB7F17BBCECAECAE</span><span class="sxs-lookup"><span data-stu-id="128bd-163">The *certificateThumbprint* should look something like:  AF3143EB61D43F6727842115BB7F17BBCECAECAE</span></span>
* <span data-ttu-id="128bd-164">certificateName︰您自己選擇的好記字串識別碼，可用來識別憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-164">*certificateName*:  A friendly string identifier of your own choosing used to identity the certificate.</span></span>  <span data-ttu-id="128bd-165">此名稱做為 Microsoft.Web/certificates  實體 (表示 SSL 憑證) 的唯一 Azure Resource Manager 識別碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="128bd-165">The name is used as part of the unique Azure Resource Manager identifier for the *Microsoft.Web/certificates* entity representing the SSL certificate.</span></span>  <span data-ttu-id="128bd-166">名稱**必須**以下列尾碼結尾︰\_yourASENameHere_InternalLoadBalancingASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-166">The name **must** end with the following suffix:  \_yourASENameHere_InternalLoadBalancingASE.</span></span>  <span data-ttu-id="128bd-167">入口網站會使用這個尾碼做為憑證要用於保護啟用 ILB 之 ASE 的指示器。</span><span class="sxs-lookup"><span data-stu-id="128bd-167">This suffix is used by the portal as an indicator that the certificate is used for securing an ILB-enabled ASE.</span></span>

<span data-ttu-id="128bd-168">「azuredeploy.parameters.json」  的縮寫範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="128bd-168">An abbreviated example of *azuredeploy.parameters.json* is shown below:</span></span>

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

<span data-ttu-id="128bd-169">一旦填入「azuredeploy.parameters.json」  檔案，就可以使用下列 Powershell 程式碼片段設定 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-169">Once the *azuredeploy.parameters.json* file has been filled in, the default SSL certificate can be configured using the following Powershell code snippet.</span></span>  <span data-ttu-id="128bd-170">變更檔案 PATH，以符合 Azure Resource Manager 範本檔案位於您電腦上的位置。</span><span class="sxs-lookup"><span data-stu-id="128bd-170">Change the file PATHs to match where the Azure Resource Manager template files are located on your machine.</span></span>  <span data-ttu-id="128bd-171">也請記得提供您自己的 Azure Resource Manager 部署名稱和資源群組名稱的值。</span><span class="sxs-lookup"><span data-stu-id="128bd-171">Also remember to supply your own values for the Azure Resource Manager deployment name, and resource group name.</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="128bd-172">提交 Azure Resource Manager 範本之後，每個 ASE 前端需要大約 40 分鐘的時間套用變更。</span><span class="sxs-lookup"><span data-stu-id="128bd-172">After the Azure Resource Manager template is submitted it will take roughly forty minutes minutes per ASE front-end to apply the change.</span></span>  <span data-ttu-id="128bd-173">例如，有一個預設大小的 ASE 使用兩個前端，則範本將需要大約一小時 20 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="128bd-173">For example, with a default sized ASE using two front-ends, the template will take around one hour and twenty minutes to complete.</span></span>  <span data-ttu-id="128bd-174">執行範本時，將無法調整 ASE。</span><span class="sxs-lookup"><span data-stu-id="128bd-174">While the template is running the ASE will not be able to scaled.</span></span>  

<span data-ttu-id="128bd-175">完成範本後，可透過 HTTPS 存取 ILB ASE 上的應用程式，並使用預設 SSL 憑證保護連線。</span><span class="sxs-lookup"><span data-stu-id="128bd-175">Once the template completes, apps on the ILB ASE can be accessed over HTTPS and the connections will be secured using the default SSL certificate.</span></span>  <span data-ttu-id="128bd-176">如果 ILB ASE 上的應用程式是使用應用程式名稱加上預設主機名稱的組合來定址，則會使用預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-176">The default SSL certificate will be used when apps on the ILB ASE are addressed using a combination of the application name plus the default hostname.</span></span>  <span data-ttu-id="128bd-177">例如，https://mycustomapp.internal-contoso.com 會使用 *.internal contoso.com 的預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="128bd-177">For example *https://mycustomapp.internal-contoso.com* would use the default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="128bd-178">不過，就如同在公用多租用戶服務上執行的應用程式，開發人員也可以為個別的應用程式設定自訂主機名稱，然後為個別的應用程式設定唯一的 SNI SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="128bd-178">However, just like apps running on the public multi-tenant service, developers can also configure custom host names for individual apps, and then configure unique SNI SSL certificate bindings for individual apps.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="128bd-179">開始使用</span><span class="sxs-lookup"><span data-stu-id="128bd-179">Getting started</span></span>
<span data-ttu-id="128bd-180">若要開始使用 App Service 環境，請參閱 [App Service 環境簡介](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="128bd-180">To get started with App Service Environments, see [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

<span data-ttu-id="128bd-181">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="128bd-181">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

