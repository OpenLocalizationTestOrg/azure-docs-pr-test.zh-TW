---
title: "aaaCreate Contentkey 的.NET"
description: "了解如何 toocreate 提供安全的內容金鑰存取 tooAssets。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="a3658-103">使用 .NET 建立 ContentKeys</span><span class="sxs-lookup"><span data-stu-id="a3658-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3658-104">REST</span><span class="sxs-lookup"><span data-stu-id="a3658-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="a3658-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a3658-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="a3658-106">Media Services 可讓您 toocreate 和傳遞加密的資產。</span><span class="sxs-lookup"><span data-stu-id="a3658-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="a3658-107">A **ContentKey**提供安全地存取 tooyour**資產**s。</span><span class="sxs-lookup"><span data-stu-id="a3658-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="a3658-108">當您建立新的資產 (例如，您之前[將檔案上傳](media-services-dotnet-upload-files.md))，您可以指定下列加密選項的 hello: **StorageEncrypted**， **CommonEncryptionProtected**，或**EnvelopeEncryptionProtected**。</span><span class="sxs-lookup"><span data-stu-id="a3658-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="a3658-109">當您傳遞資產 tooyour 用戶端時，您可以[設定的動態加密的資產 toobe](media-services-dotnet-configure-asset-delivery-policy.md)與 hello 下列兩個加密的其中一個： **DynamicEnvelopeEncryption**或**DynamicCommonEncryption**。</span><span class="sxs-lookup"><span data-stu-id="a3658-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="a3658-110">加密的資產有相關聯的 toobe **ContentKey**s。</span><span class="sxs-lookup"><span data-stu-id="a3658-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="a3658-111">本文說明如何 toocreate 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="a3658-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="a3658-112">當建立新**StorageEncrypted**資產使用 hello Media Services.NET SDK，hello **ContentKey**自動建立及連結與 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="a3658-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="a3658-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a3658-113">ContentKeyType</span></span>
<span data-ttu-id="a3658-114">其中一個 hello 值，您必須設定時建立內容金鑰是 hello 內容金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="a3658-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="a3658-115">選擇其中一個值的 hello。</span><span class="sxs-lookup"><span data-stu-id="a3658-115">Choose from one of hello following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <span data-ttu-id="a3658-116"><a id="envelope_contentkey"></a>建立信封類型 ContentKey</span><span class="sxs-lookup"><span data-stu-id="a3658-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="a3658-117">hello 下列程式碼片段會建立內容金鑰 hello 信封加密類型。</span><span class="sxs-lookup"><span data-stu-id="a3658-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="a3658-118">它接著將 hello 金鑰與 hello 指定資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a3658-118">It then associates hello key with hello specified asset.</span></span>

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

        asset.ContentKeys.Add(key);

        return key;
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

<span data-ttu-id="a3658-119">call</span><span class="sxs-lookup"><span data-stu-id="a3658-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="a3658-120"><a id="common_contentkey"></a>建立一般類型 ContentKey</span><span class="sxs-lookup"><span data-stu-id="a3658-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="a3658-121">hello 下列程式碼片段會建立內容金鑰 hello 一般加密類型。</span><span class="sxs-lookup"><span data-stu-id="a3658-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="a3658-122">它接著將 hello 金鑰與 hello 指定資產產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a3658-122">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
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
<span data-ttu-id="a3658-123">call</span><span class="sxs-lookup"><span data-stu-id="a3658-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="a3658-124">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a3658-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a3658-125">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a3658-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

