---
title: "依國家/地區的 Azure CDN 內容 aaaRestrict |Microsoft 文件"
description: "了解如何 toorestrict 存取 tooyour Azure CDN 內容使用 hello 地理篩選功能。"
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>依國家/地區限制 Azure CDN 內容

## <a name="overview"></a>概觀
當使用者要求您的內容，根據預設時，會提供 hello 內容，不論 hello 使用者進行此要求的位置。 在某些情況下，您可以依國家/地區的 toorestrict 存取 tooyour 內容。 本主題說明如何 toouse hello**地理篩選**順序 tooconfigure hello 服務 tooallow 或封鎖存取依國家/地區中的功能。

> [!IMPORTANT]
> hello Verizon 和 Akamai 產品提供 hello 相同的地理篩選功能，但有 te 它們支援的國家/地區碼上有些許不同。 針對連結 toohello 差異，請參閱步驟 3。


如需適用於 tooconfiguring 考量這種類型的限制，請參閱 hello[考量](cdn-restrict-access-by-country.md#considerations)hello hello 主題結尾的區段。  

![國家 (地區) 篩選](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>步驟 1： 定義 hello 目錄路徑
選取您的端點內 hello 入口網站，並尋找 hello 地理篩選索引標籤上 hello 左側導覽 toofind 這項功能。

在設定的國家 （地區） 篩選器時，您必須指定將允許或拒絕存取 hello 相對路徑 toohello 位置 toowhich 的使用者。 您可以使用 "/"，或藉由指定目錄路徑 "/pictures/" 來選取資料夾，為所有檔案套用地區篩選。 您也可以套用地理篩選 tooa 單一檔案 hello 檔案指定並留下任何 hello 結尾斜線"/ pictures/city.png"。

目錄路徑篩選器範例：

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>步驟 2： 定義 hello 動作： 封鎖或允許
**禁止：** hello 使用者指定的國家 （地區） 將會遭到拒絕存取 tooassets 要求從該遞迴路徑。 若尚未設定該位置的其他國家 (地區) 篩選選項，則其他所有使用者都將允許存取。

**允許：**只有 hello 的使用者指定的國家 （地區），都可以存取 tooassets 要求從該遞迴路徑。

## <a name="step-3-define-hello-countries"></a>步驟 3： 定義 hello 國家 （地區）
選取您想 tooblock 或 hello 路徑允許的 hello 國家/地區。 

例如，封鎖 /Photos/Strasbourg/hello 規則會篩選檔案包括：

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>國碼
hello**地理篩選**功能使用國家/地區代碼 toodefine hello 國家 （地區） 的要求將會允許或封鎖受保護的目錄。 您會發現 hello 中的國家/地區代碼[Azure CDN 國家/地區代碼](https://msdn.microsoft.com/library/mt761717.aspx)。 

## <a id="considerations"></a>考量
* 它可能會佔用 too90 Verizon、 分鐘或幾分鐘 Akamai，以變更 tooyour 國家 （地區） 篩選組態 tootake 效果。
* 這項功能不支援萬用字元 (例如，‘*’)。
* hello 相對路徑相關聯的 hello 地理篩選組態將會遞迴地套用的 toothat 路徑。
* 只要一個規則可套用的 toohello 相同的相對路徑 (您無法建立多個國家 （地區） 篩選該點 toohello 相同的相對路徑。 不過，一個資料夾可有多個國家 (地區) 篩選。 這是因為國家 （地區） 篩選器 toohello 遞迴性質。 換句話說，可以將不同的國家 (地區) 篩選指派給先前設定之資料夾的子資料夾。

