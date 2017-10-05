---
title: "使用 Resource Manager 範本建立 Azure App Service Environment"
description: "說明如何使用 Resource Manager 範本建立外部或 ILB Azure App Service Environment"
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
ms.openlocfilehash: e6b21086488352c1da914b4656ad1d216fd6de85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="4c27a-103">使用 Azure Resource Manager 範本立 ASE</span><span class="sxs-lookup"><span data-stu-id="4c27a-103">Create an ASE by using an Azure Resource Manager template</span></span>

## <a name="overview"></a><span data-ttu-id="4c27a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4c27a-104">Overview</span></span>
<span data-ttu-id="4c27a-105">Azure App Service Environment (ASE) 可以使用網際網路可存取端點，或是 Azure 虛擬網路 (VNet) 中內部位址上的端點來建立。</span><span class="sxs-lookup"><span data-stu-id="4c27a-105">Azure App Service environments (ASEs) can be created with an internet-accessible endpoint or an endpoint on an internal address in an Azure virtual network (VNet).</span></span> <span data-ttu-id="4c27a-106">使用內部端點建立時，該端點是由稱為內部負載平衡器 (ILB) 的 Azure 元件提供。</span><span class="sxs-lookup"><span data-stu-id="4c27a-106">When created with an internal endpoint, that endpoint is provided by an Azure component called an internal load balancer (ILB).</span></span> <span data-ttu-id="4c27a-107">使用內部 IP 位址的 ASE 稱為 ILB ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-107">The ASE on an internal IP address is called an ILB ASE.</span></span> <span data-ttu-id="4c27a-108">具有公用端點的 ASE 稱為外部 ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-108">The ASE with a public endpoint is called an External ASE.</span></span> 

<span data-ttu-id="4c27a-109">ASE 可以使用 Azure 入口網站或 Azure Resource Manager 範本來建立。</span><span class="sxs-lookup"><span data-stu-id="4c27a-109">An ASE can be created by using the Azure portal or an Azure Resource Manager template.</span></span> <span data-ttu-id="4c27a-110">本文逐步解說使用 Resource Manager 範本建立外部 ASE 或 ILB ASE 所需的步驟和語法。</span><span class="sxs-lookup"><span data-stu-id="4c27a-110">This article walks through the steps and syntax you need to create an External ASE or ILB ASE with Resource Manager templates.</span></span> <span data-ttu-id="4c27a-111">若要了解如何在 Azure 入口網站中建立 ASE，請參閱 [建立外部 ASE][MakeExternalASE] 或 [建立 ILB ASE][MakeILBASE] 。</span><span class="sxs-lookup"><span data-stu-id="4c27a-111">To learn how to create an ASE in the Azure portal, see [Make an External ASE][MakeExternalASE] or [Make an ILB ASE][MakeILBASE].</span></span>

<span data-ttu-id="4c27a-112">在入口網站中建立 ASE 時，可以選擇同時建立 VNet，或選擇要部署至既有 VNet。</span><span class="sxs-lookup"><span data-stu-id="4c27a-112">When you create an ASE in the Azure portal, you can create your VNet at the same time or choose a preexisting VNet to deploy into.</span></span> <span data-ttu-id="4c27a-113">從範本建立 ASE 時，必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="4c27a-113">When you create an ASE from a template, you must start with:</span></span> 

* <span data-ttu-id="4c27a-114">Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="4c27a-114">A Resource Manager VNet.</span></span>
* <span data-ttu-id="4c27a-115">該 VNet 中的子網路。</span><span class="sxs-lookup"><span data-stu-id="4c27a-115">A subnet in that VNet.</span></span> <span data-ttu-id="4c27a-116">建議的 ASE 子網路是 `/25`，並具有 128 個位址，以容納未來成長。</span><span class="sxs-lookup"><span data-stu-id="4c27a-116">We recommend an ASE subnet size of `/25` with 128 addresses to accomodate future growth.</span></span> <span data-ttu-id="4c27a-117">ASE 建立之後，無法變更大小。</span><span class="sxs-lookup"><span data-stu-id="4c27a-117">After the ASE is created, you can't change the size.</span></span>
* <span data-ttu-id="4c27a-118">您的 VNnet 中的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="4c27a-118">The resource ID from your VNet.</span></span> <span data-ttu-id="4c27a-119">您可以從 Azure 入口網站中的虛擬網路屬性底下取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4c27a-119">You can get this information from the Azure portal under your virtual network properties.</span></span>
* <span data-ttu-id="4c27a-120">您想要部署的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c27a-120">The subscription you want to deploy into.</span></span>
* <span data-ttu-id="4c27a-121">您想要部署的位置。</span><span class="sxs-lookup"><span data-stu-id="4c27a-121">The location you want to deploy into.</span></span>

