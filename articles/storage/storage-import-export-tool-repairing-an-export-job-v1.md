---
title: "Azure 匯入/匯出匯出工作-v1 aaaRepairing |Microsoft 文件"
description: "了解如何匯出工作，所建立及執行使用 toorepair hello Azure 匯入/匯出服務。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>修復匯出作業
匯出工作完成後，您可以執行 Microsoft Azure 匯入/匯出工具提供從內部部署的 hello:  
  
1.  下載 hello Azure 匯入/匯出服務是無法 tooexport 任何檔案。  
  
2.  驗證 hello 磁碟機上的 hello 檔案已正確匯出。  
  
您必須擁有連線 tooAzure 儲存體 toouse 這項功能。  
  
hello 命令來修復匯入工作是**RepairExport**。

## <a name="repairexport-parameters"></a>RepairExport 參數

hello 指定下列參數可以與**RepairExport**:  
  
|參數|說明|  
|---------------|-----------------|  
|**/r:<RepairFile\>**|必要。 路徑 toohello 修復檔案，追蹤 hello hello 修復進度，並可讓您 tooresume 中斷的修復。 每個磁碟機需要一個修復檔案，而且只能有一個。 當您開始在給定的磁碟機的修復時，您將會傳入 hello 路徑 tooa 修復檔案尚不存在。 tooresume 中斷的修復，您應傳入 hello 現有的修復檔名稱。 一律必須指定 hello 修復檔案對應 toohello 目標磁碟機。|  
|**/logdir:\><LogDirectory**|選用。 hello 記錄檔目錄。 詳細資訊記錄檔會寫入 toothis 目錄。 如果未不指定任何記錄檔目錄，則 hello 目前的目錄會用作 hello 記錄檔目錄。|  
|**/d:<TargetDirectory\>**|必要。 hello 目錄 toovalidate 和修復。 這通常是 hello 根目錄的 hello 匯出磁碟機，但無法同時也網路檔案共用包含匯出的 hello 檔案的複本。|  
|**/bk:<BitLockerKey\>**|選用。 如果您想 hello 工具 toounlock 儲存加密 hello 匯出的檔案，您應該指定 hello BitLocker 金鑰。|  
|**/sn:<StorageAccountName\>**|必要。 hello 名稱 hello hello 儲存體帳戶匯出工作。|  
|**/sk:<StorageAccountKey\>**|如果未指定 (且只有在未指定) 容器 SAS 時，才是**必要**參數。 hello hello hello 的儲存體帳戶的帳戶金鑰匯出工作。|  
|**/csas:<ContainerSas\>**|**需要**如果且只有未指定 hello 儲存體帳戶金鑰。 用於存取與 hello 匯出工作相關聯的 hello blob hello 容器 SAS。|  
|**/CopyLogFile:<DriveCopyLogFile\>**|必要。 hello 路徑 toohello 磁碟機複製記錄檔。 hello 檔案 hello Windows Azure 匯入/匯出服務所產生，並可從 hello 與 hello 工作相關聯的 blob 儲存體下載。 hello 複製記錄檔包含失敗的 blob 或檔案，也就是 toobe 修復的相關資訊。|  
|**/ManifestFile:<DriveManifestFile\>**|選用。 hello 路徑 toohello 匯出磁碟機的資訊清單檔案。 這個檔案是 hello Windows Azure 匯入/匯出服務所產生，而且儲存 hello 匯出磁碟機，並選擇性地在 hello 與 hello 工作相關聯的儲存體帳戶中的 blob。<br /><br /> hello hello hello 匯出磁碟機上的檔案的內容將會驗證與此檔案包含 hello MD5 雜湊。 決定的 toobe 損毀的檔案會下載並重寫 toohello 目標目錄。|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>使用 RepairExport 模式 toocorrect 無法匯出  
您可以使用無法 tooexport hello Azure 匯入/匯出工具 toodownload 檔案。 hello 複製記錄檔會包含失敗 tooexport 的檔案清單。  
  
hello 的匯出失敗的原因包括下列可能性 hello:  
  
-   損壞的磁碟機  
  
-   hello hello 傳輸程序期間變更的儲存體帳戶金鑰  
  
中的 toorun hello 工具**RepairExport**模式中，您必須先包含 hello 匯出的檔案 tooyour 電腦 tooconnect hello 磁碟機。 接下來，執行 Azure 匯入/匯出工具，以 hello 指定 hello 路徑 toothat 磁碟機 hello`/d`參數。 您也需要您下載的 toospecify hello 路徑 toohello 磁碟機的複製記錄檔。 hello 下方的下列命令列範例會執行 hello 工具 toorepair 失敗 tooexport 任何檔案：  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
hello 如下顯示的一個區塊中 hello blob 失敗 tooexport 複製記錄檔的範例：  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
hello 複製記錄檔指出 hello Windows Azure 匯入/匯出服務將其中一個下載 hello 匯出磁碟機上的 hello blob 的區塊 toohello 檔案時發生失敗。 hello hello 檔案成功，下載的其他元件，並已正確設定 hello 檔案長度。 在此情況下，hello 工具會開啟 hello hello 磁碟機上的檔案，請下載 hello 區塊從 hello 儲存體帳戶，並將它寫 toohello 檔案範圍從長度為 65536 位移 65536 開始。  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>使用 RepairExport toovalidate 磁碟機內容  
您也可以使用 Azure 匯入/匯出以 hello **RepairExport** hello 磁碟機上的選項 toovalidate hello 內容是否正確。 hello 每個匯出磁碟機上的資訊清單檔包含 hello hello 磁碟機內容的 md5。  
  
hello Azure 匯入/匯出服務也可以儲存 hello 資訊清單檔案 tooa 儲存體帳戶期間 hello 匯出程序。 hello hello 資訊清單檔案的位置可透過 hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 作業已完成的作業。 請參閱[匯入/匯出服務資訊清單檔案格式](storage-import-export-file-format-metadata-and-properties.md)有關 hello 格式的磁碟機資訊清單檔案。  
  
hello 下列範例示範如何 toorun hello 以 hello 的 Azure 匯入/匯出工具**/ManifestFile**和**/CopyLogFile**參數：  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
hello 以下是範例資訊清單檔案：  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
分頁裝訂的 hello 修復程序之後, hello 工具會透過參考 hello 資訊清單檔中每個檔案讀取，並確認 hello 檔案的完整性與 hello MD5 雜湊。 對於上述的 hello 資訊清單，它將會經歷下列元件的 hello。  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Hello 驗證失敗的任何元件會下載 hello 工具，而且重寫的 toohello 相同 hello 磁碟機的檔案。  
  
## <a name="next-steps"></a>後續步驟
 
* [正在設定 hello Azure 匯入/匯出工具](storage-import-export-tool-setup-v1.md)   
* [針對匯入作業準備硬碟](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [利用複製記錄檔檢閱作業狀態](storage-import-export-tool-reviewing-job-status-v1.md)   
* [修復匯入作業](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [疑難排解 hello Azure 匯入/匯出工具](storage-import-export-tool-troubleshooting-v1.md)
