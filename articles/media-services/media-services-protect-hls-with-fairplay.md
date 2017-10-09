---
title: "使用 Microsoft PlayReady 或 Apple FairPlay-Azure 的 aaaProtect HLS 內容 |Microsoft 文件"
description: "本主題提供概觀，並顯示如何 toouse Azure Media Services toodynamically 加密 Apple FairPlay HTTP Live Streaming (HLS) 內容。 它也會示範如何 toouse hello Media Services 授權傳遞服務 toodeliver FairPlay 授權 tooclients。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="be868-104">使用 Apple FairPlay 或 Microsoft PlayReady 保護 HLS 內容</span><span class="sxs-lookup"><span data-stu-id="be868-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="be868-105">Azure 媒體服務可讓您 toodynamically 加密使用下列格式的 hello HTTP Live Streaming (HLS) 的內容：</span><span class="sxs-lookup"><span data-stu-id="be868-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="be868-106">**AES-128 信封清除金鑰**</span><span class="sxs-lookup"><span data-stu-id="be868-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="be868-107">hello 整個區塊會使用加密 hello **AES 128 CBC**模式。</span><span class="sxs-lookup"><span data-stu-id="be868-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="be868-108">hello 解密 hello 資料流的原生支援的 iOS 和 OS X 播放程式。</span><span class="sxs-lookup"><span data-stu-id="be868-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="be868-109">如需詳細資訊，請參閱[使用 AES-128 動態加密和金鑰傳遞服務](media-services-protect-with-aes128.md)。</span><span class="sxs-lookup"><span data-stu-id="be868-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="be868-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="be868-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="be868-111">hello 個別的視訊和音訊範例使用加密的 hello **AES 128 CBC**模式。</span><span class="sxs-lookup"><span data-stu-id="be868-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="be868-112">**資料流 FairPlay** (FPS) 已整合至 hello 裝置作業系統，使用 iOS 和 Apple TV 的原生支援。</span><span class="sxs-lookup"><span data-stu-id="be868-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="be868-113">OS X 上的 safari 使用 hello 加密媒體擴充功能 (EME) 介面的支援，以啟用 FPS。</span><span class="sxs-lookup"><span data-stu-id="be868-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="be868-114">**Microsoft PlayReady (英文)**</span><span class="sxs-lookup"><span data-stu-id="be868-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="be868-115">hello 下列影像顯示 hello **HLS + FairPlay 或 PlayReady 動態加密**工作流程。</span><span class="sxs-lookup"><span data-stu-id="be868-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![動態加密工作流程的圖表](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="be868-117">本主題示範如何 toouse Media Services toodynamically 加密 Apple FairPlay HLS 內容。</span><span class="sxs-lookup"><span data-stu-id="be868-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="be868-118">它也會示範如何 toouse hello Media Services 授權傳遞服務 toodeliver FairPlay 授權 tooclients。</span><span class="sxs-lookup"><span data-stu-id="be868-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="be868-119">如果您也想 tooencrypt HLS 以 PlayReady 內容，您會需要 toocreate 常見的內容金鑰，並將它與您的 asset 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="be868-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="be868-120">您也需要 tooconfigure hello 內容金鑰授權原則，如中所述[使用 PlayReady 動態一般加密](media-services-protect-with-drm.md)。</span><span class="sxs-lookup"><span data-stu-id="be868-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="be868-121">需求和考量</span><span class="sxs-lookup"><span data-stu-id="be868-121">Requirements and considerations</span></span>

<span data-ttu-id="be868-122">需要 hello 下列憑證具有 FairPlay，但 toodeliver FairPlay 授權使用 Media Services toodeliver 加密 HLS 時：</span><span class="sxs-lookup"><span data-stu-id="be868-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="be868-123">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="be868-123">An Azure account.</span></span> <span data-ttu-id="be868-124">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="be868-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="be868-125">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="be868-125">A Media Services account.</span></span> <span data-ttu-id="be868-126">toocreate 其中一個，請參閱[建立 Azure 媒體服務帳戶使用 Azure 入口網站 hello](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="be868-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="be868-127">註冊 [Apple Development Program](https://developer.apple.com/)。</span><span class="sxs-lookup"><span data-stu-id="be868-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="be868-128">Apple 要求 hello 內容擁有者 tooobtain hello[部署套件](https://developer.apple.com/contact/fps/)。</span><span class="sxs-lookup"><span data-stu-id="be868-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="be868-129">您已實作金鑰安全性模組 (KSM) 使用媒體服務和要求 hello 最終的 FPS 封裝的狀態。</span><span class="sxs-lookup"><span data-stu-id="be868-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="be868-130">有的 hello 最終 FPS 封裝 toogenerate 憑證，並取得中指示 hello 應用程式密碼金鑰 （請要求）。</span><span class="sxs-lookup"><span data-stu-id="be868-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="be868-131">您使用詢問 tooconfigure FairPlay。</span><span class="sxs-lookup"><span data-stu-id="be868-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="be868-132">Azure 媒體服務 .NET SDK **3.6.0** 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="be868-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="be868-133">必須設定 Media Services 金鑰傳遞端 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="be868-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="be868-134">**應用程式的憑證 (AC)**： 這是包含 hello 私密金鑰的.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="be868-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="be868-135">您可建立這個檔案並以密碼加密。</span><span class="sxs-lookup"><span data-stu-id="be868-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="be868-136">當您設定的金鑰傳遞原則時，您必須提供該密碼和 hello.pfx 檔案，以 Base64 格式。</span><span class="sxs-lookup"><span data-stu-id="be868-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="be868-137">hello 下列步驟說明如何 toogenerate.pfx 憑證檔 FairPlay:</span><span class="sxs-lookup"><span data-stu-id="be868-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="be868-138">從 https://slproweb.com/products/Win32OpenSSL.html 安裝 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="be868-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="be868-139">移 toohello 都 hello FairPlay 憑證和 Apple 所傳送的其他檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="be868-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="be868-140">執行 hello hello 命令列中的下列命令。</span><span class="sxs-lookup"><span data-stu-id="be868-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="be868-141">這會將轉換 hello.cer 檔案 tooa.pem 檔案。</span><span class="sxs-lookup"><span data-stu-id="be868-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="be868-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="be868-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="be868-143">執行 hello hello 命令列中的下列命令。</span><span class="sxs-lookup"><span data-stu-id="be868-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="be868-144">這會將與 hello 私用的索引鍵轉換 hello.pem 檔案 tooa.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="be868-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="be868-145">hello.pfx 檔案的 hello 密碼然後要求 OpenSSL 程式。</span><span class="sxs-lookup"><span data-stu-id="be868-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="be868-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="be868-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="be868-147">**應用程式憑證密碼**: hello 密碼建立 hello.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="be868-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="be868-148">**應用程式憑證的密碼識別碼**： 您必須上傳它們上傳其他媒體服務金鑰的類似 toohow hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="be868-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="be868-149">使用 hello **ContentKeyType.FairPlayPfxPassword**列舉值 tooget hello Media Services 識別碼。</span><span class="sxs-lookup"><span data-stu-id="be868-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="be868-150">這是他們的需要 toouse 內 hello 金鑰傳遞原則選項。</span><span class="sxs-lookup"><span data-stu-id="be868-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="be868-151">**iv**︰這是 16 位元組的隨機值。</span><span class="sxs-lookup"><span data-stu-id="be868-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="be868-152">它必須符合 iv hello hello 資產傳遞原則中。</span><span class="sxs-lookup"><span data-stu-id="be868-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="be868-153">您產生 hello iv，並將其放在這兩個地方： hello 資產傳遞原則和 hello 金鑰傳遞原則選項。</span><span class="sxs-lookup"><span data-stu-id="be868-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="be868-154">**詢問**： 當您使用 hello Apple 開發人員入口網站產生 hello 憑證時收到此機碼。</span><span class="sxs-lookup"><span data-stu-id="be868-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="be868-155">每個開發小組都會收到一個唯一的 ASK。</span><span class="sxs-lookup"><span data-stu-id="be868-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="be868-156">儲存一份 hello 發問，並將它儲存在安全的地方。</span><span class="sxs-lookup"><span data-stu-id="be868-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="be868-157">您稍後會需要 tooconfigure 詢問為 FairPlayAsk tooMedia 服務。</span><span class="sxs-lookup"><span data-stu-id="be868-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="be868-158"> **ASK 識別碼**︰當您將 ASK 上傳至媒體服務時，會取得這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="be868-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="be868-159">您必須使用上傳詢問 hello **ContentKeyType.FairPlayAsk**列舉值。</span><span class="sxs-lookup"><span data-stu-id="be868-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="be868-160">因此 hello hello Media Services 識別碼傳回，而這是設定 hello 金鑰傳遞原則選項時應該使用什麼。</span><span class="sxs-lookup"><span data-stu-id="be868-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="be868-161">hello 下列項目必須設定 hello FPS 用戶端：</span><span class="sxs-lookup"><span data-stu-id="be868-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="be868-162">**應用程式的憑證 (AC)**： 這是包含 hello 公開金鑰，哪些 hello 作業系統使用 tooencrypt 某些裝載.cer/.der 檔案。</span><span class="sxs-lookup"><span data-stu-id="be868-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="be868-163">Media Services 需要資訊，請參閱 tooknow 因為 hello 播放程式需要它。</span><span class="sxs-lookup"><span data-stu-id="be868-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="be868-164">hello 金鑰傳遞服務會解密使用 hello 相對應的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="be868-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="be868-165">tooplay 備份 FairPlay 加密的資料流、 取得實際詢問第一次，並接著產生實際的憑證。</span><span class="sxs-lookup"><span data-stu-id="be868-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="be868-166">該處理程序會建立所有 3 個部分︰</span><span class="sxs-lookup"><span data-stu-id="be868-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="be868-167">.der 檔案</span><span class="sxs-lookup"><span data-stu-id="be868-167">.der file</span></span>
  * <span data-ttu-id="be868-168">.pfx 檔案</span><span class="sxs-lookup"><span data-stu-id="be868-168">.pfx file</span></span>
  * <span data-ttu-id="be868-169">hello.pfx 的密碼</span><span class="sxs-lookup"><span data-stu-id="be868-169">password for hello .pfx</span></span>

<span data-ttu-id="be868-170">hello 下列用戶端支援使用 HLS **AES 128 CBC**加密： OS X、 Apple TV iOS 上的 Safari。</span><span class="sxs-lookup"><span data-stu-id="be868-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="be868-171">設定 FairPlay 動態加密和授權傳遞服務</span><span class="sxs-lookup"><span data-stu-id="be868-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="be868-172">hello 以下是使用 hello Media Services 授權傳遞服務，以及使用動態加密保護 FairPlay 您資產的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="be868-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="be868-173">建立資產，並將檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="be868-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="be868-174">Hello 資產編碼包含 hello 檔案 toohello 彈性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="be868-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="be868-175">建立內容金鑰，並將它與 hello 編碼資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="be868-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="be868-176">設定 hello 內容金鑰授權原則。</span><span class="sxs-lookup"><span data-stu-id="be868-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="be868-177">指定 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="be868-177">Specify hello following:</span></span>

   * <span data-ttu-id="be868-178">hello 傳遞方法 （在此情況下，FairPlay）。</span><span class="sxs-lookup"><span data-stu-id="be868-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="be868-179">FairPlay 原則選項組態。</span><span class="sxs-lookup"><span data-stu-id="be868-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="be868-180">如需詳細資訊，如何 tooconfigure FairPlay，請參閱 hello **ConfigureFairPlayPolicyOptions()** hello 以下範例中的方法。</span><span class="sxs-lookup"><span data-stu-id="be868-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="be868-181">通常，您會想 tooconfigure FairPlay 原則選項一次，因為將只有一個憑證和詢問的集合。</span><span class="sxs-lookup"><span data-stu-id="be868-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="be868-182">限制 (開放或權杖)。</span><span class="sxs-lookup"><span data-stu-id="be868-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="be868-183">定義 hello 金鑰如何傳遞 toohello 用戶端資訊特定 toohello 金鑰傳遞類型。</span><span class="sxs-lookup"><span data-stu-id="be868-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="be868-184">設定 hello 資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="be868-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="be868-185">hello 傳遞原則設定包括：</span><span class="sxs-lookup"><span data-stu-id="be868-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="be868-186">hello 傳遞通訊協定 (HLS)。</span><span class="sxs-lookup"><span data-stu-id="be868-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="be868-187">hello 動態加密 （一般 CBC 加密） 的類型。</span><span class="sxs-lookup"><span data-stu-id="be868-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="be868-188">hello 授權取得 URL。</span><span class="sxs-lookup"><span data-stu-id="be868-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="be868-189">如果您想 toodeliver 加密 FairPlay 與另一個數位版權管理 (DRM) 系統的資料流時，您會有 tooconfigure 個別的傳遞原則：</span><span class="sxs-lookup"><span data-stu-id="be868-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="be868-190">一個 IAssetDeliveryPolicy tooconfigure over HTTP (DASH) 與 Common Encryption (CENC) （PlayReady + Widevine），並使用 PlayReady 的 Smooth 動態彈性資料流</span><span class="sxs-lookup"><span data-stu-id="be868-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="be868-191">另一個 IAssetDeliveryPolicy tooconfigure FairPlay 的 HLS</span><span class="sxs-lookup"><span data-stu-id="be868-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="be868-192">建立 OnDemand 定位器 tooget 串流 URL。</span><span class="sxs-lookup"><span data-stu-id="be868-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="be868-193">透過播放程式應用程式使用 FairPlay 金鑰傳遞</span><span class="sxs-lookup"><span data-stu-id="be868-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="be868-194">您可以使用 hello iOS SDK 來開發播放器應用程式。</span><span class="sxs-lookup"><span data-stu-id="be868-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="be868-195">toobe 無法 tooplay FairPlay 內容，您必須 tooimplement hello 授權交換通訊協定。</span><span class="sxs-lookup"><span data-stu-id="be868-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="be868-196">此通訊協定不是由 Apple 指定。</span><span class="sxs-lookup"><span data-stu-id="be868-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="be868-197">是由 tooeach 應用程式如何 toosend 金鑰傳遞要求。</span><span class="sxs-lookup"><span data-stu-id="be868-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="be868-198">hello Media Services FairPlay 金鑰傳遞服務會預期 hello SPC toocome www-form-url 編碼的文章中的訊息，下列表單的 hello:</span><span class="sxs-lookup"><span data-stu-id="be868-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="be868-199">Azure Media Player 不支援 hello 現成的 FairPlay 播放。</span><span class="sxs-lookup"><span data-stu-id="be868-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="be868-200">在 MAC OS X 上，tooget FairPlay 播放從 hello Apple 開發人員帳戶取得 hello 範例播放程式。</span><span class="sxs-lookup"><span data-stu-id="be868-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="be868-201">串流 URL</span><span class="sxs-lookup"><span data-stu-id="be868-201">Streaming URLs</span></span>
<span data-ttu-id="be868-202">如果您的資產使用一個以上的 DRM 加密，您應該使用的加密標記 hello 串流 URL: (格式 ='m3u8-aapl' 加密 = 'xxx')。</span><span class="sxs-lookup"><span data-stu-id="be868-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="be868-203">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="be868-203">hello following considerations apply:</span></span>

* <span data-ttu-id="be868-204">僅可指定零個或一個加密類型。</span><span class="sxs-lookup"><span data-stu-id="be868-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="be868-205">hello 加密類型沒有 toobe hello URL 中指定，如果只有一個加密已套用的 toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="be868-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="be868-206">hello 加密類型為不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="be868-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="be868-207">您可以指定下列加密類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="be868-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="be868-208">**cenc**︰一般加密 (PlayReady 或 Widevine)</span><span class="sxs-lookup"><span data-stu-id="be868-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="be868-209">**cbcs-aapl**：FairPlay</span><span class="sxs-lookup"><span data-stu-id="be868-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="be868-210">**cbc**：AES 信封加密</span><span class="sxs-lookup"><span data-stu-id="be868-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="be868-211">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="be868-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="be868-212">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="be868-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="be868-213">新增下列項目太 hello**appSettings** app.config 檔案中所定義：</span><span class="sxs-lookup"><span data-stu-id="be868-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="be868-214">範例</span><span class="sxs-lookup"><span data-stu-id="be868-214">Example</span></span>

<span data-ttu-id="be868-215">下列範例中的 hello 示範 hello 能力 toouse Media Services toodeliver FairPlay 以加密您的內容。</span><span class="sxs-lookup"><span data-stu-id="be868-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="be868-216">這項功能已引入 hello Azure Media Services SDK for.NET 版本 3.6.0。</span><span class="sxs-lookup"><span data-stu-id="be868-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="be868-217">Hello 本節中所顯示的程式碼來覆寫您 Program.cs 檔案中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="be868-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="be868-218">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="be868-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="be868-219">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="be868-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="be868-220">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="be868-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="be868-221">請確定 tooupdate 變數 toopoint toofolders 輸入的檔案的所在位置。</span><span class="sxs-lookup"><span data-stu-id="be868-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="be868-222">後續步驟：媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="be868-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="be868-223">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="be868-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
