---
title: "使用 Azure 入口網站設定內容保護原則 | Microsoft Docs"
description: "本文章示範如何使用 Azure 入口網站設定內容保護原則。 文章也會說明如何啟用資產的動態加密。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="09311-104">使用 Azure 入口網站設定內容保護原則</span><span class="sxs-lookup"><span data-stu-id="09311-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="09311-105">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="09311-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="09311-106">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="09311-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="09311-107">Overview</span><span class="sxs-lookup"><span data-stu-id="09311-107">Overview</span></span>
<span data-ttu-id="09311-108">Microsoft Azure 媒體服務 (AMS) 可讓您保護媒體從離開電腦到進行儲存、處理和傳遞時的安全。</span><span class="sxs-lookup"><span data-stu-id="09311-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="09311-109">媒體服務可讓您傳遞利用進階加密標準 (AES) (使用 128 位元加密金鑰) 動態加密、使用 PlayReady 和/或 Widevine DRM 的一般加密 (CENC) 和 Apple FairPlay 的內容。</span><span class="sxs-lookup"><span data-stu-id="09311-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="09311-110">AMS 提供一種服務，將 DRM 授權和 AES 純文字金鑰傳遞給授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="09311-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="09311-111">Azure 入口網站可讓您針對所有加密類型建立一個 **金鑰/授權的授權原則** 。</span><span class="sxs-lookup"><span data-stu-id="09311-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="09311-112">本文章示範如何使用 Azure 入口網站設定內容保護原則。</span><span class="sxs-lookup"><span data-stu-id="09311-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="09311-113">文章也會說明如何將動態加密套用到資產。</span><span class="sxs-lookup"><span data-stu-id="09311-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="09311-114">如果您是使用 Azure 傳統入口網站建立保護原則，原則可能不會出現在 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="09311-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="09311-115">不過，所有舊的原則仍然存在。</span><span class="sxs-lookup"><span data-stu-id="09311-115">However, all the old polices still exist.</span></span> <span data-ttu-id="09311-116">您可以使用 Azure 媒體服務 .NET SDK 或 [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) 工具來檢查這些原則 (若要參閱原則，請以滑鼠右鍵按一下 [資產] -> [顯示資訊] \(F4) -> 按一下 [內容金鑰] 索引標籤 -> 按一下金鑰)。</span><span class="sxs-lookup"><span data-stu-id="09311-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="09311-117">如果您想要使用新的原則加密資產，請使用 Azure 入口網站設定它們、按一下 [儲存]，然後重新套用動態加密。</span><span class="sxs-lookup"><span data-stu-id="09311-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="09311-118">開始設定內容保護</span><span class="sxs-lookup"><span data-stu-id="09311-118">Start configuring content protection</span></span>
<span data-ttu-id="09311-119">若要使用入口網站開始設定內容保護，對 AMS 帳戶設為全域，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="09311-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="09311-120">在 [Azure 入口網站](https://portal.azure.com/)中，選取您的 Azure 媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="09311-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="09311-121">選取 [設定] > [內容保護]。</span><span class="sxs-lookup"><span data-stu-id="09311-121">Select **Settings** > **Content protection**.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="09311-123">金鑰/授權的授權原則</span><span class="sxs-lookup"><span data-stu-id="09311-123">Key/license authorization policy</span></span>
<span data-ttu-id="09311-124">AMS 支援多種方式來驗證提出金鑰或授權要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="09311-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="09311-125">內容金鑰授權原則必須由您設定，而且您的用戶端必須符合條件，才能將金鑰/授權傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="09311-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="09311-126">內容金鑰授權原則可能會有一個或多個授權限制：**open** 或 **token** 限制。</span><span class="sxs-lookup"><span data-stu-id="09311-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="09311-127">Azure 入口網站可讓您針對所有加密類型建立一個 **金鑰/授權的授權原則** 。</span><span class="sxs-lookup"><span data-stu-id="09311-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="09311-128">開啟</span><span class="sxs-lookup"><span data-stu-id="09311-128">Open</span></span>
<span data-ttu-id="09311-129">Open 限制表示系統將會傳送金鑰給提出金鑰要求的任何人。</span><span class="sxs-lookup"><span data-stu-id="09311-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="09311-130">這項限制可用於測試用途。</span><span class="sxs-lookup"><span data-stu-id="09311-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="09311-131">token</span><span class="sxs-lookup"><span data-stu-id="09311-131">Token</span></span>
<span data-ttu-id="09311-132">token 限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="09311-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="09311-133">媒體服務支援簡單 Web 權杖 (SWT) 格式和 JSON Web 權杖 (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="09311-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="09311-134">媒體服務不提供安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="09311-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="09311-135">您可以建立自訂 STS，或利用 Microsoft Azure ACS 來發行權杖。</span><span class="sxs-lookup"><span data-stu-id="09311-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="09311-136">STS 必須設定為建立使用指定的索引鍵和問題宣告您在權杖限制組態中指定簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="09311-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="09311-137">如果權杖有效，且權杖中的宣告符合針對金鑰 (或授權) 所設定的宣告，媒體服務金鑰傳遞服務會將所要求的金鑰 (或授權) 傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="09311-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="09311-138">設定 token 限制原則時，您必須指定主要驗證金鑰、簽發者和對象參數。</span><span class="sxs-lookup"><span data-stu-id="09311-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="09311-139">主要驗證金鑰包含簽署權杖使用的金鑰，簽發者是發行權杖的安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="09311-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="09311-140">對象 (有時稱為範圍) 描述權杖或權杖獲授權存取之資源的用途。</span><span class="sxs-lookup"><span data-stu-id="09311-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="09311-141">媒體服務金鑰傳遞服務會驗證權杖中的這些值符合在範本中的值。</span><span class="sxs-lookup"><span data-stu-id="09311-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="09311-143">PlayReady 權限範本</span><span class="sxs-lookup"><span data-stu-id="09311-143">PlayReady rights template</span></span>
<span data-ttu-id="09311-144">如需 PlayReady 權限範本的詳細資訊，請參閱 [媒體服務 PlayReady 授權範本概觀](media-services-playready-license-template-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="09311-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="09311-145">非持續性</span><span class="sxs-lookup"><span data-stu-id="09311-145">Non persistent</span></span>
<span data-ttu-id="09311-146">如果您將授權設定為非持續性，則當播放程式使用授權時，授權只會保留在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="09311-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="09311-148">持續性</span><span class="sxs-lookup"><span data-stu-id="09311-148">Persistent</span></span>
<span data-ttu-id="09311-149">如果您將授權設定為持續性，它會儲存在用戶端上的永續性儲存體中。</span><span class="sxs-lookup"><span data-stu-id="09311-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="09311-151">Widevine 權限範本</span><span class="sxs-lookup"><span data-stu-id="09311-151">Widevine rights template</span></span>
<span data-ttu-id="09311-152">如需 Widevine 權限範本的詳細資訊，請參閱 [Widevine 授權範本概觀](media-services-widevine-license-template-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="09311-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="09311-153">基本</span><span class="sxs-lookup"><span data-stu-id="09311-153">Basic</span></span>
<span data-ttu-id="09311-154">當您選取 [基本] 時，會使用所有預設值建立範本。</span><span class="sxs-lookup"><span data-stu-id="09311-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="09311-155">進階</span><span class="sxs-lookup"><span data-stu-id="09311-155">Advanced</span></span>
<span data-ttu-id="09311-156">如需有關 Widevine 組態進階選項的詳細說明，請參閱 [這個](media-services-widevine-license-template-overview.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="09311-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="09311-158">FairPlay 組態</span><span class="sxs-lookup"><span data-stu-id="09311-158">FairPlay configuration</span></span>
<span data-ttu-id="09311-159">若要啟用 FairPlay 加密，您必須透過 FairPlay 組態選項提供應用程式憑證和應用程式秘密金鑰 (ASK)。</span><span class="sxs-lookup"><span data-stu-id="09311-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="09311-160">如需 FairPlay 組態和需求的詳細資訊，請參閱 [這個](media-services-protect-hls-with-fairplay.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="09311-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="09311-162">將動態加密套用到您的資產</span><span class="sxs-lookup"><span data-stu-id="09311-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="09311-163">若要利用動態封裝功能，您必須將您的來源檔案編碼成一組調適性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="09311-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="09311-164">選取您要加密的資產</span><span class="sxs-lookup"><span data-stu-id="09311-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="09311-165">若要查看您所有的資產，請選取 [設定] > [資產]。</span><span class="sxs-lookup"><span data-stu-id="09311-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="09311-167">使用 AES 或 DRM 加密</span><span class="sxs-lookup"><span data-stu-id="09311-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="09311-168">一旦您在資產上按下 [加密] 後，會看到兩個選擇︰[AES] 或 [DRM]。</span><span class="sxs-lookup"><span data-stu-id="09311-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="09311-169">AES</span><span class="sxs-lookup"><span data-stu-id="09311-169">AES</span></span>
<span data-ttu-id="09311-170">AES 清除金鑰加密將會在所有串流通訊協定上啟用︰Smooth Streaming、HLS 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="09311-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="09311-172">DRM</span><span class="sxs-lookup"><span data-stu-id="09311-172">DRM</span></span>
<span data-ttu-id="09311-173">當您選取 DRM 索引標籤時，會看到不同內容保護原則的選擇 (您現在必須已設定) + 一組串流通訊協定。</span><span class="sxs-lookup"><span data-stu-id="09311-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="09311-174">**PlayReady 和 Widevine 與 MPEG-DASH** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="09311-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="09311-175">**PlayReady 和 Widevine 與 MPEG-DASH + FairPlay 與 HLS** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="09311-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="09311-176">並且會使用 FairPlay 加密您的 HLS 串流。</span><span class="sxs-lookup"><span data-stu-id="09311-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="09311-177">**PlayReady 僅與 Smooth Streaming、HLS 和 MPEG-DASH** - 會使用 PlayReady DRM 動態加密 Smooth Streaming、HLS、MPEG-DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="09311-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="09311-178">**Widevine 僅與 MPEG-DASH** - 會使用 Widevine DRM 動態加密您的 MPEG-DASH。</span><span class="sxs-lookup"><span data-stu-id="09311-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="09311-179">**FairPlay 僅與 HLS** - 會使用 FairPlay 動態加密您的 HLS 串流。</span><span class="sxs-lookup"><span data-stu-id="09311-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="09311-180">若要啟用 FairPlay 加密，您必須透過內容保護設定刀鋒視窗的 FairPlay 組態選項提供應用程式憑證和應用程式秘密金鑰 (ASK)。</span><span class="sxs-lookup"><span data-stu-id="09311-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="09311-182">一旦您進行加密選取後，按下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="09311-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="09311-183">如果您想要在 Safari 中播放 AES 加密的 HLS，請參閱[這篇部落格](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)。</span><span class="sxs-lookup"><span data-stu-id="09311-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09311-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09311-184">Next steps</span></span>
<span data-ttu-id="09311-185">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="09311-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09311-186">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="09311-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

