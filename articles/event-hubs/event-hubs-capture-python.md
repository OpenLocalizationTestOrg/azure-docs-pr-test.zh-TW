---
title: "事件中心擷取逐步解說 aaaAzure |Microsoft 文件"
description: "使用 hello Azure Python SDK toodemonstrate 使用 hello 事件中心擷取功能的範例。"
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>事件中樞擷取逐步解說︰Python

擷取的事件中樞是一項功能，可讓您 tooautomatically 事件中心提供您的事件中樞 tooan 您選擇的 Azure Blob 儲存體帳戶中的資料流的 hello。 這項功能可讓處理即時串流資料的簡易 tooperform 批次。 本文說明如何使用 Python 的 toouse 事件中心擷取。 如需有關事件中心擷取的詳細資訊，請參閱 hello[概觀文章](event-hubs-archive-overview.md)。

這個範例會使用 hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello 擷取功能。 hello sender.py 程式模擬環境遙測 tooEvent 中樞 JSON 格式傳送。 hello 事件中樞設定 toouse hello 擷取功能 toowrite 批次中的此資料 tooblob 存放裝置。 hello capturereader.py 應用程式再讀取這些 blob 並建立附加的檔案以每個裝置，然後將 hello 資料寫入至.csv 檔案。

## <a name="what-will-be-accomplished"></a>將會完成的工作

1. 建立 Azure Blob 儲存體帳戶和 blob 容器內，使用 hello Azure 入口網站。
2. 建立事件中樞命名空間，使用 hello Azure 入口網站。
3. 建立事件中樞與 hello 擷取功能已啟用，使用 hello Azure 入口網站。
4. 傳送資料 toohello 事件中心的 Python 指令碼。
5. Hello 檔案讀取 hello 擷取及處理它們的另一個的 Python 指令碼。

## <a name="prerequisites"></a>必要條件

- Python 2.7.x
- Azure 訂用帳戶
- 作用中的[事件中樞命名空間和事件中樞](event-hubs-create.md)。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>建立 Azure 儲存體帳戶
1. 登入 toohello [Azure 入口網站][Azure portal]。
2. 在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**儲存體**，然後按一下**儲存體帳戶**。
3. 完成 hello 儲存體帳戶 刀鋒視窗中的 hello 欄位，然後按一下**建立**。
   
   ![][1]
4. Vez que aparezca hello**部署成功**訊息中，按一下 hello 名稱 hello 新儲存體帳戶並在 hello **Essentials**刀鋒視窗中，按一下  **Blob**。 當 hello **Blob 服務**開啟刀鋒視窗中，按一下**+ 容器**hello 頂端。 名稱 hello 容器**擷取**，請關閉然後 hello **Blob 服務**刀鋒視窗。
5. 按一下**存取金鑰**在 hello 左刀鋒視窗，然後複製 hello hello 儲存體帳戶名稱和值 hello **key1**。 儲存這些值 tooNotepad 或一些其他的暫存位置。

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>建立 Python 指令碼 toosend 事件 tooyour 事件中樞
1. 開啟您慣用的 Python 編輯器，例如 [Visual Studio 程式碼][Visual Studio Code]。
2. 建立稱為 **sender.py**的指令碼。 此指令碼會傳送 200 事件 tooyour 事件中心。 這些事件是以 JSON 格式傳送的簡單環境數據。
3. 貼上下列程式碼到 sender.py hello:
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. 更新您的命名空間名稱、 索引鍵值和建立 hello 事件中樞命名空間時取得的事件中樞名稱前面的程式碼 toouse hello。

## <a name="create-a-python-script-tooread-your-capture-files"></a>建立 Python 指令碼 tooread 擷取檔案

1. 填寫 [hello] 刀鋒視窗，並按一下**建立**。
2. 建立名為 **capturereader.py** 的指令碼。 此指令碼會讀取 hello 擷取檔案，並建立該裝置僅針對每一裝置 toowrite hello 資料檔案。
3. 貼上下列程式碼到 capturereader.py hello:
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. 您的儲存體帳戶名稱和金鑰在 hello 呼叫太 hello 適當的值是確定 toopaste`startProcessing`。

## <a name="run-hello-scripts"></a>執行 hello 指令碼
1. 開啟命令提示字元在其路徑中，具有 Python，然後執行這些命令 tooinstall Python 先決條件封裝：
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  如果您有舊版的 azure 儲存體或 azure，您可能需要 toouse hello **-升級**選項
   
  您可能也需要 toorun hello 遵循 （不需要在大多數系統上）：
   
  ```
  pip install cryptography
  ```
2. 變更您的目錄 toowherever 儲存 sender.py 和 capturereader.py，並執行下列命令：
   
  ```
  start python sender.py
  ```
   
  此命令會啟動新 Python 程序 toorun hello 寄件者。
3. 現在，請稍候幾分鐘，讓 hello 擷取 toorun。 然後輸入 hello 到原始的命令視窗，下列命令：
   
   ```
   python capturereader.py
   ```

   此擷取處理器會使用 hello 本機目錄 toodownload hello 儲存體帳戶/容器的所有 hello blob。 它會處理任何不是空白，並將 hello 結果.csv 檔案的形式寫入至 hello 本機目錄。

## <a name="next-steps"></a>後續步驟

您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞擷取概觀][Overview of Event Hubs Capture]
* [使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]。
* hello[範圍外使用事件中心的事件處理][ Scale out Event Processing with Event Hubs]範例。
* [事件中樞概觀][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
