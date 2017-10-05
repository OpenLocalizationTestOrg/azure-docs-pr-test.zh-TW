---
title: "使用 Azure 入口網站建立 IoT 中樞 | Microsoft Docs"
description: "如何透過 Azure 入口網站建立、管理和刪除 Azure IoT 中樞。 其中包括定價層、調整、安全性和傳訊組態的相關資訊。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="6d935-104">使用 Azure 入口網站建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6d935-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6d935-105">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="6d935-105">This article describes:</span></span>

* <span data-ttu-id="6d935-106">如何在 Azure 入口網站中找到 IoT 中樞服務。</span><span class="sxs-lookup"><span data-stu-id="6d935-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="6d935-107">如何建立和管理 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="6d935-108">IoT 中樞服務的所在位置</span><span class="sxs-lookup"><span data-stu-id="6d935-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="6d935-109">您可以在入口網站的下列位置中找到 IoT 中樞服務：</span><span class="sxs-lookup"><span data-stu-id="6d935-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="6d935-110">選擇 [+ 新增]，然後選擇 [物聯網]。</span><span class="sxs-lookup"><span data-stu-id="6d935-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="6d935-111">在 Marketplace 中，選擇 [物聯網]。</span><span class="sxs-lookup"><span data-stu-id="6d935-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="6d935-112">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6d935-112">Create an IoT hub</span></span>

<span data-ttu-id="6d935-113">您可以使用下列方法建立 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="6d935-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="6d935-114">[+ 新增] 選項會開啟下列螢幕擷取畫面中顯示的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6d935-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="6d935-115">透過這個方法以及透過 Marketplace 建立 IoT 中樞的步驟完全相同。</span><span class="sxs-lookup"><span data-stu-id="6d935-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="6d935-116">在 Marketplace 中，選擇 [建立] 以開啟下列螢幕擷取畫面中顯示的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6d935-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="6d935-117">下列幾節說明建立 IoT 中樞的幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="6d935-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="6d935-118">選擇 IoT 中樞的名稱</span><span class="sxs-lookup"><span data-stu-id="6d935-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="6d935-119">若要建立 IoT 中樞，您必須替 IoT 中樞命名。</span><span class="sxs-lookup"><span data-stu-id="6d935-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="6d935-120">此名稱不得與任何 IoT 中樞之名稱重複。</span><span class="sxs-lookup"><span data-stu-id="6d935-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="6d935-121">選擇定價層。</span><span class="sxs-lookup"><span data-stu-id="6d935-121">Choose the pricing tier</span></span>

<span data-ttu-id="6d935-122">您可以從 4 個層級中選擇：**免費**、**標準 1**、**標準 2** 和**標準 S3**。</span><span class="sxs-lookup"><span data-stu-id="6d935-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="6d935-123">免費層只允許 500 個裝置連接至 IoT 中樞，每天最多 8,000 封訊息。</span><span class="sxs-lookup"><span data-stu-id="6d935-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="6d935-124">**標準 S1**：如果 IoT 解決方案擁有大量裝置，但每個裝置只會產生少量資料，請使用 S1 版本。</span><span class="sxs-lookup"><span data-stu-id="6d935-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="6d935-125">S1 版本的每個單位可讓您跨所有連接的裝置，每天傳輸高達 400,000 封訊息。</span><span class="sxs-lookup"><span data-stu-id="6d935-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="6d935-126">**標準 S2**：如果 IoT 解決方案中的裝置會產生大量資料，請使用 S2 版本。</span><span class="sxs-lookup"><span data-stu-id="6d935-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="6d935-127">S2 版本的每個單位可讓您跨所有連接的裝置，每天傳輸高達 6 百萬封訊息。</span><span class="sxs-lookup"><span data-stu-id="6d935-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="6d935-128">**標準 S3**：如果 IoT 解決方案會產生大量資料，請使用 S3 版本。</span><span class="sxs-lookup"><span data-stu-id="6d935-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="6d935-129">S3 版本的每個單位可讓您跨所有連接的裝置，每天傳輸高達 3 億封訊息。</span><span class="sxs-lookup"><span data-stu-id="6d935-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="6d935-130">IoT 中樞只允許每個 Azure 訂用帳戶有一個免費中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="6d935-131">IoT 中樞單位</span><span class="sxs-lookup"><span data-stu-id="6d935-131">IoT hub units</span></span>

<span data-ttu-id="6d935-132">每天每單位允許的訊息數目取決於您的中樞定價層。</span><span class="sxs-lookup"><span data-stu-id="6d935-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="6d935-133">例如，如果您想要 IoT 中樞支援 700,000 封訊息的輸入，您可以選擇 2 個 S1 層單位。</span><span class="sxs-lookup"><span data-stu-id="6d935-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="6d935-134">裝置到雲端分割及資源群組</span><span class="sxs-lookup"><span data-stu-id="6d935-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="6d935-135">您可以變更 IoT 中樞的分割數目。</span><span class="sxs-lookup"><span data-stu-id="6d935-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="6d935-136">分割的預設數目是 4，您可以從下拉式清單中選擇不同的數字。</span><span class="sxs-lookup"><span data-stu-id="6d935-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="6d935-137">您不需要明確建立空的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d935-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="6d935-138">您可以在建立資源時，選擇建立新的資源群組，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d935-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="6d935-139">選擇訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6d935-139">Choose subscription</span></span>

