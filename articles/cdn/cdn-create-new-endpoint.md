---
title: "開始使用 Azure CDN 的 aaaGetting |Microsoft 文件"
description: "本主題說明如何 tooenable hello Azure 內容傳遞網路 (CDN)。 hello 教學課程引導 hello 建立新的 CDN 設定檔和端點。"
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
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="98d8a-104">開始使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="98d8a-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="98d8a-105">本主題將逐步解說如何透過建立新的 CDN 設定檔和端點來啟用 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="98d8a-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98d8a-106">如簡介 toohow CDN 如何運作，以及的功能清單，請參閱 hello [CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="98d8a-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="98d8a-107">建立新的 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="98d8a-107">Create a new CDN profile</span></span>
<span data-ttu-id="98d8a-108">CDN 設定檔就是 CDN 端點的集合。</span><span class="sxs-lookup"><span data-stu-id="98d8a-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="98d8a-109">每個設定檔皆包含一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="98d8a-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="98d8a-110">您可能希望 toouse 多個設定檔 tooorganize 您的 CDN 端點的網際網路網域、 web 應用程式，或其他一些準則。</span><span class="sxs-lookup"><span data-stu-id="98d8a-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="98d8a-111">根據預設，單一 Azure 訂用帳戶是有限的 tooeight CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="98d8a-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="98d8a-112">每個 CDN 設定檔是有限的 tooten CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="98d8a-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="98d8a-113">CDN 定價為套用於 hello CDN 設定檔層級。</span><span class="sxs-lookup"><span data-stu-id="98d8a-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="98d8a-114">如果您想 toouse 混合 Azure CDN 的定價層，您需要多個的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="98d8a-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="98d8a-115">建立新的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="98d8a-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="98d8a-116">**toocreate 新的 CDN 端點**</span><span class="sxs-lookup"><span data-stu-id="98d8a-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="98d8a-117">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="98d8a-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="98d8a-118">您可能已釘選它 toohello 儀表板 hello 上一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="98d8a-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="98d8a-119">如果您不是，您可以找到它，即可**瀏覽**，然後**CDN 設定檔**，而且 hello 設定檔上按一下您想 tooadd 至您的端點。</span><span class="sxs-lookup"><span data-stu-id="98d8a-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="98d8a-120">hello CDN 設定檔 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="98d8a-120">hello CDN profile blade appears.</span></span>
   
    ![CDN 設定檔][cdn-profile-settings]
2. <span data-ttu-id="98d8a-122">按一下 hello**加入端點** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d8a-122">Click hello **Add Endpoint** button.</span></span>
   
    ![[加入端點] 按鈕][cdn-new-endpoint-button]
   
    <span data-ttu-id="98d8a-124">hello**將端點加入**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="98d8a-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![[加入端點] 刀鋒視窗][cdn-add-endpoint]
