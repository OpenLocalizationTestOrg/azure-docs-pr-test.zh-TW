---
title: "使用 aaaConfiguring 內容保護原則 hello Azure 入口網站 |Microsoft 文件"
description: "本文示範如何 toouse hello Azure 入口網站 tooconfigure 內容保護原則。 hello 文章也顯示如何為您資產的 tooenable 動態加密。"
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
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="7180f-104">設定使用 hello Azure 入口網站的內容保護原則</span><span class="sxs-lookup"><span data-stu-id="7180f-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="7180f-105">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7180f-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="7180f-106">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7180f-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="7180f-107">概觀</span><span class="sxs-lookup"><span data-stu-id="7180f-107">Overview</span></span>
<span data-ttu-id="7180f-108">Microsoft Azure 媒體服務 (AMS) 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。</span><span class="sxs-lookup"><span data-stu-id="7180f-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="7180f-109">Media Services 可讓您 toodeliver 您的內容加密以動態方式使用進階加密標準 (AES) （使用 128 位元加密金鑰），使用 PlayReady 和/或 Widevine DRM 和 Apple FairPlay 一般加密 (CENC)。</span><span class="sxs-lookup"><span data-stu-id="7180f-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="7180f-110">AMS 提供服務，以傳遞授權 DRM 和 AES 清除金鑰 tooauthorized 用戶端。</span><span class="sxs-lookup"><span data-stu-id="7180f-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="7180f-111">hello Azure 入口網站可讓您其中一個 toocreate**金鑰授權授權原則**所有類型的加密。</span><span class="sxs-lookup"><span data-stu-id="7180f-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="7180f-112">本文示範如何 tooconfigure 內容保護原則 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7180f-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="7180f-113">hello 文章也顯示如何 tooapply 動態加密 tooyour 資產。</span><span class="sxs-lookup"><span data-stu-id="7180f-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="7180f-114">如果您使用 hello Azure 傳統入口網站 toocreate 保護原則，hello 原則可能不會出現在 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7180f-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7180f-115">不過，所有舊的 hello 原則仍然存在。</span><span class="sxs-lookup"><span data-stu-id="7180f-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="7180f-116">您可以檢查它們是否使用 Azure Media Services.NET SDK 或 hello hello [Azure 媒體服務-總管](https://github.com/Azure/Azure-Media-Services-Explorer/releases)工具 (toosee hello 原則，以滑鼠右鍵按一下 hello 資產]-> [的顯示資訊 (F4)-> 中，按一下 [內容]-> [索引標籤的索引鍵按一下 hello 索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="7180f-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="7180f-117">如果您想 tooencrypt 資產使用新的原則，設定這些文件以 hello Azure 入口網站中，按一下 [儲存]，重新套用動態加密。</span><span class="sxs-lookup"><span data-stu-id="7180f-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="7180f-118">開始設定內容保護</span><span class="sxs-lookup"><span data-stu-id="7180f-118">Start configuring content protection</span></span>
<span data-ttu-id="7180f-119">設定內容的保護，全域 tooyour AMS 帳戶 toouse hello 入口 toostart hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7180f-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="7180f-120">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7180f-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="7180f-121">選取 [設定] > [內容保護]。</span><span class="sxs-lookup"><span data-stu-id="7180f-121">Select **Settings** > **Content protection**.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="7180f-123">金鑰/授權的授權原則</span><span class="sxs-lookup"><span data-stu-id="7180f-123">Key/license authorization policy</span></span>
<span data-ttu-id="7180f-124">AMS 支援多種方式來驗證提出金鑰或授權要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="7180f-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="7180f-125">hello 內容金鑰授權原則必須由您設定，並且符合您的用戶端 hello 金鑰/授權 toobe delived 的 toohello 用戶端的順序。</span><span class="sxs-lookup"><span data-stu-id="7180f-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="7180f-126">hello 內容金鑰授權原則可能會有一或多個授權限制：**開啟**或**語彙基元**限制。</span><span class="sxs-lookup"><span data-stu-id="7180f-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="7180f-127">hello Azure 入口網站可讓您其中一個 toocreate**金鑰授權授權原則**所有類型的加密。</span><span class="sxs-lookup"><span data-stu-id="7180f-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="7180f-128">開啟</span><span class="sxs-lookup"><span data-stu-id="7180f-128">Open</span></span>
<span data-ttu-id="7180f-129">開放限制表示 hello 系統將會傳送 hello 金鑰 tooanyone 人員提出金鑰要求。</span><span class="sxs-lookup"><span data-stu-id="7180f-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="7180f-130">這項限制可用於測試用途。</span><span class="sxs-lookup"><span data-stu-id="7180f-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="7180f-131">權杖</span><span class="sxs-lookup"><span data-stu-id="7180f-131">Token</span></span>
<span data-ttu-id="7180f-132">hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="7180f-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="7180f-133">Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="7180f-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="7180f-134">媒體服務不提供安全權杖服務。</span><span class="sxs-lookup"><span data-stu-id="7180f-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="7180f-135">您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7180f-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="7180f-136">hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。</span><span class="sxs-lookup"><span data-stu-id="7180f-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="7180f-137">hello Media Services 金鑰傳遞服務會傳回 hello 要求金鑰 （或授權） toohello 用戶端 hello 語彙基元是否有效並 hello 宣告 hello 語彙基元在比對中所設定的 hello 金鑰 （或授權）。</span><span class="sxs-lookup"><span data-stu-id="7180f-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="7180f-138">在設定 hello 權杖限制的原則時，您必須指定 hello 主要驗證金鑰、 簽發者和對象的參數。</span><span class="sxs-lookup"><span data-stu-id="7180f-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="7180f-139">hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7180f-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="7180f-140">hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。</span><span class="sxs-lookup"><span data-stu-id="7180f-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="7180f-141">hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7180f-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="7180f-143">PlayReady 權限範本</span><span class="sxs-lookup"><span data-stu-id="7180f-143">PlayReady rights template</span></span>
<span data-ttu-id="7180f-144">如需 hello PlayReady 權限範本的詳細資訊，請參閱[媒體服務 PlayReady 授權範本概觀](media-services-playready-license-template-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7180f-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="7180f-145">非持續性</span><span class="sxs-lookup"><span data-stu-id="7180f-145">Non persistent</span></span>
<span data-ttu-id="7180f-146">如果您將授權設定為非持續性時，它是只在記憶體中時保留 hello 播放程式會使用 hello 授權。</span><span class="sxs-lookup"><span data-stu-id="7180f-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="7180f-148">持續性</span><span class="sxs-lookup"><span data-stu-id="7180f-148">Persistent</span></span>
<span data-ttu-id="7180f-149">如果您將 hello 授權設定為持續性時，將它儲存在永續性儲存體 hello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="7180f-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="7180f-151">Widevine 權限範本</span><span class="sxs-lookup"><span data-stu-id="7180f-151">Widevine rights template</span></span>
<span data-ttu-id="7180f-152">如需 hello Widevine 權限範本的詳細資訊，請參閱[Widevine 授權範本概觀](media-services-widevine-license-template-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7180f-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="7180f-153">基本</span><span class="sxs-lookup"><span data-stu-id="7180f-153">Basic</span></span>
<span data-ttu-id="7180f-154">當您選取**基本**，hello 範本將會建立使用所有預設值。</span><span class="sxs-lookup"><span data-stu-id="7180f-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="7180f-155">進階</span><span class="sxs-lookup"><span data-stu-id="7180f-155">Advanced</span></span>
<span data-ttu-id="7180f-156">如需有關 Widevine 組態進階選項的詳細說明，請參閱 [這個](media-services-widevine-license-template-overview.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="7180f-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="7180f-158">FairPlay 組態</span><span class="sxs-lookup"><span data-stu-id="7180f-158">FairPlay configuration</span></span>
<span data-ttu-id="7180f-159">tooenable FairPlay 加密，您需要 tooprovide hello 應用程式的憑證和應用程式密碼金鑰 （詢問） 透過 hello FairPlay 組態選項。</span><span class="sxs-lookup"><span data-stu-id="7180f-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="7180f-160">如需 FairPlay 組態和需求的詳細資訊，請參閱 [這個](media-services-protect-hls-with-fairplay.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="7180f-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="7180f-162">套用動態加密 tooyour 資產</span><span class="sxs-lookup"><span data-stu-id="7180f-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="7180f-163">tootake 利用動態加密，您需要 tooencode 原始程式檔成一組彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="7180f-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="7180f-164">選取您想 tooencrypt 資產</span><span class="sxs-lookup"><span data-stu-id="7180f-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="7180f-165">所有的資產，選取 toosee**設定** > **資產**。</span><span class="sxs-lookup"><span data-stu-id="7180f-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="7180f-167">使用 AES 或 DRM 加密</span><span class="sxs-lookup"><span data-stu-id="7180f-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="7180f-168">一旦您在資產上按下 [加密] 後，會看到兩個選擇︰[AES] 或 [DRM]。</span><span class="sxs-lookup"><span data-stu-id="7180f-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="7180f-169">AES</span><span class="sxs-lookup"><span data-stu-id="7180f-169">AES</span></span>
<span data-ttu-id="7180f-170">AES 清除金鑰加密將會在所有串流通訊協定上啟用︰Smooth Streaming、HLS 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="7180f-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="7180f-172">DRM</span><span class="sxs-lookup"><span data-stu-id="7180f-172">DRM</span></span>
<span data-ttu-id="7180f-173">當您選取 hello DRM 索引標籤時，您會有不同的內容保護原則的選擇 （其中，您必須設定到目前為止） + 串流處理通訊協定的一組。</span><span class="sxs-lookup"><span data-stu-id="7180f-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="7180f-174">**PlayReady 和 Widevine 與 MPEG-DASH** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="7180f-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="7180f-175">**PlayReady 和 Widevine 與 MPEG-DASH + FairPlay 與 HLS** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="7180f-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="7180f-176">並且會使用 FairPlay 加密您的 HLS 串流。</span><span class="sxs-lookup"><span data-stu-id="7180f-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="7180f-177">**PlayReady 僅與 Smooth Streaming、HLS 和 MPEG-DASH** - 會使用 PlayReady DRM 動態加密 Smooth Streaming、HLS、MPEG-DASH 串流。</span><span class="sxs-lookup"><span data-stu-id="7180f-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="7180f-178">**Widevine 僅與 MPEG-DASH** - 會使用 Widevine DRM 動態加密您的 MPEG-DASH。</span><span class="sxs-lookup"><span data-stu-id="7180f-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="7180f-179">**FairPlay 僅與 HLS** - 會使用 FairPlay 動態加密您的 HLS 串流。</span><span class="sxs-lookup"><span data-stu-id="7180f-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="7180f-180">tooenable FairPlay 加密，您需要 tooprovide hello 應用程式的憑證和應用程式密碼金鑰 （詢問） 透過 hello hello 內容保護設定 刀鋒視窗的 FairPlay 組態選項。</span><span class="sxs-lookup"><span data-stu-id="7180f-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="7180f-182">一旦您進行 hello 加密 選項，請按**套用**。</span><span class="sxs-lookup"><span data-stu-id="7180f-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="7180f-183">如果您計劃 tooplay AES 加密 HLS Safari 中的，請參閱[這篇部落格](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)。</span><span class="sxs-lookup"><span data-stu-id="7180f-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7180f-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7180f-184">Next steps</span></span>
<span data-ttu-id="7180f-185">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="7180f-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7180f-186">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="7180f-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