<span data-ttu-id="6d935-140">Azure IoT 中樞會自動列出使用者帳戶所連結的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d935-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="6d935-141">您可以選擇要與 IoT 中樞相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d935-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="6d935-142">選擇位置</span><span class="sxs-lookup"><span data-stu-id="6d935-142">Choose the location</span></span>

<span data-ttu-id="6d935-143">[位置] 選項提供可在其中使用 IoT 中樞的區域清單。</span><span class="sxs-lookup"><span data-stu-id="6d935-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="6d935-144">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6d935-144">Create the IoT hub</span></span>

<span data-ttu-id="6d935-145">完成上述的所有步驟之後，您便可以建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="6d935-146">按一下 [建立] 以啟動後端程序，並透過您選擇的選項建立和部署 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="6d935-147">由於要在適當的位置伺服器上執行後端部署需要時間，因此建立 IoT 中樞會需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="6d935-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="6d935-148">變更 IoT 中樞的設定</span><span class="sxs-lookup"><span data-stu-id="6d935-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="6d935-149">從 IoT 中樞刀鋒視窗建立 IoT 中樞後，您可以變更此現有 IoT 中樞的設定。</span><span class="sxs-lookup"><span data-stu-id="6d935-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="6d935-150">**共用存取原則**：這些原則定義了裝置與服務連接至 IoT 中樞的權限。</span><span class="sxs-lookup"><span data-stu-id="6d935-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="6d935-151">您可以按一下 [一般] 之下的 [共用存取原則] 來存取這些原則。</span><span class="sxs-lookup"><span data-stu-id="6d935-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="6d935-152">在這個刀鋒視窗中，您可以修改現有的原則或新增原則。</span><span class="sxs-lookup"><span data-stu-id="6d935-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="6d935-153">建立原則</span><span class="sxs-lookup"><span data-stu-id="6d935-153">Create a policy</span></span>

* <span data-ttu-id="6d935-154">按一下 [新增] 開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6d935-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="6d935-155">您可以在此輸入新的原則名稱以及您想要與此原則產生關聯的權限，如在下一個圖中所示：</span><span class="sxs-lookup"><span data-stu-id="6d935-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="6d935-156">有許多權限可與這些共用原則產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6d935-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="6d935-157">[登錄讀取] 和 [登錄寫入] 原則會授與讀取和寫入存取權給身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="6d935-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="6d935-158">選擇寫入選項就會自動選擇讀取選項。</span><span class="sxs-lookup"><span data-stu-id="6d935-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="6d935-159">[服務連線] 原則會授與存取服務端點的權限，例如**接收裝置到雲端**。</span><span class="sxs-lookup"><span data-stu-id="6d935-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="6d935-160">[裝置連線] 原則會授與使用 IoT 中樞裝置端端點傳送和接收訊息的權限。</span><span class="sxs-lookup"><span data-stu-id="6d935-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="6d935-161">按一下 [建立]  將此新建立的原則新增至現有的清單。</span><span class="sxs-lookup"><span data-stu-id="6d935-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="6d935-162">端點</span><span class="sxs-lookup"><span data-stu-id="6d935-162">Endpoints</span></span>

<span data-ttu-id="6d935-163">按一下 [端點] 以顯示您正在修改之 IoT 中樞的端點清單。</span><span class="sxs-lookup"><span data-stu-id="6d935-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="6d935-164">端點有兩個類型︰IoT 中樞內建的端點，以及您在 IoT 中樞建立後新增的端點。</span><span class="sxs-lookup"><span data-stu-id="6d935-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="6d935-165">內建端點</span><span class="sxs-lookup"><span data-stu-id="6d935-165">Built-in endpoints</span></span>

