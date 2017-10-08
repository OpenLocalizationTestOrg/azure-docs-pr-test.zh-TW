---
title: "aaaUse hello Azure 入口網站 toocreate IoT 中樞 |Microsoft 文件"
description: "如何 toocreate、 管理及刪除透過 hello Azure 入口網站的 Azure IoT 中樞。 其中包括定價層、調整、安全性和傳訊組態的相關資訊。"
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
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="8c6a5-104">建立 IoT 中心使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8c6a5-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="8c6a5-105">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-105">This article describes:</span></span>

* <span data-ttu-id="8c6a5-106">如何 toofind hello IoT 中樞 hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="8c6a5-107">如何 toocreate 並管理 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="8c6a5-108">其中 toofind hello IoT 中心服務</span><span class="sxs-lookup"><span data-stu-id="8c6a5-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="8c6a5-109">您可以在下列位置 hello 入口網站中的 hello 找到 hello IoT 中樞服務：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="8c6a5-110">選擇 [+ 新增]，然後選擇 [物聯網]。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="8c6a5-111">在 hello Marketplace，選擇 **物聯網**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="8c6a5-112">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8c6a5-112">Create an IoT hub</span></span>

<span data-ttu-id="8c6a5-113">您可以建立 IoT 中心使用 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="8c6a5-114">hello **+ 新增**選項會開啟 hello 下列螢幕擷取畫面所示的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="8c6a5-115">建立 hello IoT 中樞，透過這個方法，以及透過 hello marketplace hello 步驟完全相同。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="8c6a5-116">在 hello Marketplace，選擇 **建立**tooopen hello 刀鋒視窗 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="8c6a5-117">hello 下列各節說明 hello 幾個步驟 toocreate IoT 中心：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="8c6a5-118">選擇 hello hello IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="8c6a5-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="8c6a5-119">toocreate IoT 中樞，您必須命名 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="8c6a5-120">此名稱不得與任何 IoT 中樞之名稱重複。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="8c6a5-121">選擇定價層的 hello</span><span class="sxs-lookup"><span data-stu-id="8c6a5-121">Choose hello pricing tier</span></span>

<span data-ttu-id="8c6a5-122">您可以從 4 個層級中選擇：**免費**、**標準 1**、**標準 2** 和**標準 S3**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="8c6a5-123">只有 500 裝置 toobe 連線 toohello IoT 中樞，並 too8，每天 000 訊息上，可讓 hello 免費層。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="8c6a5-124">**標準 S1**： 大量的每個產生的少量資料的裝置與 IoT 解決方案使用 hello S1 版本。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="8c6a5-125">每個單位的 hello S1 edition 可讓向上 too400，000 到所有連線的裝置每天的訊息。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="8c6a5-126">**標準 S2**： 使用 hello S2 edition 的 IoT 解決方案所在的裝置會產生大量的資料。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="8c6a5-127">每個單位的 hello S2 edition 可讓向上 too6 百萬個訊息每日之間所有連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="8c6a5-128">**標準 S3**： 產生大量資料的 IoT 解決方案使用 hello S3 版本。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="8c6a5-129">每個單位的 hello S3 edition 可讓向上 too300 百萬個訊息每日之間所有連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="8c6a5-130">IoT 中樞只允許每個 Azure 訂用帳戶有一個免費中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="8c6a5-131">IoT 中樞單位</span><span class="sxs-lookup"><span data-stu-id="8c6a5-131">IoT hub units</span></span>

<span data-ttu-id="8c6a5-132">hello 訊息允許每個每日的單位數目取決於您的中樞定價層。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="8c6a5-133">例如，如果您想 hello IoT 中樞 toosupport 輸入的 700,000 訊息時，您可以選擇 S1 層的兩個單位。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="8c6a5-134">裝置 toocloud 資料分割和資源群組</span><span class="sxs-lookup"><span data-stu-id="8c6a5-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="8c6a5-135">您可以變更 hello IoT 中樞的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="8c6a5-136">hello 的資料分割的預設值為 4，您可以從 hello 下拉式清單選擇不同的數字。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="8c6a5-137">您不需要 tooexplicitly 建立空的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="8c6a5-138">當您建立資源時，您可以選擇在新的任一 toocreate，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="8c6a5-139">選擇訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8c6a5-139">Choose subscription</span></span>

