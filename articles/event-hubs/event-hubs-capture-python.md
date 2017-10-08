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
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="bed22-103">事件中樞擷取逐步解說︰Python</span><span class="sxs-lookup"><span data-stu-id="bed22-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="bed22-104">擷取的事件中樞是一項功能，可讓您 tooautomatically 事件中心提供您的事件中樞 tooan 您選擇的 Azure Blob 儲存體帳戶中的資料流的 hello。</span><span class="sxs-lookup"><span data-stu-id="bed22-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="bed22-105">這項功能可讓處理即時串流資料的簡易 tooperform 批次。</span><span class="sxs-lookup"><span data-stu-id="bed22-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="bed22-106">本文說明如何使用 Python 的 toouse 事件中心擷取。</span><span class="sxs-lookup"><span data-stu-id="bed22-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="bed22-107">如需有關事件中心擷取的詳細資訊，請參閱 hello[概觀文章](event-hubs-archive-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bed22-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="bed22-108">這個範例會使用 hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello 擷取功能。</span><span class="sxs-lookup"><span data-stu-id="bed22-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="bed22-109">hello sender.py 程式模擬環境遙測 tooEvent 中樞 JSON 格式傳送。</span><span class="sxs-lookup"><span data-stu-id="bed22-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="bed22-110">hello 事件中樞設定 toouse hello 擷取功能 toowrite 批次中的此資料 tooblob 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="bed22-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="bed22-111">hello capturereader.py 應用程式再讀取這些 blob 並建立附加的檔案以每個裝置，然後將 hello 資料寫入至.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="bed22-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="bed22-112">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="bed22-112">What will be accomplished</span></span>

1. <span data-ttu-id="bed22-113">建立 Azure Blob 儲存體帳戶和 blob 容器內，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bed22-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="bed22-114">建立事件中樞命名空間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bed22-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="bed22-115">建立事件中樞與 hello 擷取功能已啟用，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bed22-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="bed22-116">傳送資料 toohello 事件中心的 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bed22-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="bed22-117">Hello 檔案讀取 hello 擷取及處理它們的另一個的 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bed22-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bed22-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="bed22-118">Prerequisites</span></span>

- <span data-ttu-id="bed22-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="bed22-119">Python 2.7.x</span></span>
- <span data-ttu-id="bed22-120">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bed22-120">An Azure subscription</span></span>
- <span data-ttu-id="bed22-121">作用中的[事件中樞命名空間和事件中樞](event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="bed22-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="bed22-122">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bed22-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="bed22-123">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="bed22-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="bed22-124">在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**儲存體**，然後按一下**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="bed22-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="bed22-125">完成 hello 儲存體帳戶 刀鋒視窗中的 hello 欄位，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="bed22-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="bed22-126">Vez que aparezca hello**部署成功**訊息中，按一下 hello 名稱 hello 新儲存體帳戶並在 hello **Essentials**刀鋒視窗中，按一下  **Blob**。</span><span class="sxs-lookup"><span data-stu-id="bed22-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="bed22-127">當 hello **Blob 服務**開啟刀鋒視窗中，按一下**+ 容器**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="bed22-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="bed22-128">名稱 hello 容器**擷取**，請關閉然後 hello **Blob 服務**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bed22-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="bed22-129">按一下**存取金鑰**在 hello 左刀鋒視窗，然後複製 hello hello 儲存體帳戶名稱和值 hello **key1**。</span><span class="sxs-lookup"><span data-stu-id="bed22-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="bed22-130">儲存這些值 tooNotepad 或一些其他的暫存位置。</span><span class="sxs-lookup"><span data-stu-id="bed22-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="bed22-131">建立 Python 指令碼 toosend 事件 tooyour 事件中樞</span><span class="sxs-lookup"><span data-stu-id="bed22-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="bed22-132">開啟您慣用的 Python 編輯器，例如 [Visual Studio 程式碼][Visual Studio Code]。</span><span class="sxs-lookup"><span data-stu-id="bed22-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="bed22-133">建立稱為 **sender.py**的指令碼。</span><span class="sxs-lookup"><span data-stu-id="bed22-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="bed22-134">此指令碼會傳送 200 事件 tooyour 事件中心。</span><span class="sxs-lookup"><span data-stu-id="bed22-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="bed22-135">這些事件是以 JSON 格式傳送的簡單環境數據。</span><span class="sxs-lookup"><span data-stu-id="bed22-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="bed22-136">貼上下列程式碼到 sender.py hello:</span><span class="sxs-lookup"><span data-stu-id="bed22-136">Paste hello following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="bed22-137">更新您的命名空間名稱、 索引鍵值和建立 hello 事件中樞命名空間時取得的事件中樞名稱前面的程式碼 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="bed22-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="bed22-138">建立 Python 指令碼 tooread 擷取檔案</span><span class="sxs-lookup"><span data-stu-id="bed22-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="bed22-139">填寫 [hello] 刀鋒視窗，並按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="bed22-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="bed22-140">建立名為 **capturereader.py** 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="bed22-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="bed22-141">此指令碼會讀取 hello 擷取檔案，並建立該裝置僅針對每一裝置 toowrite hello 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="bed22-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="bed22-142">貼上下列程式碼到 capturereader.py hello:</span><span class="sxs-lookup"><span data-stu-id="bed22-142">Paste hello following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="bed22-143">您的儲存體帳戶名稱和金鑰在 hello 呼叫太 hello 適當的值是確定 toopaste`startProcessing`。</span><span class="sxs-lookup"><span data-stu-id="bed22-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="bed22-144">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="bed22-144">Run hello scripts</span></span>
1. <span data-ttu-id="bed22-145">開啟命令提示字元在其路徑中，具有 Python，然後執行這些命令 tooinstall Python 先決條件封裝：</span><span class="sxs-lookup"><span data-stu-id="bed22-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="bed22-146">如果您有舊版的 azure 儲存體或 azure，您可能需要 toouse hello **-升級**選項</span><span class="sxs-lookup"><span data-stu-id="bed22-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="bed22-147">您可能也需要 toorun hello 遵循 （不需要在大多數系統上）：</span><span class="sxs-lookup"><span data-stu-id="bed22-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="bed22-148">變更您的目錄 toowherever 儲存 sender.py 和 capturereader.py，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="bed22-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="bed22-149">此命令會啟動新 Python 程序 toorun hello 寄件者。</span><span class="sxs-lookup"><span data-stu-id="bed22-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="bed22-150">現在，請稍候幾分鐘，讓 hello 擷取 toorun。</span><span class="sxs-lookup"><span data-stu-id="bed22-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="bed22-151">然後輸入 hello 到原始的命令視窗，下列命令：</span><span class="sxs-lookup"><span data-stu-id="bed22-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="bed22-152">此擷取處理器會使用 hello 本機目錄 toodownload hello 儲存體帳戶/容器的所有 hello blob。</span><span class="sxs-lookup"><span data-stu-id="bed22-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="bed22-153">它會處理任何不是空白，並將 hello 結果.csv 檔案的形式寫入至 hello 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="bed22-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bed22-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bed22-154">Next steps</span></span>

<span data-ttu-id="bed22-155">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="bed22-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="bed22-156">[事件中樞擷取概觀][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="bed22-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="bed22-157">[使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]。</span><span class="sxs-lookup"><span data-stu-id="bed22-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="bed22-158">hello[範圍外使用事件中心的事件處理][ Scale out Event Processing with Event Hubs]範例。</span><span class="sxs-lookup"><span data-stu-id="bed22-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="bed22-159">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="bed22-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
