---
title: "aaaHow tooadd IoT 中樞事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋的 tooadd 事件來源也就是如何連接 tooan IoT 中樞 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a><span data-ttu-id="4b71c-103">如何 tooadd IoT 中樞事件來源</span><span class="sxs-lookup"><span data-stu-id="4b71c-103">How tooadd an IoT Hub event source</span></span>

<span data-ttu-id="4b71c-104">本教學課程涵蓋如何 toouse 會 hello Azure 入口網站 tooadd 從 IoT 中樞 tooyour 時間數列 Insights 環境中讀取事件來源。</span><span class="sxs-lookup"><span data-stu-id="4b71c-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an IoT Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b71c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b71c-105">Prerequisites</span></span>

<span data-ttu-id="4b71c-106">您已建立 IoT 中樞，並在撰寫事件 tooit。</span><span class="sxs-lookup"><span data-stu-id="4b71c-106">You have created an IoT Hub and are writing events tooit.</span></span> <span data-ttu-id="4b71c-107">如需有關 IoT 中樞的詳細資訊，請參閱 <https://azure.microsoft.com/services/iot-hub/></span><span class="sxs-lookup"><span data-stu-id="4b71c-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="4b71c-108">[取用者群組]每個時間序列 Insights 事件來源必須 toohave 未與任何其他取用者共用其自己專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="4b71c-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="4b71c-109">如果多個讀取器會使用來自事件 hello 相同取用者群組，所有的讀取器都可能 toosee 失敗。</span><span class="sxs-lookup"><span data-stu-id="4b71c-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="4b71c-110">如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南](../iot-hub/iot-hub-devguide.md)。</span><span class="sxs-lookup"><span data-stu-id="4b71c-110">For details, see hello [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="4b71c-111">選擇匯入選項</span><span class="sxs-lookup"><span data-stu-id="4b71c-111">Choose an Import option</span></span>

<span data-ttu-id="4b71c-112">您可以手動輸入 hello 事件來源的 hello 設定路徑，或選取 hello IoT 中樞已可用 tooyou 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4b71c-112">hello settings for hello event source can be entered manually or an IoT hub can be selected from hello IoT hubs that are available tooyou.</span></span>
<span data-ttu-id="4b71c-113">在 hello**匯入選項**選取器選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="4b71c-113">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="4b71c-114">手動提供 IoT 中樞設定</span><span class="sxs-lookup"><span data-stu-id="4b71c-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="4b71c-115">從可用的訂用帳戶使用 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="4b71c-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="4b71c-116">選取可用的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="4b71c-116">Select an available IoT Hub</span></span>

