---
title: "aaaManage 串流端點，其中包含 hello Azure 入口網站 |Microsoft 文件"
description: "本主題說明如何 toomanage 串流端點，其中包含 hello Azure 入口網站。"
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="eb2e6-103">管理以 hello Azure 入口網站的串流端點</span><span class="sxs-lookup"><span data-stu-id="eb2e6-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="eb2e6-104">本主題說明如何 toouse hello Azure 入口網站 toomanage 串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="eb2e6-105">請確定 tooreview hello[概觀](media-services-streaming-endpoints-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="eb2e6-106">如需如何 tooscale hello 串流端點資訊，請參閱[這](media-services-portal-scale-streaming-endpoints.md)主題。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="eb2e6-107">開始管理串流端點</span><span class="sxs-lookup"><span data-stu-id="eb2e6-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="eb2e6-108">管理您的帳戶，串流端點 toostart hello 遵循。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="eb2e6-109">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="eb2e6-110">在 hello**設定**刀鋒視窗中，選取**串流端點**。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="eb2e6-112">只有當串流端點處於執行中狀態時，才會向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="eb2e6-113">新增/移除串流端點</span><span class="sxs-lookup"><span data-stu-id="eb2e6-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="eb2e6-114">無法刪除 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="eb2e6-115">tooadd/刪除串流端點使用 hello Azure 入口網站中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="eb2e6-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="eb2e6-116">tooadd 串流端點中，按一下 hello **+ 端點**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="eb2e6-117">您可能會想多個串流端點，如果您計劃 toohave 不同 Cdn 或 CDN 和直接存取。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="eb2e6-118">toodelete 串流端點，請按**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="eb2e6-119">按一下 hello**啟動**按鈕 toostart hello 串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="eb2e6-121"><a id="configure_streaming_endpoints"></a>設定 hello 串流端點</span><span class="sxs-lookup"><span data-stu-id="eb2e6-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="eb2e6-122">串流端點可讓您 tooconfigure hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="eb2e6-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="eb2e6-123">存取控制</span><span class="sxs-lookup"><span data-stu-id="eb2e6-123">Access control</span></span>
* <span data-ttu-id="eb2e6-124">快取控制</span><span class="sxs-lookup"><span data-stu-id="eb2e6-124">Cache control</span></span>
* <span data-ttu-id="eb2e6-125">跨站台存取原則</span><span class="sxs-lookup"><span data-stu-id="eb2e6-125">Cross site access policies</span></span>

<span data-ttu-id="eb2e6-126">如需這些屬性的詳細資訊，請參閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="eb2e6-127">您可以設定串流端點，藉由下列 hello:</span><span class="sxs-lookup"><span data-stu-id="eb2e6-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="eb2e6-128">選取串流端點想 tooconfigure hello。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="eb2e6-129">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-129">Click **Settings**.</span></span>

<span data-ttu-id="eb2e6-130">遵循 hello 欄位的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-130">A brief description of hello fields follows.</span></span>

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="eb2e6-132">最大快取原則： 使用的 tooconfigure 資產的快取生命週期服務透過此串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="eb2e6-133">如果未不設定任何值，則會使用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="eb2e6-134">hello 預設值也可以直接在 Azure 儲存體中定義。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="eb2e6-135">Hello 串流端點啟用 Azure CDN，如果您不應將 hello 快取原則值 tooless 比 600 秒。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="eb2e6-136">允許的 IP 位址： 使用 toospecify tooconnect toohello 發佈串流端點允許的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="eb2e6-137">如果沒有指定的 IP 位址，任何 IP 位址是無法 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="eb2e6-138">IP 位址可以指定為單一 IP 位址 (例如 ‘10.0.0.1’)、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1/22’)，或是使用 IP 位址和小數點十進位子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1(255.255.255.0)’)。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="eb2e6-139">Akamai 簽章標頭驗證設定： 使用的 toospecify 設定來自 Akamai 伺服器的簽章標頭驗證要求的方式。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="eb2e6-140">到期時間的格式為 UTC。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="eb2e6-141">調整您的進階串流端點</span><span class="sxs-lookup"><span data-stu-id="eb2e6-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="eb2e6-142">如需詳細資訊，請參閱 [這個](media-services-portal-scale-streaming-endpoints.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="eb2e6-143"><a id="enable_cdn"></a>啟用 Azure CDN 整合</span><span class="sxs-lookup"><span data-stu-id="eb2e6-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="eb2e6-144">當您建立新的帳戶時，依預設會啟用預設串流端點 Azure CDN 整合。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="eb2e6-145">如果您稍後想 toodisable/啟用 hello CDN，您的串流端點必須在 hello**停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="eb2e6-146">可能需要跨所有 hello CDN 快顯 hello Azure CDN 整合 tooget 啟用和使用中的 hello 變更 toobe too2 小時。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="eb2e6-147">不過，您可以從串流端點的 hello 啟動串流端點和且不被中斷的資料流和 hello 整合完成之後，直接從 hello CDN 傳送嗨資料流。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="eb2e6-148">在佈建期間 hello 期間您的串流端點將處於**啟動**狀態，而且您可能會發現 degredad 效能。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="eb2e6-149">所有 hello Azure 資料中心 execpt 中國和美國聯邦公文區域中，會啟用 CDN 整合。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="eb2e6-150">一旦啟用後，hello**存取控制**，**自訂主機名稱**和**Akamai 簽章驗證**組態取得停用。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="eb2e6-151">如果是標準串流端點，Azure 媒體服務與 Azure CDN 的整合是在**來自 Verizon 的 Azure CDN** 上實作。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="eb2e6-152">您可以使用所有 **Azure CDN 定價層和提供者**來設定進階串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="eb2e6-153">如需有關 Azure CDN 功能的詳細資訊，請參閱 hello [CDN 概觀](../cdn/cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="eb2e6-154">其他考量</span><span class="sxs-lookup"><span data-stu-id="eb2e6-154">Additional considerations</span></span>

* <span data-ttu-id="eb2e6-155">為串流端點啟用 CDN 時，用戶端無法直接從 hello 原始要求內容。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="eb2e6-156">如果您需要 hello 能力 tootest 您不論 CDN 的內容，您可以建立另一個未啟用 CDN 的串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="eb2e6-157">您的串流端點主機名稱維持 hello 相同啟用 CDN 之後。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="eb2e6-158">啟用 CDN 之後您不需要指定 toomake 任何變更 tooyour 媒體服務工作流程。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="eb2e6-159">例如，如果您的串流端點主機名稱是 strasbourg.streaming.mediaservices.windows.net，啟用 CDN 之後，會使用 hello 完全相同的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="eb2e6-160">針對新的資料流端點，您可以啟用 CDN 只是藉由建立新的端點。針對現有的資料流端點，您需要 toofirst 停止 hello 端點，然後啟用/停用 hello CDN。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="eb2e6-161">只有透過 Azure 管理入口網站使用 **Verizon 標準 CDN 提供者**，才能設定標準串流端點。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="eb2e6-162">不過，您可以使用 REST API 來啟用其他 Azure CDN 提供者。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="eb2e6-163">設定 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="eb2e6-163">Configure CDN profile</span></span>

<span data-ttu-id="eb2e6-164">您可以設定 hello 的 CDN 設定檔選取 hello**管理 CDN**從 hello 上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="eb2e6-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb2e6-166">Next steps</span></span>
<span data-ttu-id="eb2e6-167">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="eb2e6-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="eb2e6-168">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="eb2e6-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

