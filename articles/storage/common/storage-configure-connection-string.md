---
title: "aaaConfigure Azure 儲存體的連接字串 |Microsoft 文件"
description: "設定 Azure 儲存體帳戶的連接字串。 連接字串包含 hello 資訊所需 tooauthenticate 存取 tooa 儲存體帳戶從您的應用程式在執行階段。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>設定 Azure 儲存體連接字串

連接字串包含所需的應用程式 tooaccess 資料在執行階段的 Azure 儲存體帳戶中的 hello 驗證資訊。 您可以設定連接字串，以進行下列動作：

* 連接 toohello Azure 儲存體模擬器。
* 在 Azure 中存取儲存體帳戶。
* 透過共用存取簽章 (SAS) 存取 Azure 中的指定資源。

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>儲存您的連接字串
您的應用程式必須在執行階段 tooauthenticate 提出的要求 tooAzure 儲存體 tooaccess hello 連接字串。 您有幾種選項可用來儲存連接字串：

* 應用程式正在執行 hello 桌面或裝置上可以儲存中的 hello 連接字串**app.config**或**web.config**檔案。 新增 hello 連接字串 toohello **AppSettings**這些檔案中的區段。
* 在 Azure 雲端服務中執行的應用程式可以將 hello 連接字串儲存在 hello [Azure 服務組態結構描述 (.cscfg) 檔](https://msdn.microsoft.com/library/ee758710.aspx)。 新增 hello 連接字串 toohello **ConfigurationSettings** hello 服務組態檔區段。
* 您可以直接在您的程式碼中使用連接字串。 不過，在大部分情況下，建議您在組態檔中儲存連接字串。

儲存您的連接字串組態檔中，可以輕鬆 tooupdate hello 連接字串 tooswitch hello 儲存體模擬器與 Azure 儲存體帳戶之間 hello 雲端中。 您只需要 tooedit hello 連接字串 toopoint tooyour 目標環境。

您可以使用 hello [Microsoft Azure 組態管理員](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)tooaccess 在執行階段，不論您的應用程式執行所在的連接字串。

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>建立 hello 儲存體模擬器的連接字串
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

如需 hello 儲存體模擬器的詳細資訊，請參閱[使用 hello Azure 儲存體模擬器進行開發和測試](storage-use-emulator.md)。

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>建立 Azure 儲存體帳戶的連接字串
toocreate Azure 儲存體帳戶的連接字串，使用 hello 下列格式。 表示是否要 tooconnect toohello 儲存體帳戶，透過 HTTPS （建議選項） 或 HTTP，而取代`myAccountName`同名的儲存體帳戶，並取代 hello`myAccountKey`與您的帳戶存取金鑰：

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

例如，您的連接字串看起來可能如下所示︰

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

雖然 Azure 儲存體可同時支援連接字串中的 HTTP 和 HTTPS，但*強烈建議您使用 HTTPS*。

> [!TIP]
> 您可以找到您的儲存體帳戶連接字串 hello [Azure 入口網站](https://portal.azure.com)。 瀏覽過**設定** > **存取金鑰**儲存體帳戶的功能表刀鋒視窗 toosee 連接字串中這兩個主要和次要存取金鑰。
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>使用共用存取簽章建立連接字串
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>建立明確儲存體端點的連接字串
您可以在連接字串，而不是使用 hello 預設端點中指定明確的服務端點。 toocreate 連接字串，指定了明確的端點，指定下列格式的 hello hello 完整服務端點的每個服務，包括 hello 通訊協定規格 （HTTPS （建議選項） 或 HTTP）：

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

您可能希望 toospecify 了明確的端點的其中一個案例是當您已對應您的 Blob 儲存體端點 tooa[自訂網域](../blobs/storage-custom-domain-name.md)。 在此情況下，您可以在連接字串中指定 Blob 儲存體的自訂端點。 您可以選擇性地指定 hello hello 預設端點的其他服務如果應用程式使用它們。

指定明確 hello Blob 服務端點的連接字串範例如下：

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

這個範例會指定明確端點的所有服務，包括 hello Blob 服務的自訂網域：

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

連接字串中的 hello 端點值是使用的 tooconstruct hello 要求 Uri toohello 儲存體服務，並指示 hello 形式傳回 tooyour 程式碼的任何 Uri。

如果您已對應儲存體端點 tooa 自訂網域，並省略從連接字串，該端點，然後就可以 toouse 該連接字串 tooaccess 該服務，從您的程式碼中的資料。

> [!IMPORTANT]
> 連接字串中的服務端點值必須是格式正確的 URI，包括 `https://`(建議) 或 `http://`。 因為 Azure 儲存體還不支援 HTTPS 的自訂網域，但您*必須*指定`http://`為任何端點 URI 指向 tooa 自訂網域。
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>建立包含端點尾碼的連接字串
toocreate 連接字串儲存體服務中的區域或不同的端點尾碼，具有執行個體這類中國 Azure 或 Azure 政府，使用下列連接字串格式的 hello。 表示是否要 tooconnect toohello 儲存體帳戶，透過 HTTPS （建議選項） 或 HTTP，而取代`myAccountName`hello 您的儲存體帳戶名稱，以取代`myAccountKey`與您的帳戶存取金鑰，取代`mySuffix`以 hello URI後置詞：

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

以下是 Azure China 中儲存體服務的連接字串範例：

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>剖析連接字串
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>後續步驟
* [使用 hello Azure 儲存體模擬器進行開發和測試](storage-use-emulator.md)
* [Azure 儲存體總管](storage-explorers.md)
* [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)