<span data-ttu-id="4c27a-122">若要自動化 ASE 建立：</span><span class="sxs-lookup"><span data-stu-id="4c27a-122">To automate your ASE creation:</span></span>

1. <span data-ttu-id="4c27a-123">從範本建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-123">Create the ASE from a template.</span></span> <span data-ttu-id="4c27a-124">如果是建立外部 ASE，完成此步驟就建立完成。</span><span class="sxs-lookup"><span data-stu-id="4c27a-124">If you create an External ASE, you're finished after this step.</span></span> <span data-ttu-id="4c27a-125">如果是建立 ILB ASE，還要再執行一些工作。</span><span class="sxs-lookup"><span data-stu-id="4c27a-125">If you create an ILB ASE, there are a few more things to do.</span></span>

2. <span data-ttu-id="4c27a-126">建立 ILB ASE 之後，會上傳與您的 ILB ASE 網域相符的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-126">After your ILB ASE is created, an SSL certificate that matches your ILB ASE domain is uploaded.</span></span>

3. <span data-ttu-id="4c27a-127">上傳的 SSL 憑證會指派給 ILB ASE 作為其「預設」SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-127">The uploaded SSL certificate is assigned to the ILB ASE as its "default" SSL certificate.</span></span>  <span data-ttu-id="4c27a-128">如果 ILB ASE 上的應用程式是使用指派給 ASE 的一般根網域 (例如 https://someapp.mycustomrootcomain.com)，此憑證將使用於此應用程式的 SSL 流量。</span><span class="sxs-lookup"><span data-stu-id="4c27a-128">This certificate is used for SSL traffic to apps on the ILB ASE when they use the common root domain that's assigned to the ASE (for example, https://someapp.mycustomrootcomain.com).</span></span>


## <a name="create-the-ase"></a><span data-ttu-id="4c27a-129">建立 ASE</span><span class="sxs-lookup"><span data-stu-id="4c27a-129">Create the ASE</span></span>
<span data-ttu-id="4c27a-130">在 GitHub 上的[範例][quickstartasev2create]中有可建立 ASE 的 Resource Manager 範本及其相關聯的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="4c27a-130">A Resource Manager template that creates an ASE and its associated parameters file is available [in an example][quickstartasev2create] on GitHub.</span></span>

<span data-ttu-id="4c27a-131">如果您想要建立 ILB ASE，請使用這些 Resource Manager 範本[範例][quickstartilbasecreate]。</span><span class="sxs-lookup"><span data-stu-id="4c27a-131">If you want to make an ILB ASE, use these Resource Manager template [examples][quickstartilbasecreate].</span></span> <span data-ttu-id="4c27a-132">它們符合該使用案例。</span><span class="sxs-lookup"><span data-stu-id="4c27a-132">They cater to that use case.</span></span> <span data-ttu-id="4c27a-133">azuredeploy.parameters.json 檔案中的大部分參數是建立 ILB ASE 和外部 ASE 的通用參數。</span><span class="sxs-lookup"><span data-stu-id="4c27a-133">Most of the parameters in the *azuredeploy.parameters.json* file are common to the creation of ILB ASEs and External ASEs.</span></span> <span data-ttu-id="4c27a-134">建立 ILB ASE 時，以下清單會呼叫特殊附註的參數或唯一參數︰</span><span class="sxs-lookup"><span data-stu-id="4c27a-134">The following list calls out parameters of special note, or that are unique, when you create an ILB ASE:</span></span>

