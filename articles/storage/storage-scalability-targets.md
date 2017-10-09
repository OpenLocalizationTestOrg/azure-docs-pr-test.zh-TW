---
title: "aaaAzure 儲存體延展性和效能目標 |Microsoft 文件"
description: "Azure 儲存體，包括容量、 要求率，以及傳入和傳出的頻寬，這兩個標準和進階儲存體帳戶，以了解 hello 延展性和效能目標。 了解內的每個 hello Azure 儲存體服務的資料分割的效能目標。"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Azure 儲存體延展性和效能目標
## <a name="overview"></a>概觀
本主題描述 Microsoft Azure 儲存體 hello 延展性和效能主題。 如需其他 Azure 限制的摘要，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。

> [!NOTE]
> 所有儲存體帳戶 hello 新的平面網路拓撲上執行，而且支援下面所述，不論它們在何時建立 hello 延展性和效能目標。 如需 hello Azure 儲存體平面網路架構及延展性的詳細資訊，請參閱[Microsoft Azure 儲存體： 高可用雲端儲存體服務具有強式一致性](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。
> 
> [!IMPORTANT]
> 此處所列的 hello 延展性和效能目標是高階的目標，但是可達成。 在所有情況下，hello 要求率和頻寬，方法是儲存體帳戶取決於儲存時，物件 hello 大小 hello 存取模式的使用率，並 hello 應用程式執行的工作負載類型。 會確定 tootest 服務 toodetermine 無論其效能是某符合您的需求。 可能的話，請避免 hello 流量速率中的突然出現尖峰，並確保流量平均分散到資料分割。
> 
> 當您的應用程式達到 hello 限制的資料分割可以處理您的工作負載時，Azure 儲存體將會開始 tooreturn 錯誤碼 503 （伺服器忙碌） 或錯誤碼 500 （作業逾時） 回應。 當發生這種情況時，hello 應用程式應該使用指數輪詢原則的重試。 hello 指數型輪詢允許流量 toothat 資料分割中的 hello hello 分割 toodecrease 及 tooease 出尖峰負載。
> 
> 

如果 hello 應用程式需要超過 hello 延展性目標的單一儲存體帳戶，您可以建置應用程式 toouse 多個儲存體帳戶，並這些儲存體帳戶間分割您的資料物件。 如需批量價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 。

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Blob、佇列、資料表和檔案的延展性目標
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>虛擬機器磁碟的延展性目標
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

如需詳細資訊，請參閱 [Windows VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="managed-virtual-machine-disks"></a>受管理的虛擬機器磁碟

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>未受管理的虛擬機器磁碟
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Azure Resource Manager 的延展性目標
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Azure 儲存體中的分割
保存資料儲存在 Azure 儲存體 （blob、 訊息、 實體和檔案） 中的每個物件所屬 tooa 分割，並由資料分割索引鍵識別。 hello 資料分割可決定如何 Azure 儲存體進行負載平衡的 blob、 訊息、 實體和檔案跨伺服器 toomeet hello 傳輸需要這些物件。 hello 資料分割索引鍵是唯一的且使用的 toolocate blob、 訊息或實體。

在上面顯示的 hello 資料表[標準儲存體帳戶的延展性目標](#standard-storage-accounts)清單 hello 每個服務的單一資料分割的效能目標。

資料分割會影響 hello hello 下列方式中的儲存體服務的每個負載平衡和延展性：

* **Blob**: hello blob 的資料分割索引鍵是帳戶名稱 + 容器名稱 + blob 名稱。 這表示如果 hello blob 上的負載需要它的每個 blob 可以有自己的資料分割。 Blob 可以分散安裝在存取 toothem 出順序 tooscale 中許多伺服器，但只可由單一伺服器提供單一 blob。 雖然 Blog 可以在 Blog 容器中邏輯分組，但這種分組方式的意涵卻非分割。
* **檔案**: hello 檔案的資料分割索引鍵是帳戶名稱 + 檔案共用名稱。 這表示檔案共用中的所有檔案也都位於單一分割區中。
* **訊息**: hello 訊息的資料分割索引鍵並 hello 帳戶名稱 + 佇列名稱，因此佇列中的所有訊息會分組成單一資料分割，會由單一伺服器。 可能由不同的伺服器，但是儲存體帳戶可能有許多佇列 toobalance hello 載入處理不同的佇列。
* **實體**: hello 實體的資料分割索引鍵是帳戶名稱 + 資料表名稱 + 資料分割索引鍵，其中 hello 資料分割索引鍵是所需的 hello hello 值使用者定義**PartitionKey** hello 實體的屬性。 以相同的資料分割索引鍵的值分組到相同資料分割，且會由 hello 相同的 hello hello 的所有實體都分割伺服器。 這是重要的點 toounderstand 設計您的應用程式。 您的應用程式應該 hello 延展性的優勢散佈跨多個資料分割的實體群組於單一資料分割的 hello 資料存取優點與實體之間取得平衡。  

主要優點 toogrouping 至單一資料分割的資料表中的實體集是的 hello 相同資料分割，因為在單一伺服器上存在的資料分割中的實體為可能 tooperform 不可部分完成的批次作業。 因此，如果您想 tooperform 批次作業上的實體群組，請考慮群組它們文件以 hello 相同的資料分割索引鍵。 

在 hello 另一方面，hello 相同資料表，但有不同的資料分割索引鍵中的實體可以進行負載平衡到不同的伺服器，因此可能 toohave 較大的延展性。

[這裡](https://msdn.microsoft.com/library/azure/hh508997.aspx)可以找到設計資料表分割策略的詳細建議。

## <a name="see-also"></a>另請參閱
* [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)
* [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)
* [Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)
* [Azure 儲存體複寫](storage-redundancy.md)
* [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)
* [Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務。](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

