---
title: "aaaAzure IoT 中樞 IP 連線篩選器 |Microsoft 文件"
description: "如何篩選 tooblock 連接從特定 IP 的 toouse IP 位址 tooyour Azure IoT 中樞。 您可以封鎖來自個別 IP 位址或 IP 位址範圍的連接。"
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="9cb96-104">使用 IP 篩選器</span><span class="sxs-lookup"><span data-stu-id="9cb96-104">Use IP filters</span></span>

<span data-ttu-id="9cb96-105">安全性是任何以 Azure IoT 中樞為基礎之 IoT 解決方案的重要一環。</span><span class="sxs-lookup"><span data-stu-id="9cb96-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="9cb96-106">有時候您需要 tooexplicitly hello IP 位址的裝置都能連接指定做為您的安全性組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cb96-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="9cb96-107">hello _IP 篩選器_功能可讓您 tooconfigure 規則拒絕或接受來自特定的 IPv4 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="9cb96-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="9cb96-108">當 toouse</span><span class="sxs-lookup"><span data-stu-id="9cb96-108">When toouse</span></span>

<span data-ttu-id="9cb96-109">特定的 IP 位址的有用 tooblock hello IoT 中樞端點時，有兩個特定的使用案例：</span><span class="sxs-lookup"><span data-stu-id="9cb96-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="9cb96-110">您的 IoT 中樞只應接收來自指定 IP 位址範圍的流量，並拒絕其他所有流量。</span><span class="sxs-lookup"><span data-stu-id="9cb96-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="9cb96-111">例如，您使用您的 IoT 中樞與[Azure Express Route] toocreate IoT 中樞與您在內部部署基礎結構之間的私人連線。</span><span class="sxs-lookup"><span data-stu-id="9cb96-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="9cb96-112">您必須從已經由 hello IoT 中樞管理員識別為可疑的 IP 位址的 tooreject 流量。</span><span class="sxs-lookup"><span data-stu-id="9cb96-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="9cb96-113">篩選器規則的套用方式</span><span class="sxs-lookup"><span data-stu-id="9cb96-113">How filter rules are applied</span></span>

<span data-ttu-id="9cb96-114">hello IP 篩選器規則會套用在 hello IoT 中樞服務層級。</span><span class="sxs-lookup"><span data-stu-id="9cb96-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="9cb96-115">因此 hello IP 篩選器規則適用於 tooall 連線從裝置和使用任何支援的通訊協定的後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cb96-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="9cb96-116">嘗試建立連線的 IP 位址若符合 IoT 中樞內的拒絕 IP 規則，將會收到未授權 401 狀態碼和描述。</span><span class="sxs-lookup"><span data-stu-id="9cb96-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="9cb96-117">hello 回應訊息不會提到 hello IP 規則。</span><span class="sxs-lookup"><span data-stu-id="9cb96-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="9cb96-118">預設設定</span><span class="sxs-lookup"><span data-stu-id="9cb96-118">Default setting</span></span>

<span data-ttu-id="9cb96-119">根據預設，hello **IP 篩選器**IoT 中樞的 hello 入口網站中的方格是空的。</span><span class="sxs-lookup"><span data-stu-id="9cb96-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="9cb96-120">這項預設設定表示您的中樞可接受來自任何 IP 位址的連線。</span><span class="sxs-lookup"><span data-stu-id="9cb96-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="9cb96-121">這項預設值是對等 tooa 規則可接受 hello 0.0.0.0/0 的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="9cb96-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![IoT 中樞預設 IP 篩選器設定][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="9cb96-123">新增或編輯 IP 篩選器規則</span><span class="sxs-lookup"><span data-stu-id="9cb96-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="9cb96-124">當您新增的 IP 篩選器規則時，系統會提示您 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="9cb96-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="9cb96-125">**IP 篩選器規則名稱**必須是唯一、 不區分大小寫英數字元組成 too128 字元字串。</span><span class="sxs-lookup"><span data-stu-id="9cb96-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="9cb96-126">只有 hello ASCII 7 位元英數字元加上`{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`接受。</span><span class="sxs-lookup"><span data-stu-id="9cb96-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="9cb96-127">選取**拒絕**或**接受**為 hello**動作**hello IP 篩選規則。</span><span class="sxs-lookup"><span data-stu-id="9cb96-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="9cb96-128">提供單一 IPv4 位址或以 CIDR 標記法表示的 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="9cb96-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="9cb96-129">例如，在 CIDR 標記法 192.168.100.0/22 代表 hello 1024 IPv4 位址從 192.168.100.0 too192.168.103.255。</span><span class="sxs-lookup"><span data-stu-id="9cb96-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![新增 IP 篩選器規則 tooan IoT 中樞][img-ip-filter-add-rule]