* <span data-ttu-id="4c27a-135">interalLoadBalancingMode：在大多數情況下，此屬性設定為 3，這表示連接埠 80/443 上的 HTTP/HTTPS 流量，以及 ASE 上的 FTP 服務所接聽的控制項/資料通道連接埠將會繫結至 ILB 配置的虛擬網路內部位址。</span><span class="sxs-lookup"><span data-stu-id="4c27a-135">*interalLoadBalancingMode*: In most cases, set this to 3, which means both HTTP/HTTPS traffic on ports 80/443, and the control/data channel ports listened to by the FTP service on the ASE, will be bound to an ILB-allocated virtual network internal address.</span></span> <span data-ttu-id="4c27a-136">如果此屬性設定為 2，只有 FTP 服務相關的連接埠 (控制和資料通道) 會繫結至 ILB 位址，</span><span class="sxs-lookup"><span data-stu-id="4c27a-136">If this property is set to 2, only the FTP service-related ports (both control and data channels) are bound to an ILB address.</span></span> <span data-ttu-id="4c27a-137">HTTP/HTTPS 流量將保留在公用 VIP 上。</span><span class="sxs-lookup"><span data-stu-id="4c27a-137">The HTTP/HTTPS traffic remains on the public VIP.</span></span>
* <span data-ttu-id="4c27a-138">dnsSuffix︰這個參數定義要指派給 ASE 的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="4c27a-138">*dnsSuffix*: This parameter defines the default root domain that's assigned to the ASE.</span></span> <span data-ttu-id="4c27a-139">在 Azure App Service 的公用種變化中，所有 Web 應用程式的預設根網域皆為 azurewebsites.net 。</span><span class="sxs-lookup"><span data-stu-id="4c27a-139">In the public variation of Azure App Service, the default root domain for all web apps is *azurewebsites.net*.</span></span> <span data-ttu-id="4c27a-140">由於 ILB ASE 位於客戶虛擬網路的內部，所以不適合使用公用服務的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="4c27a-140">Because an ILB ASE is internal to a customer's virtual network, it doesn't make sense to use the public service's default root domain.</span></span> <span data-ttu-id="4c27a-141">相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。</span><span class="sxs-lookup"><span data-stu-id="4c27a-141">Instead, an ILB ASE should have a default root domain that makes sense for use within a company's internal virtual network.</span></span> <span data-ttu-id="4c27a-142">例如，Contoso Corporation 可能會將 internal-contoso.com 的預設根網域用於只能在 Contoso 虛擬網路內解析和存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c27a-142">For example, Contoso Corporation might use a default root domain of *internal-contoso.com* for apps that are intended to be resolvable and accessible only within Contoso's virtual network.</span></span> 
* <span data-ttu-id="4c27a-143">ipSslAddressCount︰在 azuredeploy.json 檔案中，這個參數的值會自動預設為 0，因為 ILB ASE 只有單一 ILB 位址。</span><span class="sxs-lookup"><span data-stu-id="4c27a-143">*ipSslAddressCount*: This parameter automatically defaults to a value of 0 in the *azuredeploy.json* file because ILB ASEs only have a single ILB address.</span></span> <span data-ttu-id="4c27a-144">ILB ASE 沒有明確的 IP-SSL 位址。</span><span class="sxs-lookup"><span data-stu-id="4c27a-144">There are no explicit IP-SSL addresses for an ILB ASE.</span></span> <span data-ttu-id="4c27a-145">因此，ILB ASE 的 IP-SSL 位址集區必須設定為零。</span><span class="sxs-lookup"><span data-stu-id="4c27a-145">Hence, the IP-SSL address pool for an ILB ASE must be set to zero.</span></span> <span data-ttu-id="4c27a-146">否則，就會發生佈建錯誤。</span><span class="sxs-lookup"><span data-stu-id="4c27a-146">Otherwise, a provisioning error occurs.</span></span> 

