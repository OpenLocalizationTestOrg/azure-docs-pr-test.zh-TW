---
title: "產生並匯出點對站的憑證：PowerShell：Azure | Microsoft Docs"
description: "本文中的步驟用來建立自我簽署的根憑證、匯出公開金鑰，以及使用 PowerShell 在 Windows 10 上產生用戶端憑證。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: f96b9b212b9322d0677e49ff95184d0feccca2df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="5f39e-103">使用 Windows 10 的 PowerShell 來產生並匯出點對站連線的憑證</span><span class="sxs-lookup"><span data-stu-id="5f39e-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="5f39e-104">點對站連線使用憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="5f39e-105">本文說明如何使用 Windows 10 的 PowerShell 來建立自我簽署的根憑證，以及產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-105">This article shows you how to create a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="5f39e-106">如果您要尋找點對站設定步驟 (例如如何上傳根憑證)，請從下列清單中選取其中一篇＜設定點對站＞文章：</span><span class="sxs-lookup"><span data-stu-id="5f39e-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f39e-107">建立自我簽署憑證 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f39e-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="5f39e-108">建立自我簽署憑證 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="5f39e-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="5f39e-109">設定點對站 - Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5f39e-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="5f39e-110">設定點對站 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f39e-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="5f39e-111">設定點對站 - 傳統 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5f39e-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="5f39e-112">您必須在執行 Windows 10 的電腦上執行本文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f39e-112">You must perform the steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="5f39e-113">用於產生憑證的 PowerShell Cmdlet 是屬於 Windows 10 作業系統的一部分，在其他 Windows 版本上無法運作。</span><span class="sxs-lookup"><span data-stu-id="5f39e-113">The PowerShell cmdlets that you use to generate certificates are part of the Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="5f39e-114">因此，您需要使用 Windows 10 電腦來產生憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-114">The Windows 10 computer is only needed to generate the certificates.</span></span> <span data-ttu-id="5f39e-115">產生憑證之後，您即可上傳憑證或將其安裝在任何支援的用戶端作業系統上。</span><span class="sxs-lookup"><span data-stu-id="5f39e-115">Once the certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="5f39e-116">如果您無法存取 Windows 10 電腦，則可以使用 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) 來產生憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-116">If you do not have access to a Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) to generate certificates.</span></span> <span data-ttu-id="5f39e-117">使用任一種方法所產生的憑證均可安裝在任何[支援的](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)用戶端作業系統上。</span><span class="sxs-lookup"><span data-stu-id="5f39e-117">The certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="5f39e-118"><a name="rootcert"></a>建立自我簽署根憑證</span><span class="sxs-lookup"><span data-stu-id="5f39e-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="5f39e-119">您可以使用 New-SelfSignedCertificate Cmdlet 來建立自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-119">Use the New-SelfSignedCertificate cmdlet to create a self-signed root certificate.</span></span> <span data-ttu-id="5f39e-120">如需其他的參數資訊，請參閱 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="5f39e-121">從執行 Windows 10 的電腦，以提高的權限開啟 Windows PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="5f39e-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="5f39e-122">使用下列範例建立自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-122">Use the following example to create the self-signed root certificate.</span></span> <span data-ttu-id="5f39e-123">下列範例會建立名為 'P2SRootCert' 的自我簽署的根憑證，其自動安裝在 'Certificates-Current User\Personal\Certificates' 中。</span><span class="sxs-lookup"><span data-stu-id="5f39e-123">The following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="5f39e-124">您可以開啟 *certmgr.msc* 或 [管理使用者憑證] 來檢視憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-124">You can view the certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="5f39e-125"><a name="cer"></a>匯出公開金鑰 (.cer)</span><span class="sxs-lookup"><span data-stu-id="5f39e-125"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="5f39e-126">匯出的 .cer 檔案必須上傳到 Azure。</span><span class="sxs-lookup"><span data-stu-id="5f39e-126">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="5f39e-127">如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-rm-ps.md#upload)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="5f39e-128">若要新增其他可信任的根憑證，請參閱文章的[這一節](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-128">To add an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of the article.</span></span>

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a><span data-ttu-id="5f39e-129">匯出自我簽署根憑證和公開金鑰來儲存它 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="5f39e-129">Export the self-signed root certificate and public key to store it (optional)</span></span>

