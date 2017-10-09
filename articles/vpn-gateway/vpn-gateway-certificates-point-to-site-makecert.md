---
title: "產生並匯出點對站的憑證：MakeCert：Azure | Microsoft Docs"
description: "本文章包含步驟 toocreate 自我簽署的根憑證、 匯出 hello 公開金鑰，並產生使用 MakeCert 的用戶端憑證。"
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
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a><span data-ttu-id="43c23-103">使用 MakeCert 來產生並匯出點對站連線的憑證</span><span class="sxs-lookup"><span data-stu-id="43c23-103">Generate and export certificates for Point-to-Site connections using MakeCert</span></span>

<span data-ttu-id="43c23-104">點對站連線使用憑證 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="43c23-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="43c23-105">本文示範如何 toocreate 的自我簽署根憑證，並產生使用 MakeCert 的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using MakeCert.</span></span> <span data-ttu-id="43c23-106">如果您要尋找的點對站台的設定步驟，例如 tooupload 根憑證，來選取其中一個 hello '設定點對站' 發行項的 hello 下列清單的方式：</span><span class="sxs-lookup"><span data-stu-id="43c23-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43c23-107">建立自我簽署憑證 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="43c23-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="43c23-108">建立自我簽署憑證 - MakeCert</span><span class="sxs-lookup"><span data-stu-id="43c23-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="43c23-109">設定點對站 - Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="43c23-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="43c23-110">設定點對站 - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="43c23-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="43c23-111">設定點對站 - 傳統 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="43c23-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

<span data-ttu-id="43c23-112">雖然我們建議您使用 hello [Windows 10 PowerShell 步驟](vpn-gateway-certificates-point-to-site.md)toocreate 您的憑證，我們提供這些 MakeCert 指示為選擇性的方法。</span><span class="sxs-lookup"><span data-stu-id="43c23-112">While we recommend using hello [Windows 10 PowerShell steps](vpn-gateway-certificates-point-to-site.md) toocreate your certificates, we provide these MakeCert instructions as an optional method.</span></span> <span data-ttu-id="43c23-113">您可以產生使用哪一種方法的 hello 憑證可以安裝在[任何支援的用戶端作業系統](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq)。</span><span class="sxs-lookup"><span data-stu-id="43c23-113">hello certificates that you generate using either method can be installed on [any supported client operating system](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).</span></span> <span data-ttu-id="43c23-114">不過，MakeCert 有下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="43c23-114">However, MakeCert has hello following limitation:</span></span>

* <span data-ttu-id="43c23-115">MakeCert 已被取代。</span><span class="sxs-lookup"><span data-stu-id="43c23-115">MakeCert is deprecated.</span></span> <span data-ttu-id="43c23-116">這表示無法在任何時間點移除這項工具。</span><span class="sxs-lookup"><span data-stu-id="43c23-116">This means that this tool could be removed at any point.</span></span> <span data-ttu-id="43c23-117">當無法再使用 MakeCert 時，任何您已經使用 MakeCert 所產生的憑證將不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="43c23-117">Any certificates that you already generated using MakeCert won't be affected when MakeCert is no longer available.</span></span> <span data-ttu-id="43c23-118">MakeCert 是只使用的 toogenerate hello 憑證，不會做為驗證機制。</span><span class="sxs-lookup"><span data-stu-id="43c23-118">MakeCert is only used toogenerate hello certificates, not as a validating mechanism.</span></span>

## <span data-ttu-id="43c23-119"><a name="rootcert"></a>建立自我簽署根憑證</span><span class="sxs-lookup"><span data-stu-id="43c23-119"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="43c23-120">hello 下列步驟顯示如何 toocreate 的自我簽署憑證使用 MakeCert。</span><span class="sxs-lookup"><span data-stu-id="43c23-120">hello following steps show you how toocreate a self-signed certificate using MakeCert.</span></span> <span data-ttu-id="43c23-121">這些並非部署模型特定的步驟。</span><span class="sxs-lookup"><span data-stu-id="43c23-121">These steps are not deployment-model specific.</span></span> <span data-ttu-id="43c23-122">它們同樣適用於資源管理員和傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="43c23-122">They are valid for both Resource Manager and classic.</span></span>

