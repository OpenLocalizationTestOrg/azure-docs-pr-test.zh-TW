---
title: "aaaConfiguring 和使用 hello 儲存體模擬器與 Visual Studio |Microsoft 文件"
description: "設定和使用 Visual Studio 中的 hello 儲存體模擬器"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>設定和使用 Visual Studio 中的 hello 儲存體模擬器
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>概觀
hello Azure SDK 開發環境，包括 hello 儲存體模擬器，模擬 hello Blob、 佇列和資料表儲存體服務在本機開發電腦上可用在 Azure 中的公用程式。 如果您是建立雲端服務採用 hello Azure 儲存體服務，或撰寫任何外部的應用程式呼叫 hello 儲存體服務，您可以測試您的程式碼，在本機憑藉 hello 儲存體模擬器。 hello Azure Tools for Microsoft Visual Studio 會將 hello 儲存體模擬器的管理整合到 Visual Studio。 hello Azure Tools 會初始化 hello 儲存體模擬器資料庫第一次使用、 啟動 hello 儲存體模擬器服務，當您執行或偵錯您的程式碼，從 Visual Studio，並提供唯讀存取 toohello 儲存體模擬器資料可經由 hello Azure 儲存體總管。

詳細資訊，在 hello 儲存體模擬器，包括系統需求和自訂組態指示，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](storage/common/storage-use-emulator.md)。

> [!NOTE]
> 有一些功能 hello 儲存體模擬器模擬和 hello Azure 儲存體服務之間的差異。 請參閱[之間的差異 hello 儲存體模擬器和 Azure 儲存體服務](storage/common/storage-use-emulator.md)hello hello 特定差異的資訊的 Azure SDK 文件中。
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Hello 儲存體模擬器設定連接字串
tooaccess hello 從角色中的程式碼的儲存體模擬器，您會想 tooconfigure 連接字串該點 toohello 儲存體模擬器，並稍後可以變更的 toopoint tooan Azure 儲存體帳戶。 連接字串會是您的角色可以在執行階段 tooconnect tooa 儲存體帳戶讀取的組態設定。 如需有關如何 toocreate 的連接字串，請參閱[設定 hello Azure 應用程式](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage)。

> [!NOTE]
> 您可以從您的程式碼傳回參考 toohello 儲存體模擬器帳戶使用 hello **DevelopmentStorageAccount**屬性。 如果您想要 tooaccess hello 從您的程式碼的儲存體模擬器，而如果您計劃 toopublish 應用程式 tooAzure，您將需要 Azure 儲存體帳戶連接字串 tooaccess toocreate 並修改程式碼 toouse 這種方法運作正常，發行之前，連接字串。 如果您經常之間切換 hello 儲存體模擬器帳戶和 Azure 儲存體帳戶，連接字串將可以簡化這個程序。
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>初始化及執行 hello 儲存體模擬器
您可以指定，當您執行或偵錯在 Visual Studio 服務時，Visual Studio 會自動啟動 hello 儲存體模擬器。 在 方案總管 中，開啟 hello 的捷徑功能表您**Azure**專案，選擇**屬性**。 在 hello**開發**索引標籤上，在 hello**啟動 Azure 儲存體模擬器**清單中，選擇**True** （如果尚未設定 toothat 值）。

hello 第一次您執行或偵錯在 Visual Studio 中的 hello 儲存體模擬器服務會啟動初始化處理程序。 此程序會保留 hello 儲存體模擬器的本機連接埠，並建立 hello 儲存體模擬器資料庫。 完成後，此程序不需要 toorun 再次除非 hello 儲存體模擬器資料庫遭刪除。

> [!NOTE]
> 從 hello Azure Tools 的 hello 2012 年 6 月版本開始，hello 儲存體模擬器執行，依預設，在 SQL Express LocalDB。 在舊版的 hello Azure Tools，hello 儲存體模擬器則是針對預設執行個體的 SQL Express 2005 或 2008，您必須安裝之前您可以安裝 hello Azure SDK。 您也可以執行 hello 針對具名執行個體的 SQL Express 或具名或預設的 Microsoft SQL Server 的執行個體的儲存體模擬器。 如果您需要 tooconfigure hello 儲存體模擬器 toorun 針對 hello 預設執行個體以外的執行個體，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](storage/common/storage-use-emulator.md)。
> 
> 

hello 儲存體模擬器提供 hello 本機儲存體服務的使用者介面 tooview hello 狀態和 toostart，停止和重新設定它們。 一旦啟動 hello 儲存體模擬器服務，您可以顯示 hello 使用者介面，或啟動或停止 hello 服務以 hello 通知區域圖示，以滑鼠右鍵按一下 hello hello Windows 工作列中的 Microsoft Azure 模擬器。

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>在 [伺服器總管] 中檢視儲存體模擬器資料
在伺服器總管 中的 hello Azure 儲存體節點可讓您 tooview 資料和變更設定，blob 和資料表資料儲存體帳戶，包括在 hello 儲存體模擬器。 如需詳細資訊，請參閱[使用儲存體總管管理 Azure Blob 儲存體資源 (預覽)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)。