<span data-ttu-id="4b71c-117">hello 下表說明包含其描述的 hello 新的事件來源 索引標籤中的每個選項做為事件來源中選取可用的 IoT 中樞時：</span><span class="sxs-lookup"><span data-stu-id="4b71c-117">hello following table explains each option in hello New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="4b71c-118">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-118">PROPERTY NAME</span></span> | <span data-ttu-id="4b71c-119">說明</span><span class="sxs-lookup"><span data-stu-id="4b71c-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="4b71c-120">事件來源名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-120">Event source name</span></span> | <span data-ttu-id="4b71c-121">hello 事件來源名稱。</span><span class="sxs-lookup"><span data-stu-id="4b71c-121">hello name of your event source.</span></span> <span data-ttu-id="4b71c-122">此名稱在 Time Series Insights 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4b71c-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="4b71c-123">來源</span><span class="sxs-lookup"><span data-stu-id="4b71c-123">Source</span></span> | <span data-ttu-id="4b71c-124">選擇**IoT 中樞**toocreate IoT 中樞事件來源。</span><span class="sxs-lookup"><span data-stu-id="4b71c-124">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="4b71c-125">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="4b71c-125">Subscription Id</span></span> | <span data-ttu-id="4b71c-126">選取在其中建立此 IoT 中心 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b71c-126">Select hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="4b71c-127">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-127">IoT hub name</span></span> | <span data-ttu-id="4b71c-128">選取 hello hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="4b71c-128">Select hello name of hello IoT Hub.</span></span>
| <span data-ttu-id="4b71c-129">IoT 中樞原則名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-129">IoT hub policy name</span></span> | <span data-ttu-id="4b71c-130">選取 hello 共用存取原則，可以在 hello IoT 中樞設定 索引標籤找到。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="4b71c-130">Select hello shared access policy, which can be found on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="4b71c-131">hello 共用存取原則的事件來源*必須*有**服務連線**權限。</span><span class="sxs-lookup"><span data-stu-id="4b71c-131">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="4b71c-132">IoT 中樞取用者群組</span><span class="sxs-lookup"><span data-stu-id="4b71c-132">IoT hub consumer group</span></span> | <span data-ttu-id="4b71c-133">hello hello IoT 中樞取用者群組 tooread 事件。</span><span class="sxs-lookup"><span data-stu-id="4b71c-133">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="4b71c-134">它強烈建議 toouse 事件來源的專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="4b71c-134">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="4b71c-135">手動提供 IoT 中樞設定</span><span class="sxs-lookup"><span data-stu-id="4b71c-135">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="4b71c-136">hello 下列資料表說明 hello 其描述與新的事件來源 索引標籤中的每個屬性輸入的設定時以手動方式：</span><span class="sxs-lookup"><span data-stu-id="4b71c-136">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="4b71c-137">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-137">PROPERTY NAME</span></span> | <span data-ttu-id="4b71c-138">說明</span><span class="sxs-lookup"><span data-stu-id="4b71c-138">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="4b71c-139">事件來源名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-139">Event source name</span></span> | <span data-ttu-id="4b71c-140">hello 事件來源名稱。</span><span class="sxs-lookup"><span data-stu-id="4b71c-140">hello name of your event source.</span></span> <span data-ttu-id="4b71c-141">此名稱在 Time Series Insights 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4b71c-141">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="4b71c-142">來源</span><span class="sxs-lookup"><span data-stu-id="4b71c-142">Source</span></span> | <span data-ttu-id="4b71c-143">選擇**IoT 中樞**toocreate IoT 中樞事件來源。</span><span class="sxs-lookup"><span data-stu-id="4b71c-143">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="4b71c-144">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="4b71c-144">Subscription Id</span></span> | <span data-ttu-id="4b71c-145">此 IoT 中樞建立所在的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b71c-145">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="4b71c-146">資源群組</span><span class="sxs-lookup"><span data-stu-id="4b71c-146">Resource group</span></span> | <span data-ttu-id="4b71c-147">此 IoT 中樞建立所在的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b71c-147">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="4b71c-148">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-148">IoT hub name</span></span> | <span data-ttu-id="4b71c-149">hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="4b71c-149">hello name of your IoT Hub.</span></span> <span data-ttu-id="4b71c-150">當您建立 IoT 中樞時，您也會指定特定名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-150">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="4b71c-151">IoT 中樞原則名稱</span><span class="sxs-lookup"><span data-stu-id="4b71c-151">IoT hub policy name</span></span> | <span data-ttu-id="4b71c-152">hello 共用存取原則，可以建立 hello IoT 中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="4b71c-152">hello shared access policy, which can be created on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="4b71c-153">hello 共用存取原則的事件來源*必須*有**服務連線**權限。</span><span class="sxs-lookup"><span data-stu-id="4b71c-153">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="4b71c-154">IoT 中樞原則金鑰</span><span class="sxs-lookup"><span data-stu-id="4b71c-154">IoT hub policy key</span></span> | <span data-ttu-id="4b71c-155">使用 tooauthenticate 存取 toohello 服務匯流排命名空間的 hello 共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="4b71c-155">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="4b71c-156">輸入 hello 主要或次要金鑰這裡。</span><span class="sxs-lookup"><span data-stu-id="4b71c-156">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="4b71c-157">IoT 中樞取用者群組</span><span class="sxs-lookup"><span data-stu-id="4b71c-157">IoT hub consumer group</span></span> | <span data-ttu-id="4b71c-158">hello hello IoT 中樞取用者群組 tooread 事件。</span><span class="sxs-lookup"><span data-stu-id="4b71c-158">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="4b71c-159">它強烈建議 toouse 事件來源的專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="4b71c-159">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b71c-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b71c-160">Next steps</span></span>

1. <span data-ttu-id="4b71c-161">新增資料存取原則 tooyour 環境[定義資料存取原則](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="4b71c-161">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="4b71c-162">存取您的環境中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4b71c-162">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