<span data-ttu-id="8c6a5-140">Azure IoT 中樞自動列出 hello hello Azure 訂用帳戶的使用者帳戶會連結到。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="8c6a5-141">您可以選擇 hello Azure 訂用帳戶 tooassociate hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="8c6a5-142">選擇 hello 位置</span><span class="sxs-lookup"><span data-stu-id="8c6a5-142">Choose hello location</span></span>

<span data-ttu-id="8c6a5-143">hello 位置選項提供 hello IoT 中樞所在的地區的清單。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="8c6a5-144">建立 hello IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8c6a5-144">Create hello IoT hub</span></span>

<span data-ttu-id="8c6a5-145">上述所有步驟完成時，您可以建立 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="8c6a5-146">按一下**建立**toostart hello 後端程序 toocreate 及部署您所選擇的 hello 選項與 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="8c6a5-147">它可能需要幾分鐘的時間 toocreate hello IoT 中樞，因為它需要花費一些時間 hello 後端部署 toorun hello 適當位置的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="8c6a5-148">變更 hello hello IoT 中樞設定</span><span class="sxs-lookup"><span data-stu-id="8c6a5-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="8c6a5-149">建立從 hello IoT 中樞刀鋒視窗之後，您可以變更現有的 IoT 中樞 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="8c6a5-150">**共用存取原則**： 這些原則定義裝置與服務 tooconnect tooIoT 中樞的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="8c6a5-151">您可以按一下 [一般] 之下的 [共用存取原則] 來存取這些原則。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="8c6a5-152">在這個刀鋒視窗中，您可以修改現有的原則或新增原則。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="8c6a5-153">建立原則</span><span class="sxs-lookup"><span data-stu-id="8c6a5-153">Create a policy</span></span>

* <span data-ttu-id="8c6a5-154">按一下**新增**tooopen 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="8c6a5-155">您可以在這裡輸入 hello 新原則的名稱和圖 hello 下列所示，想要與此原則，tooassociate hello 權限：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="8c6a5-156">有許多權限可與這些共用原則產生關聯。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="8c6a5-157">hello**登錄讀取**和**登錄寫入**原則授與讀取和寫入存取權限 toohello 身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="8c6a5-158">自動選擇 hello 寫入選項選擇 hello 讀取選項。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="8c6a5-159">hello**服務連線**原則授與權限 tooaccess 服務端點，例如**接收裝置到雲端**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="8c6a5-160">hello**裝置連線**原則授與傳送和接收訊息使用 hello IoT 中樞裝置端端點的權限。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="8c6a5-161">按一下**建立**tooadd 此新建立的原則 toohello 現有清單。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="8c6a5-162">端點</span><span class="sxs-lookup"><span data-stu-id="8c6a5-162">Endpoints</span></span>

<span data-ttu-id="8c6a5-163">按一下**端點**toodisplay hello IoT 中樞，您要修改的端點清單。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="8c6a5-164">有兩種類型的端點： hello IoT 中樞，內建的端點和您在建立之後新增 toohello IoT 中樞端點。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="8c6a5-165">內建端點</span><span class="sxs-lookup"><span data-stu-id="8c6a5-165">Built-in endpoints</span></span>

