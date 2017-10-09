---
title: "aaaAzure 匯入/匯出資訊清單檔案格式 |Microsoft 文件"
description: "了解 hello hello 磁碟機資訊清單檔案格式，以描述 Azure Blob 儲存體中的 blob 與 hello 匯入/匯出服務中的匯入或匯出作業中的磁碟機上的檔案之間的 hello 對應。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Azure 匯入/匯出服務資訊清單檔案格式
hello 磁碟機資訊清單檔描述 Azure Blob 儲存體中的 blob 和組成匯入或匯出工作的磁碟機上的檔案之間的 hello 對應。 匯入作業，hello 資訊清單檔案會建立 hello 磁碟機準備程序的一部分，而且 hello 機寄送 toohello Azure 資料中心之前儲存在 hello 磁碟機上。 匯出作業期間，會建立 hello 資訊清單，並將其儲存在 hello 磁碟機上的 hello Azure 匯入/匯出服務中。  
  
同時匯入和匯出工作，hello 磁碟機資訊清單檔案會儲存在 hello 匯入或匯出磁碟機。它不是傳輸 toohello 服務透過任何 API 作業。  
  
hello 以下描述 hello 的磁碟機資訊清單檔的一般格式：  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>資訊清單的 XML 元素和屬性

下表中的 hello 中指定 hello 磁碟機資訊清單 XML 格式的 hello 資料元素和屬性。  
  