<span data-ttu-id="6d935-166">有兩種內建端點︰**雲端到裝置回饋**和**事件**。</span><span class="sxs-lookup"><span data-stu-id="6d935-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="6d935-167">**雲端到裝置回饋**設定：此設定有 2 個子設定：訊息的**雲端到裝置 TTL** (存留時間) 和**保留時間** (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="6d935-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="6d935-168">當您第一次建立 IoT 中樞時，這兩個設定的預設值都是一個小時。</span><span class="sxs-lookup"><span data-stu-id="6d935-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="6d935-169">若要調整這些設定，可使用滑桿或輸入值。</span><span class="sxs-lookup"><span data-stu-id="6d935-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="6d935-170">**事件**設定：這個設定有數個子設定，其中有些是唯讀。</span><span class="sxs-lookup"><span data-stu-id="6d935-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="6d935-171">下列清單說明這些設定：</span><span class="sxs-lookup"><span data-stu-id="6d935-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="6d935-172">**分割**：當 IoT 中樞建立後會設定預設值。</span><span class="sxs-lookup"><span data-stu-id="6d935-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="6d935-173">您可以透過此設定變更分割數目。</span><span class="sxs-lookup"><span data-stu-id="6d935-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="6d935-174">**事件中樞相容的名稱和端點**：建立 IoT 中樞時，事件中樞會在內部建立，而您在某些情況下可能需要其存取權。</span><span class="sxs-lookup"><span data-stu-id="6d935-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="6d935-175">您無法自訂事件中樞的相容名稱和端點值，但可以按一下 [複製] 來複製它們。</span><span class="sxs-lookup"><span data-stu-id="6d935-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="6d935-176">**保留時間**：預設為一天，但可以使用下拉式清單變更。</span><span class="sxs-lookup"><span data-stu-id="6d935-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="6d935-177">這是裝置到雲端設定以天為單位的值。</span><span class="sxs-lookup"><span data-stu-id="6d935-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="6d935-178">**取用者群組**：取用者群組可讓多個讀取器從 IoT 中樞獨立讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="6d935-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="6d935-179">每個 IoT 中樞都是使用預設取用者群組建立的。</span><span class="sxs-lookup"><span data-stu-id="6d935-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="6d935-180">不過，您可以使用這個設定新增或刪除 IoT 中樞的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="6d935-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6d935-181">預設的取用者群組無法編輯或刪除。</span><span class="sxs-lookup"><span data-stu-id="6d935-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="6d935-182">自訂端點</span><span class="sxs-lookup"><span data-stu-id="6d935-182">Custom endpoints</span></span>

<span data-ttu-id="6d935-183">您可以使用入口網站在 IoT 中樞上新增自訂端點。</span><span class="sxs-lookup"><span data-stu-id="6d935-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="6d935-184">從 [端點] 刀鋒視窗，按一下頂端的 [新增] 以開啟 [新增端點] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6d935-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="6d935-185">輸入必要資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d935-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="6d935-186">您的自訂端點現在會列在主要 [端點] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="6d935-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="6d935-187">您可以在[參考 - IoT 中樞端點][lnk-devguide-endpoints]中深入了解自訂端點。</span><span class="sxs-lookup"><span data-stu-id="6d935-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="6d935-188">路由</span><span class="sxs-lookup"><span data-stu-id="6d935-188">Routes</span></span>

<span data-ttu-id="6d935-189">按一下 [路由] 以管理 IoT 中樞分派您的裝置到雲端訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="6d935-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="6d935-190">您可以將路由新增至 IoT 中樞，方法是按一下 [路由]* 刀鋒視窗頂端的 [新增]、輸入必要資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d935-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="6d935-191">接著您的路由會列在主要 [路由] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="6d935-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="6d935-192">您可以在路由清單中按一下路由來編輯它。</span><span class="sxs-lookup"><span data-stu-id="6d935-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="6d935-193">若要啟用路由，按一下路由清單中的路由，並將 [已啟用] 切換為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="6d935-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="6d935-194">若要儲存變更，請按一下刀鋒視窗底部的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d935-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="6d935-195">價格和調整</span><span class="sxs-lookup"><span data-stu-id="6d935-195">Pricing and scale</span></span>

<span data-ttu-id="6d935-196">現有 IoT 中樞的價格可透過 [價格]  設定變更，但是有下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="6d935-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="6d935-197">在目前的實作中，具有免費 SKU 的 IoT 中樞無法變更為付費 SKU 層，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="6d935-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="6d935-198">在 Azure 訂用帳戶中只能有一個免費層 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="6d935-199">該日傳送的訊息數目超過較低層級的配額時，您才能從較高層級移至較低層級。</span><span class="sxs-lookup"><span data-stu-id="6d935-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="6d935-200">例如，如果每天的訊息數目都超過 400,000，則 IoT 中樞的層會變更。</span><span class="sxs-lookup"><span data-stu-id="6d935-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="6d935-201">不過，如果您變更為 S1 層，IoT 中樞當天會進行節流。</span><span class="sxs-lookup"><span data-stu-id="6d935-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="6d935-202">刪除 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6d935-202">Delete the IoT hub</span></span>

<span data-ttu-id="6d935-203">您可以藉由按一下 [瀏覽] ，然後選擇要刪除的適當中樞，即可瀏覽至您想要刪除的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6d935-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="6d935-204">若要刪除 IoT 中樞，請按一下 IoT 中樞名稱下方的 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d935-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d935-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d935-205">Next steps</span></span>

<span data-ttu-id="6d935-206">遵循下列連結以深入了解如何管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="6d935-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="6d935-207">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="6d935-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="6d935-208">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6d935-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="6d935-209">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6d935-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="6d935-210">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="6d935-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6d935-211">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6d935-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6d935-212">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6d935-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="6d935-213">[徹底保護您的 IoT 解決方案][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="6d935-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
