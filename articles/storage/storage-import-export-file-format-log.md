---
title: "aaaAzure 匯入/匯出記錄檔檔案格式 |Microsoft 文件"
description: "深入了解 hello hello 建立之記錄檔的步驟執行匯入/匯出服務作業時的格式。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Azure 匯入/匯出服務記錄檔格式
當 hello Microsoft Azure 匯入/匯出服務磁碟機上執行的動作，匯入工作或匯出工作的一部分時，記錄檔寫入 tooblock blob hello 與該工作相關聯的儲存體帳戶中。  
  
有兩個可能 hello 匯入/匯出服務所寫入的記錄檔：  
  
-   hello 錯誤事件中，一定會產生 hello 錯誤記錄檔。  
  
-   hello 詳細資訊記錄檔未啟用依預設，但是可能加以啟用設定 hello`EnableVerboseLog`屬性[Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)或[Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update)作業。  
  
## <a name="log-file-location"></a>記錄檔位置  
hello 記錄檔寫入 tooblock blob hello 容器或 hello 所指定的虛擬目錄中`ImportExportStatesPath`設定，您可以設定`Put Job`作業。 hello 位置 toowhich hello 記錄檔寫入取決於如何指定 hello 作業，以及指定 hello 值驗證`ImportExportStatesPath`。 您可以透過儲存體帳戶金鑰或容器 SAS （共用的存取簽章） 指定 hello 工作的驗證。  
  
hello hello 容器或虛擬目錄的名稱可能是預設名稱 hello `waimportexport`，或另一個容器或您指定的虛擬目錄名稱。  
  
hello 下表顯示 hello 可能的選項：  
  
|驗證方法|`ImportExportStatesPath` 元素的值|記錄檔 Blob 的位置|  
|---------------------------|----------------------------------------------|---------------------------|  
|儲存體帳戶金鑰|預設值|名為的容器`waimportexport`，這是 hello 預設容器。 例如：<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|儲存體帳戶金鑰|使用者指定值|名為 hello 使用者的容器。 例如：<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|容器 SAS|預設值|命名的虛擬目錄`waimportexport`，這是 hello hello SAS 中指定的容器下方的 hello 預設名稱。<br /><br /> 例如，如果 hello SAS 指定 hello 工作是`https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，則會是 hello 記錄檔位置`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|容器 SAS|使用者指定值|由 hello hello SAS 中指定的容器下方的 hello 使用者命名的虛擬目錄。<br /><br /> 例如，如果 hello SAS 指定 hello 工作是`https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`，而且 hello 可讓您指定虛擬目錄叫作`mylogblobs`，hello 記錄檔位置將是`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`。|  
  
您可以擷取 hello 錯誤和詳細資訊記錄檔的 hello URL 呼叫 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate)作業。 hello 磁碟機處理完成後，並提供 hello 記錄。  
  
## <a name="log-file-format"></a>記錄檔格式  
hello 這兩個記錄的格式是 hello 相同： blob，其中包含的 hello 事件複製 hello 硬碟機和 hello 客戶帳戶之間的 blob 時所發生的 XML 描述。  
  
hello 詳細資訊記錄檔包含 hello 複製作業，每個 blob （用於匯入工作） 或 （適用於匯出工作），檔案的 hello 狀態的完整資訊，而 hello 錯誤記錄檔只包含 hello 資訊之 blob 或 hello 期間發生錯誤的檔案匯入或匯出工作。  
  
hello 詳細資訊記錄檔格式如下所示。 hello 錯誤記錄檔有的 hello 相同結構，但是它會篩選出成功的作業。  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

hello 下表描述 hello hello 記錄檔項目。  
  
