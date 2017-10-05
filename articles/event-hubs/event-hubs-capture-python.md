---
title: "Azure 事件中樞擷取逐步解說 | Microsoft Docs"
description: "此範例使用 Azure Python SDK 來示範如何使用事件中樞擷取功能。"
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
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="ebfb2-103">事件中樞擷取逐步解說︰Python</span><span class="sxs-lookup"><span data-stu-id="ebfb2-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="ebfb2-104">「事件中樞擷取」是「事件中樞」的功能，可讓您將事件中樞內的串流資料自動傳遞給您選擇的 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="ebfb2-105">此功能可讓您輕鬆地對即時串流資料執行批次處理。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="ebfb2-106">本文說明如何搭配使用事件中樞擷取與 Python。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="ebfb2-107">如需事件中樞擷取的詳細資訊，請參閱[概觀文章](event-hubs-archive-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="ebfb2-108">此範例使用 [Azure Python SDK](https://azure.microsoft.com/develop/python/) 來示範「擷取」功能。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="ebfb2-109">sender.py 程式會以 JSON 格式將模擬的環境遙測傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="ebfb2-110">事件中樞已設定為使用「擷取」功能將此資料批次寫入至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="ebfb2-111">capturereader.py 應用程式接著會讀取這些 Blob 並為每個裝置建立附加檔案，然後將資料寫入至 .csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ebfb2-112">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="ebfb2-112">What will be accomplished</span></span>

1. <span data-ttu-id="ebfb2-113">使用 Azure 入口網站建立 Azure Blob 儲存體帳戶和其中所含的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="ebfb2-114">使用 Azure 入口網站建立事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="ebfb2-115">使用 Azure 入口網站來建立已啟用「擷取」功能的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="ebfb2-116">使用 Python 指令碼將資料傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="ebfb2-117">使用另一個 Python 指令碼讀取擷取的檔案並加以處理。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebfb2-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="ebfb2-118">Prerequisites</span></span>

- <span data-ttu-id="ebfb2-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="ebfb2-119">Python 2.7.x</span></span>
- <span data-ttu-id="ebfb2-120">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ebfb2-120">An Azure subscription</span></span>
- <span data-ttu-id="ebfb2-121">作用中的[事件中樞命名空間和事件中樞](event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ebfb2-122">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ebfb2-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="ebfb2-123">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="ebfb2-124">在入口網站的左方瀏覽窗格中，依序按一下 [新增]、[儲存體] 及 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="ebfb2-125">完成儲存體帳戶刀鋒視窗中的欄位，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="ebfb2-126">在看到**部署成功**訊息之後，按一下新儲存體帳戶的名稱，並在 [基本功能] 刀鋒視窗中按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="ebfb2-127">當 [Blob 服務] 刀鋒視窗開啟時，按一下頂端的 [+ 容器]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="ebfb2-128">將容器命名為**擷取**，然後關閉 [Blob 服務] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="ebfb2-129">按一下左側刀鋒視窗的 [存取金鑰]，然後複製儲存體帳戶名稱和 **key1** 的值。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="ebfb2-130">將這些值儲存到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="ebfb2-131">建立 Python 指令碼以將事件傳送到事件中樞</span><span class="sxs-lookup"><span data-stu-id="ebfb2-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="ebfb2-132">開啟您慣用的 Python 編輯器，例如 [Visual Studio 程式碼][Visual Studio Code]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="ebfb2-133">建立稱為 **sender.py**的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="ebfb2-134">此指令碼會將 200 個事件傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="ebfb2-135">這些事件是以 JSON 格式傳送的簡單環境數據。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="ebfb2-136">將下列程式碼貼到 sender.py：</span><span class="sxs-lookup"><span data-stu-id="ebfb2-136">Paste the following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="ebfb2-137">更新上述程式碼，以使用您在建立「事件中樞」命名空間時取得的命名空間名稱、金鑰值及事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="ebfb2-138">建立 Python 指令碼來讀取擷取檔案</span><span class="sxs-lookup"><span data-stu-id="ebfb2-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="ebfb2-139">填寫刀鋒視窗，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="ebfb2-140">建立名為 **capturereader.py** 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="ebfb2-141">此指令碼會讀取擷取檔案，並為每個裝置建立檔案以便只寫入該裝置的資料。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="ebfb2-142">將下列程式碼貼到 capturereader.py：</span><span class="sxs-lookup"><span data-stu-id="ebfb2-142">Paste the following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="ebfb2-143">請務必在 `startProcessing`的呼叫中貼上儲存體帳戶名稱和金鑰的適當值。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="ebfb2-144">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="ebfb2-144">Run the scripts</span></span>
1. <span data-ttu-id="ebfb2-145">開啟在其路徑中具有 Python 的命令提示字元，並執行下列命令來安裝 Python 必要條件封裝︰</span><span class="sxs-lookup"><span data-stu-id="ebfb2-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="ebfb2-146">如果您有舊版的 Azure 儲存體或 Azure，您可能需要使用 **--upgrade** 選項</span><span class="sxs-lookup"><span data-stu-id="ebfb2-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="ebfb2-147">您可能也需要執行下列命令 (在大部分系統上並不需要)︰</span><span class="sxs-lookup"><span data-stu-id="ebfb2-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="ebfb2-148">將目錄變更為儲存了 sender.py 和 capturereader.py 的任何位置，並執行此命令︰</span><span class="sxs-lookup"><span data-stu-id="ebfb2-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="ebfb2-149">此命令會啟動新的 Python 程序來執行傳送器。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="ebfb2-150">現在等候擷取執行幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="ebfb2-151">然後在原始命令視窗中輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ebfb2-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="ebfb2-152">此擷取處理器會使用本機目錄從儲存體帳戶/容器下載所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="ebfb2-153">它會處理任何非空白的 Blob，並將結果以 .csv 檔案的形式寫入到本機目錄。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebfb2-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebfb2-154">Next steps</span></span>

<span data-ttu-id="ebfb2-155">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ebfb2-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="ebfb2-156">[事件中樞擷取概觀][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="ebfb2-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="ebfb2-157">[使用事件中樞的完整範例應用程式][sample application that uses Event Hubs]。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="ebfb2-158">[使用事件中樞相應放大事件處理][Scale out Event Processing with Event Hubs]範例。</span><span class="sxs-lookup"><span data-stu-id="ebfb2-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="ebfb2-159">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="ebfb2-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
