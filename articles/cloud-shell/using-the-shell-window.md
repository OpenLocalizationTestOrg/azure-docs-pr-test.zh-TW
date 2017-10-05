---
title: "使用 Azure Cloud Shell (預覽) 視窗 | Microsoft Docs"
description: "逐步解說 Azure Cloud Shell 視窗。"
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
ms.openlocfilehash: a47961dfdaf178a6b793bd68105d9792a9275bb3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-azure-cloud-shell-window"></a><span data-ttu-id="fa949-103">使用 Azure Cloud Shell 視窗</span><span class="sxs-lookup"><span data-stu-id="fa949-103">Using the Azure Cloud Shell window</span></span>

<span data-ttu-id="fa949-104">本文件說明如何使用 Cloud Shell 視窗。</span><span class="sxs-lookup"><span data-stu-id="fa949-104">This document explains how to use the Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="fa949-105">並行工作階段</span><span class="sxs-lookup"><span data-stu-id="fa949-105">Concurrent sessions</span></span>
<span data-ttu-id="fa949-106">Cloud Shell 可透過允許每個工作階段以個別 Bash 處理序的形式存在，來允許跨瀏覽器索引標籤進行多個並行工作階段。</span><span class="sxs-lookup"><span data-stu-id="fa949-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.</span></span>
<span data-ttu-id="fa949-107">如果要結束工作階段，請務必從每個工作階段視窗結束，因為每個處理序雖然是在相同的電腦上執行，但卻是獨立執行的。</span><span class="sxs-lookup"><span data-stu-id="fa949-107">If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="fa949-108">重新啟動 Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="fa949-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="fa949-109">重新啟動 Cloud Shell 將會重設電腦狀態，而所有未由檔案共用保存的檔案都將遺失。</span><span class="sxs-lookup"><span data-stu-id="fa949-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="fa949-110">按一下工具列上的 [重新啟動] 圖示，即可接收新的 Cloud Shell 環境。</span><span class="sxs-lookup"><span data-stu-id="fa949-110">Click the restart icon on the toolbar to receive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="fa949-111">將 Cloud Shell 視窗最大化和最小化</span><span class="sxs-lookup"><span data-stu-id="fa949-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="fa949-112">按一下視窗右上方的 [最小化] 圖示，即可將視窗隱藏。</span><span class="sxs-lookup"><span data-stu-id="fa949-112">Click the minimize icon on the top right of the window to hide it.</span></span> <span data-ttu-id="fa949-113">再按一下 [Cloud Shell] 圖示，即可取消隱藏。</span><span class="sxs-lookup"><span data-stu-id="fa949-113">Click the Cloud Shell icon again to unhide.</span></span>
* <span data-ttu-id="fa949-114">按一下 [最大化] 圖示，即可將視窗設成最大高度。</span><span class="sxs-lookup"><span data-stu-id="fa949-114">Click the maximize icon to set window to max height.</span></span> <span data-ttu-id="fa949-115">若要將視窗還原到先前的大小，請按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="fa949-115">To restore window to previous size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="fa949-116">複製和貼上</span><span class="sxs-lookup"><span data-stu-id="fa949-116">Copy and paste</span></span>
* <span data-ttu-id="fa949-117">Windows：`Ctrl-insert` 進行複製，`Shift-insert` 即可貼上。</span><span class="sxs-lookup"><span data-stu-id="fa949-117">Windows: `Ctrl-insert` to copy and `Shift-insert` to paste.</span></span> <span data-ttu-id="fa949-118">在下拉式清單上按一下滑鼠右鍵，也能進行複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="fa949-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="fa949-119">FireFox/IE 可能無法正確支援剪貼簿權限。</span><span class="sxs-lookup"><span data-stu-id="fa949-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="fa949-120">Mac 作業系統：`Cmd-c` 進行複製，`Cmd-v` 即可貼上。</span><span class="sxs-lookup"><span data-stu-id="fa949-120">Mac OS: `Cmd-c` to copy and `Cmd-v` to paste.</span></span> <span data-ttu-id="fa949-121">在下拉式清單上按一下滑鼠右鍵，也能進行複製/貼上。</span><span class="sxs-lookup"><span data-stu-id="fa949-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="fa949-122">調整 Cloud Shell 視窗大小</span><span class="sxs-lookup"><span data-stu-id="fa949-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="fa949-123">按一下工具列上邊緣並向上或向下拖曳，即可調整 Cloud Shell 視窗大小。</span><span class="sxs-lookup"><span data-stu-id="fa949-123">Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="fa949-124">捲動文字顯示</span><span class="sxs-lookup"><span data-stu-id="fa949-124">Scrolling text display</span></span>
* <span data-ttu-id="fa949-125">使用您的滑鼠或觸控板來捲動終端機文字。</span><span class="sxs-lookup"><span data-stu-id="fa949-125">Scroll with your mouse or touchpad to move terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="fa949-126">結束命令</span><span class="sxs-lookup"><span data-stu-id="fa949-126">Exit command</span></span>
<span data-ttu-id="fa949-127">執行 `exit` 可終止作用中的工作階段。</span><span class="sxs-lookup"><span data-stu-id="fa949-127">Running `exit` terminates the active session.</span></span> <span data-ttu-id="fa949-128">此行為預設會在 20 分鐘後發生，不須進行互動。</span><span class="sxs-lookup"><span data-stu-id="fa949-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa949-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa949-129">Next steps</span></span>
[<span data-ttu-id="fa949-130">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="fa949-130">Cloud Shell Quickstart</span></span>](quickstart.md)