|XML 元素|類型|說明|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML 元素|代表磁碟機記錄檔。|  
|`Version`|屬性、字串|hello hello 記錄格式版本。|  
|`DriveId`|String|hello 磁碟機的硬體序號。|  
|`Status`|String|Hello 磁碟機處理的狀態。 請參閱 hello`Drive Status Codes`表格如需詳細資訊。|  
|`Blob`|巢狀的 XML 元素|代表 Blob。|  
|`Blob/BlobPath`|String|hello hello blob 的 URI。|  
|`Blob/FilePath`|String|hello 相對路徑 toohello hello 磁碟機檔案。|  
|`Blob/Snapshot`|DateTime|hello hello blob，僅限於匯出工作的快照集版本。|  
|`Blob/Length`|Integer|hello 的 hello blob 以位元組為單位的總長度。|  
|`Blob/LastModified`|DateTime|hello 日期/時間 hello blob 上次修改僅限於匯出工作。|  
|`Blob/ImportDisposition`|String|hello 匯入的 hello blob，僅限於匯入工作的配置。|  
|`Blob/ImportDisposition/@Status`|屬性、字串|hello hello 狀態匯入配置。|  
|`PageRangeList`|巢狀的 XML 元素|代表分頁 Blob 的頁面範圍清單。|  
|`PageRange`|XML 元素|代表頁面範圍。|  
|`PageRange/@Offset`|屬性、整數|Hello blob 中的起始位移 hello 頁面範圍。|  
|`PageRange/@Length`|屬性、整數|以位元組為單位的 hello 頁面範圍的長度。|  
|`PageRange/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 頁面範圍。|  
|`PageRange/@Status`|屬性、字串|處理 hello 頁面範圍的狀態。|  
|`BlockList`|巢狀的 XML 元素|代表區塊 Blob 的區塊清單。|  
|`Block`|XML 元素|代表區塊。|  
|`Block/@Offset`|屬性、整數|Hello blob 中的 hello 區塊起始位移。|  
|`Block/@Length`|屬性、整數|以位元組為單位的 hello 區塊的長度。|  
|`Block/@Id`|屬性、字串|hello 區塊識別碼。|  
|`Block/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 區塊。|  
|`Block/@Status`|屬性、字串|處理 hello 區塊的狀態。|  
|`Metadata`|巢狀的 XML 元素|代表 hello blob 的中繼資料。|  
|`Metadata/@Status`|屬性、字串|Hello blob 中繼資料的處理狀態。|  
|`Metadata/GlobalPath`|String|相對路徑 toohello 全域中繼資料檔案。|  
|`Metadata/GlobalPath/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 全域中繼資料檔案。|  
|`Metadata/Path`|String|相對路徑 toohello 中繼資料檔案。|  
|`Metadata/Path/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 中繼資料檔案。|  
|`Properties`|巢狀的 XML 元素|代表 hello blob 屬性。|  
|`Properties/@Status`|屬性、字串|狀態處理 hello blob 屬性，例如找不到檔案，已完成。|  
|`Properties/GlobalPath`|String|相對路徑 toohello 全域屬性檔。|  
|`Properties/GlobalPath/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 全域屬性檔。|  
|`Properties/Path`|String|相對路徑 toohello 屬性檔。|  
|`Properties/Path/@Hash`|屬性、字串|Base16 編碼 MD5 雜湊的 hello 屬性檔。|  
|`Blob/Status`|String|處理 hello blob 的狀態。|  
  
# <a name="drive-status-codes"></a>磁碟機狀態碼  
hello 下表列出處理磁碟機的 hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Completed`|hello 磁碟機已完成處理，沒有任何錯誤。|  
|`CompletedWithWarnings`|hello 磁碟機已完成處理，但每 hello hello blob 指定的匯入配置出現一個或多個 blob 中的警告。|  
|`CompletedWithErrors`|hello 磁碟機已完成但一或多個 blob 或區塊發生錯誤。|  
|`DiskNotFound`|Hello 磁碟機上找到的磁碟。|  
|`VolumeNotNtfs`|hello 第一個資料磁碟上的磁碟區 hello 不是 NTFS 格式。|  
|`DiskOperationFailed`|Hello 磁碟機上執行作業時發生未知的失敗。|  
|`BitLockerVolumeNotFound`|找不到 BitLocker 可加密磁碟區。|  
|`BitLockerNotActivated`|不會在 hello 磁碟區上啟用 BitLocker。|  
|`BitLockerProtectorNotFound`|hello 數字密碼金鑰保護裝置 hello 磁碟區上不存在。|  
|`BitLockerKeyInvalid`|提供的 hello 數字密碼無法解除鎖定 hello 磁碟區。|  
|`BitLockerUnlockVolumeFailed`|嘗試 toounlock hello 磁碟區時，發生未知的失敗。|  
|`BitLockerFailed`|執行 BitLocker 作業時發生未知的失敗。|  
|`ManifestNameInvalid`|hello 資訊清單檔案名稱無效。|  
|`ManifestNameTooLong`|hello 資訊清單檔案名稱過長。|  
|`ManifestNotFound`|找不到 hello 資訊清單檔案。|  
|`ManifestAccessDenied`|拒絕存取 toohello 資訊清單檔案。|  
|`ManifestCorrupted`|hello 資訊清單檔案已損毀 （hello 內容不符合其雜湊）。|  
|`ManifestFormatInvalid`|hello 資訊清單內容不符合 toohello 所需的格式。|  
|`ManifestDriveIdMismatch`|hello hello 資訊清單檔中的識別碼不符合的 hello 一個讀取 hello 磁碟機的磁碟機。|  
|`ReadManifestFailed`|Hello 資訊清單讀取時發生磁碟 I/O 失敗。|  
|`BlobListFormatInvalid`|hello 匯出 blob 清單 blob 不符合 toohello 所需的格式。|  
|`BlobRequestForbidden`|禁止存取 toohello blob hello 儲存體帳戶中。 這可能是由於 tooinvalid 儲存體帳戶金鑰或容器 SAS。|  
|`InternalError`|和處理 hello 磁碟機時發生內部錯誤。|  
  