1. <span data-ttu-id="43c23-123">下載並安裝 [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="43c23-123">Download and install [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).</span></span>
2. <span data-ttu-id="43c23-124">安裝之後，您通常可以找到 hello makecert.exe 公用程式在此路徑: ' C:\Program Files (x86) \Windows Kits\10\bin\<a c h >'。</span><span class="sxs-lookup"><span data-stu-id="43c23-124">After installation, you can typically find hello makecert.exe utility under this path: 'C:\Program Files (x86)\Windows Kits\10\bin\<arch>'.</span></span> <span data-ttu-id="43c23-125">雖然很可能已安裝的 tooanother 位置。</span><span class="sxs-lookup"><span data-stu-id="43c23-125">Although, it's possible that it was installed tooanother location.</span></span> <span data-ttu-id="43c23-126">開啟命令提示字元，以系統管理員身分，並瀏覽 toohello hello MakeCert 公用程式位置。</span><span class="sxs-lookup"><span data-stu-id="43c23-126">Open a command prompt as administrator and navigate toohello location of hello MakeCert utility.</span></span> <span data-ttu-id="43c23-127">您可以使用下列範例中，調整的 hello 適當的位置 hello:</span><span class="sxs-lookup"><span data-stu-id="43c23-127">You can use hello following example, adjusting for hello proper location:</span></span>

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. <span data-ttu-id="43c23-128">建立及 hello 個人憑證存放區，您的電腦上安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-128">Create and install a certificate in hello Personal certificate store on your computer.</span></span> <span data-ttu-id="43c23-129">hello 下列範例會建立對應*.cer*設定 P2S 時上, 傳 tooAzure 檔案。</span><span class="sxs-lookup"><span data-stu-id="43c23-129">hello following example creates a corresponding *.cer* file that you upload tooAzure when configuring P2S.</span></span> <span data-ttu-id="43c23-130">您要 hello 憑證 toouse hello 名稱取代 'P2SRootCert' 和 'P2SRootCert.cer'。</span><span class="sxs-lookup"><span data-stu-id="43c23-130">Replace 'P2SRootCert' and 'P2SRootCert.cer' with hello name that you want toouse for hello certificate.</span></span> <span data-ttu-id="43c23-131">hello 憑證位於您 '憑證-目前 \'。</span><span class="sxs-lookup"><span data-stu-id="43c23-131">hello certificate is located in your 'Certificates - Current User\Personal\Certificates'.</span></span>

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <span data-ttu-id="43c23-132"><a name="cer"></a>匯出 hello 公開金鑰 (.cer)</span><span class="sxs-lookup"><span data-stu-id="43c23-132"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="43c23-133">hello exported.cer 檔案必須上傳的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="43c23-133">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="43c23-134">如需相關指示，請參閱[設定點對站連線](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile)。</span><span class="sxs-lookup"><span data-stu-id="43c23-134">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile).</span></span> <span data-ttu-id="43c23-135">tooadd 其他信任的根憑證，請參閱[本節](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add)hello 發行項。</span><span class="sxs-lookup"><span data-stu-id="43c23-135">tooadd an additional trusted root certificate, see [this section](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) of hello article.</span></span>

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a><span data-ttu-id="43c23-136">匯出 hello 自我簽署的憑證與私用金鑰 toostore 它 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="43c23-136">Export hello self-signed certificate and private key toostore it (optional)</span></span>

