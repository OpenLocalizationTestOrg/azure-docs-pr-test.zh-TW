---
title: "Azure 資料湖存放區常見問題 aaaFrequently |Microsoft 文件"
description: "針對 Azure Data Lake Store 的問題進行疑難排解或加以減緩的指導方針"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Azure Data Lake Store 常見問題集
本文章中，您將了解常見問題集相關 tooAzure 資料湖存放區。

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>如何進一步保護我的資料以防止區域全面性災害或意外刪除？
Azure Data Lake Store 帳戶中的 hello 資料是透過自動化複本區域內的彈性 tootransient 硬體故障。 這可確保持久性和高可用性，會議 hello Azure 資料湖存放區 SLA。 以下是一些指引上 toofurther 從極少數的整個區域的中斷或意外刪除所保護的資料。

### <a name="disaster-recovery-guidance"></a>災害復原指引
每個客戶 tooprepare 重要他們自己的嚴重損壞復原計畫。 請嚴重損壞修復規劃，參閱 toohello toobuild 下方的 Azure 文件。 這裡有一些資源可協助您建立自己的計畫。

* [Azure 應用程式的災害復原和高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Azure 復原技術指導](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>最佳作法
我們建議您在另一個地區的災害復原計畫的頻率對齊 toohello 需要複製您的重要資料 tooanother Data Lake Store 帳戶。 有各種不同的方法 toocopy 資料包括[ADLCopy](data-lake-store-copy-data-azure-storage-blob.md)， [Azure PowerShell](data-lake-store-get-started-powershell.md)或[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)。 Azure Data Factory 這項服務很適合用來反覆建立和部署資料移動管線。

如果地區的中斷發生時，然後您可以存取您 hello 區域複製 hello 資料的位置中的資料。您可以監視 hello [Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)toodetermine hello 跨 hello 全球 Azure 服務狀態。

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>資料損毀或意外刪除復原指引
雖然 Azure Data Lake Store 可透過自動化複本提供資料恢復，但這無法防止應用程式 (或開發人員/使用者) 的資料遭到損毀或意外刪除。

#### <a name="best-practices"></a>最佳作法
tooprevent 被意外刪除，我們建議您先設定您的 Data Lake Store 帳戶的 hello 正確的存取原則。  這包括套用[Azure 資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)重要的資源，以及使用可用的 hello 的套用帳戶和檔案層級的存取控制向 toolock[資料湖存放區的安全性功能](data-lake-store-security-overview.md)。 另外，也建議您使用 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md)、[Azure PowerShell](data-lake-store-get-started-powershell.md) 或 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)，在另一個 Data Lake Store 帳戶、資料夾或 Azure 訂用帳戶定期建立重要資料的複本。  這可以是使用的 toorecover 從資料損毀或刪除事件。 Azure Data Factory 這項服務很適合用來反覆建立和部署資料移動管線。

組織也可以啟用[診斷記錄](data-lake-store-diagnostic-logs.md)其 Azure Data Lake Store 帳戶 toocollect 提供者可能已刪除或更新檔案的相關資訊的資料存取稽核記錄。

## <a name="next-steps"></a>後續步驟
* [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)