## <a name="blob-status-codes"></a>Blob 狀態碼  
hello 下表列出處理 blob hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Completed`|hello blob 已完成處理，沒有錯誤。|  
|`CompletedWithErrors`|hello blob 已完成處理，但其中一個或多個頁面範圍或區塊、 中繼資料或屬性中的錯誤。|  
|`FileNameInvalid`|hello 檔案名稱無效。|  
|`FileNameTooLong`|hello 檔案名稱過長。|  
|`FileNotFound`|找不到 hello 檔案。|  
|`FileAccessDenied`|拒絕存取 toohello 檔案。|  
|`BlobRequestFailed`|hello tooaccess hello blob 的 Blob 服務要求失敗。|  
|`BlobRequestForbidden`|禁止 hello tooaccess hello blob 的 Blob 服務要求。 這可能是由於 tooinvalid 儲存體帳戶金鑰或容器 SAS。|  
|`RenameFailed`|無法 toorename hello blob （用於匯入工作） 或 hello 檔案 （適用於匯出工作）。|  
|`BlobUnexpectedChange`|Hello blob （用於匯出工作） 發生未預期的變更。|  
|`LeasePresent`|沒有 hello blob 上出現租用。|  
|`IOFailed`|處理 hello blob 時發生磁碟或網路 I/O 失敗。|  
|`Failed`|處理 hello blob 時發生未知的失敗。|  
  
## <a name="import-disposition-status-codes"></a>匯入配置狀態碼  
hello 下表列出解決匯入配置 hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Created`|已建立 hello blob。|  
|`Renamed`|hello blob 已重新命名每個重新命名匯入配置。 hello`Blob/BlobPath`元素包含 hello URI hello 重新命名 blob。|  
|`Skipped`|每個已略過 hello blob`no-overwrite`匯入配置。|  
|`Overwritten`|hello blob 已覆寫現有的 blob，每個`overwrite`匯入配置。|  
|`Cancelled`|先前的失敗已停止進一步處理 hello 匯入配置。|  
  
