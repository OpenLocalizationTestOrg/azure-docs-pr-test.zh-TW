---
title: "產生並匯出點對站的憑證：MakeCert：Azure | Microsoft Docs"
description: "本文包含的步驟可用來建立自我簽署的根憑證、匯出公開金鑰，以及使用 MakeCert 來產生用戶端憑證。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 4c51edac3b1cdafae8f9543bd0e3133b6a050f73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a><span data-ttu-id="31920-103">使用 MakeCert 來產生並匯出點對站連線的憑證</span><span class="sxs-lookup"><span data-stu-id="31920-103">Generate and export certificates for Point-to-Site connections using MakeCert</span></span>

<span data-ttu-id="31920-104">點對站連線使用憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="31920-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="31920-105">本文說明如何建立自我簽署的根憑證，以及使用 MakeCert 來產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-105">This article shows you how to create a self-signed root certificate and generate client certificates using MakeCert.</span></span> <span data-ttu-id="31920-106">如果您要尋找點對站設定步驟 (例如如何上傳根憑證)，請從下列清單中選取其中一篇＜設定點對站＞文章：</span><span class="sxs-lookup"><span data-stu-id="31920-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31920-107">建立自我簽署憑證 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="31920-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="31920-108">建立自我簽署憑證 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="31920-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="31920-109">設定點對站 - Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31920-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="31920-110">設定點對站 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="31920-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="31920-111">設定點對站 - 傳統 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31920-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

<span data-ttu-id="31920-112">雖然建議您使用 [Windows 10 PowerShell 步驟](vpn-gateway-certificates-point-to-site.md)建立您的憑證，但是提供這些 MakeCert 指示作為選擇性方法。</span><span class="sxs-lookup"><span data-stu-id="31920-112">While we recommend using the [Windows 10 PowerShell steps](vpn-gateway-certificates-point-to-site.md) to create your certificates, we provide these MakeCert instructions as an optional method.</span></span> <span data-ttu-id="31920-113">您使用任一種方法所產生的憑證可以安裝於[任何支援的用戶端作業系統](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)。</span><span class="sxs-lookup"><span data-stu-id="31920-113">The certificates that you generate using either method can be installed on [any supported client operating system](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).</span></span> <span data-ttu-id="31920-114">不過，MakeCert 具有下列限制：</span><span class="sxs-lookup"><span data-stu-id="31920-114">However, MakeCert has the following limitation:</span></span>

* <span data-ttu-id="31920-115">MakeCert 已被取代。</span><span class="sxs-lookup"><span data-stu-id="31920-115">MakeCert is deprecated.</span></span> <span data-ttu-id="31920-116">這表示無法在任何時間點移除這項工具。</span><span class="sxs-lookup"><span data-stu-id="31920-116">This means that this tool could be removed at any point.</span></span> <span data-ttu-id="31920-117">當無法再使用 MakeCert 時，任何您已經使用 MakeCert 所產生的憑證將不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="31920-117">Any certificates that you already generated using MakeCert won't be affected when MakeCert is no longer available.</span></span> <span data-ttu-id="31920-118">MakeCert 只用來產生憑證，而不是驗證機制。</span><span class="sxs-lookup"><span data-stu-id="31920-118">MakeCert is only used to generate the certificates, not as a validating mechanism.</span></span>

## <span data-ttu-id="31920-119"><a name="rootcert"></a>建立自我簽署根憑證</span><span class="sxs-lookup"><span data-stu-id="31920-119"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="31920-120">下列步驟說明如何使用 MakeCert 來建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-120">The following steps show you how to create a self-signed certificate using MakeCert.</span></span> <span data-ttu-id="31920-121">這些並非部署模型特定的步驟。</span><span class="sxs-lookup"><span data-stu-id="31920-121">These steps are not deployment-model specific.</span></span> <span data-ttu-id="31920-122">它們同樣適用於資源管理員和傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="31920-122">They are valid for both Resource Manager and classic.</span></span>