<span data-ttu-id="4c27a-147">填入 azuredeploy.parameters.json 檔案後，就可以使用下列 Powershell 程式碼片段建立 ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-147">After the *azuredeploy.parameters.json* file is filled in, create the ASE by using the PowerShell code snippet.</span></span> <span data-ttu-id="4c27a-148">將檔案路徑變更為您電腦上 Resource Manager 範本檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="4c27a-148">Change the file paths to match the Resource Manager template-file locations on your machine.</span></span> <span data-ttu-id="4c27a-149">記得提供您自己的 Resource Manager 部署名稱和資源群組名稱的值：</span><span class="sxs-lookup"><span data-stu-id="4c27a-149">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="4c27a-150">建立 ASE 約需一小時。</span><span class="sxs-lookup"><span data-stu-id="4c27a-150">It takes about an hour for the ASE to be created.</span></span> <span data-ttu-id="4c27a-151">然後在入口網站中，ASE 會顯示在觸發部署之訂用帳戶的 ASE 清單中。</span><span class="sxs-lookup"><span data-stu-id="4c27a-151">Then the ASE shows up in the portal in the list of ASEs for the subscription that triggered the deployment.</span></span>

## <a name="upload-and-configure-the-default-ssl-certificate"></a><span data-ttu-id="4c27a-152">上傳和設定預設SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="4c27a-152">Upload and configure the "default" SSL certificate</span></span>
<span data-ttu-id="4c27a-153">SSL 憑證必須與 ASE 相關聯，作為用來建立應用程式的 SSL 連線的「預設」SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-153">An SSL certificate must be associated with the ASE as the "default" SSL certificate that's used to establish SSL connections to apps.</span></span> <span data-ttu-id="4c27a-154">如果 ASE 的預設 DNS 尾碼是 internal-contoso.com，則連線到 https://some-random-app.internal-contoso.com 需要 *.internal contoso.com 的有效 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-154">If the ASE's default DNS suffix is *internal-contoso.com*, a connection to https://some-random-app.internal-contoso.com requires an SSL certificate that's valid for **.internal-contoso.com*.</span></span> 

<span data-ttu-id="4c27a-155">使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證，取得有效的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-155">Obtain a valid SSL certificate by using internal certificate authorities, purchasing a certificate from an external issuer, or using a self-signed certificate.</span></span> <span data-ttu-id="4c27a-156">無論 SSL 憑證的來源為何，都需要正確設定下列憑證屬性︰</span><span class="sxs-lookup"><span data-stu-id="4c27a-156">Regardless of the source of the SSL certificate, the following certificate attributes must be configured properly:</span></span>

* <span data-ttu-id="4c27a-157">**Subject**：此屬性必須設為 *.your-root-domain-here.com。</span><span class="sxs-lookup"><span data-stu-id="4c27a-157">**Subject**: This attribute must be set to **.your-root-domain-here.com*.</span></span>
* <span data-ttu-id="4c27a-158">**Subject Alternative Name**此屬性必須同時包含 *.your-root-domain-here.com 和 *.scm.your-root-domain-here.com。</span><span class="sxs-lookup"><span data-stu-id="4c27a-158">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here.com* and **.scm.your-root-domain-here.com*.</span></span> <span data-ttu-id="4c27a-159">系統將使用 your-app-name.scm.your-root-domain-here.com 形式的位址，進行與每個應用程式相關聯的 SCM/Kudu 網站的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="4c27a-159">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here.com*.</span></span>

<span data-ttu-id="4c27a-160">備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。</span><span class="sxs-lookup"><span data-stu-id="4c27a-160">With a valid SSL certificate in hand, two additional preparatory steps are needed.</span></span> <span data-ttu-id="4c27a-161">將 SSL 憑證轉換/儲存為 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c27a-161">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="4c27a-162">請記住，.pfx 檔案必須包含所有中繼和根憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-162">Remember that the .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="4c27a-163">使用密碼保護其安全。</span><span class="sxs-lookup"><span data-stu-id="4c27a-163">Secure it with a password.</span></span>