<span data-ttu-id="5f39e-130">您可能想要匯出自我簽署的根憑證，並將它安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="5f39e-130">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="5f39e-131">如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f39e-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="5f39e-132">若要將自我簽署的根憑證匯出為 .pfx，請選取根憑證，然後使用與[匯出用戶端憑證](#clientexport)所述的相同步驟來匯出。</span><span class="sxs-lookup"><span data-stu-id="5f39e-132">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="5f39e-133"><a name="clientcert"></a>產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="5f39e-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="5f39e-134">每個使用點對站連線至 VNet 的用戶端電腦都必須安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-134">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="5f39e-135">您可以從自我簽署根憑證產生用戶端憑證，然後匯出及安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-135">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="5f39e-136">如果未安裝用戶端憑證，則驗證會失敗。</span><span class="sxs-lookup"><span data-stu-id="5f39e-136">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="5f39e-137">下列步驟將逐步引導您完成從自我簽署的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-137">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="5f39e-138">您可以從相同根憑證產生多個用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-138">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="5f39e-139">當您使用下列步驟產生用戶端憑證時，用戶端憑證會自動安裝在您用來產生憑證的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5f39e-139">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="5f39e-140">如果您想要在另一部用戶端電腦上安裝用戶端憑證，您可以匯出憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-140">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>

<span data-ttu-id="5f39e-141">此範例會使用 New-SelfSignedCertificate Cmdlet 來產生有效期為一年的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-141">The examples use the New-SelfSignedCertificate cmdlet to generate a client certificate that expires in one year.</span></span> <span data-ttu-id="5f39e-142">如需其他的參數資訊 (例如針對用戶端憑證設定不同的到期值)，請參閱 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-142">For additional parameter information, such as setting a different expiration value for the client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="5f39e-143">範例 1</span><span class="sxs-lookup"><span data-stu-id="5f39e-143">Example 1</span></span>

<span data-ttu-id="5f39e-144">此範例會使用從上一節宣告的 '$cert' 變數。</span><span class="sxs-lookup"><span data-stu-id="5f39e-144">This example uses the declared '$cert' variable from the previous section.</span></span> <span data-ttu-id="5f39e-145">如果您在建立自我簽署根憑證之後關閉 PowerShell 主控台，或是在新的 PowerShell 主控台工作階段中建立其他用戶端憑證，請使用[範例 2](#ex2) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f39e-145">If you closed the PowerShell console after creating the self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use the steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="5f39e-146">修改並執行範例以產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-146">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="5f39e-147">如果您執行下列範例，但未加以修改，結果會是名為 'P2SChildCert' 的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-147">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="5f39e-148">如果您要將子憑證命名為其他名稱，請修改 CN 值。</span><span class="sxs-lookup"><span data-stu-id="5f39e-148">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="5f39e-149">執行這個範例時，請勿變更 TextExtension。</span><span class="sxs-lookup"><span data-stu-id="5f39e-149">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="5f39e-150">您產生的用戶端憑證會自動安裝在您電腦的 'Certificates - Current User\Personal\Certificates' 中。</span><span class="sxs-lookup"><span data-stu-id="5f39e-150">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="5f39e-151"><a name="ex2"></a>範例 2</span><span class="sxs-lookup"><span data-stu-id="5f39e-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="5f39e-152">如果您要建立其他用戶端憑證，或者不是使用您用來建立自我簽署根憑證的相同 PowerShell 工作階段，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5f39e-152">If you are creating additional client certificates, or are not using the same PowerShell session that you used to create your self-signed root certificate, use the following steps:</span></span>

1. <span data-ttu-id="5f39e-153">識別安裝在電腦上的自我簽署根憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-153">Identify the self-signed root certificate that is installed on the computer.</span></span> <span data-ttu-id="5f39e-154">此 Cmdlet 會傳回安裝於電腦上的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="5f39e-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="5f39e-155">從傳回的清單尋找主體名稱，然後將其旁邊的指紋複製到文字檔。</span><span class="sxs-lookup"><span data-stu-id="5f39e-155">Locate the subject name from the returned list, then copy the thumbprint that is located next to it to a text file.</span></span> <span data-ttu-id="5f39e-156">在下列範例中，有兩個憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-156">In the following example, there are two certificates.</span></span> <span data-ttu-id="5f39e-157">CN 名稱是您要從中產生子憑證之自我簽署根憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f39e-157">The CN name is the name of the self-signed root certificate from which you want to generate a child certificate.</span></span> <span data-ttu-id="5f39e-158">在此例中為 'P2SRootCert'。</span><span class="sxs-lookup"><span data-stu-id="5f39e-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="5f39e-159">使用上一個步驟中的指紋，為根憑證宣告一個變數。</span><span class="sxs-lookup"><span data-stu-id="5f39e-159">Declare a variable for the root certificate using the thumbprint from the previous step.</span></span> <span data-ttu-id="5f39e-160">將 THUMBPRINT 替換為您要從中產生子憑證之根憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="5f39e-160">Replace THUMBPRINT with the thumbprint of the root certificate from which you want to generate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="5f39e-161">例如，使用上一個步驟中的 P2SRootCert 的指紋，變數會如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5f39e-161">For example, using the thumbprint for P2SRootCert in the previous step, the variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="5f39e-162">修改並執行範例以產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-162">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="5f39e-163">如果您執行下列範例，但未加以修改，結果會是名為 'P2SChildCert' 的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f39e-163">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="5f39e-164">如果您要將子憑證命名為其他名稱，請修改 CN 值。</span><span class="sxs-lookup"><span data-stu-id="5f39e-164">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="5f39e-165">執行這個範例時，請勿變更 TextExtension。</span><span class="sxs-lookup"><span data-stu-id="5f39e-165">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="5f39e-166">您產生的用戶端憑證會自動安裝在您電腦的 'Certificates - Current User\Personal\Certificates' 中。</span><span class="sxs-lookup"><span data-stu-id="5f39e-166">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="5f39e-167"><a name="clientexport"></a>匯出用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="5f39e-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="5f39e-168"><a name="install"></a>安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="5f39e-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f39e-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f39e-169">Next steps</span></span>

<span data-ttu-id="5f39e-170">繼續使用您的點對站設定。</span><span class="sxs-lookup"><span data-stu-id="5f39e-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="5f39e-171">如需 **Resource Manager** 部署模型步驟，請參閱[設定 VNet 的點對站連線](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="5f39e-172">如需**傳統**部署模型步驟，請參閱[設定 VNet 的點對站 VPN 連線 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5f39e-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>