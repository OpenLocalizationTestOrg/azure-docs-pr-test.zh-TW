---
title: "匯出工作的 Azure 匯入/匯出 aaaCreate |Microsoft 文件"
description: "了解 toocreate 匯出的 hello Microsoft Azure 匯入/匯出服務的工作。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>建立匯出工作的 hello Azure 匯入/匯出服務
建立匯出工作使用 hello REST API 的 hello Microsoft Azure 匯入/匯出服務包括 hello 下列步驟：

-   選取 hello blob tooexport。

-   取得寄送位置。

-   建立 hello 匯出工作。

-   傳送您的空磁碟機 tooMicrosoft 透過支援的貨運服務。

-   使用 hello 封裝資訊更新 hello 匯出作業。

-   從 Microsoft 接收 hello 磁碟機。

 請參閱[使用 hello Windows Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)概觀 hello 匯入/匯出服務和教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com/)toocreate 及管理匯入和匯出工作。

## <a name="selecting-blobs-tooexport"></a>選取 blob tooexport
 toocreate 匯出工作，您將需要 tooprovide 的 tooexport 從儲存體帳戶的 blob 清單。 有幾種方式 tooselect blob toobe 匯出：

-   您可以使用相對 blob 路徑 tooselect 單一 blob 和其所有快照集。

-   您可以使用相對 blob 路徑 tooselect 單一 blob 但排除其快照集。

-   您可以使用相對 blob 路徑和快照集時間 tooselect 單一快照集。

-   可以使用 blob 前置詞 tooselect 所有 blob 和快照集，以指定前置詞的 hello。

-   您可以匯出所有 blob 和快照 hello 儲存體帳戶中。

 如需有關指定 blob tooexport，請參閱 < hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。

## <a name="obtaining-your-shipping-location"></a>取得寄送位置
在建立匯出工作之前，您需要 tooobtain 寄送地點名稱和地址的呼叫 hello[取得位置](https://portal.azure.com)或[列出位置](/rest/api/storageimportexport/listlocations)作業。 `List Locations` 會傳回位置及其郵寄地址的清單。 您可以從 hello 傳回清單中選取位置並寄送您的硬碟機 toothat 地址。 您也可以使用 hello`Get Location`作業 tooobtain hello 直接傳送的特定位置的位址。

請遵循以下 tooobtain hello 傳送位置 hello 步驟：

-   識別 hello hello 位置的儲存體帳戶名稱。 這個值可以找到 hello**位置**hello 儲存體帳戶的欄位**儀表板**hello 傳統入口網站或使用 hello 服務管理 API 作業的查詢中[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)。

-   擷取 hello 位置的可用 tooprocess 這個儲存體帳戶呼叫 hello`Get Location`作業。

-   如果 hello `AlternateLocations` hello 位置包含 hello 位置本身，則無妨 toouse 這個位置。 否則，呼叫 hello`Get Location`使用其中一個 hello 替代位置，然後再次的作業。 維護可能暫時關閉 hello 原始位置。

## <a name="creating-hello-export-job"></a>建立 hello 匯出工作
 toocreate hello 匯出工作，呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。 您需要下列資訊 tooprovide hello:

-   Hello 工作的名稱。

-   hello 儲存體帳戶名稱。

-   hello 傳送 hello 上一個步驟中取得的位置名稱。

-   作業類型 (匯出)。

-   hello 傳回位址 hello 匯出作業完成之後，傳送 hello 磁碟機。

-   hello 的 blob （或 blob 首碼） 清單 toobe 匯出。

## <a name="shipping-your-drives"></a>寄送您的磁碟機
 接著，使用的磁碟機需要 toosend，根據您已選取 toobe 匯出的 hello blob hello Azure 匯入/匯出工具 toodetermine hello 數目並 hello 磁碟機大小。 請參閱 hello [Azure 匯入/匯出工具參考](storage-import-export-tool-how-to-v1.md)如需詳細資訊。

 封裝在單一封裝 hello 磁碟機，並將它們寄送 toohello hello 中取得的地址稍早步驟。 請注意 hello 追蹤您的封裝進行 hello 下一個步驟的數目。

> [!NOTE]
>  您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。

## <a name="updating-hello-export-job-with-your-package-information"></a>使用您的封裝資訊更新 hello 匯出作業
 取得追蹤號碼之後，請呼叫 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業 tooupdated hello 電信業者名稱和追蹤號碼 hello 作業。 您可以選擇性地指定 hello 磁碟機數目、 hello 傳回位址及 hello 寄送日期。

## <a name="receiving-hello-package"></a>收到 hello 封裝
 匯出作業處理完成之後，您的磁碟機將會傳回 tooyou 與加密的資料。 您可以針對每個由呼叫 hello hello 磁碟機擷取 hello BitLocker 金鑰[Get Job](/rest/api/storageimportexport/jobs#Jobs_Get)作業。 然後您就可以解除鎖定使用 hello 金鑰 hello 磁碟機。 hello 每個磁碟機上的磁碟機資訊清單檔包含 hello hello 磁碟機，以及 hello 原始 blob 位址上的每個檔案的檔案清單。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)
