---
title: "aaaCloud 服務和管理憑證 |Microsoft 文件"
description: "了解如何 toocreate 和使用憑證搭配 Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a><span data-ttu-id="50d1c-103">Azure 雲端服務的憑證概觀</span><span class="sxs-lookup"><span data-stu-id="50d1c-103">Certificates overview for Azure Cloud Services</span></span>
<span data-ttu-id="50d1c-104">憑證可用於在 Azure 中雲端服務 ([服務憑證](#what-are-service-certificates)) 以及使用 hello 管理 API 進行驗證 ([管理憑證](#what-are-management-certificates)時使用 hello Azure 傳統入口網站而非hello 非傳統 Azure 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="50d1c-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with hello management API ([management certificates](#what-are-management-certificates) when using hello Azure classic portal and not hello non-classic Azure portal).</span></span> <span data-ttu-id="50d1c-105">本主題提供這兩種憑證類型，一般概觀如何太[建立](#create)和[部署](#deploy)它們 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="50d1c-105">This topic gives a general overview of both certificate types, how too[create](#create) and [deploy](#deploy) them tooAzure.</span></span>

<span data-ttu-id="50d1c-106">在 Azure 中使用的憑證是 x.509 v3 憑證，而且可以由其他受信任的憑證簽署，或者可以自我簽署。</span><span class="sxs-lookup"><span data-stu-id="50d1c-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span></span> <span data-ttu-id="50d1c-107">自我簽署的憑證是由自己的建立者簽署，因此預設不受到信任。</span><span class="sxs-lookup"><span data-stu-id="50d1c-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span></span> <span data-ttu-id="50d1c-108">大部分的瀏覽器都可以忽略這個問題。</span><span class="sxs-lookup"><span data-stu-id="50d1c-108">Most browsers can ignore this problem.</span></span> <span data-ttu-id="50d1c-109">您應該僅在開發和測試雲端服務時使用自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-109">You should only use self-signed certificates when developing and testing your cloud services.</span></span> 

<span data-ttu-id="50d1c-110">Azure 所使用的憑證可以包含私密或公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="50d1c-110">Certificates used by Azure can contain a private or a public key.</span></span> <span data-ttu-id="50d1c-111">憑證具有指紋提供表示 tooidentify 它們模稜兩可的方式。</span><span class="sxs-lookup"><span data-stu-id="50d1c-111">Certificates have a thumbprint that provides a means tooidentify them in an unambiguous way.</span></span> <span data-ttu-id="50d1c-112">Hello Azure 會使用此憑證指紋[組態檔](cloud-services-configure-ssl-certificate.md)tooidentify 其中一項雲端服務的憑證應該使用。</span><span class="sxs-lookup"><span data-stu-id="50d1c-112">This thumbprint is used in hello Azure [configuration file](cloud-services-configure-ssl-certificate.md) tooidentify which certificate a cloud service should use.</span></span> 

## <a name="what-are-service-certificates"></a><span data-ttu-id="50d1c-113">什麼是服務憑證？</span><span class="sxs-lookup"><span data-stu-id="50d1c-113">What are service certificates?</span></span>
<span data-ttu-id="50d1c-114">服務憑證是附加的 toocloud 服務，以及啟用安全通訊 tooand 從 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="50d1c-114">Service certificates are attached toocloud services and enable secure communication tooand from hello service.</span></span> <span data-ttu-id="50d1c-115">例如，如果您部署 web 角色，您會想 toosupply 可以驗證公開的 HTTPS 端點的憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-115">For example, if you deployed a web role, you would want toosupply a certificate that can authenticate an exposed HTTPS endpoint.</span></span> <span data-ttu-id="50d1c-116">服務憑證，定義在服務定義中，會執行您的角色執行個體的自動部署的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="50d1c-116">Service certificates, defined in your service definition, are automatically deployed toohello virtual machine that is running an instance of your role.</span></span> 

<span data-ttu-id="50d1c-117">您可以上傳服務憑證 tooAzure 傳統入口網站使用 hello Azure 傳統入口網站，或使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="50d1c-117">You can upload service certificates tooAzure classic portal either using hello Azure classic portal or by using hello classic deployment model.</span></span> <span data-ttu-id="50d1c-118">服務憑證是與特定的雲端服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="50d1c-118">Service certificates are associated with a specific cloud service.</span></span> <span data-ttu-id="50d1c-119">它們會指派 tooa hello 服務定義檔中的部署。</span><span class="sxs-lookup"><span data-stu-id="50d1c-119">They are assigned tooa deployment in hello service definition file.</span></span>

<span data-ttu-id="50d1c-120">服務憑證可以與您的服務分開管理，而且可以由不同的人員管理。</span><span class="sxs-lookup"><span data-stu-id="50d1c-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span></span> <span data-ttu-id="50d1c-121">例如，開發人員，可能是指，IT 管理員先前上傳 tooAzure tooa 憑證將服務套件上傳。</span><span class="sxs-lookup"><span data-stu-id="50d1c-121">For example, a developer may upload a service package that refers tooa certificate that an IT manager has previously uploaded tooAzure.</span></span> <span data-ttu-id="50d1c-122">IT 管理員可以管理和更新 （變更 hello hello 服務組態） 該憑證，而不需要 tooupload 新的服務封裝。</span><span class="sxs-lookup"><span data-stu-id="50d1c-122">An IT manager can manage and renew that certificate (changing hello configuration of hello service) without needing tooupload a new service package.</span></span> <span data-ttu-id="50d1c-123">沒有新的服務封裝更新可能會是因為 hello 邏輯名稱、 商店名稱和位置 hello 憑證的正在 hello 服務定義檔中時 hello 服務組態檔中指定 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="50d1c-123">Updating without a new service package is possible because hello logical name, store name, and location of hello certificate is in hello service definition file and while hello certificate thumbprint is specified in hello service configuration file.</span></span> <span data-ttu-id="50d1c-124">tooupdate hello 憑證，它是只需要 tooupload hello 服務組態檔中的新憑證及變更 hello 指紋值。</span><span class="sxs-lookup"><span data-stu-id="50d1c-124">tooupdate hello certificate, it's only necessary tooupload a new certificate and change hello thumbprint value in hello service configuration file.</span></span>

>[!Note]
><span data-ttu-id="50d1c-125">hello [Cloud Services 常見問題集](cloud-services-faq.md)發行項有一些很有幫助憑證的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="50d1c-125">hello [Cloud Services FAQ](cloud-services-faq.md) article has some helpful information about certificates.</span></span>

## <a name="what-are-management-certificates"></a><span data-ttu-id="50d1c-126">什麼是管理憑證？</span><span class="sxs-lookup"><span data-stu-id="50d1c-126">What are management certificates?</span></span>
<span data-ttu-id="50d1c-127">管理憑證可讓您 tooauthenticate 與 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="50d1c-127">Management certificates allow you tooauthenticate with hello classic deployment model.</span></span> <span data-ttu-id="50d1c-128">許多程式和工具 （例如 Visual Studio 或 Azure SDK hello） 使用這些憑證 tooautomate 組態和各種 Azure 服務的部署。</span><span class="sxs-lookup"><span data-stu-id="50d1c-128">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="50d1c-129">這些不是真的相關的 toocloud 服務。</span><span class="sxs-lookup"><span data-stu-id="50d1c-129">These are not really related toocloud services.</span></span> 

> [!WARNING]
> <span data-ttu-id="50d1c-130">請務必小心！</span><span class="sxs-lookup"><span data-stu-id="50d1c-130">Be careful!</span></span> <span data-ttu-id="50d1c-131">這些憑證類型允許驗證它們的任何人 toomanage hello 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="50d1c-131">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span> 
> 
> 

### <a name="limitations"></a><span data-ttu-id="50d1c-132">限制</span><span class="sxs-lookup"><span data-stu-id="50d1c-132">Limitations</span></span>
<span data-ttu-id="50d1c-133">每個訂用帳戶有 100 個管理憑證的限制。</span><span class="sxs-lookup"><span data-stu-id="50d1c-133">There is a limit of 100 management certificates per subscription.</span></span> <span data-ttu-id="50d1c-134">此外，在特定服務管理員的使用者識別碼底下的所有訂用帳戶也有 100 個管理憑證的限制。</span><span class="sxs-lookup"><span data-stu-id="50d1c-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span></span> <span data-ttu-id="50d1c-135">如果 hello hello 帳戶管理員的使用者識別碼已經用的 tooadd 100 管理憑證，而且需要更多的憑證，您可以加入共同管理員 tooadd hello 其他憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-135">If hello user ID for hello account administrator has already been used tooadd 100 management certificates and there is a need for more certificates, you can add a co-administrator tooadd hello additional certificates.</span></span> 

<span data-ttu-id="50d1c-136">加入超過 100 個憑證之前，請查看您是否可以重複使用現有的憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span></span> <span data-ttu-id="50d1c-137">使用共同管理員加入可能不必要的複雜性 tooyour 憑證管理程序。</span><span class="sxs-lookup"><span data-stu-id="50d1c-137">Using co-administrators adds potentially unneeded complexity tooyour certificate management process.</span></span>

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="50d1c-138">建立新的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="50d1c-138">Create a new self-signed certificate</span></span>
<span data-ttu-id="50d1c-139">您可以使用任何工具可用 toocreate 自我簽署憑證，只要遵守 toothese 設定：</span><span class="sxs-lookup"><span data-stu-id="50d1c-139">You can use any tool available toocreate a self-signed certificate as long as they adhere toothese settings:</span></span>

* <span data-ttu-id="50d1c-140">X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-140">An X.509 certificate.</span></span>
* <span data-ttu-id="50d1c-141">包含一個私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="50d1c-141">Contains a private key.</span></span>
* <span data-ttu-id="50d1c-142">針對金鑰交換 (.pfx 檔案) 而建立。</span><span class="sxs-lookup"><span data-stu-id="50d1c-142">Created for key exchange (.pfx file).</span></span>
* <span data-ttu-id="50d1c-143">主體名稱必須符合 hello 用網域 tooaccess hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="50d1c-143">Subject name must match hello domain used tooaccess hello cloud service.</span></span>

    > <span data-ttu-id="50d1c-144">您無法取得 hello.cloudapp.net 的 SSL 憑證 (或任何 Azure 相關) 網域。hello 憑證的主體名稱必須符合您的應用程式的 hello 自訂網域名稱使用 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="50d1c-144">You cannot acquire an SSL certificate for hello cloudapp.net (or for any Azure-related) domain; hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="50d1c-145">例如，**contoso.net**，而非 **contoso.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="50d1c-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span></span>

* <span data-ttu-id="50d1c-146">至少為 2048 位元加密。</span><span class="sxs-lookup"><span data-stu-id="50d1c-146">Minimum of 2048-bit encryption.</span></span>
* <span data-ttu-id="50d1c-147">**只有服務憑證**： 用戶端憑證必須位於 hello*個人*憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="50d1c-147">**Service Certificate Only**: Client-side certificate must reside in hello *Personal* certificate store.</span></span>

<span data-ttu-id="50d1c-148">有兩個簡單的方法 toocreate 憑證在 Windows 中，以 hello`makecert.exe`公用程式或 IIS。</span><span class="sxs-lookup"><span data-stu-id="50d1c-148">There are two easy ways toocreate a certificate on Windows, with hello `makecert.exe` utility, or IIS.</span></span>

### <a name="makecertexe"></a><span data-ttu-id="50d1c-149">Makecert.exe</span><span class="sxs-lookup"><span data-stu-id="50d1c-149">Makecert.exe</span></span>
<span data-ttu-id="50d1c-150">此公用程式已被取代，此處不再說明。</span><span class="sxs-lookup"><span data-stu-id="50d1c-150">This utility has been deprecated and is no longer documented here.</span></span> <span data-ttu-id="50d1c-151">如需詳細資訊，請參閱[此 MSDN 文章](https://msdn.microsoft.com/library/windows/desktop/aa386968)。</span><span class="sxs-lookup"><span data-stu-id="50d1c-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span></span>

### <a name="powershell"></a><span data-ttu-id="50d1c-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50d1c-152">PowerShell</span></span>
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> <span data-ttu-id="50d1c-153">如果您想 toouse hello 憑證，而不是網域的 IP 位址，請在 hello-DnsName 參數中使用 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="50d1c-153">If you want toouse hello certificate with an IP address instead of a domain, use hello IP address in hello -DnsName parameter.</span></span>


<span data-ttu-id="50d1c-154">如果您要 toouse [hello 管理入口網站憑證](../azure-api-management-certs.md)，將它匯出 tooa **.cer**檔案：</span><span class="sxs-lookup"><span data-stu-id="50d1c-154">If you want toouse this [certificate with hello management portal](../azure-api-management-certs.md), export it tooa **.cer** file:</span></span>

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a><span data-ttu-id="50d1c-155">網際網路資訊服務 (IIS)</span><span class="sxs-lookup"><span data-stu-id="50d1c-155">Internet Information Services (IIS)</span></span>
<span data-ttu-id="50d1c-156">Hello 上有許多網頁網際網路，其中涵蓋如何 toodo 這與 IIS。</span><span class="sxs-lookup"><span data-stu-id="50d1c-156">There are many pages on hello internet that cover how toodo this with IIS.</span></span> <span data-ttu-id="50d1c-157">[這裡](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) 是我找到的其中一個我認為說明得很好的網頁。</span><span class="sxs-lookup"><span data-stu-id="50d1c-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span></span> 

### <a name="java"></a><span data-ttu-id="50d1c-158">Java</span><span class="sxs-lookup"><span data-stu-id="50d1c-158">Java</span></span>
<span data-ttu-id="50d1c-159">您也可以使用 Java[建立憑證](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate)。</span><span class="sxs-lookup"><span data-stu-id="50d1c-159">You can use Java too[create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span></span>

### <a name="linux"></a><span data-ttu-id="50d1c-160">Linux</span><span class="sxs-lookup"><span data-stu-id="50d1c-160">Linux</span></span>
<span data-ttu-id="50d1c-161">[這](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)文章說明 toocreate 透過 SSH 的憑證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how toocreate certificates with SSH.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50d1c-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50d1c-162">Next steps</span></span>
<span data-ttu-id="50d1c-163">[上傳您的服務憑證 toohello Azure 傳統入口網站](cloud-services-configure-ssl-certificate.md)(或 hello [Azure 入口網站](cloud-services-configure-ssl-certificate-portal.md))。</span><span class="sxs-lookup"><span data-stu-id="50d1c-163">[Upload your service certificate toohello Azure classic portal](cloud-services-configure-ssl-certificate.md) (or hello [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span></span>

<span data-ttu-id="50d1c-164">上傳[管理 API 憑證](../azure-api-management-certs.md)toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="50d1c-164">Upload a [management API certificate](../azure-api-management-certs.md) toohello Azure classic portal.</span></span> <span data-ttu-id="50d1c-165">hello Azure 入口網站不使用管理憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="50d1c-165">hello Azure portal does not use management certificates for authentication.</span></span>