<span data-ttu-id="43c23-137">您可能想 tooexport hello 自我簽署根憑證，並將它安全地儲存。</span><span class="sxs-lookup"><span data-stu-id="43c23-137">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="43c23-138">如有需要，您可以稍後在另一部電腦上安裝這個自我簽署憑證，然後產生更多用戶端憑證，或匯出另一個 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="43c23-138">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="43c23-139">tooexport hello 自我簽署根憑證.pfx hello 選取根憑證，使用 hello 相同的步驟中所述[用戶端憑證匯出](#clientexport)。</span><span class="sxs-lookup"><span data-stu-id="43c23-139">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <a name="create-and-install-client-certificates"></a><span data-ttu-id="43c23-140">建立並安裝用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="43c23-140">Create and install client certificates</span></span>

<span data-ttu-id="43c23-141">您未直接在 hello 用戶端電腦上安裝 hello 自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-141">You don't install hello self-signed certificate directly on hello client computer.</span></span> <span data-ttu-id="43c23-142">您需要 toogenerate hello 自我簽署憑證從用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-142">You need toogenerate a client certificate from hello self-signed certificate.</span></span> <span data-ttu-id="43c23-143">您接著匯出，並安裝 hello 用戶端憑證 toohello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="43c23-143">You then export and install hello client certificate toohello client computer.</span></span> <span data-ttu-id="43c23-144">hello 步驟不是特定的部署模型。</span><span class="sxs-lookup"><span data-stu-id="43c23-144">hello following steps are not deployment-model specific.</span></span> <span data-ttu-id="43c23-145">它們同樣適用於資源管理員和傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="43c23-145">They are valid for both Resource Manager and classic.</span></span>

### <span data-ttu-id="43c23-146"><a name="clientcert"></a>產生用戶端憑證 </span><span class="sxs-lookup"><span data-stu-id="43c23-146"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="43c23-147">每個連線 tooa 的用戶端電腦使用點對站台的 VNet 必須安裝用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-147">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="43c23-148">您 hello 自我簽署的根憑證，從產生的用戶端憑證，然後匯出及安裝 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-148">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="43c23-149">如果未安裝 hello 用戶端憑證，驗證將會失敗。</span><span class="sxs-lookup"><span data-stu-id="43c23-149">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="43c23-150">hello 下列步驟引導您完成從自我簽署的根憑證產生用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-150">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="43c23-151">您可以從 hello 產生多個用戶端憑證相同的根憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-151">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="43c23-152">當您產生用戶端憑證使用 hello 執行下列步驟時，hello 用戶端憑證會自動安裝 hello 電腦上，您會使用 toogenerate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-152">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="43c23-153">如果您想 tooinstall 另一部用戶端電腦上的用戶端憑證，您可以匯出 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-153">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>
 
1. <span data-ttu-id="43c23-154">Hello 在同一部電腦使用 toocreate hello 的自我簽署憑證，請開啟命令提示字元，以系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="43c23-154">On hello same computer that you used toocreate hello self-signed certificate, open a command prompt as administrator.</span></span>
2. <span data-ttu-id="43c23-155">修改並執行 hello 範例 toogenerate 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-155">Modify and run hello sample toogenerate a client certificate.</span></span>
  * <span data-ttu-id="43c23-156">變更*"P2SRootCert"* toohello hello hello 用戶端憑證，從產生的自我簽署根名稱。</span><span class="sxs-lookup"><span data-stu-id="43c23-156">Change *"P2SRootCert"* toohello name of hello self-signed root that you are generating hello client certificate from.</span></span> <span data-ttu-id="43c23-157">請確定您使用 hello 根憑證，也就是任何 hello hello 名稱 ' CN =' 的值為您指定當您建立 hello 自我簽署的根。</span><span class="sxs-lookup"><span data-stu-id="43c23-157">Make sure you are using hello name of hello root certificate, which is whatever hello 'CN=' value was that you specified when you created hello self-signed root.</span></span>
  * <span data-ttu-id="43c23-158">變更*P2SChildCert*想 toogenerate 用戶端憑證 toobe toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="43c23-158">Change *P2SChildCert* toohello name you want toogenerate a client certificate toobe.</span></span>

  <span data-ttu-id="43c23-159">如果您執行而不需修改下列範例中的 hello，hello 結果會是名為 P2SChildcert 所產生的根憑證 P2SRootCert 您個人憑證存放區中的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="43c23-159">If you run hello following example without modifying it, hello result is a client certificate named P2SChildcert in your Personal certificate store that was generated from root certificate P2SRootCert.</span></span>

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <span data-ttu-id="43c23-160"><a name="clientexport"></a>匯出用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="43c23-160"><a name="clientexport"></a>Export a client certificate</span></span>

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <span data-ttu-id="43c23-161"><a name="install"></a>安裝匯出的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="43c23-161"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="43c23-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43c23-162">Next steps</span></span>

<span data-ttu-id="43c23-163">繼續使用您的點對站設定。</span><span class="sxs-lookup"><span data-stu-id="43c23-163">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="43c23-164">如**資源管理員**部署模型的步驟，請參閱[設定點對站連線 tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="43c23-164">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="43c23-165">如**傳統**部署模型的步驟，請參閱[設定點對站 VPN 連線 tooa VNet （傳統）](vpn-gateway-howto-point-to-site-classic-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="43c23-165">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
