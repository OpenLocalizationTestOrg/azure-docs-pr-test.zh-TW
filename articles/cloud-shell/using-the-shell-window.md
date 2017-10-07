---
title: "aaaUsing hello Azure 雲端殼層 （預覽） 視窗 |Microsoft 文件"
description: "逐步解說 hello Azure 雲端殼層 視窗。"
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
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="d66e7-103">使用 hello Azure 雲端殼層 視窗</span><span class="sxs-lookup"><span data-stu-id="d66e7-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="d66e7-104">本文件說明如何 toouse hello 雲端殼層 視窗。</span><span class="sxs-lookup"><span data-stu-id="d66e7-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="d66e7-105">並行工作階段</span><span class="sxs-lookup"><span data-stu-id="d66e7-105">Concurrent sessions</span></span>
<span data-ttu-id="d66e7-106">雲端殼層跨瀏覽器索引標籤可讓多個並行工作階段，藉由使用個別的 Bash 程序的每個工作階段 tooexist。</span><span class="sxs-lookup"><span data-stu-id="d66e7-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="d66e7-107">如果結束工作階段，請務必從每個工作階段視窗 tooexit 雖然它們在上執行每個處理序執行獨立 hello 相同的電腦。</span><span class="sxs-lookup"><span data-stu-id="d66e7-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="d66e7-108">重新啟動 Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d66e7-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="d66e7-109">重新啟動 Cloud Shell 將會重設電腦狀態，而所有未由檔案共用保存的檔案都將遺失。</span><span class="sxs-lookup"><span data-stu-id="d66e7-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="d66e7-110">按一下新的雲端 Shell 環境的 hello 工具列 tooreceive hello 重新啟動圖示。</span><span class="sxs-lookup"><span data-stu-id="d66e7-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="d66e7-111">將 Cloud Shell 視窗最大化和最小化</span><span class="sxs-lookup"><span data-stu-id="d66e7-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="d66e7-112">按一下 hello hello 圖示最小化右上角的 hello 視窗 toohide 它。</span><span class="sxs-lookup"><span data-stu-id="d66e7-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="d66e7-113">再按一下 hello 雲端殼層圖示 toounhide。</span><span class="sxs-lookup"><span data-stu-id="d66e7-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="d66e7-114">按一下 hello 最大化圖示 tooset 視窗 toomax 高度。</span><span class="sxs-lookup"><span data-stu-id="d66e7-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="d66e7-115">toorestore 視窗 tooprevious 大小，請按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="d66e7-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="d66e7-116">複製和貼上</span><span class="sxs-lookup"><span data-stu-id="d66e7-116">Copy and paste</span></span>
* <span data-ttu-id="d66e7-117">Windows: `Ctrl-insert` toocopy 和`Shift-insert`toopaste。</span><span class="sxs-lookup"><span data-stu-id="d66e7-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="d66e7-118">在下拉式清單上按一下滑鼠右鍵，也能進行複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="d66e7-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="d66e7-119">FireFox/IE 可能無法正確支援剪貼簿權限。</span><span class="sxs-lookup"><span data-stu-id="d66e7-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="d66e7-120">Mac OS: `Cmd-c` toocopy 和`Cmd-v`toopaste。</span><span class="sxs-lookup"><span data-stu-id="d66e7-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="d66e7-121">在下拉式清單上按一下滑鼠右鍵，也能進行複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="d66e7-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="d66e7-122">調整 Cloud Shell 視窗大小</span><span class="sxs-lookup"><span data-stu-id="d66e7-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="d66e7-123">按一下並拖曳 hello hello 工具列上的邊緣向上或向下 tooresize hello 雲端殼層 視窗。</span><span class="sxs-lookup"><span data-stu-id="d66e7-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="d66e7-124">捲動文字顯示</span><span class="sxs-lookup"><span data-stu-id="d66e7-124">Scrolling text display</span></span>
* <span data-ttu-id="d66e7-125">使用滑鼠或觸控板 toomove 終端機文字捲動。</span><span class="sxs-lookup"><span data-stu-id="d66e7-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="d66e7-126">結束命令</span><span class="sxs-lookup"><span data-stu-id="d66e7-126">Exit command</span></span>
<span data-ttu-id="d66e7-127">執行`exit`終止 hello 作用中工作階段。</span><span class="sxs-lookup"><span data-stu-id="d66e7-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="d66e7-128">此行為預設會在 20 分鐘後發生，不須進行互動。</span><span class="sxs-lookup"><span data-stu-id="d66e7-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d66e7-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d66e7-129">Next steps</span></span>
[<span data-ttu-id="d66e7-130">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="d66e7-130">Cloud Shell Quickstart</span></span>](quickstart.md)