3. <span data-ttu-id="98d8a-126">輸入這個 CDN 端點的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="98d8a-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="98d8a-127">此名稱將會使用的 tooaccess hello 網域您快取的資源`<endpointname>.azureedge.net`。</span><span class="sxs-lookup"><span data-stu-id="98d8a-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="98d8a-128">在 hello**來源類型**下拉式清單中，選取您的來源類型。</span><span class="sxs-lookup"><span data-stu-id="98d8a-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="98d8a-129">針對 Azure 儲存體帳戶選取 [儲存體]、針對 Azure 雲端服務選取 [雲端服務]、針對 Azure Web 應用程式選取 [Web 應用程式]，若為其他任何可公開存取的 Web 伺服器來源 (裝載於 Azure 或其他位置)，則請選取 [自訂原始來源]。</span><span class="sxs-lookup"><span data-stu-id="98d8a-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![CDN 原始來源類型](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="98d8a-131">在 hello**來源主機名稱**下拉式清單中，選取或輸入您原始網域。</span><span class="sxs-lookup"><span data-stu-id="98d8a-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="98d8a-132">hello 下拉式清單中會列出所有可用的來源，您指定在步驟 4 中的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="98d8a-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="98d8a-133">如果您選取*自訂來源*做為您**來源類型**，您會輸入 hello 您自訂的原始網域。</span><span class="sxs-lookup"><span data-stu-id="98d8a-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="98d8a-134">在 hello**原始路徑**文字方塊中，輸入您想要 toocache 或保持空白 tooallow 快取任何資源，您在步驟 5 中指定的 hello 網域 hello 路徑 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="98d8a-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="98d8a-135">在 hello**原始主機標頭**，輸入您想要 hello 與每個要求，CDN toosend hello 主機標頭，或保留預設值，hello。</span><span class="sxs-lookup"><span data-stu-id="98d8a-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="98d8a-136">原始來源，例如 Azure 儲存體和 Web 應用程式，某些類型需要 hello 主機標頭 toomatch hello hello 原始網域。</span><span class="sxs-lookup"><span data-stu-id="98d8a-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="98d8a-137">除非您需要從其網域不同的主機標頭的原始主機，您應該保留 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="98d8a-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="98d8a-138">如**通訊協定**和**來源連接埠**、 指定 hello 通訊協定和連接埠使用的 tooaccess hello 原點在您的資源。</span><span class="sxs-lookup"><span data-stu-id="98d8a-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="98d8a-139">至少必須選取一個通訊協定 (HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="98d8a-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98d8a-140">hello**來源連接埠**只會影響哪些連接埠 hello 端點會使用從 hello 原點 tooretrieve 資訊。</span><span class="sxs-lookup"><span data-stu-id="98d8a-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="98d8a-141">hello 本身的端點才會使用 tooend 用戶端 hello 預設 HTTP 和 HTTPS 連接埠 （80 和 443），不論 hello**來源連接埠**。</span><span class="sxs-lookup"><span data-stu-id="98d8a-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="98d8a-142">**Azure CDN 從 Akamai**端點不允許 hello 完整 TCP 連接埠範圍的來源。</span><span class="sxs-lookup"><span data-stu-id="98d8a-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="98d8a-143">如需不允許的原始連接埠清單，請參閱 [來自 Akamai 的 Azure CDN 允許的原始連接埠](https://msdn.microsoft.com/library/mt757337.aspx)。</span><span class="sxs-lookup"><span data-stu-id="98d8a-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="98d8a-144">內容使用 HTTPS 存取 CDN 有下列條件約束的 hello:</span><span class="sxs-lookup"><span data-stu-id="98d8a-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="98d8a-145">您必須使用 hello hello CDN 所提供的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="98d8a-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="98d8a-146">不支援第三方憑證。</span><span class="sxs-lookup"><span data-stu-id="98d8a-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="98d8a-147">您必須使用 hello 提供 CDN 網域 (`<endpointname>.azureedge.net`) tooaccess HTTPS 內容。</span><span class="sxs-lookup"><span data-stu-id="98d8a-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="98d8a-148">HTTPS 支援不適用於自訂網域名稱 (Cname) 因為 hello CDN 目前不支援自訂憑證。</span><span class="sxs-lookup"><span data-stu-id="98d8a-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="98d8a-149">按一下 hello**新增**按鈕 toocreate hello 新端點。</span><span class="sxs-lookup"><span data-stu-id="98d8a-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="98d8a-150">一旦建立 hello 端點時，它會出現在 hello 設定檔的端點清單。</span><span class="sxs-lookup"><span data-stu-id="98d8a-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="98d8a-151">hello 清單檢視會顯示 hello URL toouse tooaccess 快取內容，以及 hello 原始網域。</span><span class="sxs-lookup"><span data-stu-id="98d8a-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![CDN 端點][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="98d8a-153">hello 端點將不立即可供使用，因為它需要花費一些時間透過 hello CDN hello 註冊 toopropagate。</span><span class="sxs-lookup"><span data-stu-id="98d8a-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="98d8a-154">在 [通訊協定] <b>來自 Akamai 的 Azure CDN</b> 設定檔，通常會在一分鐘之內完成傳播。</span><span class="sxs-lookup"><span data-stu-id="98d8a-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="98d8a-155">若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。</span><span class="sxs-lookup"><span data-stu-id="98d8a-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="98d8a-156">再試一次 toouse hello CDN 網域名稱之前傳播到 toohello 快顯 hello 端點組態的使用者會收到 HTTP 404 回應碼。</span><span class="sxs-lookup"><span data-stu-id="98d8a-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="98d8a-157">如果在端點建立好後已過了好幾個小時，而您仍然收到 404 回應，請參閱 [針對傳回 404 狀態的 CDN 端點進行疑難排解](cdn-troubleshoot-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="98d8a-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="98d8a-158">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98d8a-158">See Also</span></span>
* [<span data-ttu-id="98d8a-159">使用查詢字串控制 CDN 要求的快取行為</span><span class="sxs-lookup"><span data-stu-id="98d8a-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="98d8a-160">如何 tooMap CDN 內容 tooa 自訂網域</span><span class="sxs-lookup"><span data-stu-id="98d8a-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="98d8a-161">在 Azure CDN 端點上預先載入資產</span><span class="sxs-lookup"><span data-stu-id="98d8a-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="98d8a-162">清除 Azure CDN 端點</span><span class="sxs-lookup"><span data-stu-id="98d8a-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="98d8a-163">針對傳回 404 狀態的 CDN 端點進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="98d8a-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
