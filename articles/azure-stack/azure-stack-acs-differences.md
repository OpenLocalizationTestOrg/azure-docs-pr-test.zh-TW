---
title: "Azure Stack 儲存體：差異與考量"
description: "了解 hello 差異 Azure 堆疊儲存體和 Azure 儲存體，以及 Azure 堆疊部署考量。"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: xiaofmao
ms.openlocfilehash: a1f8e2180b046b835c89fd658e2dbaff004b8786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-storage-differences-and-considerations"></a>Azure Stack 儲存體：差異與考量
Azure 堆疊儲存體是 hello 組儲存在 Microsoft Azure 堆疊中的雲端服務。 「Azure Stack 儲存體」使用與 Azure 一致的語意來提供 Blob、資料表、佇列及帳戶管理功能。

本文摘要說明 hello 已知 Azure 堆疊儲存體從 Azure 儲存體的差異。 當您部署 Azure 堆疊時，它也摘要列出記住其他考量 tookeep。 toolearn 高階 Azure 堆疊與 Azure 之間的差異，請參閱 「 hello[金鑰考量](azure-stack-considerations.md)主題。

## <a name="cheat-sheet-storage-differences"></a>速查表：儲存體差異

| 功能 | Azure (全域) | Azure Stack |
| --- | --- | --- |
|檔案儲存體|支援雲端式 SMB 檔案共用|尚不支援
|待用資料加密|256 位元 AES 加密|尚不支援
|儲存體帳戶類型|一般用途和 Azure Blob 儲存體帳戶|僅一般用途
|複寫選項|本地備援儲存體、異地備援儲存體、讀取權限異地備援儲存體，以及區域備援儲存體|本地備援儲存體
|進階儲存體|完全支援|可佈建，但無效能限制或保證
|受控磁碟|支援進階和標準|尚不支援
|Blob 名稱|1,024 個字元 (2,048 個位元組)|880 個字元 (1,760 個位元組)
|區塊 Blob 大小上限|4.75 TB (100 MB X 50,000 個區塊)|50,000 x 4 MB (約為 195 GB)
|分頁 Blob 增量快照複製|支援進階和標準 Azure 分頁 Blob|尚不支援
|分頁 Blob 大小上限|8 TB|1 TB
|分頁 Blob 分頁大小|512 個位元組|4 KB
|資料表分割區索引鍵和資料列索引鍵大小|1,024 個字元 (2,048 個位元組)|400 個字元 (800 個位元組)

### <a name="metrics"></a>度量
儲存體度量也有一些差異：
* 在儲存體度量的 hello 交易資料不會區分內部或外部網路頻寬。
* 在儲存體度量的 hello 交易資料不包含虛擬機器存取 toohello 掛接磁碟。

## <a name="api-version"></a>API 版本
支援下列版本的 hello Azure 堆疊儲存體：

* Azure 儲存體資料服務：[2015-04-05 REST API 版本](https://docs.microsoft.com/en-us/rest/api/storageservices/Version-2015-04-05?redirectedfrom=MSDN)
* Azure 儲存體管理服務：[2015-05-01-preview、2015-06-15 及 2016-01-01](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN) 

## <a name="next-steps"></a>後續步驟

* [開始使用 Azure Stack 儲存體開發工具](azure-stack-storage-dev.md)
* [簡介 tooAzure 堆疊儲存體](azure-stack-storage-overview.md)

