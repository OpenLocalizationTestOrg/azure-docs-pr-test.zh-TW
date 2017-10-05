---
title: "開始使用 Azure CDN | Microsoft Docs"
description: "本主題說明如何啟用 Azure 內容傳遞網路 (CDN)。 本教學課程會逐步建立新的 CDN 設定檔和端點。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="e3db5-104">開始使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e3db5-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="e3db5-105">本主題將逐步解說如何透過建立新的 CDN 設定檔和端點來啟用 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="e3db5-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3db5-106">如需 CDN 運作方式的簡介以及功能清單，請參閱 [CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e3db5-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="e3db5-107">建立新的 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="e3db5-107">Create a new CDN profile</span></span>
<span data-ttu-id="e3db5-108">CDN 設定檔就是 CDN 端點的集合。</span><span class="sxs-lookup"><span data-stu-id="e3db5-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="e3db5-109">每個設定檔皆包含一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e3db5-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="e3db5-110">您可能會想要使用多個設定檔，依網際網路網域、Web 應用程式或其他準則來組織您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e3db5-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="e3db5-111">依預設，一個 Azure 訂用帳戶只能擁有八個 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="e3db5-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="e3db5-112">而每個 CDN 設定檔則只能擁有十個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e3db5-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="e3db5-113">CDN 定價是根據 CDN 設定檔層級來套用的。</span><span class="sxs-lookup"><span data-stu-id="e3db5-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="e3db5-114">如果您想要混合使用 Azure CDN 定價層，您需要擁有多個 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="e3db5-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="e3db5-115">建立新的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="e3db5-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="e3db5-116">**建立新的 CDN 端點**</span><span class="sxs-lookup"><span data-stu-id="e3db5-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="e3db5-117">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="e3db5-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="e3db5-118">您可能已在先前步驟中將其釘選至儀表板。</span><span class="sxs-lookup"><span data-stu-id="e3db5-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="e3db5-119">若否，則您可依序按一下 [瀏覽]、[CDN 設定檔] 尋找該設定檔，然後再按一下您要在其中新增端點的設定檔。</span><span class="sxs-lookup"><span data-stu-id="e3db5-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="e3db5-120">此時會顯示 [CDN 設定檔] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e3db5-120">The CDN profile blade appears.</span></span>
   
    ![CDN 設定檔][cdn-profile-settings]