## <a name="page-rangeblock-status-codes"></a>頁面範圍/區塊狀態碼  
hello 下表列出處理頁面範圍或區塊 hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Completed`|hello 頁面範圍或區塊已完成處理，沒有任何錯誤。|  
|`Committed`|hello 區塊已認可，但不是在 hello 完整區塊清單，因為其他區塊失敗，或放置完整區塊清單本身失敗。|  
|`Uncommitted`|hello 區塊是上傳，但尚未認可。|  
|`Corrupted`|hello 頁面範圍或區塊已損毀 （hello 內容不符合其雜湊）。|  
|`FileUnexpectedEnd`|發現非預期的檔案結尾。|  
|`BlobUnexpectedEnd`|發現非預期的 Blob 結尾。|  
|`BlobRequestFailed`|hello Blob 服務要求 tooaccess hello 頁面範圍或區塊已失敗。|  
|`IOFailed`|處理 hello 頁面範圍或區塊時發生磁碟或網路 I/O 失敗。|  
|`Failed`|處理 hello 頁面範圍或區塊時發生未知的失敗。|  
|`Cancelled`|先前的失敗已停止進一步處理 hello 頁面範圍或區塊。|  
  
## <a name="metadata-status-codes"></a>中繼資料狀態碼  
hello 下表列出處理 blob 中繼資料的 hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Completed`|hello 中繼資料已完成處理，沒有錯誤。|  
|`FileNameInvalid`|hello 中繼資料檔案名稱無效。|  
|`FileNameTooLong`|hello 中繼資料檔案名稱過長。|  
|`FileNotFound`|找不到 hello 中繼資料檔案。|  
|`FileAccessDenied`|拒絕存取 toohello 中繼資料檔案。|  
|`Corrupted`|hello 中繼資料檔案已損毀 （hello 內容不符合其雜湊）。|  
|`XmlReadFailed`|hello 中繼資料內容不符合 toohello 所需的格式。|  
|`XmlWriteFailed`|撰寫 hello 中繼資料 XML 失敗。|  
|`BlobRequestFailed`|hello tooaccess hello 中繼資料的 Blob 服務要求失敗。|  
|`IOFailed`|處理 hello 中繼資料時發生磁碟或網路 I/O 失敗。|  
|`Failed`|處理 hello 中繼資料時發生未知的失敗。|  
|`Cancelled`|先前的失敗已停止進一步處理 hello 中繼資料。|  
  
## <a name="properties-status-codes"></a>屬性狀態碼  
hello 下表列出處理 blob 屬性 hello 狀態碼。  
  
|狀態碼|說明|  
|-----------------|-----------------|  
|`Completed`|hello 屬性已完成處理，沒有任何錯誤。|  
|`FileNameInvalid`|hello 屬性檔名稱無效。|  
|`FileNameTooLong`|hello 屬性檔名稱過長。|  
|`FileNotFound`|找不到 hello 屬性檔。|  
|`FileAccessDenied`|拒絕存取 toohello 屬性檔。|  
|`Corrupted`|hello 屬性檔已損毀 （hello 內容不符合其雜湊）。|  
|`XmlReadFailed`|hello 屬性內容不符合 toohello 所需的格式。|  
|`XmlWriteFailed`|寫入 hello 屬性 XML 失敗。|  
|`BlobRequestFailed`|hello tooaccess hello 屬性的 Blob 服務要求失敗。|  
|`IOFailed`|處理 hello 屬性時發生磁碟或網路 I/O 失敗。|  
|`Failed`|處理 hello 屬性時發生未知的失敗。|  
|`Cancelled`|先前的失敗已停止進一步處理 hello 屬性。|  
  
## <a name="sample-logs"></a>範例記錄  
hello 下列是範例的詳細資訊記錄檔。  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
hello 對應錯誤記錄檔如下所示。  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 匯入工作的 hello 後續錯誤記錄檔包含 hello 匯入磁碟機上找不到檔案的相關錯誤。 請注意，後續元件 hello 狀態`Cancelled`。  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

hello 下列的錯誤記錄檔，匯出工作的表示，hello blob 內容已成功寫入 toohello 磁碟機，但匯出 hello blob 的內容時，發生錯誤。  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>後續步驟
 
* [儲存體匯入/匯出 REST API](/rest/api/storageimportexport/)
