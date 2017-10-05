---
title: "Azure Cloud Shell (預覽) 限制 | Microsoft Docs"
description: "Azure Cloud Shell 限制的概觀"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="65cc1-103">Azure Cloud Shell 限制</span><span class="sxs-lookup"><span data-stu-id="65cc1-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="65cc1-104">Azure Cloud Shell 具有下列已知限制：</span><span class="sxs-lookup"><span data-stu-id="65cc1-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="65cc1-105">系統狀態和持續性</span><span class="sxs-lookup"><span data-stu-id="65cc1-105">System state and persistence</span></span>
<span data-ttu-id="65cc1-106">提供 Cloud Shell 工作階段的電腦只是暫時性，在工作階段閒置 20 分鐘後就會回收。</span><span class="sxs-lookup"><span data-stu-id="65cc1-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="65cc1-107">Cloud Shell 需要掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="65cc1-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="65cc1-108">因此，您的訂用帳戶必須能夠設定儲存體資源，才可存取 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="65cc1-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="65cc1-109">其他考量包括：</span><span class="sxs-lookup"><span data-stu-id="65cc1-109">Other considerations include:</span></span>
* <span data-ttu-id="65cc1-110">在掛接的儲存體中，只會保存 `$Home` 目錄或 `clouddrive` 目錄內的修改。</span><span class="sxs-lookup"><span data-stu-id="65cc1-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="65cc1-111">只能從您的[已指派區域](persisting-shell-storage.md#mount-a-new-clouddrive)內掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="65cc1-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="65cc1-112">Azure 檔案只支援本機備援儲存體和異地備援儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65cc1-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="65cc1-113">使用者權限</span><span class="sxs-lookup"><span data-stu-id="65cc1-113">User permissions</span></span>
<span data-ttu-id="65cc1-114">權限設定為沒有 sudo 存取權的一般使用者。</span><span class="sxs-lookup"><span data-stu-id="65cc1-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="65cc1-115">將不會保存 `$Home` 目錄之外的任何安裝。</span><span class="sxs-lookup"><span data-stu-id="65cc1-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="65cc1-116">雖然 `git clone` 目錄內的某些命令 (例如 `clouddrive`) 沒有適當的權限，但您的 `$Home` 目錄有適當的權限。</span><span class="sxs-lookup"><span data-stu-id="65cc1-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="65cc1-117">瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="65cc1-117">Browser support</span></span>
<span data-ttu-id="65cc1-118">Cloud Shell 支援最新版的 Microsoft Edge、Microsoft Internet Explorer、Google Chrome、Mozilla Firefox 及 Apple Safari。</span><span class="sxs-lookup"><span data-stu-id="65cc1-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="65cc1-119">不支援 Safari 私密瀏覽模式。</span><span class="sxs-lookup"><span data-stu-id="65cc1-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="65cc1-120">複製和貼上</span><span class="sxs-lookup"><span data-stu-id="65cc1-120">Copy and paste</span></span>
<span data-ttu-id="65cc1-121">Ctrl+C 和 Ctrl+V 無法在 Windows 電腦的 Cloud Shell 中做為複製/貼上的快速鍵運作，請分別使用 Ctrl+Insert 和 Shift+Insert 來複製及貼上。</span><span class="sxs-lookup"><span data-stu-id="65cc1-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="65cc1-122">也提供滑鼠右鍵的複製貼上選項，但滑鼠右鍵功能取決於瀏覽器特定的剪貼簿存取。</span><span class="sxs-lookup"><span data-stu-id="65cc1-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="65cc1-123">編輯 .bashrc</span><span class="sxs-lookup"><span data-stu-id="65cc1-123">Editing .bashrc</span></span>
<span data-ttu-id="65cc1-124">編輯 .bashrc 時請小心，這麼做可能會導致 Cloud Shell 發生未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="65cc1-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="65cc1-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="65cc1-125">.bash_history</span></span>
<span data-ttu-id="65cc1-126">Bash 命令的歷程記錄可能因為 Cloud Shell 工作階段中斷或並行工作階段而出現不一致的情況。</span><span class="sxs-lookup"><span data-stu-id="65cc1-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="65cc1-127">使用限制</span><span class="sxs-lookup"><span data-stu-id="65cc1-127">Usage limits</span></span>
<span data-ttu-id="65cc1-128">Cloud Shell 主要用於互動式的使用案例。</span><span class="sxs-lookup"><span data-stu-id="65cc1-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="65cc1-129">因此，任何長時間執行而沒有互動的工作階段會在不發出警告的情況下結束。</span><span class="sxs-lookup"><span data-stu-id="65cc1-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="65cc1-130">網路連線</span><span class="sxs-lookup"><span data-stu-id="65cc1-130">Network connectivity</span></span>
<span data-ttu-id="65cc1-131">Cloud Shell 中的任何延遲受限於本機網際網路連線，Cloud Shell 會繼續嘗試進行任何傳送的指示。</span><span class="sxs-lookup"><span data-stu-id="65cc1-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65cc1-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65cc1-132">Next steps</span></span>
[<span data-ttu-id="65cc1-133">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="65cc1-133">Cloud Shell Quickstart</span></span>](quickstart.md)
