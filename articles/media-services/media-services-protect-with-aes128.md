---
title: "aaaUsing aes-128 動態加密和金鑰傳遞服務 |Microsoft 文件"
description: "Microsoft Azure Media Services 可讓您 toodeliver 您使用 AES 128 位元加密金鑰加密的內容。 Media Services 也提供 hello 金鑰傳遞服務，可提供加密金鑰 tooauthorized 使用者。 本主題說明如何使用 AES 128 加密 toodynamically，及使用 hello 金鑰傳遞服務。"
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
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="3a191-105">使用 AES-128 動態加密和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="3a191-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a191-106">.NET</span><span class="sxs-lookup"><span data-stu-id="3a191-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="3a191-107">Java</span><span class="sxs-lookup"><span data-stu-id="3a191-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="3a191-108">PHP</span><span class="sxs-lookup"><span data-stu-id="3a191-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="3a191-109">概觀</span><span class="sxs-lookup"><span data-stu-id="3a191-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="3a191-110">請參閱[這](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption)視訊的方式 tooprotect 您的媒體內容的 AES 加密概觀。</span><span class="sxs-lookup"><span data-stu-id="3a191-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="3a191-111">Microsoft Azure Media Services 可讓您 toodeliver Http-即時的資料流 (HLS) 和 Smooth Streaming 透過進階加密標準 (AES) 加密 （使用 128 位元加密金鑰）。</span><span class="sxs-lookup"><span data-stu-id="3a191-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="3a191-112">Media Services 也提供 hello 金鑰傳遞服務，可提供加密金鑰 tooauthorized 使用者。</span><span class="sxs-lookup"><span data-stu-id="3a191-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="3a191-113">如果想要讓 Media Services tooencrypt 資產，您需要 tooassociate hello 資產的加密金鑰，也可以設定 hello 金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="3a191-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="3a191-114">Media Services 時，播放程式要求串流時，使用指定的 hello 金鑰 toodynamically 加密使用 AES 加密的內容。</span><span class="sxs-lookup"><span data-stu-id="3a191-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="3a191-115">toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。</span><span class="sxs-lookup"><span data-stu-id="3a191-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="3a191-116">toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。</span><span class="sxs-lookup"><span data-stu-id="3a191-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="3a191-117">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a191-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="3a191-118">hello 內容金鑰授權原則可能會有一或多個授權限制： 開啟或語彙基元限制。</span><span class="sxs-lookup"><span data-stu-id="3a191-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="3a191-119">hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="3a191-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="3a191-120">Media Services 支援語彙基元中 hello[簡單 Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)(SWT) 格式和[JSON Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)(JWT) 格式。</span><span class="sxs-lookup"><span data-stu-id="3a191-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="3a191-121">如需詳細資訊，請參閱[設定 hello 內容金鑰授權原則](media-services-protect-with-aes128.md#configure_key_auth_policy)。</span><span class="sxs-lookup"><span data-stu-id="3a191-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="3a191-122">tootake 利用動態加密，您需要 toohave 包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案的資產。</span><span class="sxs-lookup"><span data-stu-id="3a191-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="3a191-123">您也需要 tooconfigure hello 傳遞原則 （在本主題稍後所述） 的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="3a191-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="3a191-124">然後，根據 hello hello 串流 URL 中指定的格式，hello 隨選串流伺服器可確保您已選擇 hello 通訊協定傳遞該 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="3a191-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="3a191-125">如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="3a191-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3a191-126">本主題會在應用程式，以便將受保護的媒體運作的有用 toodevelopers。</span><span class="sxs-lookup"><span data-stu-id="3a191-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="3a191-127">hello 主題將說明如何 tooconfigure hello 與授權原則的金鑰傳遞服務，讓只有獲得授權的用戶端，可能會收到 hello 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a191-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="3a191-128">它也會示範如何 toouse 動態加密。</span><span class="sxs-lookup"><span data-stu-id="3a191-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="3a191-129">使用 AES-128 動態加密和金鑰傳遞服務工作流程</span><span class="sxs-lookup"><span data-stu-id="3a191-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="3a191-130">hello 下面是使用 AES 使用 hello Media Services 金鑰傳遞服務，並且使用動態加密資產的加密時，您會需要 tooperform 的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="3a191-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="3a191-131">[建立資產，並將檔案上傳到資產 hello](media-services-protect-with-aes128.md#create_asset)。</span><span class="sxs-lookup"><span data-stu-id="3a191-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="3a191-132">[包含 hello 檔案 toohello 彈性位元速率 MP4 集 hello 資產編碼](media-services-protect-with-aes128.md#encode_asset)。</span><span class="sxs-lookup"><span data-stu-id="3a191-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="3a191-133">[建立內容金鑰，並將它與 hello 編碼資產產生關聯](media-services-protect-with-aes128.md#create_contentkey)。</span><span class="sxs-lookup"><span data-stu-id="3a191-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="3a191-134">在 Media Services hello 內容金鑰包含 hello 資產的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a191-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="3a191-135">[設定 hello 內容金鑰授權原則](media-services-protect-with-aes128.md#configure_key_auth_policy)。</span><span class="sxs-lookup"><span data-stu-id="3a191-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="3a191-136">hello 內容金鑰授權原則必須由您設定並符合 hello 為了讓 hello 內容金鑰 toobe 傳遞的 toohello 用戶端的用戶端。</span><span class="sxs-lookup"><span data-stu-id="3a191-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="3a191-137">[設定資產的 hello 傳遞原則](media-services-protect-with-aes128.md#configure_asset_delivery_policy)。</span><span class="sxs-lookup"><span data-stu-id="3a191-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="3a191-138">hello 傳遞原則設定包括： 金鑰取得 URL 和初始化向量 (IV) (AES 128 時，必須的 hello 相同的 IV toobe 提供加密和解密），傳遞通訊協定 （例如，MPEG DASH、 HLS、 Smooth Streaming 或全部），hello 類型動態加密 （例如信封或非動態加密）。</span><span class="sxs-lookup"><span data-stu-id="3a191-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="3a191-139">您可以套用不同的原則 tooeach 通訊協定 hello 上相同的資產。</span><span class="sxs-lookup"><span data-stu-id="3a191-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="3a191-140">例如，您可以套用 PlayReady 加密 tooSmooth/DASH 和 AES 信封 tooHLS。</span><span class="sxs-lookup"><span data-stu-id="3a191-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="3a191-141">傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。</span><span class="sxs-lookup"><span data-stu-id="3a191-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="3a191-142">hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="3a191-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="3a191-143">然後，將允許 hello 清除所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3a191-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="3a191-144">[建立 OnDemand 定位器](media-services-protect-with-aes128.md#create_locator)中排序 tooget 串流 URL。</span><span class="sxs-lookup"><span data-stu-id="3a191-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="3a191-145">hello 主題也顯示[用戶端應用程式如何從 hello 金鑰傳遞服務要求金鑰](media-services-protect-with-aes128.md#client_request)。</span><span class="sxs-lookup"><span data-stu-id="3a191-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="3a191-146">您會發現完整.NET[範例](media-services-protect-with-aes128.md#example)hello hello 主題結尾處。</span><span class="sxs-lookup"><span data-stu-id="3a191-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="3a191-147">hello 下列影像示範上述的 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="3a191-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="3a191-148">本文 hello 語彙基元用來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3a191-148">Here hello token is used for authentication.</span></span>

![利用 AES 128 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="3a191-150">本主題的 hello 其餘提供詳細的說明、 程式碼範例，以及連結 tootopics 可為您示範如何 tooachieve hello 上面所述的工作。</span><span class="sxs-lookup"><span data-stu-id="3a191-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="3a191-151">目前的限制</span><span class="sxs-lookup"><span data-stu-id="3a191-151">Current limitations</span></span>
<span data-ttu-id="3a191-152">如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。</span><span class="sxs-lookup"><span data-stu-id="3a191-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="3a191-153"><a id="create_asset"></a>建立資產，並將檔案上傳到資產 hello</span><span class="sxs-lookup"><span data-stu-id="3a191-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="3a191-154">順序 toomanage 中編碼和串流您的視訊，您必須先將內容上傳到 Microsoft Azure Media Services。</span><span class="sxs-lookup"><span data-stu-id="3a191-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="3a191-155">上傳之後，您的內容會安全地儲存在 hello 雲端進行進一步處理和串流。</span><span class="sxs-lookup"><span data-stu-id="3a191-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="3a191-156">如需詳細資訊，請參閱 [上傳檔案到媒體服務帳戶](media-services-dotnet-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="3a191-157"><a id="encode_asset"></a>編碼 hello 資產包含 hello 檔案 toohello 彈性位元速率 MP4 集</span><span class="sxs-lookup"><span data-stu-id="3a191-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="3a191-158">使用動態加密您只需要為 toocreate 包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案的資產。</span><span class="sxs-lookup"><span data-stu-id="3a191-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="3a191-159">然後，hello hello 資訊清單中指定的格式為基礎或片段要求中 hello 隨選串流伺服器可確保您已選擇 hello 通訊協定接收 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="3a191-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="3a191-160">如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="3a191-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="3a191-161">如需詳細資訊，請參閱 hello[動態封裝概觀](media-services-dynamic-packaging-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="3a191-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="3a191-162">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a191-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3a191-163">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="3a191-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="3a191-164">此外，toobe 無法 toouse 動態封裝和動態加密您的資產必須包含一組彈性位元速率 mp4 或彈性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="3a191-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="3a191-165">如需有關指示 tooencode，請參閱[如何 tooencode 資產使用媒體編碼器標準](media-services-dotnet-encode-with-media-encoder-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="3a191-166"><a id="create_contentkey"></a>建立內容金鑰，並將它與 hello 編碼資產產生關聯</span><span class="sxs-lookup"><span data-stu-id="3a191-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="3a191-167">在 Media Services hello 內容金鑰包含您想 tooencrypt 資產的 hello 索引鍵使用。</span><span class="sxs-lookup"><span data-stu-id="3a191-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="3a191-168">如需詳細資訊，請參閱 [建立內容金鑰](media-services-dotnet-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="3a191-169"><a id="configure_key_auth_policy"></a>設定 hello 內容金鑰授權原則</span><span class="sxs-lookup"><span data-stu-id="3a191-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="3a191-170">媒體服務支援多種方式來驗證提出金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a191-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="3a191-171">hello 內容金鑰授權原則必須由您設定，並且符合 hello 用戶端 （播放器），才能傳遞 toohello 用戶端 hello 金鑰 toobe。</span><span class="sxs-lookup"><span data-stu-id="3a191-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="3a191-172">hello 內容金鑰授權原則可能會有一或多個授權限制： 開放、 權杖限制或 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="3a191-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="3a191-173">如需詳細資訊，請參閱 [設定內容金鑰授權原則](media-services-dotnet-configure-content-key-auth-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="3a191-174"><a id="configure_asset_delivery_policy"></a>設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="3a191-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="3a191-175">設定 hello 您資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="3a191-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="3a191-176">Hello 資產傳遞原則設定的一些事項包括：</span><span class="sxs-lookup"><span data-stu-id="3a191-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="3a191-177">hello 金鑰取得 URL。</span><span class="sxs-lookup"><span data-stu-id="3a191-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="3a191-178">hello hello 信封加密的初始化向量 (IV) toouse。</span><span class="sxs-lookup"><span data-stu-id="3a191-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="3a191-179">AES 128 時，必須加密和解密時，提供相同的 IV toobe hello。</span><span class="sxs-lookup"><span data-stu-id="3a191-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="3a191-180">hello 資產傳遞通訊協定 (例如，MPEG DASH、 HLS、 Smooth Streaming 或全部）。</span><span class="sxs-lookup"><span data-stu-id="3a191-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="3a191-181">hello 類型動態加密 （例如 AES 信封） 或非動態加密。</span><span class="sxs-lookup"><span data-stu-id="3a191-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="3a191-182">如需詳細資訊，請參閱 [設定資產傳遞原則 ](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="3a191-183"><a id="create_locator"></a>建立資料流中順序 tooget 串流 URL 定位器 OnDemand</span><span class="sxs-lookup"><span data-stu-id="3a191-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="3a191-184">您將需要 tooprovide 您的使用者，以 hello URL Smooth、 DASH 或 HLS 資料流。</span><span class="sxs-lookup"><span data-stu-id="3a191-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="3a191-185">如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。</span><span class="sxs-lookup"><span data-stu-id="3a191-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="3a191-186">如需有關如何 toopublish 資產和建置串流 URL，請參閱指示[建置串流 URL](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="3a191-187">取得測試權杖</span><span class="sxs-lookup"><span data-stu-id="3a191-187">Get a test token</span></span>
<span data-ttu-id="3a191-188">取得測試權杖根據 hello 用於 hello 金鑰授權原則的權杖限制。</span><span class="sxs-lookup"><span data-stu-id="3a191-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="3a191-189">您可以使用 hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest 您的資料流。</span><span class="sxs-lookup"><span data-stu-id="3a191-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="3a191-190"><a id="client_request"></a>您如何的用戶端要求的索引鍵從 hello 金鑰傳遞服務？</span><span class="sxs-lookup"><span data-stu-id="3a191-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="3a191-191">在 hello 先前步驟中，您可以建構 hello URL 指向 tooa 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="3a191-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="3a191-192">您的用戶端必須從串流資訊清單檔案順序 toomake 要求 toohello 金鑰傳遞服務中的 hello tooextract hello 必要資訊。</span><span class="sxs-lookup"><span data-stu-id="3a191-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="3a191-193">資訊清單檔案</span><span class="sxs-lookup"><span data-stu-id="3a191-193">Manifest files</span></span>
<span data-ttu-id="3a191-194">hello 用戶端必須 tooextract hello URL （其中也包含內容金鑰識別碼 (kid)） 從 hello 資訊清單檔案的值。</span><span class="sxs-lookup"><span data-stu-id="3a191-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="3a191-195">hello 用戶端將再重試 hello 金鑰傳遞服務 tooget hello 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a191-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="3a191-196">hello 用戶端也必須 tooextract hello IV 值，並使用它執行解密 hello stream.hello 下列程式碼片段顯示 hello <Protection> hello Smooth Streaming 資訊清單的項目。</span><span class="sxs-lookup"><span data-stu-id="3a191-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

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

<span data-ttu-id="3a191-197">在 HLS 的 hello 情況下，hello 根資訊清單會分成區段檔案。</span><span class="sxs-lookup"><span data-stu-id="3a191-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="3a191-198">例如，hello 根資訊清單是： http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) 和它包含區段檔案名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="3a191-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="3a191-199">如果您在文字編輯器 (例如，http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should 中，開啟其中一個 hello 區段檔案包含 #EXT X-索引鍵表示該 hello 檔案已加密。</span><span class="sxs-lookup"><span data-stu-id="3a191-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

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
><span data-ttu-id="3a191-200">如果您計劃 tooplay AES 加密 HLS Safari 中的，請參閱[這篇部落格](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)。</span><span class="sxs-lookup"><span data-stu-id="3a191-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="3a191-201">要求從 hello 金鑰傳遞服務的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="3a191-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="3a191-202">hello 下列程式碼會示範如何 toosend 要求 toohello Media Services 金鑰傳遞服務使用金鑰傳遞 Uri （也就擷取自 hello 資訊清單） 和語彙基元 （本主題不討論關於如何 tooget 簡單 Web 權杖從安全權杖服務）。</span><span class="sxs-lookup"><span data-stu-id="3a191-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

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

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="3a191-203">使用 .NET 透過 AES-128 保護內容</span><span class="sxs-lookup"><span data-stu-id="3a191-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3a191-204">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="3a191-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="3a191-205">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="3a191-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="3a191-206">新增下列項目太 hello**appSettings** app.config 檔案中所定義：</span><span class="sxs-lookup"><span data-stu-id="3a191-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="3a191-207"><a id="example"></a>範例</span><span class="sxs-lookup"><span data-stu-id="3a191-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="3a191-208">Hello 本節中所顯示的程式碼來覆寫您 Program.cs 檔案中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3a191-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="3a191-209">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="3a191-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="3a191-210">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="3a191-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="3a191-211">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="3a191-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="3a191-212">請確定 tooupdate 變數 toopoint toofolders 輸入的檔案的所在位置。</span><span class="sxs-lookup"><span data-stu-id="3a191-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
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
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
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

            // Associate hello key with hello asset.
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

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
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

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

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

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file. 
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="3a191-213">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3a191-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3a191-214">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3a191-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

