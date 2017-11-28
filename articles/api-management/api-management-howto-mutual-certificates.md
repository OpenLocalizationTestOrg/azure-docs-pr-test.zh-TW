---
title: "使用用戶端憑證驗證 Azure API 管理 aaaSecure 後端服務 |Microsoft 文件"
description: "了解如何 toosecure 後端服務使用用戶端憑證驗證在 Azure API 管理。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="1ffdf-103">如何 toosecure 後端服務使用用戶端憑證驗證在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="1ffdf-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="1ffdf-104">API 管理提供 hello 功能 toosecure 存取 toohello 後端服務的應用程式開發介面使用用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="1ffdf-105">本指南也說明如何 toomanage 憑證在 hello API 發行者入口網站，以及如何 tooconfigure API toouse 憑證 tooaccess 其後端服務。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="1ffdf-106">如需使用 hello API 管理 REST API 來管理憑證資訊，請參閱[Azure API 管理 REST API 憑證實體][Azure API Management REST API Certificate entity]。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="1ffdf-107"><a name="prerequisites"> </a>必要條件</span><span class="sxs-lookup"><span data-stu-id="1ffdf-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="1ffdf-108">本指南也說明如何 tooconfigure 您 API 管理服務執行個體 toouse 用戶端憑證驗證 tooaccess hello 後端服務的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="1ffdf-109">本主題中的下列 hello 步驟之前，您應該設定為用戶端憑證驗證程式後端服務 ([tooconfigure 憑證在 Azure 網站中的驗證，請參閱 toothis 文章][ tooconfigure certificate authentication in Azure WebSites refer toothis article])，而且有存取 toohello 憑證和 hello 密碼 hello hello API 管理發行者入口網站中上傳的憑證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="1ffdf-110"><a name="step1"> </a>上傳用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="1ffdf-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="1ffdf-111">tooget 啟動，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="1ffdf-112">這會帶您 toohello API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-112">This takes you toohello API Management publisher portal.</span></span>

![API 發行者入口網站][api-management-management-console]

> <span data-ttu-id="1ffdf-114">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="1ffdf-115">按一下**安全性**從 hello **API 管理**hello 左邊，然後按一下功能表**用戶端憑證**。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Client certificates][api-management-security-client-certificates]

<span data-ttu-id="1ffdf-117">按一下 新的憑證，tooupload**將憑證上傳**。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Upload certificate][api-management-upload-certificate]

<span data-ttu-id="1ffdf-119">瀏覽 tooyour 憑證，然後輸入 hello 憑證 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="1ffdf-120">hello 憑證必須位於**.pfx**格式。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="1ffdf-121">可接受自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Upload certificate][api-management-upload-certificate-form]

<span data-ttu-id="1ffdf-123">按一下**上傳**tooupload hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="1ffdf-124">hello 憑證密碼會在此時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="1ffdf-125">如果密碼不正確，系統會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificate uploaded][api-management-certificate-uploaded]

<span data-ttu-id="1ffdf-127">一旦上傳 hello 憑證時，它是顯示在 [hello**用戶端憑證**] 索引標籤。如果您有多個憑證，請記下 hello 主旨或 hello hello 指紋，也就是使用的 tooselect hello 憑證時設定應用程式開發介面 toouse 憑證，就如同 hello 下列四個字元[設定應用程式開發介面 toouse 閘道驗證的用戶端憑證][ Configure an API toouse a client certificate for gateway authentication] > 一節。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="1ffdf-128">關閉時，例如使用自我簽署的憑證，憑證鏈結驗證 tooturn 遵循所述在常見問題集中的 hello 步驟[項目](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="1ffdf-129"><a name="step1a"> </a>刪除用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="1ffdf-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="1ffdf-130">toodelete 憑證時，按一下**刪除**旁邊 hello 所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Delete certificate][api-management-certificate-delete]

<span data-ttu-id="1ffdf-132">按一下**是，將它刪除**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-132">Click **Yes, delete it** tooconfirm.</span></span>

![Confirm delete][api-management-confirm-delete]

<span data-ttu-id="1ffdf-134">Hello 憑證是否在使用應用程式開發介面，則會顯示警告畫面。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="1ffdf-135">您必須先移除 hello toodelete hello 憑證的憑證從任何應用程式開發介面所設定的 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Confirm delete][api-management-confirm-delete-policy]

## <span data-ttu-id="1ffdf-137"><a name="step2"></a>設定 API toouse 閘道驗證的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="1ffdf-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="1ffdf-138">按一下**Api**從 hello **API 管理**hello 功能表左 hello hello 預期應用程式開發介面，名稱和按一下 hello**安全性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![API security][api-management-api-security]

<span data-ttu-id="1ffdf-140">選取**用戶端憑證**從 hello**認證**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Client certificates][api-management-mutual-certificates]

<span data-ttu-id="1ffdf-142">選取 hello 所需的憑證，從 hello**用戶端憑證**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="1ffdf-143">如果有多個憑證可以查看 hello 主旨或 hello hello 指紋 hello 前一個區段 toodetermine hello 正確的憑證所述的四個字元。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Select certificate][api-management-select-certificate]

<span data-ttu-id="1ffdf-145">按一下**儲存**toosave hello 組態變更 toohello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="1ffdf-146">這項變更會立即生效，並呼叫將會使用該應用程式開發介面的 toooperations hello 憑證 tooauthenticate hello 後端伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Save API changes][api-management-save-api]

> <span data-ttu-id="1ffdf-148">當閘道驗證 hello 後端服務的應用程式開發介面的指定憑證時，它會變成應用程式開發介面，hello 原則的一部分，而可以在 hello 原則編輯器中檢視。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Certificate policy][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="1ffdf-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ffdf-150">Next steps</span></span>
<span data-ttu-id="1ffdf-151">如需有關其他方式 toosecure 後端服務，例如 HTTP 基本] 或 [共用密碼驗證，請參閱下列視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="1ffdf-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