<span data-ttu-id="9cb96-131">儲存 hello 規則之後，您會看到警示通知您該 hello 更新正在進行中。</span><span class="sxs-lookup"><span data-stu-id="9cb96-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![有關儲存 IP 篩選器規則的通知][img-ip-filter-save-new-rule]

<span data-ttu-id="9cb96-133">hello**新增**選項已停用，當您到達 hello 最多 10 個 IP 篩選器規則。</span><span class="sxs-lookup"><span data-stu-id="9cb96-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="9cb96-134">按兩下包含 hello 規則的 hello 資料列，您可以編輯現有的規則。</span><span class="sxs-lookup"><span data-stu-id="9cb96-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="9cb96-135">拒絕 IP 位址可以防止其他 Azure 服務時 （例如 Azure Stream Analytics、 Azure 虛擬機器或在 hello 入口網站中的 hello 裝置總管） 與 hello IoT 中樞進行互動。</span><span class="sxs-lookup"><span data-stu-id="9cb96-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="9cb96-136">如果您使用 Azure 資料流分析 （asa） 一類 tooread 訊息從 IoT 中樞啟用 IP 篩選條件時，使用 hello 事件中樞相容名稱和您的 IoT 中樞端點 hello ASA 連接字串中。</span><span class="sxs-lookup"><span data-stu-id="9cb96-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="9cb96-137">刪除 IP 篩選器規則</span><span class="sxs-lookup"><span data-stu-id="9cb96-137">Delete an IP filter rule</span></span>

<span data-ttu-id="9cb96-138">toodelete IP 篩選器規則 hello 方格中按一下 選取一個或多個規則**刪除**。</span><span class="sxs-lookup"><span data-stu-id="9cb96-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![刪除 IoT 中樞 IP 篩選器規則][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="9cb96-140">IP 篩選器規則評估</span><span class="sxs-lookup"><span data-stu-id="9cb96-140">IP filter rule evaluation</span></span>

<span data-ttu-id="9cb96-141">IP 篩選器規則會套用順序並 hello 第一個規則符合 hello IP 位址，會決定 hello 接受或拒絕動作。</span><span class="sxs-lookup"><span data-stu-id="9cb96-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="9cb96-142">例如，如果您想要在 hello 範圍 192.168.100.0/22 tooaccept 位址，並拒絕所有其他項目，hello hello 方格中的第一個規則應該接受 hello 位址範圍 192.168.100.0/22。</span><span class="sxs-lookup"><span data-stu-id="9cb96-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="9cb96-143">hello 下一個規則應該拒絕所有位址使用 hello 範圍 0.0.0.0/0。</span><span class="sxs-lookup"><span data-stu-id="9cb96-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="9cb96-144">您可以變更您的 IP 篩選器規則 hello 方格中的 hello 順序按一下 hello 三個垂直的點在 hello 開頭的資料列並使用拖曳和卸除。</span><span class="sxs-lookup"><span data-stu-id="9cb96-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="9cb96-145">toosave 您新的 IP 篩選器規則的順序，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9cb96-145">toosave your new IP filter rule order, click **Save**.</span></span>

![變更您的 IoT 中樞 IP 篩選器規則 hello 順序][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="9cb96-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cb96-147">Next steps</span></span>

<span data-ttu-id="9cb96-148">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9cb96-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="9cb96-149">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="9cb96-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="9cb96-150">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="9cb96-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md