<span data-ttu-id="8c6a5-166">有兩個內建端點：**雲端 toodevice 意見反應**和**事件**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="8c6a5-167">**雲端 toodevice 意見反應**設定： 此設定有兩個 subsettings:**雲端 tooDevice TTL** （-存留時間） 和**保留時間**（以小時為單位） 的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="8c6a5-168">當您第一次建立 IoT 中樞時，這些設定會有一小時的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="8c6a5-169">tooadjust 這些設定，請使用 hello 滑桿，或輸入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="8c6a5-170">**事件**設定：這個設定有數個子設定，其中有些是唯讀。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="8c6a5-171">hello 下列清單描述這些設定：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="8c6a5-172">**資料分割**： 建立 hello IoT 中樞時，會設定預設值。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="8c6a5-173">您可以變更 hello 透過這項設定的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="8c6a5-174">**事件中樞相容的名稱和端點**： 建立 hello IoT 中樞時，事件中心建立在內部，您可能需要存取 toounder 某些情況。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="8c6a5-175">您無法自訂 hello 事件中樞相容名稱與端點的值，但您可以按一下 複製**複製**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="8c6a5-176">**保留時間**： 依預設，設定 tooone 天，但您可以使用變更 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="8c6a5-177">這個值是以 hello 裝置到雲端設定的天數。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="8c6a5-178">**取用者群組**： 取用者群組可讓多個讀取器 tooread 訊息分開 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="8c6a5-179">每個 IoT 中樞都是使用預設取用者群組建立的。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="8c6a5-180">不過，您可以新增或刪除使用此設定的取用者群組 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8c6a5-181">無法編輯或刪除 hello 預設取用者群組。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="8c6a5-182">自訂端點</span><span class="sxs-lookup"><span data-stu-id="8c6a5-182">Custom endpoints</span></span>

<span data-ttu-id="8c6a5-183">您可以加入自訂端點，在您使用 hello 入口網站的 IoT 中樞上。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="8c6a5-184">從 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooopen hello**加入端點**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="8c6a5-185">輸入 hello 所需的資訊，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="8c6a5-186">您的自訂端點現在會列示在 hello 主要**端點**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="8c6a5-187">您可以在[參考 - IoT 中樞端點][lnk-devguide-endpoints]中深入了解自訂端點。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="8c6a5-188">路由</span><span class="sxs-lookup"><span data-stu-id="8c6a5-188">Routes</span></span>

<span data-ttu-id="8c6a5-189">按一下**路由**toomanage IoT 中樞將您的裝置到雲端訊息的分派。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="8c6a5-190">您可以按一下 新增路由 tooyour IoT 中樞**新增**頂端的 hello hello**路由*** 刀鋒視窗中，輸入所需的 hello 的詳細資訊，並按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="8c6a5-191">您的路由再列於 hello 主要**路由**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="8c6a5-192">您可以編輯路由的路由 hello 清單中按一下。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="8c6a5-193">tooenable 路由，路由 hello 清單中按一下它，並設定 hello**啟用**太切換**關閉**。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="8c6a5-194">toosave hello 變更，按一下 **確定**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="8c6a5-195">價格和調整</span><span class="sxs-lookup"><span data-stu-id="8c6a5-195">Pricing and scale</span></span>

<span data-ttu-id="8c6a5-196">可以變更現有 IoT 中樞定價 hello 透過 hello**定價**設定，以下列例外狀況的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c6a5-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="8c6a5-197">Hello 目前實作中，在 IoT 中樞與可用的 SKU 無法變更層 tooone 的 hello 付費的 Sku，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="8c6a5-198">在 hello Azure 訂用帳戶只能有一個免費層 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="8c6a5-199">Hello 傳送該日的訊息數目超過 hello 較低層的 hello 配額時，才可以移動從較高的 toolower 層。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="8c6a5-200">例如，如果 hello 每天的訊息數目超過 400000，然後 hello 層 hello IoT 中樞可變更。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="8c6a5-201">不過，如果您變更 toohello S1 層 hello IoT 中心已節流的那一天。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="8c6a5-202">刪除 hello IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8c6a5-202">Delete hello IoT hub</span></span>

<span data-ttu-id="8c6a5-203">您可以瀏覽要依序按一下 toodelete toohello IoT 中樞**瀏覽**，然後選擇 hello 適當中樞 toodelete 和。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="8c6a5-204">toodelete hello IoT 中樞中，按一下 hello**刪除**hello IoT 中樞名稱下方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c6a5-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c6a5-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c6a5-205">Next steps</span></span>

<span data-ttu-id="8c6a5-206">請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="8c6a5-207">[大量管理 IoT 裝置][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="8c6a5-208">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="8c6a5-209">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="8c6a5-210">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8c6a5-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8c6a5-211">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8c6a5-212">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="8c6a5-213">[保護您的 IoT 解決方案從接地 hello][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="8c6a5-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
