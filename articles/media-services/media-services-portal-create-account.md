---
title: "aaaCreate hello Azure 入口網站的 Azure Media Services 帳戶 |Microsoft 文件"
description: "本教學課程會引導您建立 Azure Media Services 帳戶以 hello Azure 入口網站的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>建立 Azure 媒體服務帳戶使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 
> 

hello Azure 入口網站提供 tooquickly 建立 Azure 媒體服務 (AMS) 帳戶的方法。 您可以使用您的帳戶 tooaccess Media Services 可讓您 toostore、 加密、 編碼、 管理和串流處理媒體內容，在 Azure 中。 在您建立 Media Services 帳戶 hello 階段，您也建立相關聯的儲存體帳戶 （或使用現有） 在 hello 與 hello Media Services 帳戶的相同地理區域。

本文說明常見的一些概念，並顯示 toocreate Media Services 帳戶以 hello Azure 入口網站的方式。

## <a name="concepts"></a>概念
存取媒體服務時需要有兩個相關聯的帳戶：

* 媒體服務帳戶。 您的帳戶可讓您存取 tooa 組以雲端為基礎的媒體服務，可在 Azure 中。 媒體服務帳戶並不會儲存實際媒體內容。 而它將 hello 媒體內容和媒體處理作業相關的中繼資料儲存在您的帳戶。 在您建立 hello 帳戶 hello 階段，您可以選取可用的 Media Services 地區。 您選取的 hello 區是儲存您的帳戶的 hello 中繼資料記錄的資料中心。
  
* 一個 Azure 儲存體帳戶。 儲存體帳戶必須位於 hello 與 hello Media Services 帳戶的相同地理區域。 當您建立 Media Services 帳戶時，您可以選擇現有的儲存體帳戶在 hello 相同的區域，或您可以建立新的儲存體帳戶中 hello 相同的區域。 如果您刪除 Media Services 帳戶時，不會刪除相關的儲存體帳戶中的 hello blob。

> [!NOTE]
> 如需不同區域中 Azure 媒體服務功能可用性的資訊，請參閱[跨資料中心的 AMS 功能可用性](scenarios-and-availability.md#availability)。

## <a name="create-an-ams-account"></a>建立 AMS 帳戶
hello 步驟，在這個主題顯示如何 toocreate AMS 帳戶。

1. 在 hello 登入[Azure 入口網站](https://portal.azure.com/)。
2. 按一下 [+新增] > [Web + 行動] > [媒體服務]。
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new1.png)
3. 在 [建立媒體服務帳戶]  中輸入必要的值。
   
    ![建立媒體服務](./media/media-services-create-account/media-services-new3.png)
   
   1. 在**帳戶名稱**，輸入 hello hello 新 AMS 帳戶名稱。 Media Services 帳戶名稱是所有小寫字母或數字，不含空格，也 3 too24 個字元的長度。
   2. 在訂用帳戶，請在 hello 不同 Azure 訂用帳戶具有存取權之中選取。
   3. 在**資源群組**，選取 hello 新的或現有的資源。  資源群組是共用生命週期、權限及原則的資源集合。 [在此](../azure-resource-manager/resource-group-overview.md#resource-groups)深入了解。
   4. 在**位置**，選取 hello 將會使用的 toostore hello 媒體和中繼資料記錄您的 Media Services 帳戶的地理區域。 此區域會使用的 tooprocess 並串流媒體。 只有 hello 可用媒體服務區域會出現在 [hello] 下拉式清單方塊中。 
   5. 在**儲存體帳戶**，Media Services 帳戶從選取的儲存體帳戶 tooprovide blob 儲存體的 hello 媒體內容。 您可以在 hello 中選取現有的儲存體帳戶相同的地理區域，為您的 Media Services 帳戶，或您可以建立儲存體帳戶。 新的儲存體帳戶會在 hello 相同區域。 儲存體帳戶名稱的 hello 規則 hello 相同與 Media Services 帳戶。
      
       在 [這裡](../storage/common/storage-introduction.md)深入了解儲存體。
   6. 選取**Pin toodashboard** toosee hello hello 帳戶部署進度。
4. 按一下**建立**在 hello hello 表單底部。
   
    已成功建立 hello 帳戶之後, 載入概觀 頁面。 Hello 串流端點資料表 hello 帳戶會有預設串流端點在 hello**已停止**狀態。 

    >[!NOTE]
    >AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 
   
## <a name="toomanage-your-ams-account"></a>toomanage AMS 帳戶

toomanage AMS 帳戶 （例如，連接 toohello AMS API 以程式設計方式、 上傳影片、 編碼資產、 設定內容保護、 監視作業進度） 選取**設定**上 hello hello 入口網站的左側。 從 hello**設定**，瀏覽 tooone 的 hello 可用刀鋒視窗 (例如： **API 存取**，**資產**，**作業**， **內容保護**)。


## <a name="next-steps"></a>後續步驟

您現在可以將檔案上傳到 AMS 帳戶。 如需詳細資訊，請參閱 [上傳檔案](media-services-portal-upload-files.md)。

如果您計劃 tooaccess AMS API 以程式設計的方式，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

