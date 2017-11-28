---
title: "針對 Azure Blob 儲存體端點設定自訂網域名稱 | Microsoft Docs"
description: "使用 Azure 入口網站，將您專屬的正式名稱 (CNAME) 對應至 Azure 儲存體帳戶中的 Blob 儲存體端點。"
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
ms.openlocfilehash: 67a197ffa04d284e9251d7f79b36a86d03637fd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a><span data-ttu-id="86fd4-103">針對 Blob 儲存體端點設定自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="86fd4-103">Configure a custom domain name for your Blob storage endpoint</span></span>

<span data-ttu-id="86fd4-104">您可以設定自訂網域名稱，以供存取 Azure 儲存體帳戶中的 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="86fd4-104">You can configure a custom domain for accessing blob data in your Azure storage account.</span></span> <span data-ttu-id="86fd4-105">Blob 儲存體的預設端點是 `<storage-account-name>.blob.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="86fd4-105">The default endpoint for Blob storage is `<storage-account-name>.blob.core.windows.net`.</span></span> <span data-ttu-id="86fd4-106">若您將自訂網域和子網域 (如 **www.contoso.com**) 對應至儲存體帳戶的 Blob 端點，則可讓使用者使用該網域存取您儲存體帳戶中的 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="86fd4-106">If you map a custom domain and subdomain like **www.contoso.com** to the blob endpoint for your storage account, your users can then access blob data in your storage account using that domain.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86fd4-107">Azure 儲存體尚未以原生方式支援使用自訂網域的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="86fd4-107">Azure Storage does not yet natively support HTTPS with custom domains.</span></span> <span data-ttu-id="86fd4-108">您目前可以[使用 Azure CDN 透過 HTTP 以自訂網域存取 blob](storage-https-custom-domain-cdn.md)。</span><span class="sxs-lookup"><span data-stu-id="86fd4-108">You can currently [Use the Azure CDN to access blobs with custom domains over HTTPS](storage-https-custom-domain-cdn.md).</span></span>
>

<span data-ttu-id="86fd4-109">下表展示的幾個範例 URL，適用於名為 **mystorageaccount** 之儲存體帳戶中的 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="86fd4-109">The following table shows a few sample URLs for blob data located in a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="86fd4-110">針對儲存體帳戶註冊的自訂網域為 **www.contoso.com**：</span><span class="sxs-lookup"><span data-stu-id="86fd4-110">The custom domain registered for the storage account is **www.contoso.com**:</span></span>

| <span data-ttu-id="86fd4-111">資源類型</span><span class="sxs-lookup"><span data-stu-id="86fd4-111">Resource Type</span></span> | <span data-ttu-id="86fd4-112">預設 URL</span><span class="sxs-lookup"><span data-stu-id="86fd4-112">Default URL</span></span> | <span data-ttu-id="86fd4-113">自訂網域 URL</span><span class="sxs-lookup"><span data-stu-id="86fd4-113">Custom domain URL</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86fd4-114">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="86fd4-114">Storage account</span></span> | <span data-ttu-id="86fd4-115">http://mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="86fd4-115">http://mystorageaccount.blob.core.windows.net</span></span> | <span data-ttu-id="86fd4-116">http://www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="86fd4-116">http://www.contoso.com</span></span> |
| <span data-ttu-id="86fd4-117">Blob</span><span class="sxs-lookup"><span data-stu-id="86fd4-117">Blob</span></span> |<span data-ttu-id="86fd4-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="86fd4-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span></span> | <span data-ttu-id="86fd4-119">http://www.contoso.com/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="86fd4-119">http://www.contoso.com/mycontainer/myblob</span></span> |
| <span data-ttu-id="86fd4-120">根容器</span><span class="sxs-lookup"><span data-stu-id="86fd4-120">Root container</span></span> | <span data-ttu-id="86fd4-121">http://mystorageaccount.blob.core.windows.net/myblob 或 http://mystorageaccount.blob.core.windows.net/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="86fd4-121">http://mystorageaccount.blob.core.windows.net/myblob or http://mystorageaccount.blob.core.windows.net/$root/myblob</span></span>| <span data-ttu-id="86fd4-122">http://www.contoso.com/myblob 或 http://www.contoso.com/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="86fd4-122">http://www.contoso.com/myblob or http://www.contoso.com/$root/myblob</span></span> |

## <a name="direct-vs-intermediary-domain-mapping"></a><span data-ttu-id="86fd4-123">直接與中繼網域對應</span><span class="sxs-lookup"><span data-stu-id="86fd4-123">Direct vs. intermediary domain mapping</span></span>

<span data-ttu-id="86fd4-124">您可使用兩種方式，將自訂網域指向您儲存體帳戶的 Blob 端點：直接 CNAME 對應與使用 *asverify* 中繼子網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-124">There are two ways to point your custom domain to the blob endpoint for your storage account: direct CNAME mapping, and using the *asverify* intermediary subdomain.</span></span>

### <a name="direct-cname-mapping"></a><span data-ttu-id="86fd4-125">直接 CNAME 對應</span><span class="sxs-lookup"><span data-stu-id="86fd4-125">Direct CNAME mapping</span></span>

<span data-ttu-id="86fd4-126">第一種方法最為簡易，亦即建立正式名稱 (CNAME) 記錄將您的自訂網域與子網域直接對應至 Blob 端點。</span><span class="sxs-lookup"><span data-stu-id="86fd4-126">The first, and simplest, method is to create a canonical name (CNAME) record that maps your custom domain and subdomain directly to the blob endpoint.</span></span> <span data-ttu-id="86fd4-127">CNAME 記錄是將來源網域對應至目的地網域的網域名稱系統 (DNS) 功能。</span><span class="sxs-lookup"><span data-stu-id="86fd4-127">A CNAME record is a domain name system (DNS) feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="86fd4-128">在此案例中，來源網域為您的專屬自訂網域和子網域，例如 *www.contoso.com*。目的地網域為您的 Blob 服務端點，例如 *mystorageaccount.blob.core.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="86fd4-128">In this case, the source domain is your own custom domain and subdomain, for example *www.contoso.com*. The destination domain is your Blob service endpoint, for example *mystorageaccount.blob.core.windows.net*.</span></span>

<span data-ttu-id="86fd4-129">[註冊自訂網域](#register-a-custom-domain)涵蓋直接方法。</span><span class="sxs-lookup"><span data-stu-id="86fd4-129">The direct method is covered in [Register a custom domain](#register-a-custom-domain).</span></span>

### <a name="intermediary-mapping-with-asverify"></a><span data-ttu-id="86fd4-130">使用 *asverify* 的中繼對應</span><span class="sxs-lookup"><span data-stu-id="86fd4-130">Intermediary mapping with *asverify*</span></span>

<span data-ttu-id="86fd4-131">第二種方法也會使用 CNAME 記錄，但會先運用由 Azure 辨識的特殊子網域以避免停機：**asverify**。</span><span class="sxs-lookup"><span data-stu-id="86fd4-131">The second method also uses CNAME records, but first employs a special subdomain recognized by Azure to avoid downtime: **asverify**.</span></span>

<span data-ttu-id="86fd4-132">在將自訂網域對應至 Blob 端點的程序中，會由於您在 [Azure 入口網站](https://portal.azure.com)中註冊網域而導致短暫停機。</span><span class="sxs-lookup"><span data-stu-id="86fd4-132">The process of mapping your custom domain to a blob endpoint can result in a brief period of downtime for the domain while you are registering it in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="86fd4-133">若自訂網域目前支援不得發生停機之服務等級協定 (SLA) 的應用程式，您可以使用 Azure *asverify* 子網域做為中繼註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="86fd4-133">If your custom domain is currently supporting an application with a service-level agreement (SLA) that requires zero downtime, then you can use the Azure *asverify* subdomain as an intermediate registration step.</span></span> <span data-ttu-id="86fd4-134">此中繼步驟可確保讓使用者能夠在執行 DNS 對應時存取您的網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-134">This intermediate step ensures users are able to access your domain while the DNS mapping takes place.</span></span>

<span data-ttu-id="86fd4-135">[使用 *asverify* 子網域註冊自訂網域](#register-a-custom-domain-using-the-asverify-subdomain)涵蓋中繼方法。</span><span class="sxs-lookup"><span data-stu-id="86fd4-135">The intermediary method is covered in [Register a custom domain using the *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

## <a name="register-a-custom-domain"></a><span data-ttu-id="86fd4-136">註冊自訂網域</span><span class="sxs-lookup"><span data-stu-id="86fd4-136">Register a custom domain</span></span>
<span data-ttu-id="86fd4-137">若您不需要顧及使用者會短暫地無法存取網域的問題，或是自訂網域目前未主控應用程式，您可以使用此程序來註冊自訂網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-137">Use this procedure to register your custom domain if you have no concerns about the domain being briefly unavailable to your users, or if your custom domain is not currently hosting an application.</span></span>

<span data-ttu-id="86fd4-138">若自訂網域目前支援不允許發生任何停機狀況的應用程式，請遵循[使用 *asverify* 子網域註冊自訂網域](#register-a-custom-domain-using-the-asverify-subdomain)中所述的程序操作。</span><span class="sxs-lookup"><span data-stu-id="86fd4-138">If your custom domain is currently supporting an application that cannot have any downtime, follow the procedure outlined in [Register a custom domain using the *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

<span data-ttu-id="86fd4-139">若要設定自訂網域名稱，您必須在 DNS 中建立新的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="86fd4-139">To configure a custom domain name, you must create a new CNAME record in DNS.</span></span> <span data-ttu-id="86fd4-140">CNAME 記錄會指定網域名稱的別名。</span><span class="sxs-lookup"><span data-stu-id="86fd4-140">The CNAME record specifies an alias for a domain name.</span></span> <span data-ttu-id="86fd4-141">在此案例中，CNAME 記錄會將自訂網域的位址，對應至儲存體帳戶的 Blob 儲存體端點。</span><span class="sxs-lookup"><span data-stu-id="86fd4-141">In this case, it maps the address of your custom domain to the Blob storage endpoint for your storage account.</span></span>

<span data-ttu-id="86fd4-142">一般而言，您可在網域註冊機構的網站上管理網域的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="86fd4-142">Typically, you can manage your domain's DNS settings on your domain registrar's website.</span></span> <span data-ttu-id="86fd4-143">各註冊機構指定 CNAME 記錄的方法都很類似，只是稍微不同，但概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="86fd4-143">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concept is the same.</span></span> <span data-ttu-id="86fd4-144">部分基本網域註冊套件並未提供 DNS 組態，因此您可能需要先升級網域註冊套件，然後再建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="86fd4-144">Some basic domain registration packages do not offer DNS configuration, so you may need to upgrade your domain registration package before you can create the CNAME record.</span></span>

1. <span data-ttu-id="86fd4-145">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="86fd4-145">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="86fd4-146">在功能表刀鋒視窗的 [BLOB SERVICE] 下方，選取 [自訂網域] 以開啟 [自訂網域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86fd4-146">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="86fd4-147">登入網域註冊機構的網站，然後前往 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="86fd4-147">Log on to your domain registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="86fd4-148">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="86fd4-148">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="86fd4-149">尋找管理 CNAME 的區段。</span><span class="sxs-lookup"><span data-stu-id="86fd4-149">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="86fd4-150">您可能需要移至進階設定頁面，並尋找 **CNAME**、**Alias** 或 **Subdomains** 單字。</span><span class="sxs-lookup"><span data-stu-id="86fd4-150">You may have to go to an advanced settings page and look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="86fd4-151">建立新的 CNAME 記錄並提供子網域別名，如 **www** 或 **photos**。</span><span class="sxs-lookup"><span data-stu-id="86fd4-151">Create a new CNAME record and provide a subdomain alias such as **www** or **photos**.</span></span> <span data-ttu-id="86fd4-152">接著，以 **mystorageaccount.blob.core.windows.net** 格式 (其中 *mystorageaccount* 代表儲存體帳戶的名稱) 提供主機名稱 (即 Blob 服務端點)。</span><span class="sxs-lookup"><span data-stu-id="86fd4-152">Then provide a host name, which is your Blob service endpoint, in the format **mystorageaccount.blob.core.windows.net** (where *mystorageaccount* is the name of your storage account).</span></span> <span data-ttu-id="86fd4-153">在 [Azure 入口網站](https://portal.azure.com)中，主機名稱會顯示於 [自訂網域] 刀鋒視窗的項目 #1。</span><span class="sxs-lookup"><span data-stu-id="86fd4-153">The host name to use appears in item #1 of the *Custom domain* blade in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="86fd4-154">在 [Azure 入口網站](https://portal.azure.com) [自訂網域] 刀鋒視窗的文字方塊中，輸入包含子網域的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="86fd4-154">In the text box on the *Custom domain* blade in the [Azure portal](https://portal.azure.com), enter the name of your custom domain, including the subdomain.</span></span> <span data-ttu-id="86fd4-155">例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。若您的子網域為 **photos**，請輸入 **photos.contoso.com**。子網域為*必要項目*。</span><span class="sxs-lookup"><span data-stu-id="86fd4-155">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. The subdomain is *required*.</span></span>
1. <span data-ttu-id="86fd4-156">在 [自訂網域] 刀鋒視窗上選取 [儲存]，以註冊您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-156">Select **Save** on the *Custom domain* blade to register your custom domain.</span></span> <span data-ttu-id="86fd4-157">如果註冊成功，您會看見指出已成功更新儲存體帳戶的入口網站通知。</span><span class="sxs-lookup"><span data-stu-id="86fd4-157">If the registration is successful, you will see a portal notification that your storage account was successfully updated.</span></span>

<span data-ttu-id="86fd4-158">一旦透過 DNS 傳播您的新 CNAME 記錄，使用者只要具備適當權限，即可透過您的自訂網域檢視 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="86fd4-158">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have the appropriate permissions.</span></span>

## <a name="register-a-custom-domain-using-the-asverify-subdomain"></a><span data-ttu-id="86fd4-159">使用 *asverify* 子網域註冊自訂網域</span><span class="sxs-lookup"><span data-stu-id="86fd4-159">Register a custom domain using the *asverify* subdomain</span></span>
<span data-ttu-id="86fd4-160">如果自訂網域目前需支援不得發生停機時間之 SLA 的應用程式，您可以使用此程序來註冊自訂網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-160">Use this procedure to register your custom domain if your custom domain is currently supporting an application with an SLA that requires that there be no downtime.</span></span> <span data-ttu-id="86fd4-161">您可藉由建立從 `asverify.<subdomain>.<customdomain>` 指向 `asverify.<storageaccount>.blob.core.windows.net` 的 CNAME，預先透過 Azure 註冊您的網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-161">By creating a CNAME that points from `asverify.<subdomain>.<customdomain>` to `asverify.<storageaccount>.blob.core.windows.net`, you can pre-register your domain with Azure.</span></span> <span data-ttu-id="86fd4-162">接著，您可以建立從 `<subdomain>.<customdomain>` 指向 `<storageaccount>.blob.core.windows.net` 的第二個 CNAME，將傳送至自訂網域的流量引導至 Blob 端點。</span><span class="sxs-lookup"><span data-stu-id="86fd4-162">You can then create a second CNAME that points from `<subdomain>.<customdomain>` to `<storageaccount>.blob.core.windows.net`, at which point traffic to your custom domain will be directed to your blob endpoint.</span></span>

<span data-ttu-id="86fd4-163">**asverify** 子網域是 Azure 認可的特殊子網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-163">The **asverify** subdomain is a special subdomain recognized by Azure.</span></span> <span data-ttu-id="86fd4-164">在自己的子網域前加上 `asverify`，代表您允許 Azure 在不修改網域之 DNS 記錄的情況下認可自訂網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-164">By prepending `asverify` to your own subdomain, you permit Azure to recognize your custom domain without modifying the DNS record for the domain.</span></span> <span data-ttu-id="86fd4-165">一旦修改網域的 DNS 記錄，其將會在無停機的情況下對應至 Blob 端點。</span><span class="sxs-lookup"><span data-stu-id="86fd4-165">When you do modify the DNS record for the domain, it will be mapped to the blob endpoint with no downtime.</span></span>

1. <span data-ttu-id="86fd4-166">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="86fd4-166">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="86fd4-167">在功能表刀鋒視窗的 [BLOB SERVICE] 下方，選取 [自訂網域] 以開啟 [自訂網域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86fd4-167">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="86fd4-168">登入 DNS 提供者的網站，然後前往 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="86fd4-168">Log on to your DNS provider's website and go to the page for managing DNS.</span></span> <span data-ttu-id="86fd4-169">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="86fd4-169">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="86fd4-170">尋找管理 CNAME 的區段。</span><span class="sxs-lookup"><span data-stu-id="86fd4-170">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="86fd4-171">您可能需要移至進階設定頁面，並尋找 **CNAME**、**Alias** 或 **Subdomains** 單字。</span><span class="sxs-lookup"><span data-stu-id="86fd4-171">You may have to go to an advanced settings page and look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="86fd4-172">建立新的 CNAME 記錄，並提供包含 *asverify* 子網域的子網域別名。</span><span class="sxs-lookup"><span data-stu-id="86fd4-172">Create a new CNAME record, and provide a subdomain alias that includes the *asverify* subdomain.</span></span> <span data-ttu-id="86fd4-173">例如 **asverify.www** 或 **asverify.photos**。</span><span class="sxs-lookup"><span data-stu-id="86fd4-173">For example, **asverify.www** or **asverify.photos**.</span></span> <span data-ttu-id="86fd4-174">接著，以 **asverify.mystorageaccount.blob.core.windows.net** 格式 (其中 **mystorageaccount** 代表儲存體帳戶的名稱) 提供主機名稱 (即 Blob 服務端點)。</span><span class="sxs-lookup"><span data-stu-id="86fd4-174">Then provide a host name, which is your Blob service endpoint, in the format **asverify.mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is the name of your storage account).</span></span> <span data-ttu-id="86fd4-175">在 [Azure 入口網站](https://portal.azure.com)中，主機名稱會顯示於 [自訂網域] 刀鋒視窗的項目 #2。</span><span class="sxs-lookup"><span data-stu-id="86fd4-175">The host name to use appears in item #2 of the *Custom domain* blade in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="86fd4-176">在 [Azure 入口網站](https://portal.azure.com) [自訂網域] 刀鋒視窗的文字方塊中，輸入包含子網域的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="86fd4-176">In the text box on the *Custom domain* blade in the [Azure portal](https://portal.azure.com), enter the name of your custom domain, including the subdomain.</span></span> <span data-ttu-id="86fd4-177">不包含 *asverify*。</span><span class="sxs-lookup"><span data-stu-id="86fd4-177">Do not include *asverify*.</span></span> <span data-ttu-id="86fd4-178">例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。若您的子網域為 **photos**，請輸入 **photos.contoso.com**。子網域為必要項目。</span><span class="sxs-lookup"><span data-stu-id="86fd4-178">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. The subdomain is required.</span></span>
1. <span data-ttu-id="86fd4-179">選取 [使用間接 CNAME 驗證] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="86fd4-179">Select the **Use indirect CNAME validation** checkbox.</span></span>
1. <span data-ttu-id="86fd4-180">在 [自訂網域] 刀鋒視窗上選取 [儲存]，以註冊您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="86fd4-180">Select **Save** on the *Custom domain* blade to register your custom domain.</span></span> <span data-ttu-id="86fd4-181">如果註冊成功，您會看見指出已成功更新儲存體帳戶的入口網站通知。</span><span class="sxs-lookup"><span data-stu-id="86fd4-181">If the registration is successful, you will see a portal notification stating that your storage account was successfully updated.</span></span> <span data-ttu-id="86fd4-182">此時，自訂網域已通過 Azure 的驗證，不過前往網域的流量尚未路由傳送到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="86fd4-182">At this point, your custom domain has been verified by Azure, but traffic to your domain is not yet being routed to your storage account.</span></span>
1. <span data-ttu-id="86fd4-183">返回 DNS 提供者的網站，然後建立將子網域對應至 Blob 服務端點的另一個 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="86fd4-183">Return to your DNS provider's website, and create another CNAME record that maps your subdomain to your Blob service endpoint.</span></span> <span data-ttu-id="86fd4-184">例如，將子網域指定為 **www** 或 **photos** (無 *asverify*)，並將主機名稱指定為 **mystorageaccount.blob.core.windows.net** (其中 **mystorageaccount** 為您儲存體帳戶的名稱)。</span><span class="sxs-lookup"><span data-stu-id="86fd4-184">For example, specify the subdomain as **www** or **photos** (without the *asverify*), and the hostname as **mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is the name of your storage account).</span></span> <span data-ttu-id="86fd4-185">待這個步驟完成後，自訂網域的註冊作業也宣告完成。</span><span class="sxs-lookup"><span data-stu-id="86fd4-185">With this step, the registration of your custom domain is complete.</span></span>
1. <span data-ttu-id="86fd4-186">最後，您可刪除已建立的 CNAME 記錄 (包含 **asverify** 子網域)，因為只有在中繼步驟中才需要使用該記錄。</span><span class="sxs-lookup"><span data-stu-id="86fd4-186">Finally, you can delete the CNAME record you created containing the **asverify** subdomain, as it was necessary only as an intermediary step.</span></span>

<span data-ttu-id="86fd4-187">一旦透過 DNS 傳播您的新 CNAME 記錄，使用者只要具備適當權限，即可透過您的自訂網域檢視 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="86fd4-187">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have the appropriate permissions.</span></span>

## <a name="test-your-custom-domain"></a><span data-ttu-id="86fd4-188">測試自訂網域</span><span class="sxs-lookup"><span data-stu-id="86fd4-188">Test your custom domain</span></span>

<span data-ttu-id="86fd4-189">若要確認自訂網域是否確實對應至 Blob 服務端點，請在儲存體帳戶內的公用容器中建立 Blob。</span><span class="sxs-lookup"><span data-stu-id="86fd4-189">To confirm your custom domain is indeed mapped to your Blob service endpoint, create a blob in a public container within your storage account.</span></span> <span data-ttu-id="86fd4-190">接著，在網頁瀏覽器中使用以下格式的 URI 存取 Blob：</span><span class="sxs-lookup"><span data-stu-id="86fd4-190">Then, in a web browser, use a URI in the following format to access the blob:</span></span>

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

<span data-ttu-id="86fd4-191">例如，下列 URI 可讓您透過 **photos.contoso.com** 自訂子網域中的 **myforms** 容器，存取 Web 表單：</span><span class="sxs-lookup"><span data-stu-id="86fd4-191">For example, you might use the following URI to access a web form in the **myforms** container in the **photos.contoso.com** custom subdomain:</span></span>

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a><span data-ttu-id="86fd4-192">取消註冊自訂網域</span><span class="sxs-lookup"><span data-stu-id="86fd4-192">Deregister a custom domain</span></span>

<span data-ttu-id="86fd4-193">若要取消註冊您的 Blob 儲存體端點自訂網域，請使用下列其中一項程序。</span><span class="sxs-lookup"><span data-stu-id="86fd4-193">To deregister a custom domain for your Blob storage endpoint, use one of the following procedures.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="86fd4-194">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="86fd4-194">Azure portal</span></span>

<span data-ttu-id="86fd4-195">請在 Azure 入口網站中執行下列作業，以移除自訂的網域設定：</span><span class="sxs-lookup"><span data-stu-id="86fd4-195">Perform the following in the Azure portal to remove the custom domain setting:</span></span>

1. <span data-ttu-id="86fd4-196">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="86fd4-196">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="86fd4-197">在功能表刀鋒視窗的 [BLOB SERVICE] 下方，選取 [自訂網域] 以開啟 [自訂網域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86fd4-197">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="86fd4-198">清除包含自訂網域名稱的文字方塊中的內容。</span><span class="sxs-lookup"><span data-stu-id="86fd4-198">Clear the contents of the text box containing your custom domain name.</span></span>
1. <span data-ttu-id="86fd4-199">選取 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86fd4-199">Select the **Save** button.</span></span>

<span data-ttu-id="86fd4-200">順利移除自訂網域後，您會看到指出已成功更新儲存體帳戶的入口網站通知。</span><span class="sxs-lookup"><span data-stu-id="86fd4-200">When the custom domain has been removed successfully, you will see a portal notification stating that your storage account was successfully updated.</span></span>

### <a name="azure-cli-20"></a><span data-ttu-id="86fd4-201">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="86fd4-201">Azure CLI 2.0</span></span>

<span data-ttu-id="86fd4-202">使用 [az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI 命令，並指定 `--custom-domain`引數值的空字串 (`""`)，以移除自訂網域註冊。</span><span class="sxs-lookup"><span data-stu-id="86fd4-202">Use the [az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI command and specify an empty string (`""`) for the `--custom-domain` argument value to remove a custom domain registration.</span></span>

* <span data-ttu-id="86fd4-203">命令格式︰</span><span class="sxs-lookup"><span data-stu-id="86fd4-203">Command format:</span></span>

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* <span data-ttu-id="86fd4-204">命令範例︰</span><span class="sxs-lookup"><span data-stu-id="86fd4-204">Command example:</span></span>

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a><span data-ttu-id="86fd4-205">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86fd4-205">PowerShell</span></span>

<span data-ttu-id="86fd4-206">使用 [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet，並指定 `-CustomDomainName`引數值的空字串 (`""`)，以移除自訂網域註冊。</span><span class="sxs-lookup"><span data-stu-id="86fd4-206">Use the [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet and specify an empty string (`""`) for the `-CustomDomainName` argument value to remove a custom domain registration.</span></span>

* <span data-ttu-id="86fd4-207">命令格式︰</span><span class="sxs-lookup"><span data-stu-id="86fd4-207">Command format:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* <span data-ttu-id="86fd4-208">命令範例︰</span><span class="sxs-lookup"><span data-stu-id="86fd4-208">Command example:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a><span data-ttu-id="86fd4-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86fd4-209">Next steps</span></span>
* [<span data-ttu-id="86fd4-210">將自訂網域對應至 Azure 內容傳遞網路 (CDN) 端點</span><span class="sxs-lookup"><span data-stu-id="86fd4-210">Map a custom domain to an Azure Content Delivery Network (CDN) endpoint</span></span>](../../cdn/cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="86fd4-211">使用 Azure CDN 透過 HTTP 以自訂網域存取 blob</span><span class="sxs-lookup"><span data-stu-id="86fd4-211">Using the Azure CDN to access blobs with custom domains over HTTPS</span></span>](storage-https-custom-domain-cdn.md)
