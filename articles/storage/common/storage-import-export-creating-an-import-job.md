---
title: "匯入工作的 Azure 匯入/匯出 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate hello Microsoft Azure 匯入/匯出服務的匯入。"
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>建立 hello Azure 匯入/匯出服務的匯入工作

建立使用 hello REST API 的 hello Microsoft Azure 匯入/匯出服務匯入工作包括下列步驟的 hello:

-   準備磁碟機以 hello Azure 匯入/匯出工具。

-   取得 hello 位置 toowhich tooship hello 磁碟機。

-   建立 hello 匯入工作。

-   傳送嗨光碟機 tooMicrosoft 透過支援的貨運服務。

-   使用 傳送詳細資料的 hello 更新 hello 匯入作業。

 請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)概觀 hello 匯入/匯出服務和教學課程示範如何 toouse hello [Azure 入口網站](https://portal.azure.com/)toocreate 及管理匯入和匯出工作。

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>使用 Azure 匯入/匯出工具 hello 準備磁碟機

匯入工作的 hello 步驟 tooprepare 磁碟機是 hello 相同您要建立 hello jobvia hello 入口網站或透過 hello REST API。

以下是磁碟機準備的簡要概觀。 請參閱 toohello [Azure 匯入 ExportTool 參考](storage-import-export-tool-how-to-v1.md)如需完整指示。 您可以下載 Azure 匯入/匯出工具 hello[這裡](http://go.microsoft.com/fwlink/?LinkID=301900)。

準備您的磁碟機包含︰

-   用來識別 hello 資料 toobe 匯入。

-   識別 Windows Azure 儲存體中的 hello 目的地 blob。

-   在使用 hello Azure 匯入/匯出工具 toocopy 資料 tooone 或多個硬碟。

 已準備好為其 hello Azure 匯入/匯出工具也會針對每個 hello 磁碟機產生資訊清單檔案。 資訊清單檔案包含︰

-   列舉所有要上傳並從這些檔案 tooblobs hello 對應的 hello 檔案中。

-   每個檔案的 hello 區段的總和檢查碼。

-   Hello 與每個 blob 的中繼資料和屬性 tooassociate 的相關資訊。

-   列出的 hello 動作 tootake hello 正在上傳的 blob 有相同的名稱，為 hello 容器中現有的 blob。 可能的選項包括： a） 檔案，覆寫 hello blob hello、 b） 保留 hello 現有 blob 和略過上傳 hello 檔案、 c） 新增後置詞 toohello 名稱，使它不會使用其他檔案衝突。

## <a name="obtaining-your-shipping-location"></a>取得寄送位置

在建立匯入工作之前，您需要 tooobtain 寄送地點名稱和地址的呼叫 hello[列出位置](/rest/api/storageimportexport/listlocations)作業。 `List Locations` 會傳回位置及其郵寄地址的清單。 您可以從 hello 傳回清單中選取位置並寄送您的硬碟機 toothat 地址。 您也可以使用 hello`Get Location`作業 tooobtain hello 直接傳送的特定位置的位址。

 請遵循以下 tooobtain hello 傳送位置 hello 步驟：

-   識別 hello hello 位置的儲存體帳戶名稱。 這個值可以找到 hello**位置**hello 儲存體帳戶的欄位**儀表板**hello Azure 入口網站或使用 hello 服務管理 API 作業的查詢中[取得儲存體帳戶屬性](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)。

-   擷取可用 tooprocess hello 位置這個儲存體帳戶呼叫 hello`Get Location`作業。

-   如果 hello `AlternateLocations` hello 位置包含 hello 位置本身，則無妨 toouse 這個位置。 否則，呼叫 hello`Get Location`使用其中一個 hello 替代位置，然後再次的作業。 維護可能暫時關閉 hello 原始位置。

## <a name="creating-hello-import-job"></a>建立 hello 匯入工作
toocreate hello 匯入工作，呼叫 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。 您需要下列資訊 tooprovide hello:

-   Hello 工作的名稱。

-   hello 儲存體帳戶名稱。

-   hello 傳送 hello 上一個步驟中取得的位置名稱。

-   作業類型 (匯入)。

-   hello 傳回位址 hello 匯入作業完成之後，傳送 hello 磁碟機。

-   hello hello 作業中的磁碟機清單。 每個磁碟機，您必須加入 hello 下列 hello 磁碟機準備步驟期間取得的資訊：

    -   hello 磁碟機識別碼

    -   hello BitLocker 金鑰

    -   hello hello 硬碟機上的資訊清單檔案相對路徑

    -   hello Base16 編碼資訊清單檔案的 MD5 雜湊

## <a name="shipping-your-drives"></a>寄送您的磁碟機
您必須提供您取自 hello 先前步驟中，您的磁碟機 toohello 地址，而且您必須提供 hello 匯入/匯出服務以 hello 追蹤 hello 封裝的數目。

> [!NOTE]
>  您必須透過支援的貨運服務公司 (會提供您的包裹追蹤號碼) 寄送您的磁碟機。

## <a name="updating-hello-import-job-with-your-shipping-information"></a>使用 出貨資訊更新 hello 匯入作業
取得追蹤號碼之後，請呼叫 hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update)作業 tooupdate hello 傳送貨運公司名稱、 hello hello 作業的追蹤號碼與退貨 hello 承運業者帳戶號碼。 您可以選擇指定磁碟機和出貨日期以及 hello 的 hello 數目。

## <a name="next-steps"></a>後續步驟

* [使用 hello 匯入/匯出服務 REST API](storage-import-export-using-the-rest-api.md)