2. <span data-ttu-id="e3db5-122">按一下 [新增端點]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3db5-122">Click the **Add Endpoint** button.</span></span>
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    <span data-ttu-id="e3db5-124">此時會顯示 [加入端點]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e3db5-124">The **Add an endpoint** blade appears.</span></span>
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. <span data-ttu-id="e3db5-126">輸入這個 CDN 端點的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="e3db5-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="e3db5-127">此名稱會用於存取位於網域 `<endpointname>.azureedge.net`的快取資源。</span><span class="sxs-lookup"><span data-stu-id="e3db5-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="e3db5-128">在 [原始來源類型]  下拉式清單中，選取您的原始來源類型。</span><span class="sxs-lookup"><span data-stu-id="e3db5-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="e3db5-129">針對 Azure 儲存體帳戶選取 [儲存體]、針對 Azure 雲端服務選取 [雲端服務]、針對 Azure Web 應用程式選取 [Web 應用程式]，若為其他任何可公開存取的 Web 伺服器來源 (裝載於 Azure 或其他位置)，則請選取 [自訂原始來源]。</span><span class="sxs-lookup"><span data-stu-id="e3db5-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![CDN 原始來源類型](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="e3db5-131">在 [原始主機名稱]  下拉式清單中，選取您的原始網域類型。</span><span class="sxs-lookup"><span data-stu-id="e3db5-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="e3db5-132">下拉式清單會列出您在步驟 4 中指定之類型的所有可用原始來源。</span><span class="sxs-lookup"><span data-stu-id="e3db5-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="e3db5-133">如果您選取 [自訂原始來源] 作為您的 [原始來源類型]，您將會輸入自訂原始來源的網域。</span><span class="sxs-lookup"><span data-stu-id="e3db5-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="e3db5-134">在 [原始路徑]  文字方塊中，輸入您要快取的資源路徑，或保留空白以允許快取位於您在步驟 5 中指定之網域中的任何資源。</span><span class="sxs-lookup"><span data-stu-id="e3db5-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="e3db5-135">在 [原始主機標頭] 中，輸入您要 CDN 連同每個要求一起傳送的主機標頭，或保留預設值。</span><span class="sxs-lookup"><span data-stu-id="e3db5-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="e3db5-136">某些類型的原始來源 (例如 Azure 儲存體和 Web Apps) 要求主機標頭必須符合原始來源的網域。</span><span class="sxs-lookup"><span data-stu-id="e3db5-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="e3db5-137">除非您的原始來源需要與其網域不同的主機標頭，否則您應該保留預設值。</span><span class="sxs-lookup"><span data-stu-id="e3db5-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="e3db5-138">在 [通訊協定] 和 [原始連接埠] 中，指定用來存取原始來源之資源的通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="e3db5-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="e3db5-139">至少必須選取一個通訊協定 (HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="e3db5-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e3db5-140">[原始連接埠] 只會影響端點用來從原始來源擷取資訊的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e3db5-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="e3db5-141">不論 [原始連接埠] 為何，端點本身只會透過預設 HTTP 和 HTTPS 連接埠 (80 和 443) 提供給終端用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="e3db5-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="e3db5-142">**來自 Akamai 的 Azure CDN** 端點不允許原始來源的完整 TCP 連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="e3db5-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="e3db5-143">如需不允許的原始連接埠清單，請參閱 [來自 Akamai 的 Azure CDN 允許的原始連接埠](https://msdn.microsoft.com/library/mt757337.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e3db5-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="e3db5-144">使用 HTTPS 存取 CDN 內容具有下列限制：</span><span class="sxs-lookup"><span data-stu-id="e3db5-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="e3db5-145">您必須使用 CDN 所提供的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="e3db5-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="e3db5-146">不支援第三方憑證。</span><span class="sxs-lookup"><span data-stu-id="e3db5-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="e3db5-147">您必須使用 CDN 提供的網域 (`<endpointname>.azureedge.net`) 來存取 HTTPS 內容。</span><span class="sxs-lookup"><span data-stu-id="e3db5-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="e3db5-148">因為 CDN 目前不支援自訂憑證，所以自訂網域名稱 (CNAME) 不提供 HTTPS 支援。</span><span class="sxs-lookup"><span data-stu-id="e3db5-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="e3db5-149">按一下 [加入]  按鈕，以建立新的端點。</span><span class="sxs-lookup"><span data-stu-id="e3db5-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="e3db5-150">端點建立完畢之後，即會出現在設定檔的端點清單中。</span><span class="sxs-lookup"><span data-stu-id="e3db5-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="e3db5-151">此清單檢視會顯示用來存取所快取內容的 URL 以及原始網域。</span><span class="sxs-lookup"><span data-stu-id="e3db5-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![CDN 端點][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="e3db5-153">端點不會立即可供使用，因為註冊資訊需要一段時間才能傳遍 CDN。</span><span class="sxs-lookup"><span data-stu-id="e3db5-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="e3db5-154">在 [通訊協定] <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="e3db5-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="e3db5-155">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="e3db5-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="e3db5-156">嘗試在端點組態傳播到 POP 之前就使用 CDN 網域名稱的使用者會收到 HTTP 404 回應碼。</span><span class="sxs-lookup"><span data-stu-id="e3db5-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="e3db5-157">如果在端點建立好後已過了好幾個小時，而您仍然收到 404 回應，請參閱 [針對傳回 404 狀態的 CDN 端點進行疑難排解](cdn-troubleshoot-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="e3db5-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="e3db5-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3db5-158">See Also</span></span>
* [<span data-ttu-id="e3db5-159">使用查詢字串控制 CDN 要求的快取行為</span><span class="sxs-lookup"><span data-stu-id="e3db5-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="e3db5-160">如何將 CDN 內容對應至自訂網域</span><span class="sxs-lookup"><span data-stu-id="e3db5-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="e3db5-161">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="e3db5-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="e3db5-162">清除 Azure CDN 端點</span><span class="sxs-lookup"><span data-stu-id="e3db5-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="e3db5-163">針對傳回 404 狀態的 CDN 端點進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e3db5-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
