---
title: "使用 AES-128 動態加密和金鑰傳遞服務 | Microsoft Docs"
description: "Microsoft Azure 媒體服務可讓您傳遞您使用 128 位元加密金鑰加密的內容。 媒體服務也提供加密金鑰傳遞服務，將加密金鑰傳遞至授權的使用者。 本主題展示如何利用 AES-128 動態加密，以及使用金鑰傳遞服務。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="2edf0-105">使用 AES-128 動態加密和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="2edf0-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2edf0-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2edf0-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="2edf0-107">Java</span><span class="sxs-lookup"><span data-stu-id="2edf0-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2edf0-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2edf0-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2edf0-109">概觀</span><span class="sxs-lookup"><span data-stu-id="2edf0-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="2edf0-110">如需如何使用 AES 加密保護媒體內容的概觀，請參閱[此視訊](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="2edf0-111">Microsoft Azure 媒體服務可讓您傳遞您使用進階加密標準 (AES) (使用 128 位元加密金鑰) 加密的 Http-Live-Streaming (HLS) 和 Smooth Streaming 。</span><span class="sxs-lookup"><span data-stu-id="2edf0-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="2edf0-112">媒體服務也提供加密金鑰傳遞服務，將加密金鑰傳遞至授權的使用者。</span><span class="sxs-lookup"><span data-stu-id="2edf0-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="2edf0-113">如果您想要媒體服務加密資產，則需要建立加密金鑰 與資產的關聯，同時設定金鑰的授權原則。</span><span class="sxs-lookup"><span data-stu-id="2edf0-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="2edf0-114">播放程式要求串流時，媒體服務便會使用 AES 加密，使用指定的金鑰動態加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="2edf0-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="2edf0-115">為了將串流解密，播放程式將從金鑰傳遞服務要求金鑰。</span><span class="sxs-lookup"><span data-stu-id="2edf0-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="2edf0-116">為了決定使用者是否有權取得金鑰，服務會評估為金鑰指定的授權原則。</span><span class="sxs-lookup"><span data-stu-id="2edf0-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="2edf0-117">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="2edf0-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="2edf0-118">內容金鑰授權原則可能會有一個或多個授權限制：open 或 token 限制。</span><span class="sxs-lookup"><span data-stu-id="2edf0-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="2edf0-119">權杖限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="2edf0-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="2edf0-120">媒體服務支援[簡單 Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) 格式和 [JSON Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="2edf0-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="2edf0-121">如需詳細資訊，請參閱 [設定內容金鑰的授權原則](media-services-protect-with-aes128.md#configure_key_auth_policy)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="2edf0-122">若要利用動態加密，您需有一個資源，其中包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="2edf0-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2edf0-123">您也需要設定資產的傳遞原則 (本主題稍後會加以描述)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="2edf0-124">然後，根據串流 URL 中指定的格式，隨選資料流處理伺服器將確保以您所選擇的通訊協定傳遞串流。</span><span class="sxs-lookup"><span data-stu-id="2edf0-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="2edf0-125">因此，您只需要儲存及支付一種儲存格式之檔案的費用，媒體服務會根據用戶端的要求建置及提供適當的回應。</span><span class="sxs-lookup"><span data-stu-id="2edf0-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="2edf0-126">本主題將有助於開發人員開發提供受保護媒體的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2edf0-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="2edf0-127">本主題將展示如何利用授權原則設定金鑰傳遞服務，這樣只有授權的用戶端才會收到加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2edf0-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="2edf0-128">它也會展示如何使用動態加密。</span><span class="sxs-lookup"><span data-stu-id="2edf0-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="2edf0-129">使用 AES-128 動態加密和金鑰傳遞服務工作流程</span><span class="sxs-lookup"><span data-stu-id="2edf0-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="2edf0-130">以下是您利用 AES 加密資產、使用媒體服務金鑰傳遞服務，同時也使用動態加密時將需要執行的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="2edf0-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="2edf0-131">[建立資產並將檔案上傳到資產](media-services-protect-with-aes128.md#create_asset)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="2edf0-132">[將包含檔案的資產編碼為自適性位元速率 MP4 集](media-services-protect-with-aes128.md#encode_asset)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="2edf0-133">[建立內容金鑰，並將它與編碼的資產產生關聯](media-services-protect-with-aes128.md#create_contentkey)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="2edf0-134">在媒體服務中，內容金鑰包含資產的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2edf0-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="2edf0-135">[設定內容金鑰的授權原則](media-services-protect-with-aes128.md#configure_key_auth_policy)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="2edf0-136">內容金鑰授權原則必須由您設定，而且用戶端必須符合條件，才能將內容金鑰傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="2edf0-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="2edf0-137">[設定資產的傳遞原則](media-services-protect-with-aes128.md#configure_asset_delivery_policy)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="2edf0-138">傳遞原則組態包括：主要取得 URL 和初始化向量 (IV) (AES 128 會在加密和解密時要求提供相同的 IV)、傳送通訊協定 (例如，MPEG DASH、HLS、Smooth Streaming 或全部)、動態加密的類型 (例如，信封或沒有動態加密)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="2edf0-139">您可以將不同的原則套用至相同資產上的每一個通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2edf0-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="2edf0-140">例如，您可以將 PlayReady 加密套用到 Smooth/DASH，以及將 AES 信封加密套用到 HLS。</span><span class="sxs-lookup"><span data-stu-id="2edf0-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="2edf0-141">傳遞原則中未定義的任何通訊協定 (例如，您加入單一原則，它只有指定 HLS 做為通訊協定) 將會遭到封鎖無法串流。</span><span class="sxs-lookup"><span data-stu-id="2edf0-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="2edf0-142">這個狀況的例外情形是您完全沒有定義資產傳遞原則之時。</span><span class="sxs-lookup"><span data-stu-id="2edf0-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="2edf0-143">那麼，將允許所有通訊協定，不受阻礙。</span><span class="sxs-lookup"><span data-stu-id="2edf0-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="2edf0-144">[建立隨選定位器](media-services-protect-with-aes128.md#create_locator) 。</span><span class="sxs-lookup"><span data-stu-id="2edf0-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="2edf0-145">本主題也說明 [用戶端應用程式如何從金鑰傳遞服務要求金鑰](media-services-protect-with-aes128.md#client_request)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="2edf0-146">您會在本主題結尾處發現完整的.NET [範例](media-services-protect-with-aes128.md#example) 。</span><span class="sxs-lookup"><span data-stu-id="2edf0-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="2edf0-147">下圖示範上述的工作流程。</span><span class="sxs-lookup"><span data-stu-id="2edf0-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="2edf0-148">這裡的權杖用於驗證。</span><span class="sxs-lookup"><span data-stu-id="2edf0-148">Here the token is used for authentication.</span></span>

![利用 AES 128 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="2edf0-150">本主題的其餘部分會提供詳細的說明、程式碼範例，以及展示如何達成上述工作之主題的連結。</span><span class="sxs-lookup"><span data-stu-id="2edf0-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="2edf0-151">目前的限制</span><span class="sxs-lookup"><span data-stu-id="2edf0-151">Current limitations</span></span>
<span data-ttu-id="2edf0-152">如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。</span><span class="sxs-lookup"><span data-stu-id="2edf0-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="2edf0-153"><a id="create_asset"></a>建立資產並將檔案上傳到資產</span><span class="sxs-lookup"><span data-stu-id="2edf0-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="2edf0-154">為了管理、編碼及串流處理您的視訊，您必須先將內容上傳到 Microsoft Azure 媒體服務。</span><span class="sxs-lookup"><span data-stu-id="2edf0-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="2edf0-155">一旦上傳，您的內容就會安全地儲存在雲端，以進一步進行處理和串流處理。</span><span class="sxs-lookup"><span data-stu-id="2edf0-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="2edf0-156">如需詳細資訊，請參閱 [上傳檔案到媒體服務帳戶](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="2edf0-157"><a id="encode_asset"></a>將包含檔案的資產編碼為自適性位元速率 MP4 集</span><span class="sxs-lookup"><span data-stu-id="2edf0-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="2edf0-158">使用動態加密時，您只需建立一個資源，其中包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="2edf0-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2edf0-159">然後隨選資料流處理伺服器會根據資訊清單或片段要求中的指定格式，確保您以自己選擇的通訊協定接收串流。</span><span class="sxs-lookup"><span data-stu-id="2edf0-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="2edf0-160">因此，您只需要儲存及支付一種儲存格式之檔案的費用，媒體服務會根據用戶端的要求建置及提供適當的回應。</span><span class="sxs-lookup"><span data-stu-id="2edf0-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="2edf0-161">如需詳細資訊，請參閱 [動態封裝概觀](media-services-dynamic-packaging-overview.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="2edf0-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="2edf0-162">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2edf0-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="2edf0-163">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="2edf0-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="2edf0-164">此外，為了能夠使用動態封裝和動態加密功能，您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="2edf0-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="2edf0-165">如需如何編碼的指示，請參閱 [如何使用 Media Encoder Standard 為資產編碼](media-services-dotnet-encode-with-media-encoder-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="2edf0-166"><a id="create_contentkey"></a>建立內容金鑰並將它與編碼的資產產生關聯</span><span class="sxs-lookup"><span data-stu-id="2edf0-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="2edf0-167">在媒體服務中，內容金鑰包含您要加密資產時使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2edf0-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="2edf0-168">如需詳細資訊，請參閱 [建立內容金鑰](media-services-dotnet-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="2edf0-169"><a id="configure_key_auth_policy"></a>設定內容金鑰的授權原則</span><span class="sxs-lookup"><span data-stu-id="2edf0-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="2edf0-170">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="2edf0-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="2edf0-171">內容金鑰授權原則必須由您設定，而且用戶端 (播放器) 必須符合條件，才能將金鑰傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="2edf0-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="2edf0-172">內容金鑰授權原則可能會有一個或多個授權限制：Open、權杖限制或 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="2edf0-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="2edf0-173">如需詳細資訊，請參閱 [設定內容金鑰授權原則](media-services-dotnet-configure-content-key-auth-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="2edf0-174"><a id="configure_asset_delivery_policy"></a>設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="2edf0-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="2edf0-175">設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="2edf0-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="2edf0-176">資產傳遞原則組態包括：</span><span class="sxs-lookup"><span data-stu-id="2edf0-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="2edf0-177">金鑰取得 URL。</span><span class="sxs-lookup"><span data-stu-id="2edf0-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="2edf0-178">用於信封加密的初始化向量 (IV)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="2edf0-179">AES 128 會在加密和解密時要求提供相同的 IV。</span><span class="sxs-lookup"><span data-stu-id="2edf0-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="2edf0-180">資產傳遞通訊協定 (例如，MPEG DASH、HLS、Smooth Streaming 或全部)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="2edf0-181">動態加密的類型 (例如，AES 信封) 或沒有動態加密。</span><span class="sxs-lookup"><span data-stu-id="2edf0-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="2edf0-182">如需詳細資訊，請參閱 [設定資產傳遞原則 ](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="2edf0-183"><a id="create_locator"></a>建立隨選串流定位器以取得串流 URL</span><span class="sxs-lookup"><span data-stu-id="2edf0-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="2edf0-184">您必須為您的使用者提供 Smooth、DASH 或 HLS 的串流 URL。</span><span class="sxs-lookup"><span data-stu-id="2edf0-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="2edf0-185">如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。</span><span class="sxs-lookup"><span data-stu-id="2edf0-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="2edf0-186">如需有關如何發佈資產，並建置串流 URL 的指示，請參閱 [建置串流 URL](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="2edf0-187">取得測試權杖</span><span class="sxs-lookup"><span data-stu-id="2edf0-187">Get a test token</span></span>
<span data-ttu-id="2edf0-188">根據用於金鑰授權原則的權杖限制取得測試權杖。</span><span class="sxs-lookup"><span data-stu-id="2edf0-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="2edf0-189">您可以使用 [AMS 播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 來測試您的串流。</span><span class="sxs-lookup"><span data-stu-id="2edf0-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="2edf0-190"><a id="client_request"></a>您的用戶端如何從金鑰傳遞服務要求金鑰？</span><span class="sxs-lookup"><span data-stu-id="2edf0-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="2edf0-191">在上一個步驟中，您可以建構指向資訊清單檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="2edf0-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="2edf0-192">您的用戶端必須從串流資訊清單檔案擷取所需的資訊，才能向金鑰傳遞服務提出要求。</span><span class="sxs-lookup"><span data-stu-id="2edf0-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="2edf0-193">資訊清單檔案</span><span class="sxs-lookup"><span data-stu-id="2edf0-193">Manifest files</span></span>
<span data-ttu-id="2edf0-194">用戶端必須從資訊清單檔案擷取 URL (其中也包含內容金鑰識別碼 (kid)) 值。</span><span class="sxs-lookup"><span data-stu-id="2edf0-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="2edf0-195">用戶端接著會嘗試從金鑰傳遞服務取得加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2edf0-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="2edf0-196">用戶端也必須擷取 IV 值，並使用它解密串流。下列程式碼片段展示 Smooth Streaming 資訊清單的 <Protection> 項目。</span><span class="sxs-lookup"><span data-stu-id="2edf0-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="2edf0-197">在 HLS 的案例中，根資訊清單會分成區段檔案。</span><span class="sxs-lookup"><span data-stu-id="2edf0-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="2edf0-198">例如，根資訊清單是︰http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl)，其中包含區段檔案名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="2edf0-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="2edf0-199">如果您在文字編輯器中開啟其中一個區段檔案 (例如，http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl)，它應該包含表示檔案已加密的 #EXT-X-KEY。</span><span class="sxs-lookup"><span data-stu-id="2edf0-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="2edf0-200">如果您想要在 Safari 中播放 AES 加密的 HLS，請參閱[這篇部落格](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)。</span><span class="sxs-lookup"><span data-stu-id="2edf0-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="2edf0-201">從金鑰傳遞服務要求金鑰</span><span class="sxs-lookup"><span data-stu-id="2edf0-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="2edf0-202">下列程式碼展示如何使用金鑰傳遞 Uri (擷取自資訊清單) 和權杖 (本主題不會討論如何從安全性權杖服務取得簡單 Web 權杖)，將要求傳送至媒體服務金鑰傳遞服務。</span><span class="sxs-lookup"><span data-stu-id="2edf0-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="2edf0-203">使用 .NET 透過 AES-128 保護內容</span><span class="sxs-lookup"><span data-stu-id="2edf0-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2edf0-204">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="2edf0-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="2edf0-205">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="2edf0-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="2edf0-206">將下列項目新增至 app.config 檔案中定義的 **appSettings**：</span><span class="sxs-lookup"><span data-stu-id="2edf0-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="2edf0-207"><a id="example"></a>範例</span><span class="sxs-lookup"><span data-stu-id="2edf0-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="2edf0-208">以本章節中所顯示的程式碼覆寫 Program.cs 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2edf0-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="2edf0-209">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="2edf0-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2edf0-210">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="2edf0-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2edf0-211">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="2edf0-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="2edf0-212">請務必更新變數，以指向您的輸入檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2edf0-212">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file. 
            return originLocator.Path + assetFile.Name;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="2edf0-213">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="2edf0-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2edf0-214">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2edf0-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

