---
title: "產生並匯出點對站的憑證：PowerShell：Azure | Microsoft Docs"
description: "本文章包含步驟 toocreate 自我簽署的根憑證、 匯出 hello 公開金鑰，並產生使用 PowerShell 在 Windows 10 上的用戶端憑證。"
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
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="c755c-103">使用 Windows 10 的 PowerShell 來產生並匯出點對站連線的憑證</span><span class="sxs-lookup"><span data-stu-id="c755c-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="c755c-104">點對站連線使用憑證 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="c755c-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="c755c-105">本文示範如何 toocreate 的自我簽署根憑證，並產生使用 PowerShell 在 Windows 10 上的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="c755c-106">如果您要尋找的點對站台的設定步驟，例如 tooupload 根憑證，來選取其中一個 hello '設定點對站' 發行項的 hello 下列清單的方式：</span><span class="sxs-lookup"><span data-stu-id="c755c-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c755c-107">建立自我簽署憑證 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c755c-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="c755c-108">建立自我簽署憑證 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="c755c-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="c755c-109">設定點對站 - Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c755c-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c755c-110">設定點對站 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c755c-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="c755c-111">設定點對站 - 傳統 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c755c-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="c755c-112">您必須在本文中執行 Windows 10 的電腦上執行 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="c755c-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="c755c-113">您使用 toogenerate 憑證 hello PowerShell cmdlet hello Windows 10 作業系統的一部分，而且無法在其他版本的 Windows 中運作。</span><span class="sxs-lookup"><span data-stu-id="c755c-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="c755c-114">hello Windows 10 電腦是只有需要的 toogenerate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="c755c-115">一旦產生 hello 憑證，您可以上傳，或在任何支援的用戶端作業系統上安裝它們。</span><span class="sxs-lookup"><span data-stu-id="c755c-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="c755c-116">如果您沒有存取 tooa Windows 10 電腦，您可以使用[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate 憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="c755c-117">hello 憑證，您可以產生使用哪一種方法可以安裝在任何[支援](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)用戶端作業系統。</span><span class="sxs-lookup"><span data-stu-id="c755c-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="c755c-118"><a name="rootcert"></a>建立自我簽署根憑證</span><span class="sxs-lookup"><span data-stu-id="c755c-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="c755c-119">使用 hello New-selfsignedcertificate cmdlet toocreate 自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="c755c-120">如需其他的參數資訊，請參閱 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="c755c-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="c755c-121">從執行 Windows 10 的電腦，以提高的權限開啟 Windows PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="c755c-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="c755c-122">使用下列範例 toocreate hello 自我簽署的根憑證的 hello。</span><span class="sxs-lookup"><span data-stu-id="c755c-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="c755c-123">hello 下列範例會建立名為 'P2SRootCert'，會自動安裝在 '憑證-目前 \' 的自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="c755c-124">您可以開啟來檢視 hello 憑證*certmgr.msc*，或*管理使用者憑證*。</span><span class="sxs-lookup"><span data-stu-id="c755c-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="c755c-125"><a name="cer"></a>匯出 hello 公開金鑰 (.cer)</span><span class="sxs-lookup"><span data-stu-id="c755c-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="c755c-126">hello exported.cer 檔案必須上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c755c-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="c755c-127">如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-rm-ps.md#upload)。</span><span class="sxs-lookup"><span data-stu-id="c755c-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="c755c-128">tooadd 其他信任的根憑證，[本節](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert)hello 發行項。</span><span class="sxs-lookup"><span data-stu-id="c755c-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="c755c-129">匯出 hello 自我簽署的根憑證和公開金鑰的金鑰 toostore 它 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="c755c-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="c755c-130">您可能想 tooexport hello 自我簽署根憑證，並將它安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="c755c-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="c755c-131">如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="c755c-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="c755c-132">tooexport hello 自我簽署根憑證.pfx hello 選取根憑證，使用 hello 相同的步驟中所述[用戶端憑證匯出](#clientexport)。</span><span class="sxs-lookup"><span data-stu-id="c755c-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="c755c-133"><a name="clientcert"></a>產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="c755c-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="c755c-134">每個連線 tooa 的用戶端電腦使用點對站台的 VNet 必須安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="c755c-135">您 hello 自我簽署的根憑證，從產生的用戶端憑證，然後匯出及安裝 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="c755c-136">如果未安裝 hello 用戶端憑證，驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="c755c-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="c755c-137">hello 下列步驟引導您完成從自我簽署的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="c755c-138">您可以從 hello 產生多個用戶端憑證相同的根憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="c755c-139">當您產生用戶端憑證使用 hello 執行下列步驟時，hello 用戶端憑證會自動安裝 hello 電腦上，您會使用 toogenerate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="c755c-140">如果您想 tooinstall 另一部用戶端電腦上的用戶端憑證，您可以匯出 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="c755c-141">hello 範例會使用 hello New-selfsignedcertificate cmdlet toogenerate 一年中到期的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="c755c-142">額外的參數資訊，例如，設定不同的到期值 hello 用戶端憑證，請參閱[New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="c755c-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="c755c-143">範例 1</span><span class="sxs-lookup"><span data-stu-id="c755c-143">Example 1</span></span>

