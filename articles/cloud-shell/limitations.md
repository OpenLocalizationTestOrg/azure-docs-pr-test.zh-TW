---
title: "aaaAzure 雲端殼層 （預覽） 限制 |Microsoft 文件"
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
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="801c5-103">Azure Cloud Shell 限制</span><span class="sxs-lookup"><span data-stu-id="801c5-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="801c5-104">Azure 的雲端 Shell 具有 hello 下列已知限制：</span><span class="sxs-lookup"><span data-stu-id="801c5-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="801c5-105">系統狀態和持續性</span><span class="sxs-lookup"><span data-stu-id="801c5-105">System state and persistence</span></span>
<span data-ttu-id="801c5-106">提供您的雲端殼層工作階段的 hello 機器是暫時性的而且您的工作階段未使用達 20 分鐘後回收。</span><span class="sxs-lookup"><span data-stu-id="801c5-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="801c5-107">雲端殼層需要裝載檔案共用 toobe。</span><span class="sxs-lookup"><span data-stu-id="801c5-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="801c5-108">如此一來，您的訂用帳戶必須是能夠 tooset 總儲存體資源 tooaccess 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="801c5-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="801c5-109">其他考量包括：</span><span class="sxs-lookup"><span data-stu-id="801c5-109">Other considerations include:</span></span>
* <span data-ttu-id="801c5-110">在掛接的儲存體中，只會保存 `$Home` 目錄或 `clouddrive` 目錄內的修改。</span><span class="sxs-lookup"><span data-stu-id="801c5-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="801c5-111">只能從您的[已指派區域](persisting-shell-storage.md#mount-a-new-clouddrive)內掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="801c5-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="801c5-112">Azure 檔案只支援本機備援儲存體和異地備援儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="801c5-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="801c5-113">使用者權限</span><span class="sxs-lookup"><span data-stu-id="801c5-113">User permissions</span></span>
<span data-ttu-id="801c5-114">權限設定為沒有 sudo 存取權的一般使用者。</span><span class="sxs-lookup"><span data-stu-id="801c5-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="801c5-115">將不會保存 `$Home` 目錄之外的任何安裝。</span><span class="sxs-lookup"><span data-stu-id="801c5-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="801c5-116">雖然某些命令內 hello`clouddrive`目錄下，例如`git clone`，並沒有適當的權限，您`$Home`目錄沒有權限。</span><span class="sxs-lookup"><span data-stu-id="801c5-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="801c5-117">瀏覽器支援</span><span class="sxs-lookup"><span data-stu-id="801c5-117">Browser support</span></span>
<span data-ttu-id="801c5-118">雲端殼層可支援 Microsoft Edge、 Microsoft Internet Explorer、 Google Chrome、 Mozilla Firefox 及 Apple Safari hello 最新的版本。</span><span class="sxs-lookup"><span data-stu-id="801c5-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="801c5-119">不支援 Safari 私密瀏覽模式。</span><span class="sxs-lookup"><span data-stu-id="801c5-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="801c5-120">複製和貼上</span><span class="sxs-lookup"><span data-stu-id="801c5-120">Copy and paste</span></span>
<span data-ttu-id="801c5-121">Ctrl + C 和 Ctrl + V 無法運作，以及複製/貼上快速鍵在雲端介面中 Windows 電腦上，使用 Ctrl + Insert 和 Shift + Insert toocopy 貼分別。</span><span class="sxs-lookup"><span data-stu-id="801c5-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="801c5-122">以滑鼠右鍵按一下複製和貼上選項也可使用，但以滑鼠右鍵按一下函式是主體 toobrowser 特定剪貼簿存取。</span><span class="sxs-lookup"><span data-stu-id="801c5-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="801c5-123">編輯 .bashrc</span><span class="sxs-lookup"><span data-stu-id="801c5-123">Editing .bashrc</span></span>
<span data-ttu-id="801c5-124">編輯 .bashrc 時請小心，這麼做可能會導致 Cloud Shell 發生未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="801c5-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="801c5-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="801c5-125">.bash_history</span></span>
<span data-ttu-id="801c5-126">Bash 命令的歷程記錄可能因為 Cloud Shell 工作階段中斷或並行工作階段而出現不一致的情況。</span><span class="sxs-lookup"><span data-stu-id="801c5-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="801c5-127">使用限制</span><span class="sxs-lookup"><span data-stu-id="801c5-127">Usage limits</span></span>
<span data-ttu-id="801c5-128">Cloud Shell 主要用於互動式的使用案例。</span><span class="sxs-lookup"><span data-stu-id="801c5-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="801c5-129">因此，任何長時間執行而沒有互動的工作階段會在不發出警告的情況下結束。</span><span class="sxs-lookup"><span data-stu-id="801c5-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="801c5-130">網路連線</span><span class="sxs-lookup"><span data-stu-id="801c5-130">Network connectivity</span></span>
<span data-ttu-id="801c5-131">在雲端介面中的任何延遲主體 toolocal 網際網路連線，雲端殼層會繼續 tooattempt toocarry 時傳送的任何指示。</span><span class="sxs-lookup"><span data-stu-id="801c5-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="801c5-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="801c5-132">Next steps</span></span>
[<span data-ttu-id="801c5-133">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="801c5-133">Cloud Shell Quickstart</span></span>](quickstart.md)
