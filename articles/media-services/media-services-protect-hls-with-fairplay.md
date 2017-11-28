---
title: "使用 Microsoft PlayReady 或 Apple FairPlay 來保護 HLS 內容 | Microsoft Docs"
description: "本主題提供概觀及顯示如何使用 Azure 媒體服務，以 Apple FairPlay 動態加密您的 HTTP 即時串流 (HLS) 內容。 它也會顯示如何使用媒體服務授權傳遞服務，傳遞 FairPlay 授權給用戶端。"
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="4dc2a-104">使用 Apple FairPlay 或 Microsoft PlayReady 保護 HLS 內容</span><span class="sxs-lookup"><span data-stu-id="4dc2a-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="4dc2a-105">Azure 媒體服務可讓您使用下列格式，動態加密您的 HTTP 即時串流 (HLS) 內容︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="4dc2a-106">**AES-128 信封清除金鑰**</span><span class="sxs-lookup"><span data-stu-id="4dc2a-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="4dc2a-107">使用 **AES-128 CBC** 模式加密整個區塊。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="4dc2a-108">iOS 和 OS X 播放程式原本就支援資料流解密。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="4dc2a-109">如需詳細資訊，請參閱[使用 AES-128 動態加密和金鑰傳遞服務](media-services-protect-with-aes128.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="4dc2a-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="4dc2a-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="4dc2a-111">使用 **AES-128 CBC** 模式加密個別的視訊和音訊範例。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="4dc2a-112">**FairPlay 串流** (FPS) 已整合至裝置工作系統，在 iOS 和 Apple 電視上具有原生支援。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="4dc2a-113">OS X 上的 Safari 使用加密媒體擴充功能 (EME) 介面支援來啟用 FPS。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="4dc2a-114">**Microsoft PlayReady (英文)**</span><span class="sxs-lookup"><span data-stu-id="4dc2a-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="4dc2a-115">下圖顯示 **HLS + FairPlay 或 PlayReady 動態加密** 工作流程。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![動態加密工作流程的圖表](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="4dc2a-117">本主題示範如何使用媒體服務，以 Apple FairPlay 動態加密 HLS 內容。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="4dc2a-118">它也會顯示如何使用媒體服務授權傳遞服務，傳遞 FairPlay 授權給用戶端。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc2a-119">如果您也想要以 PlayReady 加密 HLS 內容，必須建立一般內容金鑰，並將它與您的資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="4dc2a-120">您也必須設定內容金鑰的授權原則，如[使用 PlayReady 動態一般加密](media-services-protect-with-drm.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="4dc2a-121">需求和考量</span><span class="sxs-lookup"><span data-stu-id="4dc2a-121">Requirements and considerations</span></span>

<span data-ttu-id="4dc2a-122">以下是使用媒體服務傳遞以 FairPlay 加密的 HLS，以及傳遞 FairPlay 授權時所需的項目：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="4dc2a-123">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-123">An Azure account.</span></span> <span data-ttu-id="4dc2a-124">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="4dc2a-125">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-125">A Media Services account.</span></span> <span data-ttu-id="4dc2a-126">若要建立一個，請參閱[使用 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="4dc2a-127">註冊 [Apple Development Program](https://developer.apple.com/)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="4dc2a-128">Apple 要求內容擁有者必須取得 [部署套件](https://developer.apple.com/contact/fps/)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="4dc2a-129">說明您已使用媒體服務實作金鑰安全性模組 (KSM)，現在想要求最終的 FPS 套件。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="4dc2a-130">最終 FPS 套件包含相關指示，用以產生憑證和取得應用程式密碼金鑰 (ASK)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="4dc2a-131">您可使用 ASK 來設定 FairPlay。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="4dc2a-132">Azure 媒體服務 .NET SDK **3.6.0** 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="4dc2a-133">必須在媒體服務金鑰傳遞端設定下列各項︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="4dc2a-134">**應用程式憑證 (AC)**︰這是包含私密金鑰的 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="4dc2a-135">您可建立這個檔案並以密碼加密。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="4dc2a-136">當您設定金鑰傳遞原則時，您必須提供該密碼和 base64 格式的 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="4dc2a-137">下列步驟說明如何產生 FairPlay 的 .pfx 憑證檔案：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="4dc2a-138">從 https://slproweb.com/products/Win32OpenSSL.html 安裝 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="4dc2a-139">移至 FairPlay 憑證和其他 Apple 提供檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="4dc2a-140">從命令列執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-140">Run the following command from the command line.</span></span> <span data-ttu-id="4dc2a-141">這會將 .cer 檔案轉換成 .pem 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="4dc2a-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="4dc2a-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="4dc2a-143">從命令列執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-143">Run the following command from the command line.</span></span> <span data-ttu-id="4dc2a-144">這會將 .pem 檔案轉換為包含私密金鑰的 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="4dc2a-145">OpenSSL 程式會接著要求 .Pfx 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="4dc2a-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="4dc2a-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="4dc2a-147">**應用程式憑證密碼** - 用來建立 .pfx 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="4dc2a-148">**應用程式憑證密碼識別碼**︰您必須上傳密碼，做法類似於其上傳其他媒體服務金鑰的方式。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="4dc2a-149">使用 **ContentKeyType.FairPlayPfxPassword** 列舉值來取得媒體服務識別碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="4dc2a-150">這是它們要在金鑰傳遞原則選項內使用所需之物。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="4dc2a-151">**iv**︰這是 16 位元組的隨機值。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="4dc2a-152">其必須符合資產傳遞原則中的 iv。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="4dc2a-153">您會產生 iv，並將它放在兩個位置︰資產傳遞原則和金鑰傳遞原則選項。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="4dc2a-154">**ASK**：當您使用 Apple 開發人員入口網站產生憑證時，會收到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="4dc2a-155">每個開發小組都會收到一個唯一的 ASK。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="4dc2a-156">儲存一份 ASK，並將它存放在安全的地方。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="4dc2a-157">您之後必須將 ASK 設定為媒體服務的 FairPlayAsk。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="4dc2a-158"> **ASK 識別碼**︰當您將 ASK 上傳至媒體服務時，會取得這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="4dc2a-159">您必須使用 **ContentKeyType.FairPlayAsk** 列舉值來上傳 ASK。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="4dc2a-160">結果會傳回媒體服務識別碼，設定金鑰傳遞原則選項時應使用此識別碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="4dc2a-161">FPS 用戶端必須設定下列各項︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="4dc2a-162">**應用程式憑證 (AC)**：這是 .cer/.der 檔案，其中包含作業系統用來加密某些承載的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="4dc2a-163">媒體服務必須了解它，因為播放程式需要它。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="4dc2a-164">金鑰傳遞服務會使用對應的私密金鑰來解密。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="4dc2a-165">若要播放 FairPlay 加密的資料流，請先取得真正的 ASK，然後產生真正的憑證。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="4dc2a-166">該處理程序會建立所有 3 個部分︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="4dc2a-167">.der 檔案</span><span class="sxs-lookup"><span data-stu-id="4dc2a-167">.der file</span></span>
  * <span data-ttu-id="4dc2a-168">.pfx 檔案</span><span class="sxs-lookup"><span data-stu-id="4dc2a-168">.pfx file</span></span>
  * <span data-ttu-id="4dc2a-169">.pfx 的密碼</span><span class="sxs-lookup"><span data-stu-id="4dc2a-169">password for the .pfx</span></span>

<span data-ttu-id="4dc2a-170">下列用戶端支援採用 **AES-128 CBC** 加密的 HLS︰OS X 上的 Safari、Apple TV、iOS.</span><span class="sxs-lookup"><span data-stu-id="4dc2a-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="4dc2a-171">設定 FairPlay 動態加密和授權傳遞服務</span><span class="sxs-lookup"><span data-stu-id="4dc2a-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="4dc2a-172">以下是使用媒體服務授權傳遞服務，以及使用動態加密時，透過 FairPlay 來保護資產的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="4dc2a-173">建立資產，並將檔案上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="4dc2a-174">將包含檔案的資產編碼為自適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="4dc2a-175">建立內容金鑰並將它與編碼的資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="4dc2a-176">設定內容金鑰的授權原則。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="4dc2a-177">指定下列各項：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-177">Specify the following:</span></span>

   * <span data-ttu-id="4dc2a-178">傳遞方法 (在此例中為 FairPlay)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="4dc2a-179">FairPlay 原則選項組態。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="4dc2a-180">如需有關如何設定 FairPlay 的詳細資訊，請參閱下列範例中的 **ConfigureFairPlayPolicyOptions()** 方法。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4dc2a-181">您通常只想要設定一次 FairPlay 原則選項，因為您只會有一組憑證和 ASK。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="4dc2a-182">限制 (開放或權杖)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="4dc2a-183">金鑰傳遞類型的特定資訊，可定義如何將金鑰傳遞至用戶端。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="4dc2a-184">設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="4dc2a-185">傳遞原則組態包括︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="4dc2a-186">傳遞通訊協定 (HLS)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="4dc2a-187">動態加密類型 (一般 CBC 加密)。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="4dc2a-188">授權取得 URL。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4dc2a-189">如果您想要傳遞使用 FairPlay 和另一個 Digital Rights Management (DRM) 系統加密的資料流，則必須設定個別的傳遞原則：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="4dc2a-190">一個 IAssetDeliveryPolicy 以設定使用一般加密 (CENC) (PlayReady + WideVine) 的 Dynamic Adaptive Streaming over HTTP (DASH)，以及使用 PlayReady 的 Smooth</span><span class="sxs-lookup"><span data-stu-id="4dc2a-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="4dc2a-191">另一個 IAssetDeliveryPolicy 以設定 HLS 的 FairPlay</span><span class="sxs-lookup"><span data-stu-id="4dc2a-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="4dc2a-192">建立隨選定位器以取得串流 URL。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="4dc2a-193">透過播放程式應用程式使用 FairPlay 金鑰傳遞</span><span class="sxs-lookup"><span data-stu-id="4dc2a-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="4dc2a-194">您可以使用 iOS SDK 開發播放應用程式。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="4dc2a-195">為了能夠播放 FairPlay 內容，您必須實作授權交換通訊協定。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="4dc2a-196">此通訊協定不是由 Apple 指定。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="4dc2a-197">而是由每個應用程式如何傳送金鑰傳遞要求而決定。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="4dc2a-198">媒體服務 FairPlay 金鑰傳遞服務會對即將到來的 SPC 視為如下列格式的 www-form-url 已編碼張貼訊息：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="4dc2a-199">Azure 媒體播放器不支援現成的 FairPlay 播放。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="4dc2a-200">若要在 MAC OS X 上播放 FairPlay，請從 Apple 開發人員帳戶取得範例播放程式。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="4dc2a-201">串流 URL</span><span class="sxs-lookup"><span data-stu-id="4dc2a-201">Streaming URLs</span></span>
<span data-ttu-id="4dc2a-202">如果使用一個以上 DRM 來加密您的資產，您應該使用串流 URL 中的加密標籤：(format='m3u8-aapl', encryption='xxx')。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="4dc2a-203">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-203">The following considerations apply:</span></span>

* <span data-ttu-id="4dc2a-204">僅可指定零個或一個加密類型。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="4dc2a-205">如果只有一個加密套用到資產，則無須在 URL 中指定加密類型。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="4dc2a-206">加密類型不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="4dc2a-207">可以指定下列加密類型︰</span><span class="sxs-lookup"><span data-stu-id="4dc2a-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="4dc2a-208">**cenc**︰一般加密 (PlayReady 或 Widevine)</span><span class="sxs-lookup"><span data-stu-id="4dc2a-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="4dc2a-209">**cbcs-aapl**：FairPlay</span><span class="sxs-lookup"><span data-stu-id="4dc2a-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="4dc2a-210">**cbc**：AES 信封加密</span><span class="sxs-lookup"><span data-stu-id="4dc2a-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4dc2a-211">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="4dc2a-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4dc2a-212">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="4dc2a-213">將下列項目新增至 app.config 檔案中定義的 **appSettings**：</span><span class="sxs-lookup"><span data-stu-id="4dc2a-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="4dc2a-214">範例</span><span class="sxs-lookup"><span data-stu-id="4dc2a-214">Example</span></span>

<span data-ttu-id="4dc2a-215">下列範例會示範如何使用媒體服務來傳遞使用 FairPlay 加密的內容。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="4dc2a-216">Azure Media Services SDK for .NET 3.6.0 版已引進這項功能。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="4dc2a-217">以本章節中所顯示的程式碼覆寫 Program.cs 檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="4dc2a-218">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4dc2a-219">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4dc2a-220">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="4dc2a-221">請務必更新變數，以指向您的輸入檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dc2a-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="4dc2a-222">後續步驟：媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="4dc2a-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4dc2a-223">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="4dc2a-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
