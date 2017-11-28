---
title: "使用 .NET 建立 ContentKeys"
description: "了解如何建立提供資產安全存取的內容金鑰。"
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
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="dd64e-103">使用 .NET 建立 ContentKeys</span><span class="sxs-lookup"><span data-stu-id="dd64e-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd64e-104">REST</span><span class="sxs-lookup"><span data-stu-id="dd64e-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="dd64e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="dd64e-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="dd64e-106">媒體服務可讓您建立資產及傳遞已加密的資產。</span><span class="sxs-lookup"><span data-stu-id="dd64e-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="dd64e-107">**ContentKey** 提供**資產**的安全存取。</span><span class="sxs-lookup"><span data-stu-id="dd64e-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="dd64e-108">當您建立新的資產時 (例如，[將檔案上傳](media-services-dotnet-upload-files.md)之前)，您可以指定下列加密選項：**StorageEncrypted**、**CommonEncryptionProtected** 或 **EnvelopeEncryptionProtected**。</span><span class="sxs-lookup"><span data-stu-id="dd64e-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="dd64e-109">當您將資產傳遞至您的用戶端時，您可以使用下列兩個加密的其中一個[設定動態加密的資產](media-services-dotnet-configure-asset-delivery-policy.md)：**DynamicEnvelopeEncryption** 或 **DynamicCommonEncryption**。</span><span class="sxs-lookup"><span data-stu-id="dd64e-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="dd64e-110">加密的資產必須與 **ContentKey**相關聯。</span><span class="sxs-lookup"><span data-stu-id="dd64e-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="dd64e-111">本文說明如何建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd64e-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="dd64e-112">使用 Media Services .NET SDK 建立新的 **StorageEncrypted** 資產時，會自動建立 **ContentKey**，並將其與資產連結。</span><span class="sxs-lookup"><span data-stu-id="dd64e-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="dd64e-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="dd64e-113">ContentKeyType</span></span>
<span data-ttu-id="dd64e-114">您在建立內容金鑰時必須設定的其中一個值就是內容金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="dd64e-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="dd64e-115">選擇下列值之一。</span><span class="sxs-lookup"><span data-stu-id="dd64e-115">Choose from one of the following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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

## <span data-ttu-id="dd64e-116"><a id="envelope_contentkey"></a>建立信封類型 ContentKey</span><span class="sxs-lookup"><span data-stu-id="dd64e-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="dd64e-117">下列程式碼片段會建立信封加密類型的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd64e-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="dd64e-118">然後建立金鑰與所指定資產的關聯。</span><span class="sxs-lookup"><span data-stu-id="dd64e-118">It then associates the key with the specified asset.</span></span>

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

<span data-ttu-id="dd64e-119">call</span><span class="sxs-lookup"><span data-stu-id="dd64e-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="dd64e-120"><a id="common_contentkey"></a>建立一般類型 ContentKey</span><span class="sxs-lookup"><span data-stu-id="dd64e-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="dd64e-121">下列程式碼片段會建立一般加密類型的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="dd64e-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="dd64e-122">然後建立金鑰與所指定資產的關聯。</span><span class="sxs-lookup"><span data-stu-id="dd64e-122">It then associates the key with the specified asset.</span></span>

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

        // Associate the key with the asset.
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
<span data-ttu-id="dd64e-123">call</span><span class="sxs-lookup"><span data-stu-id="dd64e-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="dd64e-124">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="dd64e-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd64e-125">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="dd64e-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

