---
title: "aaaMoving 大量資料至 azure 或從 Azure 中的雲端儲存體 |Microsoft 文件"
description: "Hello 不同的方法來移動資料 tooand 從 Azure 儲存體的概觀。"
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>從 Azure 儲存體移動資料 tooand
如果您想 toomove 在內部部署資料 tooAzure 儲存體 （反之亦然），有各種不同的方式 toodo 這。 最適合您的 hello 方法將取決於您的案例。 本文將提供不同案例的快速概觀和每個案例的適當供應項目。

## <a name="building-applications"></a>建置應用程式
如果您正在建置應用程式，針對 hello REST API 或其中一個我們許多用戶端程式庫開發是從 Azure 儲存體的絕佳方式，toomove 資料 tooand。

Azure 儲存體提供 .NET、iOS、Java、Android、通用 Windows 平台 (UWP)、Xamarin、c++、Node.JS、PHP、Ruby 和 Python 等豐富的用戶端程式庫。 hello 用戶端程式庫提供進階的功能，例如重試邏輯、 記錄和並行上傳。 您也可以直接對 hello REST API，可以呼叫任何提出 HTTP/HTTPS 要求的語言所開發。

請參閱[開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)toolearn 更多。

此外，我們也提供 hello [Azure 儲存體的資料移動程式庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement)這是專為高效能從 Azure 複製的資料 tooand 所設計的程式庫。 請參閱 tooour 資料移動文件庫[文件](https://github.com/Azure/azure-storage-net-data-movement)toolearn 更多。 

## <a name="quickly-viewinginteracting-with-your-data"></a>快速檢視/和資料互動
如果您想要輕鬆 tooview 您 Azure 儲存體的資料，同時也擁有 hello 能力 tooupload 並下載您的資料，請考慮使用 Azure 儲存體總管。

簽出的清單[Azure 儲存體總管](../storage-explorers.md)toolearn 更多。

## <a name="system-administration"></a>系統管理
如果您需要或更熟悉的命令列公用程式 （例如系統管理員），以下是一些您 tooconsider 選項：

### <a name="azcopy"></a>AzCopy
AzCopy 是專為高效能的資料 tooand 複製從 Azure 儲存體設計的 Windows 命令列公用程式。 您也可以複製儲存體帳戶內或不同儲存體帳戶之間的資料。

請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)toolearn 更多。

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell 模組提供 Cmdlet 讓您用於管理 Azure 上的服務。 此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。

請參閱[與 Azure 儲存體使用 Azure PowerShell](storage-powershell-guide-full.md) toolearn 更多。

### <a name="azure-cli"></a>Azure CLI
Azure CLI 提供您一組開放原始碼的跨平台命令，供您使用 Azure 服務。 Azure CLI 可在 Windows、OSX 和 Linux 上使用。

請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](../storage-azure-cli.md) toolearn 更多。

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>以較慢的網路移動大量資料
Hello 與移動大量資料相關聯的最大挑戰之一是 hello 傳輸時間。 如果您想 tooget 資料從 Azure 儲存體不需要擔心網路成本或撰寫程式碼時，Azure 匯入/匯出就會是適當的解決方案。

請參閱[Azure 匯入/匯出](../storage-import-export-service.md)toolearn 更多。

## <a name="backing-up-your-data"></a>備份您的資料
如果您只需要 toobackup 您資料 tooAzure 儲存體，Azure 備份是 hello 方式 toogo。 對於備份內部部署資料和 Azure VM，這是功能強大的解決方案。

請參閱[Azure Backup](../../backup/backup-introduction-to-azure-backup.md) toolearn 更多。

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>存取您資料的內部與 hello 雲端
如果您需要一個解決方案，來存取您資料內部及從 hello 雲端，您應該考慮使用 Azure 的混合式雲端儲存體解決方案，StorSimple。 此解決方案包含實體 StorSimple 裝置，以智慧方式將經常使用的資料儲存在 SSD 上，將偶爾使用的資料儲存在 HDD 上，並且將非作用中/備份/封存資料儲存在 Azure 儲存體上。

請參閱[StorSimple](../../storsimple/storsimple-overview.md) toolearn 更多。

## <a name="recovering-your-data"></a>復原您的資料
當您擁有內部部署工作負載和應用程式時，您將需要一個解決方案，讓您的商務 toocontinue hello 災害事件中執行。 Azure Site Recovery 可處理虛擬機器和實體伺服器的複寫、容錯移轉及復原作業。 複寫的資料會儲存在 Azure 儲存體，讓您 tooeliminate hello 需要次要站上的資料中心。

請參閱[Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn 更多。
### <a name="moving-data-faq"></a>移動資料常見問題集︰
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>我可以移轉 Vhd 從一個區域 tooanother 無需先行複製嗎？
hello 只方式 toocopy Vhd 區域之間是每個區域上的儲存體帳戶之間 toocopy hello 資料。 您可以使用 AZCopy 這樣做。 請參閱與 hello 更多的 AzCopy 命令列公用程式 toolearn 傳輸資料。 針對極大的資料量，您也可以使用 Azure 匯入/匯出。 請參閱[Azure 匯入/匯出](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service)toolearn 更多。
