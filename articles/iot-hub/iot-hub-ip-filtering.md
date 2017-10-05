---
title: "Azure IoT 中樞 IP 連線篩選器 | Microsoft Docs"
description: "如何使用 IP 篩選來封鎖從特定 IP 位址至 Azure IoT 中樞的連接。 您可以封鎖來自個別 IP 位址或 IP 位址範圍的連接。"
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
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="0484e-104">使用 IP 篩選器</span><span class="sxs-lookup"><span data-stu-id="0484e-104">Use IP filters</span></span>

<span data-ttu-id="0484e-105">安全性是任何以 Azure IoT 中樞為基礎之 IoT 解決方案的重要一環。</span><span class="sxs-lookup"><span data-stu-id="0484e-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="0484e-106">有時候您需要在執行安全性設定的程序中明確地指定可連線的裝置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0484e-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="0484e-107">「IP 篩選器」功能可讓您設定規則，以拒絕或接受來自特定 IPv4 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="0484e-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="0484e-108">使用時機</span><span class="sxs-lookup"><span data-stu-id="0484e-108">When to use</span></span>

<span data-ttu-id="0484e-109">有兩個特定使用案例適合封鎖特定 IP 位址的 IoT 中樞端點︰</span><span class="sxs-lookup"><span data-stu-id="0484e-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="0484e-110">您的 IoT 中樞只應接收來自指定 IP 位址範圍的流量，並拒絕其他所有流量。</span><span class="sxs-lookup"><span data-stu-id="0484e-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="0484e-111">例如，您搭配 [Azure Express Route] 使用 IoT 中樞來建立 IoT 中樞與內部部署基礎結構之間的私人連線。</span><span class="sxs-lookup"><span data-stu-id="0484e-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="0484e-112">您需要拒絕 IoT 中樞系統管理員認為可疑的 IP 位址所傳來的流量。</span><span class="sxs-lookup"><span data-stu-id="0484e-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="0484e-113">篩選器規則的套用方式</span><span class="sxs-lookup"><span data-stu-id="0484e-113">How filter rules are applied</span></span>

<span data-ttu-id="0484e-114">IP 篩選器規則會套用在 IoT 中樞服務層級。</span><span class="sxs-lookup"><span data-stu-id="0484e-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="0484e-115">因此，IP 篩選器規則會套用至來自裝置和後端應用程式的所有連接 (使用任何受支援的通訊協定)。</span><span class="sxs-lookup"><span data-stu-id="0484e-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="0484e-116">嘗試建立連線的 IP 位址若符合 IoT 中樞內的拒絕 IP 規則，將會收到未授權 401 狀態碼和描述。</span><span class="sxs-lookup"><span data-stu-id="0484e-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="0484e-117">回應訊息則不涉及 IP 規則。</span><span class="sxs-lookup"><span data-stu-id="0484e-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="0484e-118">預設設定</span><span class="sxs-lookup"><span data-stu-id="0484e-118">Default setting</span></span>

<span data-ttu-id="0484e-119">根據預設，IoT 中樞之入口網站中的 **IP 篩選器**方格是空的。</span><span class="sxs-lookup"><span data-stu-id="0484e-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="0484e-120">這項預設設定表示您的中樞可接受來自任何 IP 位址的連線。</span><span class="sxs-lookup"><span data-stu-id="0484e-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="0484e-121">這項預設設定等同於可接受 0.0.0.0/0 IP 位址範圍的規則。</span><span class="sxs-lookup"><span data-stu-id="0484e-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![IoT 中樞預設 IP 篩選器設定][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="0484e-123">新增或編輯 IP 篩選器規則</span><span class="sxs-lookup"><span data-stu-id="0484e-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="0484e-124">當您新增 IP 篩選器規則時，系統會提示您輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="0484e-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="0484e-125">[IP 篩選器規則名稱] 必須是唯一、不區分大小寫的英數字元字串，最長可為 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="0484e-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="0484e-126">所能接受的字元只有 ASCII 7 位元英數字元以及 `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`。</span><span class="sxs-lookup"><span data-stu-id="0484e-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="0484e-127">選取 [拒絕] 或 [接受] 做為 IP 篩選器規則的 [動作]。</span><span class="sxs-lookup"><span data-stu-id="0484e-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="0484e-128">提供單一 IPv4 位址或以 CIDR 標記法表示的 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="0484e-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="0484e-129">例如，在 CIDR 表示法中，192.168.100.0/22 表示從 192.168.100.0 到 192.168.103.255 的 1024 個 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="0484e-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![新增 IP 篩選器規則到 IoT 中樞][img-ip-filter-add-rule]

<span data-ttu-id="0484e-131">儲存規則之後，您會看到通知您正在進行更新的警示。</span><span class="sxs-lookup"><span data-stu-id="0484e-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![有關儲存 IP 篩選器規則的通知][img-ip-filter-save-new-rule]

<span data-ttu-id="0484e-133">當您達到 10 個 IP 篩選器規則的上限後，[新增] 選項便會停用。</span><span class="sxs-lookup"><span data-stu-id="0484e-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="0484e-134">您可以按兩下包含規則的資料列，以編輯現有規則。</span><span class="sxs-lookup"><span data-stu-id="0484e-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="0484e-135">拒絕 IP 位址可防止其他 Azure 服務 (例如 Azure 串流分析、Azure 虛擬機器，或入口網站中的裝置總管) 與 IoT 中樞互動。</span><span class="sxs-lookup"><span data-stu-id="0484e-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="0484e-136">如果您使用 Azure 串流分析 (ASA) 從啟用 IP 篩選的 IoT 中樞讀取訊息，請在 ASA 連接字串中使用 IoT 中樞之與事件中樞相容的名稱和端點。</span><span class="sxs-lookup"><span data-stu-id="0484e-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="0484e-137">刪除 IP 篩選器規則</span><span class="sxs-lookup"><span data-stu-id="0484e-137">Delete an IP filter rule</span></span>

<span data-ttu-id="0484e-138">若要刪除 IP 篩選器規則，請選取方格中的一個或多個規則，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0484e-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![刪除 IoT 中樞 IP 篩選器規則][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="0484e-140">IP 篩選器規則評估</span><span class="sxs-lookup"><span data-stu-id="0484e-140">IP filter rule evaluation</span></span>

<span data-ttu-id="0484e-141">IP 篩選器規則會依序套用，第一個符合 IP 位址的規則會決定接受或拒絕動作。</span><span class="sxs-lookup"><span data-stu-id="0484e-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="0484e-142">例如，如果您想要接受 192.168.100.0/22 範圍中的位址，並拒絕其他所有位址，則方格中的第一個規則應接受位址範圍 192.168.100.0/22。</span><span class="sxs-lookup"><span data-stu-id="0484e-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="0484e-143">下一個規則應使用 0.0.0.0/0 範圍拒絕所有位址。</span><span class="sxs-lookup"><span data-stu-id="0484e-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="0484e-144">按一下資料列前端呈垂直方向的三個點並使用拖放功能，即可變更方格中的 IP 篩選器規則順序。</span><span class="sxs-lookup"><span data-stu-id="0484e-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="0484e-145">若要儲存新的 IP 篩選器規則順序，請按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0484e-145">To save your new IP filter rule order, click **Save**.</span></span>

![變更 IoT 中樞 IP 篩選器規則的順序][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="0484e-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0484e-147">Next steps</span></span>

<span data-ttu-id="0484e-148">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="0484e-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="0484e-149">[作業監視][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="0484e-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="0484e-150">[IoT 中樞度量][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="0484e-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="0484e-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="0484e-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md