|XML 元素|類型|說明|  
|-----------------|----------|-----------------|  
|`DriveManifest`|根元素|hello hello 資訊清單檔案的根項目。 Hello 檔案中的其他所有項目是這個項目下方。|  
|`Version`|屬性、字串|hello hello 資訊清單檔案版本。|  
|`Drive`|巢狀的 XML 元素|包含每個磁碟機的 hello 資訊清單。|  
|`DriveId`|String|hello hello 磁碟機的唯一磁碟機識別碼。 藉由查詢 hello 磁碟機序號找到 hello 磁碟機識別元。 hello 磁碟機序號通常會印 hello 之外 hello 磁碟機。 hello`DriveID`項目必須出現在任何之前`BlobList`hello 資訊清單檔中的項目。|  
|`StorageAccountKey`|String|如果未指定 (且只有在未指定) `ContainerSas` 時，才需為匯入工作指定。 與 hello 工作相關聯的 hello hello Azure 儲存體帳戶的帳戶金鑰。<br /><br /> Hello 匯出作業的資訊清單中，會省略這個項目。|  
|`ContainerSas`|String|如果未指定 (且只有在未指定) `StorageAccountKey` 時，才需為匯入工作指定。 用於存取與 hello 工作相關聯的 hello blob hello 容器 SAS。 請參閱[Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)其格式。Hello 匯出作業的資訊清單中，會省略這個項目。|  
|`ClientCreator`|String|指定 hello 用戶端建立 hello XML 檔案。 Hello 匯入/匯出服務不會解譯這個值。|  
|`BlobList`|巢狀的 XML 元素|包含 blob 的一部分 hello 匯入或匯出工作的清單。 Blob 清單中的每個 blob 共用 hello 相同的中繼資料和屬性。|  
|`BlobList/MetadataPath`|String|選用。 指定 hello 包含將設定匯入作業的 hello blob 清單中的 hello 預設中繼資料的 hello 磁碟上的檔案相對路徑。 您可以選擇以個別的 Blob 為基礎來覆寫此中繼資料。<br /><br /> Hello 匯出作業的資訊清單中，會省略這個項目。|  
|`BlobList/MetadataPath/@Hash`|屬性、字串|指定 hello hello 中繼資料檔的 Base16 編碼 MD5 雜湊值。|  
|`BlobList/PropertiesPath`|String|選用。 指定 hello 包含 hello 預設屬性，將設定匯入作業的 hello blob 清單中的 hello 磁碟上的檔案相對路徑。 您可以選擇以個別的 Blob 為基礎來覆寫這些屬性。<br /><br /> Hello 匯出作業的資訊清單中，會省略這個項目。|  
|`BlobList/PropertiesPath/@Hash`|屬性、字串|指定 hello hello 屬性檔的 Base16 編碼 MD5 雜湊值。|  
|`Blob`|巢狀的 XML 元素|包含每個 Blob 清單中的每個 Blob 的相關資訊。|  
|`Blob/BlobPath`|String|hello 相對 URI toohello blob，並 hello 容器名稱開頭。 如果 hello blob 在根容器，它的開頭必須`$root`。|  
|`Blob/FilePath`|String|指定 hello 相對路徑 toohello 檔案 hello 磁碟機上。 匯出工作 hello blob 路徑將用於盡可能; hello 檔案路徑*例如*，`pictures/bob/wild/desert.jpg`將太匯出`\pictures\bob\wild\desert.jpg`。 不過，由於 NTFS 名稱的 toohello 限制，blob 可能是匯出的 tooa 檔案，不像 hello blob 路徑的路徑。|  
|`Blob/ClientData`|String|選用。 包含來自 hello 客戶的意見。 Hello 匯入/匯出服務不會解譯這個值。|  
|`Blob/Snapshot`|DateTime|如為匯出工作則為選擇性。 指定匯出的 blob 快照集的 hello 快照集識別碼。|  
|`Blob/Length`|Integer|指定 hello 的 hello blob 的總長度，以位元組為單位。 hello 值可能是區塊 blob 的 too200 GB 和向上 too1 TB 的分頁 blob。 對於分頁 Blob，此值需為 512 的倍數。|  
|`Blob/ImportDisposition`|String|如為匯入工作則為選擇性，匯出工作可省略。 這會指定 hello 匯入/匯出服務應該如何處理 hello 匯入工作的情況下所在相同的名稱，已經 hello 的 blob。 如果省略此值從 hello 匯入資訊清單，hello 預設值是`rename`。<br /><br /> 這個項目 hello 值包括：<br /><br /> -   `no-overwrite`： 如果目的地 blob 已存在於 hello 與相同的名稱，hello 匯入作業將會略過匯入此檔案。<br />-   `overwrite`： 任何現有的目的地 blob 會完全被 hello 新匯入檔案。<br />-   `rename`: hello 新的 blob 將上傳修改過的名稱。<br /><br /> hello 重新命名規則如下所示：<br /><br /> -如果 hello blob 名稱未包含點，會產生新的名稱附加`(2)`toohello 原始 blob 名稱; 這個新的名稱也發生衝突時的現有 blob 名稱，然後`(3)`附加取代`(2)`等等。<br />-如果 hello blob 名稱包含句點，hello 部份 hello 最後一個點視為 hello 延伸模組名稱。 上述程序，類似 toohello`(2)`插入之前 hello 最後一個點 toogenerate 新的名稱; 如果與現有的 blob 名稱仍然衝突 hello 新名稱，然後 hello 服務會嘗試`(3)`， `(4)`，依此類推，直到非衝突找到名稱。<br /><br /> 部分範例如下：<br /><br /> hello blob`BlobNameWithoutDot`將重新命名為：<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> hello blob`Seattle.jpg`將重新命名為：<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|巢狀的 XML 元素|分頁 Blob 的必要元素。<br /><br /> 匯入作業，請指定匯入檔案 toobe 位元範圍的清單。 每個頁面範圍的位移和長度 hello 描述 hello 頁面範圍，以及 hello 地區的 MD5 雜湊的原始程式檔中所描述。 hello`Hash`是必要的頁面範圍的屬性。 hello 服務將會驗證 hello hello blob 中的 hello 資料雜湊比對從 hello 頁面範圍的 hello 計算 MD5 雜湊。 任何頁面範圍的數目可能會使用的 toodescribe 匯入，與 hello 向上 too1 TB 的總大小的檔案。 所有頁面範圍必須按照位移排序，且不允許任何重疊。<br /><br /> 匯出作業，您可以指定一組 blob 的位元組範圍已匯出 toohello 磁碟機。<br /><br /> 一起 hello 頁面範圍可能涵蓋只有子範圍的 blob 或檔案。  預期 hello hello 檔案未包含任何頁面範圍的其餘部分，而且其內容可以是未定義。|  
|`PageRange`|XML 元素|代表頁面範圍。|  
|`PageRange/@Offset`|屬性、整數|指定在 hello 傳輸檔案和 hello hello 其中指定頁面範圍的 blob 中的 hello 位移開始。 此值需為 512 的倍數。|  
|`PageRange/@Length`|屬性、整數|指定 hello hello 頁面範圍長度。 此值需為 512 的倍數，且不得超過 4 MB。|  
|`PageRange/@Hash`|屬性、字串|指定 hello hello 頁面範圍的 Base16 編碼 MD5 雜湊值。|  
|`BlockList`|巢狀的 XML 元素|含有具名區塊的區塊 Blob 的必要元素。<br /><br /> 匯入作業，hello 的區塊清單會指定一組區塊將會匯入至 Azure 儲存體。 匯出作業，hello 的區塊清單會指定每個區塊已儲存在 hello 匯出磁碟機上的 hello 檔案中。 每個區塊稱為 hello 檔案和區塊長度; 中的位移每個區塊以區塊 ID 屬性，此外命名，並包含 hello 區塊的 MD5 雜湊。 向上 too50，000 區塊可能使用的 toodescribe blob。  所有區塊都必須都排序位移，同時應該涵蓋 hello 的 hello 檔案的完整範圍*也就是*，區塊之間必須有任何間距。 如果 hello blob 不超過 64 MB，hello 區塊識別碼的每個區塊必須是全部不存在，或所有已存在。 區塊識別碼是必要的 toobe Base64 編碼的字串。 請參閱 [Put Block](/rest/api/storageservices/put-block)以了解區塊識別碼的進一步需求。|  
|`Block`|XML 元素|代表區塊。|  
|`Block/@Offset`|屬性、整數|指定 hello hello 指定的區塊的開始處的位移。|  
|`Block/@Length`|屬性、整數|指定 hello 區塊; 中的 hello 的位元組數目此值必須是不超過 4 MB。|  
|`Block/@Id`|屬性、字串|指定代表 hello hello 區塊的區塊識別碼的字串。|  
|`Block/@Hash`|屬性、字串|指定 hello 的 hello 區塊的 Base16 編碼 MD5 雜湊。|  
|`Blob/MetadataPath`|String|選用。 指定 hello 的中繼資料檔案的相對路徑。 在匯入時，hello 目的地 blob 上設定 hello 中繼資料。 匯出作業期間，hello blob 的中繼資料會儲存在 hello hello 磁碟機上的中繼資料檔案。|  
|`Blob/MetadataPath/@Hash`|屬性、字串|指定 hello hello blob 的中繼資料檔案的 Base16 編碼 MD5 雜湊。|  
|`Blob/PropertiesPath`|String|選用。 指定 hello 屬性檔的相對路徑。 在匯入時，會在 hello 目的地 blob 上設定 hello 屬性。 匯出作業期間，hello blob 屬性會儲存在 hello hello 磁碟機上的內容檔案。|  
|`Blob/PropertiesPath/@Hash`|屬性、字串|指定 hello hello blob 的內容檔案的 Base16 編碼 MD5 雜湊。|  
  
## <a name="next-steps"></a>後續步驟
 
* [儲存體匯入/匯出 REST API](/rest/api/storageimportexport/)