<span data-ttu-id="c755c-144">這個範例會使用 hello '$cert' hello 前一節的變數宣告。</span><span class="sxs-lookup"><span data-stu-id="c755c-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="c755c-145">如果建立 hello 自我簽署的根憑證，或其他用戶端憑證中，以建立新的 PowerShell 主控台工作階段之後，您可以關閉 hello PowerShell 主控台，使用中的 hello 步驟[範例 2](#ex2)。</span><span class="sxs-lookup"><span data-stu-id="c755c-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="c755c-146">修改並執行 hello 範例 toogenerate 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="c755c-147">如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 'P2SChildCert' 的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="c755c-148">如果您想 tooname hello 子憑證其他項目，修改 hello CN 值。</span><span class="sxs-lookup"><span data-stu-id="c755c-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="c755c-149">執行這個範例時，請勿變更 hello TextExtension。</span><span class="sxs-lookup"><span data-stu-id="c755c-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="c755c-150">'憑證-目前的憑證' 自動安裝 hello 您產生的用戶端憑證在電腦上。</span><span class="sxs-lookup"><span data-stu-id="c755c-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="c755c-151"><a name="ex2"></a>範例 2</span><span class="sxs-lookup"><span data-stu-id="c755c-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="c755c-152">如果您要建立額外的用戶端憑證，或者不是使用 hello 相同您使用 toocreate 您的自我簽署的根憑證，下列步驟使用 hello 的 PowerShell 工作階段：</span><span class="sxs-lookup"><span data-stu-id="c755c-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="c755c-153">識別 hello hello 電腦已安裝的自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="c755c-154">此 Cmdlet 會傳回安裝於電腦上的憑證清單。</span><span class="sxs-lookup"><span data-stu-id="c755c-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="c755c-155">找出 hello 主旨名稱 hello 傳回清單，然後複製 hello 指紋是位於 下一步 tooit tooa 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="c755c-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="c755c-156">在下列範例的 hello，有兩個憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="c755c-157">hello CN 名稱是 hello hello 自我簽署的根憑證，您要 toogenerate 子憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="c755c-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="c755c-158">在此例中為 'P2SRootCert'。</span><span class="sxs-lookup"><span data-stu-id="c755c-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="c755c-159">宣告一個變數來使用 hello 先前步驟中的 hello 指紋 hello 根憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="c755c-160">憑證指紋取代 hello hello 要從中 toogenerate 子憑證的根憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="c755c-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="c755c-161">例如，使用 P2SRootCert hello 指紋 hello 上一個步驟中，hello 變數看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="c755c-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="c755c-162">修改並執行 hello 範例 toogenerate 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="c755c-163">如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 'P2SChildCert' 的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c755c-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="c755c-164">如果您想 tooname hello 子憑證其他項目，修改 hello CN 值。</span><span class="sxs-lookup"><span data-stu-id="c755c-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="c755c-165">執行這個範例時，請勿變更 hello TextExtension。</span><span class="sxs-lookup"><span data-stu-id="c755c-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="c755c-166">'憑證-目前的憑證' 自動安裝 hello 您產生的用戶端憑證在電腦上。</span><span class="sxs-lookup"><span data-stu-id="c755c-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="c755c-167"><a name="clientexport"></a>匯出用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="c755c-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="c755c-168"><a name="install"></a>安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="c755c-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c755c-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c755c-169">Next steps</span></span>

<span data-ttu-id="c755c-170">繼續使用您的點對站設定。</span><span class="sxs-lookup"><span data-stu-id="c755c-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="c755c-171">如**資源管理員**部署模型的步驟，請參閱[設定點對站連線 tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c755c-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="c755c-172">如**傳統**部署模型的步驟，請參閱[設定點對站 VPN 連線 tooa VNet （傳統）](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c755c-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
