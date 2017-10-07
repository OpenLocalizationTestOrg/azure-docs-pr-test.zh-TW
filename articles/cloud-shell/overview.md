---
title: "aaaAzure 雲端殼層 （預覽） 的概觀 |Microsoft 文件"
description: "Hello Azure 雲端殼層概觀。"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Azure Cloud Shell 的功能概觀 (預覽)
Azure Cloud Shell 是可經由瀏覽器存取的互動式殼層，應用在 Azure 資源管理上。

![](media/overview-pic.png)

## <a name="features"></a>特性
### <a name="browser-based-shell-experience"></a>以瀏覽器為基礎的體驗
雲端殼層啟用存取 tooa 瀏覽器型命令列建置體驗與 Azure 的管理工作納入考量。 利用雲端殼層 toowork untethered 從本機機器只有 hello 雲端可提供的方式。

### <a name="pre-configured-azure-workstation"></a>預先設定的 Azure 工作站
Cloud Shell 預先安裝受歡迎的命令列工具和語言支援，能加快您的工作速度。

[檢視 hello 完整的工具清單 Azure 雲端 shell。](features.md#tools)

### <a name="automatic-authentication"></a>自動驗證
雲端殼層安全地透過 hello Azure CLI 2.0 的立即存取 tooyour 資源的每個工作階段上自動驗證。

### <a name="connect-your-azure-file-storage"></a>連接您的 Azure 檔案儲存體
雲端殼層電腦是暫時性的因此需要裝載為 Azure 檔案共用 toobe `clouddrive` toopersist $Home 目錄。
第一次啟動雲端殼層提示的 toocreate 代替您共用的資源群組、 儲存體帳戶和檔案。 這是一次性的步驟，而且會針對所有工作階段自動連接。 

#### <a name="create-new-storage"></a>建立新的儲存體
![](media/basic-storage.png)

可代替您建立的本地備援儲存體 (LRS) 帳戶有一個 Azure 檔案共用，其中包含預設是 5 GB 的磁碟映像。 hello 檔案共用做為所掛接`clouddrive`檔案共用互動 hello 磁碟映像正在使用的 toosync 和保存 $Home 目錄。 所需成本和一般儲存體相同。

將代替您建立下列三個資源：
1. 名稱如下的資源群組：`cloud-shell-storage-<region>`
2. 名稱如下的儲存體帳戶：`cs<uniqueGuid>`
3. 名稱如下的檔案共用：`cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> $Home 目錄中的所有檔案 (例如 SSH 金鑰) 會都保存於已掛接檔案共用中儲存的使用者磁碟映像中。 在 $Home 目錄和已掛接的檔案共用中儲存檔案時，請套用最佳作法。

#### <a name="use-existing-resources"></a>使用現有的資源
![](media/advanced-storage.png)

進階的選項也會提供允許您 tooassociate 現有資源 tooCloud 殼層。 當看到 hello 儲存安裝程式提示字元中，按一下 [顯示進階設定] tooselect 其他選項。 下拉式清單會針對您指派的 Cloud Shell 區域和本地/全域備援儲存體帳戶進行篩選。

[了解 Cloud Shell 儲存體、更新檔案共用，以及上傳/下載檔案。](persisting-shell-storage.md)

## <a name="concepts"></a>概念
* Cloud Shell 會在以每一工作階段、每位使用者為基礎所提供的暫存機器上執行
* Cloud Shell 會在無互動活動的 20 分鐘後逾時
* 只有在已連接檔案共用時才能存取 Cloud Shell
* Cloud Shell 會以一台機器、一個使用者帳戶的方式指派
* 權限設定為一般 Linux 使用者

[深入了解所有 Cloud Shell 功能。](features.md)

## <a name="examples"></a>範例
* 建立或編輯指令碼 tooautomate Azure 管理
* 同時透過 Azure 入口網站和 Azure CLI 2.0 管理 資源
* 試用 Azure CLI 2.0

[嘗試在 hello 殼層雲端快速入門的上述所有範例。](quickstart.md)

## <a name="pricing"></a>價格
主控雲端殼層 hello 機器是免費的與掛接的 Azure 檔案的必要共用 toopersist $Home 目錄。 所需成本和一般儲存體相同。

## <a name="supported-browsers"></a>支援的瀏覽器
Cloud Shell 建議用於 Chrome、Edge 和 Safari 瀏覽器。 支援雲端殼層 Chrome、 Firefox、 Safari、 IE 以及邊緣，雲端殼層是主體 toospecific 瀏覽器設定。

## <a name="troubleshooting"></a>疑難排解
1. 當使用 Azure Active Directory 訂閱，無法建立儲存體到期 tooError: 400 DisallowedOperation。 tooresolve，請使用能夠建立儲存體資源的 Azure 訂用帳戶。 AD 訂用帳戶會無法 toocreate Azure 資源。

如需特定已知的限制，請瀏覽 [Cloud Shell 的限制](limitations.md)。