<span data-ttu-id="4c27a-164">必須將 .pfx 檔案轉換成 base64 字串，因為上傳 SSL 憑證會使用 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c27a-164">The .pfx file needs to be converted into a base64 string because the SSL certificate is uploaded by using a Resource Manager template.</span></span> <span data-ttu-id="4c27a-165">因為 Resource Manager 範本是文字檔案，所以必須將 .pfx 檔案轉換成 base64 字串，</span><span class="sxs-lookup"><span data-stu-id="4c27a-165">Because Resource Manager templates are text files, the .pfx file must be converted into a base64 string.</span></span> <span data-ttu-id="4c27a-166">如此才能將其納入範本參數。</span><span class="sxs-lookup"><span data-stu-id="4c27a-166">This way it can be included as a parameter of the template.</span></span>

<span data-ttu-id="4c27a-167">使用以下 PowerShell 程式碼片段來進行：</span><span class="sxs-lookup"><span data-stu-id="4c27a-167">Use the following PowerShell code snippet to:</span></span>

* <span data-ttu-id="4c27a-168">產生自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-168">Generate a self-signed certificate.</span></span>
* <span data-ttu-id="4c27a-169">匯出 .pfx 檔案形式的憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-169">Export the certificate as a .pfx file.</span></span>
* <span data-ttu-id="4c27a-170">將 .pfx 檔案轉換為 base64 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="4c27a-170">Convert the .pfx file into a base64-encoded string.</span></span>
* <span data-ttu-id="4c27a-171">將 base64 編碼的字串儲存到別的檔案。</span><span class="sxs-lookup"><span data-stu-id="4c27a-171">Save the base64-encoded string to a separate file.</span></span> 

<span data-ttu-id="4c27a-172">以下 base64 編碼的 Powershell 程式碼是改寫自 [Powershell 指令碼部落格][examplebase64encoding]：</span><span class="sxs-lookup"><span data-stu-id="4c27a-172">This PowerShell code for base64 encoding was adapted from the [PowerShell scripts blog][examplebase64encoding]:</span></span>

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

<span data-ttu-id="4c27a-173">成功產生 SSL 憑證並轉換成 base64 編碼字串後，使用 GitHub 上的[設定預設 SSL 憑證][quickstartconfiguressl]範例 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c27a-173">After the SSL certificate is successfully generated and converted to a base64-encoded string, use the example Resource Manager template [Configure the default SSL certificate][quickstartconfiguressl] on GitHub.</span></span> 

<span data-ttu-id="4c27a-174">azuredeploy.parameters.json 檔案中有以下參數︰</span><span class="sxs-lookup"><span data-stu-id="4c27a-174">The parameters in the *azuredeploy.parameters.json* file are listed here:</span></span>

