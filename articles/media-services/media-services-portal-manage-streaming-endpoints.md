---
title: "透過 Azure 入口網站管理串流端點 | Microsoft Docs"
description: "本主題說明如何透過 Azure 入口網站管理串流端點。"
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
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="b628f-103">透過 Azure 入口網站管理串流端點</span><span class="sxs-lookup"><span data-stu-id="b628f-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="b628f-104">本主題說明如何使用 Azure 入口網站來管理串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="b628f-105">務必檢閱[概觀](media-services-streaming-endpoints-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="b628f-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="b628f-106">如需調整串流端點的相關資訊，請參閱 [這個](media-services-portal-scale-streaming-endpoints.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="b628f-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="b628f-107">開始管理串流端點</span><span class="sxs-lookup"><span data-stu-id="b628f-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="b628f-108">若要開始管理您帳戶的串流端點，請執行下列作業。</span><span class="sxs-lookup"><span data-stu-id="b628f-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="b628f-109">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="b628f-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b628f-110">在 [設定] 刀鋒視窗中，選取 [串流端點]。</span><span class="sxs-lookup"><span data-stu-id="b628f-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="b628f-112">只有當串流端點處於執行中狀態時，才會向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="b628f-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="b628f-113">新增/移除串流端點</span><span class="sxs-lookup"><span data-stu-id="b628f-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="b628f-114">預設串流端點不可刪除。</span><span class="sxs-lookup"><span data-stu-id="b628f-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="b628f-115">若要使用 Azure 入口網站來新增或移除串流端點，以執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="b628f-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="b628f-116">若要新增串流端點，請按一下頁面頂端的 [+端點]  。</span><span class="sxs-lookup"><span data-stu-id="b628f-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="b628f-117">如果您打算有不同的 CDN 或一個 CDN 和直接存取，您可能需要有多個串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="b628f-118">若要刪除串流端點，請按下 [刪除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b628f-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="b628f-119">按一下 [啟動]  按鈕以啟動串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="b628f-121"><a id="configure_streaming_endpoints"></a>設定串流端點</span><span class="sxs-lookup"><span data-stu-id="b628f-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="b628f-122">串流端點可讓您設定下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b628f-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="b628f-123">存取控制</span><span class="sxs-lookup"><span data-stu-id="b628f-123">Access control</span></span>
* <span data-ttu-id="b628f-124">快取控制</span><span class="sxs-lookup"><span data-stu-id="b628f-124">Cache control</span></span>
* <span data-ttu-id="b628f-125">跨站台存取原則</span><span class="sxs-lookup"><span data-stu-id="b628f-125">Cross site access policies</span></span>

<span data-ttu-id="b628f-126">如需這些屬性的詳細資訊，請參閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。</span><span class="sxs-lookup"><span data-stu-id="b628f-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="b628f-127">若要設定串流端點，請執行以下作業：</span><span class="sxs-lookup"><span data-stu-id="b628f-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="b628f-128">選取您想要設定的串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="b628f-129">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="b628f-129">Click **Settings**.</span></span>

<span data-ttu-id="b628f-130">隨時顯示簡要的欄位說明。</span><span class="sxs-lookup"><span data-stu-id="b628f-130">A brief description of the fields follows.</span></span>

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="b628f-132">最大快取原則：用來設定透過此串流端點所提供的資源快取存留期。</span><span class="sxs-lookup"><span data-stu-id="b628f-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="b628f-133">如果沒有設定任何值，則會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="b628f-133">If no value is set, the default is used.</span></span> <span data-ttu-id="b628f-134">預設值也可以直接在 Azure 儲存體中定義。</span><span class="sxs-lookup"><span data-stu-id="b628f-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="b628f-135">如果 Azure CDN 已針對串流端點啟用，您便不應該將快取原則值設定成少於 600 秒。</span><span class="sxs-lookup"><span data-stu-id="b628f-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="b628f-136">允許的 IP 位址：用來指定能夠連接到已發佈之串流端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b628f-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="b628f-137">若未指定 IP 位址，則任何 IP 位址都可連接。</span><span class="sxs-lookup"><span data-stu-id="b628f-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="b628f-138">IP 位址可以指定為單一 IP 位址 (例如 ‘10.0.0.1’)、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1/22’)，或是使用 IP 位址和小數點十進位子網路遮罩的 IP 範圍 (例如 ‘10.0.0.1(255.255.255.0)’)。</span><span class="sxs-lookup"><span data-stu-id="b628f-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="b628f-139">針對 Akamai 簽章標頭驗證的設定：用來指定來自 Akamai 伺服器的簽章標頭驗證的設定方式。</span><span class="sxs-lookup"><span data-stu-id="b628f-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="b628f-140">到期時間的格式為 UTC。</span><span class="sxs-lookup"><span data-stu-id="b628f-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="b628f-141">調整您的進階串流端點</span><span class="sxs-lookup"><span data-stu-id="b628f-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="b628f-142">如需詳細資訊，請參閱 [這個](media-services-portal-scale-streaming-endpoints.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="b628f-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="b628f-143"><a id="enable_cdn"></a>啟用 Azure CDN 整合</span><span class="sxs-lookup"><span data-stu-id="b628f-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="b628f-144">當您建立新的帳戶時，依預設會啟用預設串流端點 Azure CDN 整合。</span><span class="sxs-lookup"><span data-stu-id="b628f-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="b628f-145">如果您稍後想要停用/啟用 CDN，串流端點必須處於**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="b628f-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="b628f-146">可能需要將近 2 小時，Azure CDN 整合才會啟用，變更也才會遍及所有 CDN POP。</span><span class="sxs-lookup"><span data-stu-id="b628f-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="b628f-147">不過，您可以啟動串流端點，並從串流端點不停地串流，等到整合完成後，將會從 CDN 傳送資料流。</span><span class="sxs-lookup"><span data-stu-id="b628f-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="b628f-148">在佈建期間，串流端點會處於**啟動中**狀態，您可能會發現效能下降。</span><span class="sxs-lookup"><span data-stu-id="b628f-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="b628f-149">中國和聯邦政府區域除外，其他所有 Azure 資料中心都啟用 CDN 整合。</span><span class="sxs-lookup"><span data-stu-id="b628f-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="b628f-150">啟用後，**存取控制**、**自訂主機名稱**和 **Akamai 簽章驗證**設定就會停用。</span><span class="sxs-lookup"><span data-stu-id="b628f-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="b628f-151">如果是標準串流端點，Azure 媒體服務與 Azure CDN 的整合是在**來自 Verizon 的 Azure CDN** 上實作。</span><span class="sxs-lookup"><span data-stu-id="b628f-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="b628f-152">您可以使用所有 **Azure CDN 定價層和提供者**來設定進階串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="b628f-153">如需 Azure CDN 功能的詳細資訊，請參閱 [CDN 概觀](../cdn/cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b628f-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="b628f-154">其他考量</span><span class="sxs-lookup"><span data-stu-id="b628f-154">Additional considerations</span></span>

* <span data-ttu-id="b628f-155">對串流端點啟用 CDN 時，用戶端無法直接從來源要求內容。</span><span class="sxs-lookup"><span data-stu-id="b628f-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="b628f-156">如果您需要在具有 CDN 或不具有 CDN 的情況下測試您內容的能力，您可以建立另一個未啟用 CDN 的串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="b628f-157">您的串流端點主機名稱在啟用 CDN 之後維持不變。</span><span class="sxs-lookup"><span data-stu-id="b628f-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="b628f-158">您在啟用 CDN 之後不需要對您的媒體服務工作流程進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="b628f-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="b628f-159">例如，如果您的串流端點主機名稱是 strasbourg.streaming.mediaservices.windows.net，則在啟用 CDN 之後，會使用完全相同的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b628f-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="b628f-160">對於新的串流端點，只要建立新的端點就會啟用 CDN；對於現有的串流端點，您必須先停止端點，然後啟用/停用 CDN。</span><span class="sxs-lookup"><span data-stu-id="b628f-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="b628f-161">只有透過 Azure 管理入口網站使用 **Verizon 標準 CDN 提供者**，才能設定標準串流端點。</span><span class="sxs-lookup"><span data-stu-id="b628f-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="b628f-162">不過，您可以使用 REST API 來啟用其他 Azure CDN 提供者。</span><span class="sxs-lookup"><span data-stu-id="b628f-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="b628f-163">設定 CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="b628f-163">Configure CDN profile</span></span>

<span data-ttu-id="b628f-164">您可以選取頂端的 [管理 CDN] 按鈕來設定 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b628f-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![串流端點](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="b628f-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b628f-166">Next steps</span></span>
<span data-ttu-id="b628f-167">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="b628f-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b628f-168">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="b628f-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

