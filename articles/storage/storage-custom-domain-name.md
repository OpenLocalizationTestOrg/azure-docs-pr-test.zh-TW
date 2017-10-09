---
title: "您的 Azure Blob 儲存體端點的自訂網域名稱 aaaConfigure |Microsoft 文件"
description: "使用 Azure 儲存體帳戶中的 hello Azure 入口網站 toomap 您自己的正式名稱 (CNAME) toohello Blob 儲存體端點。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a><span data-ttu-id="87eca-103">針對 Blob 儲存體端點設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="87eca-103">Configure a custom domain name for your Blob storage endpoint</span></span>

<span data-ttu-id="87eca-104">您可以設定自訂網域名稱，以供存取 Azure 儲存體帳戶中的 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="87eca-104">You can configure a custom domain for accessing blob data in your Azure storage account.</span></span> <span data-ttu-id="87eca-105">Blob 儲存體是 hello 預設端點`<storage-account-name>.blob.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="87eca-105">hello default endpoint for Blob storage is `<storage-account-name>.blob.core.windows.net`.</span></span> <span data-ttu-id="87eca-106">如果您將對應的自訂網域和子網域，像是**www.contoso.com** toohello blob 儲存體帳戶的端點，您的使用者可以存取 blob 儲存體帳戶使用該網域中的資料。</span><span class="sxs-lookup"><span data-stu-id="87eca-106">If you map a custom domain and subdomain like **www.contoso.com** toohello blob endpoint for your storage account, your users can then access blob data in your storage account using that domain.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87eca-107">Azure 儲存體尚未以原生方式支援使用自訂網域的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="87eca-107">Azure Storage does not yet natively support HTTPS with custom domains.</span></span> <span data-ttu-id="87eca-108">您可以在目前[使用透過 HTTPS 使用自訂網域的 hello Azure CDN tooaccess blob](./storage-https-custom-domain-cdn.md)。</span><span class="sxs-lookup"><span data-stu-id="87eca-108">You can currently [Use hello Azure CDN tooaccess blobs with custom domains over HTTPS](./storage-https-custom-domain-cdn.md).</span></span>
>

<span data-ttu-id="87eca-109">hello 下列表格會顯示幾個範例 Url 位於名為的儲存體帳戶的 blob 資料的**mystorageaccount**。</span><span class="sxs-lookup"><span data-stu-id="87eca-109">hello following table shows a few sample URLs for blob data located in a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="87eca-110">hello 自訂網域註冊 hello 儲存體帳戶是**www.contoso.com**:</span><span class="sxs-lookup"><span data-stu-id="87eca-110">hello custom domain registered for hello storage account is **www.contoso.com**:</span></span>

| <span data-ttu-id="87eca-111">資源類型</span><span class="sxs-lookup"><span data-stu-id="87eca-111">Resource Type</span></span> | <span data-ttu-id="87eca-112">預設 URL</span><span class="sxs-lookup"><span data-stu-id="87eca-112">Default URL</span></span> | <span data-ttu-id="87eca-113">自訂網域 URL</span><span class="sxs-lookup"><span data-stu-id="87eca-113">Custom domain URL</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87eca-114">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="87eca-114">Storage account</span></span> | <span data-ttu-id="87eca-115">http://mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="87eca-115">http://mystorageaccount.blob.core.windows.net</span></span> | <span data-ttu-id="87eca-116">http://www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="87eca-116">http://www.contoso.com</span></span> |
| <span data-ttu-id="87eca-117">Blob</span><span class="sxs-lookup"><span data-stu-id="87eca-117">Blob</span></span> |<span data-ttu-id="87eca-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="87eca-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span></span> | <span data-ttu-id="87eca-119">http://www.contoso.com/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="87eca-119">http://www.contoso.com/mycontainer/myblob</span></span> |
| <span data-ttu-id="87eca-120">根容器</span><span class="sxs-lookup"><span data-stu-id="87eca-120">Root container</span></span> | <span data-ttu-id="87eca-121">http://mystorageaccount.blob.core.windows.net/myblob 或 http://mystorageaccount.blob.core.windows.net/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="87eca-121">http://mystorageaccount.blob.core.windows.net/myblob or http://mystorageaccount.blob.core.windows.net/$root/myblob</span></span>| <span data-ttu-id="87eca-122">http://www.contoso.com/myblob 或 http://www.contoso.com/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="87eca-122">http://www.contoso.com/myblob or http://www.contoso.com/$root/myblob</span></span> |

## <a name="direct-vs-intermediary-domain-mapping"></a><span data-ttu-id="87eca-123">直接與中繼網域對應</span><span class="sxs-lookup"><span data-stu-id="87eca-123">Direct vs. intermediary domain mapping</span></span>

<span data-ttu-id="87eca-124">有兩種方式 toopoint 您的自訂網域 toohello blob 端點，您的儲存體帳戶： 直接對應，以及使用 hello CNAME *asverify*中繼子網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-124">There are two ways toopoint your custom domain toohello blob endpoint for your storage account: direct CNAME mapping, and using hello *asverify* intermediary subdomain.</span></span>

### <a name="direct-cname-mapping"></a><span data-ttu-id="87eca-125">直接 CNAME 對應</span><span class="sxs-lookup"><span data-stu-id="87eca-125">Direct CNAME mapping</span></span>

<span data-ttu-id="87eca-126">hello 第一個和最簡單方法是 toocreate toohello blob 端點直接對應您的自訂網域和子網域的正式名稱 (CNAME) 記錄。</span><span class="sxs-lookup"><span data-stu-id="87eca-126">hello first, and simplest, method is toocreate a canonical name (CNAME) record that maps your custom domain and subdomain directly toohello blob endpoint.</span></span> <span data-ttu-id="87eca-127">CNAME 記錄會對應來源網域 tooa 目的地網域的網域名稱系統 (DNS) 功能。</span><span class="sxs-lookup"><span data-stu-id="87eca-127">A CNAME record is a domain name system (DNS) feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="87eca-128">在此情況下，hello 來源網域是您自己的自訂網域和子網域，例如*www.contoso.com*。 hello 目的地網域則是 Blob 服務端點，例如*mystorageaccount.blob.core.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="87eca-128">In this case, hello source domain is your own custom domain and subdomain, for example *www.contoso.com*. hello destination domain is your Blob service endpoint, for example *mystorageaccount.blob.core.windows.net*.</span></span>

<span data-ttu-id="87eca-129">hello 直接的方法在講述[註冊自訂網域](#register-a-custom-domain)。</span><span class="sxs-lookup"><span data-stu-id="87eca-129">hello direct method is covered in [Register a custom domain](#register-a-custom-domain).</span></span>

### <a name="intermediary-mapping-with-asverify"></a><span data-ttu-id="87eca-130">使用 *asverify* 的中繼對應</span><span class="sxs-lookup"><span data-stu-id="87eca-130">Intermediary mapping with *asverify*</span></span>

<span data-ttu-id="87eca-131">hello 第二種方法也會使用 CNAME 記錄，但先採用 Azure tooavoid 停機時間所辨識的特殊子網域： **asverify**。</span><span class="sxs-lookup"><span data-stu-id="87eca-131">hello second method also uses CNAME records, but first employs a special subdomain recognized by Azure tooavoid downtime: **asverify**.</span></span>

<span data-ttu-id="87eca-132">對應您的自訂網域 tooa blob 端點的 hello 程序可能會導致在短暫的停機時間 hello 網域在它註冊在 hello 時[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-132">hello process of mapping your custom domain tooa blob endpoint can result in a brief period of downtime for hello domain while you are registering it in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="87eca-133">如果您的自訂網域目前支援的應用程式的服務等級合約 (SLA) 要求零停機時間，則您可以使用 hello Azure *asverify*子網域當做中繼註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="87eca-133">If your custom domain is currently supporting an application with a service-level agreement (SLA) that requires zero downtime, then you can use hello Azure *asverify* subdomain as an intermediate registration step.</span></span> <span data-ttu-id="87eca-134">此中繼步驟可確保使用者 hello DNS 對應時所能 tooaccess 您的網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-134">This intermediate step ensures users are able tooaccess your domain while hello DNS mapping takes place.</span></span>

<span data-ttu-id="87eca-135">hello 中繼方法在講述[註冊自訂網域使用 hello *asverify*子網域](#register-a-custom-domain-using-the-asverify-subdomain)。</span><span class="sxs-lookup"><span data-stu-id="87eca-135">hello intermediary method is covered in [Register a custom domain using hello *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

## <a name="register-a-custom-domain"></a><span data-ttu-id="87eca-136">註冊自訂網域</span><span class="sxs-lookup"><span data-stu-id="87eca-136">Register a custom domain</span></span>
<span data-ttu-id="87eca-137">使用此程序 tooregister 您的自訂網域 hello 網域被暫時無法使用 tooyour 使用者，如有任何疑慮，或您的自訂網域目前未裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="87eca-137">Use this procedure tooregister your custom domain if you have no concerns about hello domain being briefly unavailable tooyour users, or if your custom domain is not currently hosting an application.</span></span>

<span data-ttu-id="87eca-138">如果您的自訂網域目前支援的應用程式，不能有任何停機時間，請遵循 hello 程序中所述[註冊自訂網域使用 hello *asverify*子網域](#register-a-custom-domain-using-the-asverify-subdomain)。</span><span class="sxs-lookup"><span data-stu-id="87eca-138">If your custom domain is currently supporting an application that cannot have any downtime, follow hello procedure outlined in [Register a custom domain using hello *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

<span data-ttu-id="87eca-139">tooconfigure 自訂網域名稱，您必須在 DNS 中建立新的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="87eca-139">tooconfigure a custom domain name, you must create a new CNAME record in DNS.</span></span> <span data-ttu-id="87eca-140">hello CNAME 記錄指定的網域名稱的別名。</span><span class="sxs-lookup"><span data-stu-id="87eca-140">hello CNAME record specifies an alias for a domain name.</span></span> <span data-ttu-id="87eca-141">在此情況下，則會對應 hello 您的自訂網域 toohello Blob 儲存體端點位址儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87eca-141">In this case, it maps hello address of your custom domain toohello Blob storage endpoint for your storage account.</span></span>

<span data-ttu-id="87eca-142">一般而言，您可在網域註冊機構的網站上管理網域的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="87eca-142">Typically, you can manage your domain's DNS settings on your domain registrar's website.</span></span> <span data-ttu-id="87eca-143">每個註冊機構有相似但稍微不同的方法指定 CNAME 記錄，但 hello 概念是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="87eca-143">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concept is hello same.</span></span> <span data-ttu-id="87eca-144">一些基本的網域註冊套件不提供的 DNS 設定，因此您可能需要 tooupgrade 您網域的註冊套件之前，您可以建立 hello CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="87eca-144">Some basic domain registration packages do not offer DNS configuration, so you may need tooupgrade your domain registration package before you can create hello CNAME record.</span></span>

1. <span data-ttu-id="87eca-145">瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-145">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="87eca-146">在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87eca-146">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="87eca-147">登入 tooyour 網域註冊機構的網站，並移至 toohello 管理 DNS 的頁面。</span><span class="sxs-lookup"><span data-stu-id="87eca-147">Log on tooyour domain registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="87eca-148">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="87eca-148">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="87eca-149">用於管理 Cname 尋找 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="87eca-149">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="87eca-150">您可能會有 toogo tooan 進階的設定 頁面上，並查看 hello 文字**CNAME**，**別名**，或**子網域**。</span><span class="sxs-lookup"><span data-stu-id="87eca-150">You may have toogo tooan advanced settings page and look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="87eca-151">建立新的 CNAME 記錄並提供子網域別名，如 **www** 或 **photos**。</span><span class="sxs-lookup"><span data-stu-id="87eca-151">Create a new CNAME record and provide a subdomain alias such as **www** or **photos**.</span></span> <span data-ttu-id="87eca-152">然後提供主機名稱，也就是您的 Blob 服務端點，格式為 hello **mystorageaccount.blob.core.windows.net** (其中*mystorageaccount* hello 儲存體帳戶名稱)。</span><span class="sxs-lookup"><span data-stu-id="87eca-152">Then provide a host name, which is your Blob service endpoint, in hello format **mystorageaccount.blob.core.windows.net** (where *mystorageaccount* is hello name of your storage account).</span></span> <span data-ttu-id="87eca-153">hello 主機名稱 toouse 會出現在項目 #1 的 hello*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-153">hello host name toouse appears in item #1 of hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="87eca-154">Hello hello 文字方塊中*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，輸入 hello 您的自訂網域名稱，包括 hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-154">In hello text box on hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com), enter hello name of your custom domain, including hello subdomain.</span></span> <span data-ttu-id="87eca-155">例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。如果您的子網域是**相片**，輸入**photos.contoso.com**。 hello 子網域是*必要*。</span><span class="sxs-lookup"><span data-stu-id="87eca-155">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. hello subdomain is *required*.</span></span>
1. <span data-ttu-id="87eca-156">選取**儲存**上 hello*自訂網域*刀鋒視窗 tooregister 您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-156">Select **Save** on hello *Custom domain* blade tooregister your custom domain.</span></span> <span data-ttu-id="87eca-157">如果 hello 註冊成功時，您會看到已成功更新儲存體帳戶入口網站的通知。</span><span class="sxs-lookup"><span data-stu-id="87eca-157">If hello registration is successful, you will see a portal notification that your storage account was successfully updated.</span></span>

<span data-ttu-id="87eca-158">一旦您新的 CNAME 記錄傳播到透過 DNS，您的使用者可以檢視 blob 資料使用自訂網域，只要有 hello 適當的權限。</span><span class="sxs-lookup"><span data-stu-id="87eca-158">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have hello appropriate permissions.</span></span>

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a><span data-ttu-id="87eca-159">註冊自訂網域使用 hello *asverify*子網域</span><span class="sxs-lookup"><span data-stu-id="87eca-159">Register a custom domain using hello *asverify* subdomain</span></span>
<span data-ttu-id="87eca-160">使用此程序 tooregister 您的自訂網域如果您的自訂網域目前支援的應用程式所需的 SLA 會有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="87eca-160">Use this procedure tooregister your custom domain if your custom domain is currently supporting an application with an SLA that requires that there be no downtime.</span></span> <span data-ttu-id="87eca-161">藉由建立 CNAME 從`asverify.<subdomain>.<customdomain>`太`asverify.<storageaccount>.blob.core.windows.net`，您可以預先註冊您的 Azure 網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-161">By creating a CNAME that points from `asverify.<subdomain>.<customdomain>` too`asverify.<storageaccount>.blob.core.windows.net`, you can pre-register your domain with Azure.</span></span> <span data-ttu-id="87eca-162">然後，您可以建立第二個 CNAME 從`<subdomain>.<customdomain>`太`<storageaccount>.blob.core.windows.net`，此時 tooyour 自訂網域時，流量會導向的 tooyour blob 端點。</span><span class="sxs-lookup"><span data-stu-id="87eca-162">You can then create a second CNAME that points from `<subdomain>.<customdomain>` too`<storageaccount>.blob.core.windows.net`, at which point traffic tooyour custom domain will be directed tooyour blob endpoint.</span></span>

<span data-ttu-id="87eca-163">hello **asverify**子網域是 Azure 所辨識的特殊子網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-163">hello **asverify** subdomain is a special subdomain recognized by Azure.</span></span> <span data-ttu-id="87eca-164">附加在前面`asverify`tooyour 自己的子網域，您允許 Azure toorecognize 您的自訂網域而無需修改 hello hello 網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="87eca-164">By prepending `asverify` tooyour own subdomain, you permit Azure toorecognize your custom domain without modifying hello DNS record for hello domain.</span></span> <span data-ttu-id="87eca-165">當您不要修改 hello hello 網域的 DNS 記錄時，就會完全不停機的對應的 toohello blob 端點。</span><span class="sxs-lookup"><span data-stu-id="87eca-165">When you do modify hello DNS record for hello domain, it will be mapped toohello blob endpoint with no downtime.</span></span>

1. <span data-ttu-id="87eca-166">瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-166">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="87eca-167">在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87eca-167">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="87eca-168">登入 tooyour DNS 提供者的網站，並移至 toohello 管理 DNS 的頁面。</span><span class="sxs-lookup"><span data-stu-id="87eca-168">Log on tooyour DNS provider's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="87eca-169">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="87eca-169">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="87eca-170">用於管理 Cname 尋找 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="87eca-170">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="87eca-171">您可能會有 toogo tooan 進階的設定 頁面上，並查看 hello 文字**CNAME**，**別名**，或**子網域**。</span><span class="sxs-lookup"><span data-stu-id="87eca-171">You may have toogo tooan advanced settings page and look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="87eca-172">建立新的 CNAME 記錄，並提供包含 hello 的子網域別名*asverify*子網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-172">Create a new CNAME record, and provide a subdomain alias that includes hello *asverify* subdomain.</span></span> <span data-ttu-id="87eca-173">例如 **asverify.www** 或 **asverify.photos**。</span><span class="sxs-lookup"><span data-stu-id="87eca-173">For example, **asverify.www** or **asverify.photos**.</span></span> <span data-ttu-id="87eca-174">然後提供主機名稱，也就是您的 Blob 服務端點，格式為 hello **asverify.mystorageaccount.blob.core.windows.net** (其中**mystorageaccount** hello 儲存體帳戶名稱)。</span><span class="sxs-lookup"><span data-stu-id="87eca-174">Then provide a host name, which is your Blob service endpoint, in hello format **asverify.mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is hello name of your storage account).</span></span> <span data-ttu-id="87eca-175">hello 主機名稱 toouse 會出現在 hello 的項目 #2*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-175">hello host name toouse appears in item #2 of hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="87eca-176">Hello hello 文字方塊中*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，輸入 hello 您的自訂網域名稱，包括 hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-176">In hello text box on hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com), enter hello name of your custom domain, including hello subdomain.</span></span> <span data-ttu-id="87eca-177">不包含 *asverify*。</span><span class="sxs-lookup"><span data-stu-id="87eca-177">Do not include *asverify*.</span></span> <span data-ttu-id="87eca-178">例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。如果您的子網域是**相片**，輸入**photos.contoso.com**。 hello 子網域是必要項。</span><span class="sxs-lookup"><span data-stu-id="87eca-178">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. hello subdomain is required.</span></span>
1. <span data-ttu-id="87eca-179">選取 hello**使用間接 CNAME 驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="87eca-179">Select hello **Use indirect CNAME validation** checkbox.</span></span>
1. <span data-ttu-id="87eca-180">選取**儲存**上 hello*自訂網域*刀鋒視窗 tooregister 您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="87eca-180">Select **Save** on hello *Custom domain* blade tooregister your custom domain.</span></span> <span data-ttu-id="87eca-181">如果 hello 註冊成功時，您會看到一個入口網站的通知，說明已成功更新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87eca-181">If hello registration is successful, you will see a portal notification stating that your storage account was successfully updated.</span></span> <span data-ttu-id="87eca-182">此時，您的自訂網域已經通過 Azure 的驗證，但流量 tooyour 網域尚未路由 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87eca-182">At this point, your custom domain has been verified by Azure, but traffic tooyour domain is not yet being routed tooyour storage account.</span></span>
1. <span data-ttu-id="87eca-183">傳回 tooyour DNS 提供者的網站，並建立另一個對應的子網域 tooyour Blob 服務端點的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="87eca-183">Return tooyour DNS provider's website, and create another CNAME record that maps your subdomain tooyour Blob service endpoint.</span></span> <span data-ttu-id="87eca-184">例如，指定做為 hello 子網域**www**或**相片**(不含 hello *asverify*)，hello 做為主機名稱和**mystorageaccount.blob.core.windows.net** (其中**mystorageaccount** hello 儲存體帳戶名稱)。</span><span class="sxs-lookup"><span data-stu-id="87eca-184">For example, specify hello subdomain as **www** or **photos** (without hello *asverify*), and hello hostname as **mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is hello name of your storage account).</span></span> <span data-ttu-id="87eca-185">有了這個步驟中，您的自訂網域的 hello 註冊已完成。</span><span class="sxs-lookup"><span data-stu-id="87eca-185">With this step, hello registration of your custom domain is complete.</span></span>
1. <span data-ttu-id="87eca-186">最後，您可以刪除 hello CNAME 記錄，建立包含 hello **asverify**子網域，因為它是必要只做為中間步驟。</span><span class="sxs-lookup"><span data-stu-id="87eca-186">Finally, you can delete hello CNAME record you created containing hello **asverify** subdomain, as it was necessary only as an intermediary step.</span></span>

<span data-ttu-id="87eca-187">一旦您新的 CNAME 記錄傳播到透過 DNS，您的使用者可以檢視 blob 資料使用自訂網域，只要有 hello 適當的權限。</span><span class="sxs-lookup"><span data-stu-id="87eca-187">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have hello appropriate permissions.</span></span>

## <a name="test-your-custom-domain"></a><span data-ttu-id="87eca-188">測試自訂網域</span><span class="sxs-lookup"><span data-stu-id="87eca-188">Test your custom domain</span></span>

<span data-ttu-id="87eca-189">您的自訂網域是的 tooconfirm 確實對應 tooyour Blob 服務端點、 建立 blob 儲存體帳戶內的公用容器中。</span><span class="sxs-lookup"><span data-stu-id="87eca-189">tooconfirm your custom domain is indeed mapped tooyour Blob service endpoint, create a blob in a public container within your storage account.</span></span> <span data-ttu-id="87eca-190">接著，如果在 web 瀏覽器中，您可以使用 URI 中遵循格式 tooaccess hello blob 的 hello:</span><span class="sxs-lookup"><span data-stu-id="87eca-190">Then, in a web browser, use a URI in hello following format tooaccess hello blob:</span></span>

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

<span data-ttu-id="87eca-191">例如，您可能會使用下列 URI tooaccess hello web 表單的 hello **myforms**容器中 hello **photos.contoso.com**自訂子網域：</span><span class="sxs-lookup"><span data-stu-id="87eca-191">For example, you might use hello following URI tooaccess a web form in hello **myforms** container in hello **photos.contoso.com** custom subdomain:</span></span>

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a><span data-ttu-id="87eca-192">取消註冊自訂網域</span><span class="sxs-lookup"><span data-stu-id="87eca-192">Deregister a custom domain</span></span>

<span data-ttu-id="87eca-193">tooderegister 自訂網域，您的 Blob 儲存體端點，以使用其中一個 hello 下列程序。</span><span class="sxs-lookup"><span data-stu-id="87eca-193">tooderegister a custom domain for your Blob storage endpoint, use one of hello following procedures.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="87eca-194">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="87eca-194">Azure portal</span></span>

<span data-ttu-id="87eca-195">Hello Azure 入口網站 tooremove hello 自訂網域 設定中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="87eca-195">Perform hello following in hello Azure portal tooremove hello custom domain setting:</span></span>

1. <span data-ttu-id="87eca-196">瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="87eca-196">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="87eca-197">在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87eca-197">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="87eca-198">清除 hello hello 包含您的自訂網域名稱 文字方塊中的內容。</span><span class="sxs-lookup"><span data-stu-id="87eca-198">Clear hello contents of hello text box containing your custom domain name.</span></span>
1. <span data-ttu-id="87eca-199">選取 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87eca-199">Select hello **Save** button.</span></span>

<span data-ttu-id="87eca-200">當已經成功移除 hello 自訂網域時，您會看到一個入口網站的通知，說明已成功更新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87eca-200">When hello custom domain has been removed successfully, you will see a portal notification stating that your storage account was successfully updated.</span></span>

### <a name="azure-cli-20"></a><span data-ttu-id="87eca-201">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="87eca-201">Azure CLI 2.0</span></span>

<span data-ttu-id="87eca-202">使用 hello [az 儲存體帳戶更新](https://docs.microsoft.com/cli/azure/storage/account#update)CLI 命令，並指定空字串 (`""`) hello`--custom-domain`引數的值 tooremove 自訂網域註冊。</span><span class="sxs-lookup"><span data-stu-id="87eca-202">Use hello [az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI command and specify an empty string (`""`) for hello `--custom-domain` argument value tooremove a custom domain registration.</span></span>

* <span data-ttu-id="87eca-203">命令格式︰</span><span class="sxs-lookup"><span data-stu-id="87eca-203">Command format:</span></span>

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* <span data-ttu-id="87eca-204">命令範例︰</span><span class="sxs-lookup"><span data-stu-id="87eca-204">Command example:</span></span>

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a><span data-ttu-id="87eca-205">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87eca-205">PowerShell</span></span>

<span data-ttu-id="87eca-206">使用 hello[組 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet 並指定空字串 (`""`) hello`-CustomDomainName`引數的值 tooremove 自訂網域註冊。</span><span class="sxs-lookup"><span data-stu-id="87eca-206">Use hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet and specify an empty string (`""`) for hello `-CustomDomainName` argument value tooremove a custom domain registration.</span></span>

* <span data-ttu-id="87eca-207">命令格式︰</span><span class="sxs-lookup"><span data-stu-id="87eca-207">Command format:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* <span data-ttu-id="87eca-208">命令範例︰</span><span class="sxs-lookup"><span data-stu-id="87eca-208">Command example:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a><span data-ttu-id="87eca-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87eca-209">Next steps</span></span>
* [<span data-ttu-id="87eca-210">對應的自訂網域 tooan Azure 內容傳遞網路 (CDN) 端點</span><span class="sxs-lookup"><span data-stu-id="87eca-210">Map a custom domain tooan Azure Content Delivery Network (CDN) endpoint</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="87eca-211">使用自訂網域中的 hello Azure CDN tooaccess blob，透過 HTTPS</span><span class="sxs-lookup"><span data-stu-id="87eca-211">Using hello Azure CDN tooaccess blobs with custom domains over HTTPS</span></span>](./storage-https-custom-domain-cdn.md)