1. <span data-ttu-id="31920-123">下載並安裝 [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="31920-123">Download and install [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).</span></span>
2. <span data-ttu-id="31920-124">安裝之後，您通常可以在下列路徑中找到 makecert.exe 公用程式：'C:\Program Files (x86)\Windows Kits\10\bin\<arch>'。</span><span class="sxs-lookup"><span data-stu-id="31920-124">After installation, you can typically find the makecert.exe utility under this path: 'C:\Program Files (x86)\Windows Kits\10\bin\<arch>'.</span></span> <span data-ttu-id="31920-125">雖然，它有可能已安裝到另一個位置。</span><span class="sxs-lookup"><span data-stu-id="31920-125">Although, it's possible that it was installed to another location.</span></span> <span data-ttu-id="31920-126">以系統管理員身分開啟命令提示字元，然後瀏覽至 MakeCert 公用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="31920-126">Open a command prompt as administrator and navigate to the location of the MakeCert utility.</span></span> <span data-ttu-id="31920-127">您可以使用下列範例，並針對適當的位置進行調整：</span><span class="sxs-lookup"><span data-stu-id="31920-127">You can use the following example, adjusting for the proper location:</span></span>

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. <span data-ttu-id="31920-128">在您電腦上的 [個人] 憑證存放區中建立並安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-128">Create and install a certificate in the Personal certificate store on your computer.</span></span> <span data-ttu-id="31920-129">下列範例會建立對應的 .cer 檔案，您在設定 P2S 時會將此檔案上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="31920-129">The following example creates a corresponding *.cer* file that you upload to Azure when configuring P2S.</span></span> <span data-ttu-id="31920-130">將 'P2SRootCert' 和 'P2SRootCert.cer' 取代為您想使用的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="31920-130">Replace 'P2SRootCert' and 'P2SRootCert.cer' with the name that you want to use for the certificate.</span></span> <span data-ttu-id="31920-131">憑證位於您的 '[憑證 - 目前的使用者]\[個人]\[憑證]' 中。</span><span class="sxs-lookup"><span data-stu-id="31920-131">The certificate is located in your 'Certificates - Current User\Personal\Certificates'.</span></span>

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <span data-ttu-id="31920-132"><a name="cer"></a>匯出公開金鑰 (.cer)</span><span class="sxs-lookup"><span data-stu-id="31920-132"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="31920-133">匯出的 .cer 檔案必須上傳到 Azure。</span><span class="sxs-lookup"><span data-stu-id="31920-133">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="31920-134">如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)。</span><span class="sxs-lookup"><span data-stu-id="31920-134">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile).</span></span> <span data-ttu-id="31920-135">若要新增其他可信任的根憑證，請參閱這篇文章的[本節](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add)。</span><span class="sxs-lookup"><span data-stu-id="31920-135">To add an additional trusted root certificate, see [this section](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) of the article.</span></span>

### <a name="export-the-self-signed-certificate-and-private-key-to-store-it-optional"></a><span data-ttu-id="31920-136">匯出自我簽署憑證和私密金鑰來儲存它 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="31920-136">Export the self-signed certificate and private key to store it (optional)</span></span>

