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
# <a name="create-contentkeys-with-net"></a>使用 .NET 建立 ContentKeys
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Media Services 可讓您 toocreate 和傳遞加密的資產。 A **ContentKey**提供安全地存取 tooyour**資產**s。 

當您建立新的資產 (例如，您之前[將檔案上傳](media-services-dotnet-upload-files.md))，您可以指定下列加密選項的 hello: **StorageEncrypted**， **CommonEncryptionProtected**，或**EnvelopeEncryptionProtected**。 

當您傳遞資產 tooyour 用戶端時，您可以[設定的動態加密的資產 toobe](media-services-dotnet-configure-asset-delivery-policy.md)與 hello 下列兩個加密的其中一個： **DynamicEnvelopeEncryption**或**DynamicCommonEncryption**。

加密的資產有相關聯的 toobe **ContentKey**s。 本文說明如何 toocreate 內容金鑰。

> [!NOTE]
> 當建立新**StorageEncrypted**資產使用 hello Media Services.NET SDK，hello **ContentKey**自動建立及連結與 hello 資產。
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
其中一個 hello 值，您必須設定時建立內容金鑰是 hello 內容金鑰類型。 選擇其中一個值的 hello。 

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

## <a id="envelope_contentkey"></a>建立信封類型 ContentKey
hello 下列程式碼片段會建立內容金鑰 hello 信封加密類型。 它接著將 hello 金鑰與 hello 指定資產產生關聯。

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

call

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>建立一般類型 ContentKey
hello 下列程式碼片段會建立內容金鑰 hello 一般加密類型。 它接著將 hello 金鑰與 hello 指定資產產生關聯。

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
call

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