* <span data-ttu-id="4c27a-175">︰設定 ILB ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="4c27a-175">*appServiceEnvironmentName*: The name of the ILB ASE being configured.</span></span>
* <span data-ttu-id="4c27a-176">︰包含 ILB ASE 部署所在的 Azure 區域的文字字串。</span><span class="sxs-lookup"><span data-stu-id="4c27a-176">*existingAseLocation*: Text string containing the Azure region where the ILB ASE was deployed.</span></span>  <span data-ttu-id="4c27a-177">例如："South Central US (美國中南部)"。</span><span class="sxs-lookup"><span data-stu-id="4c27a-177">For example: "South Central US".</span></span>
* <span data-ttu-id="4c27a-178">pfxBlobString：.pfx 檔案的 based64 編碼字串表示法。</span><span class="sxs-lookup"><span data-stu-id="4c27a-178">*pfxBlobString*: The based64-encoded string representation of the .pfx file.</span></span> <span data-ttu-id="4c27a-179">使用稍早的程式碼片段，複製 "exportedcert.pfx.b64" 中的字串。</span><span class="sxs-lookup"><span data-stu-id="4c27a-179">Use the code snippet shown earlier and copy the string contained in "exportedcert.pfx.b64".</span></span> <span data-ttu-id="4c27a-180">貼上字串作為 pfxBlobString 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="4c27a-180">Paste it in as the value of the *pfxBlobString* attribute.</span></span>
* <span data-ttu-id="4c27a-181">: The  used to secure the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="4c27a-181">*password*: The password used to secure the .pfx file.</span></span>
* <span data-ttu-id="4c27a-182">︰憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="4c27a-182">*certificateThumbprint*: The certificate's thumbprint.</span></span> <span data-ttu-id="4c27a-183">如果您從 Powershell 擷取此值 (例如先前程式碼片段中的 $certificate.Thumbprint )，可以直接使用該值。</span><span class="sxs-lookup"><span data-stu-id="4c27a-183">If you retrieve this value from PowerShell (for example, *$certificate.Thumbprint* from the earlier code snippet), you can use the value as is.</span></span> <span data-ttu-id="4c27a-184">如果您從 Windows 憑證對話方塊中複製此值，請記得去除多餘的空格。</span><span class="sxs-lookup"><span data-stu-id="4c27a-184">If you copy the value from the Windows certificate dialog box, remember to strip out the extraneous spaces.</span></span> <span data-ttu-id="4c27a-185">CertificateThumbprint 應該像這樣：AF3143EB61D43F6727842115BB7F17BBCECAECAE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-185">The *certificateThumbprint* should look something like  AF3143EB61D43F6727842115BB7F17BBCECAECAE.</span></span>
* <span data-ttu-id="4c27a-186">︰您自己選擇的好記字串識別碼，可用來識別憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-186">*certificateName*: A friendly string identifier of your own choosing used to identity the certificate.</span></span> <span data-ttu-id="4c27a-187">Microsoft.Web/certificates 實體表示 SSL 憑證，而此名稱會作為實體的唯一 Resource Manager 識別碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="4c27a-187">The name is used as part of the unique Resource Manager identifier for the *Microsoft.Web/certificates* entity that represents the SSL certificate.</span></span> <span data-ttu-id="4c27a-188">名稱「必須」以下列尾碼結尾︰\_yourASENameHere_InternalLoadBalancingASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-188">The name *must* end with the following suffix: \_yourASENameHere_InternalLoadBalancingASE.</span></span> <span data-ttu-id="4c27a-189">Azure 入口網站會以這個尾碼為指標，表示憑證要用於保護啟用 ILB 的 ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-189">The Azure portal uses this suffix as an indicator that the certificate is used to secure an ILB-enabled ASE.</span></span>

<span data-ttu-id="4c27a-190">以下是 azuredeploy.parameters.json  的縮簡範例︰</span><span class="sxs-lookup"><span data-stu-id="4c27a-190">An abbreviated example of *azuredeploy.parameters.json* is shown here:</span></span>

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

<span data-ttu-id="4c27a-191">填入 azuredeploy.parameters.json 檔案後，使用下列 Powershell 程式碼片段設定預設 SSL。</span><span class="sxs-lookup"><span data-stu-id="4c27a-191">After the *azuredeploy.parameters.json* file is filled in, configure the default SSL certificate by using the PowerShell code snippet.</span></span> <span data-ttu-id="4c27a-192">將檔案路徑變更為您電腦上 Resource Manager 範本檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="4c27a-192">Change the file paths to match where the Resource Manager template files are located on your machine.</span></span> <span data-ttu-id="4c27a-193">記得提供您自己的 Resource Manager 部署名稱和資源群組名稱的值：</span><span class="sxs-lookup"><span data-stu-id="4c27a-193">Remember to supply your own values for the Resource Manager deployment name and the resource group name:</span></span>

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

<span data-ttu-id="4c27a-194">每個 ASE 前端套用變更大約需要 40 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4c27a-194">It takes roughly 40 minutes per ASE front end to apply the change.</span></span> <span data-ttu-id="4c27a-195">例如，有一個預設大小的 ASE 使用兩個前端，則範本將需要大約一小時 20 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="4c27a-195">For example, for a default-sized ASE that uses two front ends, the template takes around one hour and 20 minutes to complete.</span></span> <span data-ttu-id="4c27a-196">執行範本時，無法調整 ASE。</span><span class="sxs-lookup"><span data-stu-id="4c27a-196">While the template is running, the ASE can't scale.</span></span>  

