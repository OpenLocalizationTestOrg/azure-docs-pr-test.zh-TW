---
title: "Azure 儲存體延展性和效能目標 | Microsoft Docs"
description: "了解 Azure 儲存體的延展性和效能目標，包括標準和進階儲存體帳戶的容量、要求率以及輸入和輸出頻寬。 了解每一項 Azure 儲存體服務內分割的效能目標。"
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
ms.openlocfilehash: 47a1d2b87269d40716b3dae02276207060b41c24
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Azure 儲存體延展性和效能目標
## <a name="overview"></a>Overview
本主題描述 Microsoft Azure 儲存體的延展性和效能。 如需其他 Azure 限制的摘要，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../../azure-subscription-service-limits.md)。

> [!NOTE]
> 所有儲存體帳戶都能在一般網路拓撲上執行，並支援下面說明的延展性和效能目標，無論它們在何時建立。 如需 Azure 儲存體平面網路架構及延展性的詳細資訊，請參閱 [Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。
> 
> [!IMPORTANT]
> 列於此處的延展性和效能目標都是高階目標，但仍可達成。 在所有情況下，您的儲存體帳戶所達到的要求率和頻寬取決於已儲存物件的大小、使用的存取模式、應用程式執行的工作負載類型。 請務必測試您的服務，以判斷效能是否達到您的要求。 如果可能，請避免流量率突增，確保流量在不同分割之間妥善分散。
> 
> 當您的應用程式達到分割處理工作負載的限制時，Azure 儲存體會開始傳回錯誤碼 503 (伺服器忙碌) 或錯誤碼 500 (作業逾時) 回應。 當發生這種情況時，應用程式應該使用指數輪詢重試原則。 指數輪詢讓分割的負載減少，也能減輕該分割流量的尖峰。
> 
> 

如果您的應用程式需求超出單一儲存體帳戶的延展性目標，您可以建置可使用多個儲存體帳戶的應用程式，並將資料物件分割到那些儲存體帳戶中。 如需批量價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 。

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Blob、佇列、資料表和檔案的延展性目標
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>虛擬機器磁碟的延展性目標
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

如需詳細資訊，請參閱 [Windows VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="managed-virtual-machine-disks"></a>受管理的虛擬機器磁碟

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>未受管理的虛擬機器磁碟
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Azure Resource Manager 的延展性目標
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Azure 儲存體中的分割
每個在 Azure 儲存體中保存資料的物件 (Blob、訊息、實體和檔案) 都屬於分割，也都由分割索引鍵所識別。 分割會判斷 Azure 儲存體要如何在伺服器間取得 Blob、訊息、實體和檔案的負載平衡，以滿足這些物件的流量需求。 分割索引鍵是唯一的，用於尋找 Blob、訊息或實體。

上方位於 [標準儲存體帳戶的延展性目標](#standard-storage-accounts) 中的表格，列出每個服務的單一分割效能目標。

分割會影響每個儲存體服務的負載平衡和延展性，方式如下：

* **Blob**：Blob 的分割索引鍵為帳戶名稱 + 容器名稱 + Blob 名稱。 這表示每個 Blob 都可以有其專屬分割區 (Blob 上的負載需要它時)。 Blob 可以分散到多部伺服器，以相應放大對它們的存取，但是單一伺服器只能服務單一 Blob。 雖然 Blog 可以在 Blog 容器中邏輯分組，但這種分組方式的意涵卻非分割。
* **檔案**：檔案的分割索引鍵是帳戶名稱 + 檔案共用名稱。 這表示檔案共用中的所有檔案也都位於單一分割區中。
* **訊息**：訊息的分割索引鍵為帳戶名稱 + 佇列名稱，所以所有佇列中的訊息都能分組到單一分割，並由單一伺服器所服務。 不同佇列可能由不同伺服器所處理以平衡負載，無論儲存體帳戶可能有多少佇列。
* **實體**：實體的分割索引鍵為帳戶名稱 + 資料表名稱 + 分割索引鍵，其中分割索引鍵是該實體由使用者定義的 **PartitionKey** 屬性所需的值。 所有具有相同分割區索引鍵的實體都分組成一個相同的分割，並由相同的分割伺服器服務。 在設計您的應用程式時，這是要了解的重點。 藉由將實體分組到單一分割的資料存取優勢，您的應用程式應該會在多個分割中分配實體時取得延展性優勢的平衡。  

將資料表中的一組實體分組成一個單一分割的主要優點在於，這能讓它在相同分割中的實體之間執行不可部分完成的批次作業，因為單一伺服器上存有一個分割。 因此，如果您想要對一組實體執行批次作業，請考慮使用相同的分割索引鍵將它們分組在一起。 

另一方面，位於相同資料表但具有不同分割索引鍵的實體，可在不同伺服器之間達到負載平衡，這可以具有較大的延展性。

[這裡](https://msdn.microsoft.com/library/azure/hh508997.aspx)可以找到設計資料表分割策略的詳細建議。

## <a name="see-also"></a>另請參閱
* [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)
* [Azure 訂用帳戶和服務限制、配額與限制](../../azure-subscription-service-limits.md)
* [Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../storage-premium-storage.md)
* [Azure 儲存體複寫](../storage-redundancy.md)
* [Microsoft Azure 儲存體效能與延展性檢查清單](../storage-performance-checklist.md)
* [Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務。](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