<span data-ttu-id="31920-137">您可能想要匯出自我簽署的根憑證，並將它安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="31920-137">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="31920-138">如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="31920-138">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="31920-139">若要將自我簽署的根憑證匯出為 .pfx，請選取根憑證，然後使用與[匯出用戶端憑證](#clientexport)所述的相同步驟來匯出。</span><span class="sxs-lookup"><span data-stu-id="31920-139">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <a name="create-and-install-client-certificates"></a><span data-ttu-id="31920-140">建立並安裝用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="31920-140">Create and install client certificates</span></span>

<span data-ttu-id="31920-141">您未直接在用戶端電腦上安裝自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-141">You don't install the self-signed certificate directly on the client computer.</span></span> <span data-ttu-id="31920-142">您需要從自我簽署憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-142">You need to generate a client certificate from the self-signed certificate.</span></span> <span data-ttu-id="31920-143">您接著會將用戶端憑證匯出並安裝到用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="31920-143">You then export and install the client certificate to the client computer.</span></span> <span data-ttu-id="31920-144">下列步驟並非針對特定部署模型。</span><span class="sxs-lookup"><span data-stu-id="31920-144">The following steps are not deployment-model specific.</span></span> <span data-ttu-id="31920-145">它們同樣適用於資源管理員和傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="31920-145">They are valid for both Resource Manager and classic.</span></span>

### <span data-ttu-id="31920-146"><a name="clientcert"></a>產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="31920-146"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="31920-147">每個使用點對站連線至 VNet 的用戶端電腦都必須安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-147">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="31920-148">您可以從自我簽署根憑證產生用戶端憑證，然後匯出及安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-148">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="31920-149">如果未安裝用戶端憑證，則驗證會失敗。</span><span class="sxs-lookup"><span data-stu-id="31920-149">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="31920-150">下列步驟將逐步引導您完成從自我簽署的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-150">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="31920-151">您可以從相同根憑證產生多個用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-151">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="31920-152">當您使用下列步驟產生用戶端憑證時，用戶端憑證會自動安裝在您用來產生憑證的電腦上。</span><span class="sxs-lookup"><span data-stu-id="31920-152">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="31920-153">如果您想要在另一部用戶端電腦上安裝用戶端憑證，您可以匯出憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-153">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>
 
1. <span data-ttu-id="31920-154">在用來建立自我簽署憑證的相同電腦上，以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="31920-154">On the same computer that you used to create the self-signed certificate, open a command prompt as administrator.</span></span>
2. <span data-ttu-id="31920-155">修改並執行範例以產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="31920-155">Modify and run the sample to generate a client certificate.</span></span>
  * <span data-ttu-id="31920-156">將 *"P2SRootCert"* 變更為您從中產生用戶端憑證的自我簽署根憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="31920-156">Change *"P2SRootCert"* to the name of the self-signed root that you are generating the client certificate from.</span></span> <span data-ttu-id="31920-157">確定您使用的是根憑證名稱，亦即您建立自我簽署根憑證時所指定的 'CN=' 值。</span><span class="sxs-lookup"><span data-stu-id="31920-157">Make sure you are using the name of the root certificate, which is whatever the 'CN=' value was that you specified when you created the self-signed root.</span></span>
  * <span data-ttu-id="31920-158">將 *P2SChildCert* 變更為所產生的用戶端憑證要使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="31920-158">Change *P2SChildCert* to the name you want to generate a client certificate to be.</span></span>

  <span data-ttu-id="31920-159">如果您執行以下範例而未做任何修改，您的個人憑證存放區中就會有一個從根憑證 P2SRootCert 產生的用戶端憑證，名為 P2SChildcert。</span><span class="sxs-lookup"><span data-stu-id="31920-159">If you run the following example without modifying it, the result is a client certificate named P2SChildcert in your Personal certificate store that was generated from root certificate P2SRootCert.</span></span>

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <span data-ttu-id="31920-160"><a name="clientexport"></a>匯出用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="31920-160"><a name="clientexport"></a>Export a client certificate</span></span>

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <span data-ttu-id="31920-161"><a name="install"></a>安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="31920-161"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="31920-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31920-162">Next steps</span></span>

<span data-ttu-id="31920-163">繼續使用您的點對站設定。</span><span class="sxs-lookup"><span data-stu-id="31920-163">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="31920-164">如需 **Resource Manager** 部署模型步驟，請參閱[設定 VNet 的點對站連線](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="31920-164">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="31920-165">如需**傳統**部署模型步驟，請參閱[設定 VNet 的點對站 VPN 連線 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="31920-165">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