<span data-ttu-id="4c27a-197">範本完成之後，可以透過 HTTPS 存取 ILB ASE 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c27a-197">After the template finishes, apps on the ILB ASE can be accessed over HTTPS.</span></span> <span data-ttu-id="4c27a-198">此連線使用預設 SSL 憑證加以保護。</span><span class="sxs-lookup"><span data-stu-id="4c27a-198">The connections are secured by using the default SSL certificate.</span></span> <span data-ttu-id="4c27a-199">如果 ILB ASE 上的應用程式是使用應用程式名稱加上預設主機名稱的組合來定址，則會使用預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-199">The default SSL certificate is used when apps on the ILB ASE are addressed by using a combination of the application name plus the default host name.</span></span> <span data-ttu-id="4c27a-200">例如，https://mycustomapp.internal-contoso.com 會使用 *.internal contoso.com 的預設 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4c27a-200">For example, https://mycustomapp.internal-contoso.com uses the default SSL certificate for **.internal-contoso.com*.</span></span>

<span data-ttu-id="4c27a-201">不過，就如同在公用多租用戶服務上執行的應用程式，開發人員可以為個別的應用程式設定自訂主機名稱。</span><span class="sxs-lookup"><span data-stu-id="4c27a-201">However, just like apps that run on the public multitenant service, developers can configure custom host names for individual apps.</span></span> <span data-ttu-id="4c27a-202">他們也可以為個別的應用程式設定唯一 SNI SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="4c27a-202">They also can configure unique SNI SSL certificate bindings for individual apps.</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="4c27a-203">App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="4c27a-203">App Service Environment v1</span></span> ##
<span data-ttu-id="4c27a-204">App Service Environment 有兩個版本：ASEv1 和 ASEv2。</span><span class="sxs-lookup"><span data-stu-id="4c27a-204">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="4c27a-205">前述資訊架構在 ASEv2 上。</span><span class="sxs-lookup"><span data-stu-id="4c27a-205">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="4c27a-206">本節說明 ASEv1 與 ASEv2 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="4c27a-206">This section shows you the differences between ASEv1 and ASEv2.</span></span>

<span data-ttu-id="4c27a-207">在 ASEv1 中，要手動管理所有資源，</span><span class="sxs-lookup"><span data-stu-id="4c27a-207">In ASEv1, you manage all of the resources manually.</span></span> <span data-ttu-id="4c27a-208">包括前端、背景工作角色和用於 IP 型 SSL 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4c27a-208">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="4c27a-209">首先，您必須將想要在其中裝載的背景工作角色集區相應放大，才能相應放大 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4c27a-209">Before you can scale out your App Service plan, you must scale out the worker pool that you want to host it.</span></span>

<span data-ttu-id="4c27a-210">ASEv1 使用與 ASEv2 不同的定價模式。</span><span class="sxs-lookup"><span data-stu-id="4c27a-210">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="4c27a-211">在 ASEv1 中，要支付每個配置的核心，</span><span class="sxs-lookup"><span data-stu-id="4c27a-211">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="4c27a-212">包括用於前端或未裝載任何工作負載之背景工作角色的核心。</span><span class="sxs-lookup"><span data-stu-id="4c27a-212">That includes cores that are used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="4c27a-213">在 ASEv1 中，ASE 的預設最大調整大小總計是 55 個主機，</span><span class="sxs-lookup"><span data-stu-id="4c27a-213">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="4c27a-214">包括背景工作角色與前端。</span><span class="sxs-lookup"><span data-stu-id="4c27a-214">That includes workers and front ends.</span></span> <span data-ttu-id="4c27a-215">ASEv1 的其中一個優點，是可以部署在傳統虛擬網路和 Resource Manager虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="4c27a-215">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="4c27a-216">若要深入了解 ASEv1，請參閱 [App Service Environment v1 簡介][ASEv1Intro]。</span><span class="sxs-lookup"><span data-stu-id="4c27a-216">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<span data-ttu-id="4c27a-217">若要使用 Resource Manager 範本建立 ASEv1，請參閱[使用 Resource Manager 範本建立 ILB ASE v1][ILBASEv1Template]。</span><span class="sxs-lookup"><span data-stu-id="4c27a-217">To create an ASEv1 by using a Resource Manager template, see [Create an ILB ASE v1 with a Resource Manager template][ILBASEv1Template].</span></span>


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
