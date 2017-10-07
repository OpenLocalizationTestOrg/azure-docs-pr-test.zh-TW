---
title: "aaaMicrosoft 威脅模型化工具-Azure |Microsoft 文件"
description: "深入了解 hello 威脅模型化工具中可用的所有 hello 功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="afa4c-103">威脅模型化工具功能概觀</span><span class="sxs-lookup"><span data-stu-id="afa4c-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="afa4c-104">我們很高興您威脅分析模型的需求選擇 toouse hello 威脅模型化工具 ！</span><span class="sxs-lookup"><span data-stu-id="afa4c-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="afa4c-105">如果您尚未這麼做，請瀏覽 **[hello 威脅模型化工具使用者入門](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="afa4c-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="afa4c-106">我們的工具會經常更新，因此請查看這引導通常 toosee 我們最新功能和增強功能。</span><span class="sxs-lookup"><span data-stu-id="afa4c-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="afa4c-107">按一下 hello 「 建立新模型 」 按鈕會開啟空白起始頁下, 面類似的 toohello 影像：</span><span class="sxs-lookup"><span data-stu-id="afa4c-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![空白起始分頁](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="afa4c-109">使用 hello 威脅模型由我們的團隊在 hello **[入門](./azure-security-threat-modeling-tool-getting-started.md)**範例中，讓我們今天簽出 hello 工具中可用的所有 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="afa4c-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![基本威脅模型](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="afa4c-111">導覽</span><span class="sxs-lookup"><span data-stu-id="afa4c-111">Navigation</span></span>

<span data-ttu-id="afa4c-112">一頭栽進 hello 內建功能，再看一下 hello hello 工具中找到的主要元件</span><span class="sxs-lookup"><span data-stu-id="afa4c-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="afa4c-113">功能表項目</span><span class="sxs-lookup"><span data-stu-id="afa4c-113">Menu items</span></span>

<span data-ttu-id="afa4c-114">hello 體驗應該類似 tooother Microsoft 產品。</span><span class="sxs-lookup"><span data-stu-id="afa4c-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="afa4c-115">讓我們先經過 hello 最上層功能表項目：</span><span class="sxs-lookup"><span data-stu-id="afa4c-115">Let’s begin by going through hello top-level menu items:</span></span>

![功能表項目](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="afa4c-117">標籤</span><span class="sxs-lookup"><span data-stu-id="afa4c-117">Label</span></span>                               | <span data-ttu-id="afa4c-118">詳細資料</span><span class="sxs-lookup"><span data-stu-id="afa4c-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-119">**檔案**</span><span class="sxs-lookup"><span data-stu-id="afa4c-119">**File**</span></span> | <ul><li><span data-ttu-id="afa4c-120">開啟、儲存並關閉檔案</span><span class="sxs-lookup"><span data-stu-id="afa4c-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="afa4c-121">登入/登出 OneDrive 帳戶</span><span class="sxs-lookup"><span data-stu-id="afa4c-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="afa4c-122">共用連結 (檢視 + 編輯)</span><span class="sxs-lookup"><span data-stu-id="afa4c-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="afa4c-123">檢視檔案資訊</span><span class="sxs-lookup"><span data-stu-id="afa4c-123">View File Information</span></span></li><li><span data-ttu-id="afa4c-124">套用新的範本 tooExisting 模型</span><span class="sxs-lookup"><span data-stu-id="afa4c-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="afa4c-125">**編輯**</span><span class="sxs-lookup"><span data-stu-id="afa4c-125">**Edit**</span></span> | <span data-ttu-id="afa4c-126">復原/重做動作，以及複製、貼上和刪除</span><span class="sxs-lookup"><span data-stu-id="afa4c-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="afa4c-127">**檢視**</span><span class="sxs-lookup"><span data-stu-id="afa4c-127">**View**</span></span> | <ul><li><span data-ttu-id="afa4c-128">在**分析**和**設計**檢視之間切換</span><span class="sxs-lookup"><span data-stu-id="afa4c-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="afa4c-129">開啟已關閉的視窗 (例如，樣板、元素屬性和訊息)</span><span class="sxs-lookup"><span data-stu-id="afa4c-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="afa4c-130">重設配置 toodefault 設定</span><span class="sxs-lookup"><span data-stu-id="afa4c-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="afa4c-131">**圖表**</span><span class="sxs-lookup"><span data-stu-id="afa4c-131">**Diagram**</span></span> | <span data-ttu-id="afa4c-132">新增/刪除圖表並且瀏覽圖表的「索引標籤」</span><span class="sxs-lookup"><span data-stu-id="afa4c-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="afa4c-133">**報告**</span><span class="sxs-lookup"><span data-stu-id="afa4c-133">**Reports**</span></span> | <span data-ttu-id="afa4c-134">與其他人建立 HTML 報表 tooshare</span><span class="sxs-lookup"><span data-stu-id="afa4c-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="afa4c-135">**說明**</span><span class="sxs-lookup"><span data-stu-id="afa4c-135">**Help**</span></span> | <span data-ttu-id="afa4c-136">引導您使用 hello 工具 toohelp</span><span class="sxs-lookup"><span data-stu-id="afa4c-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="afa4c-137">hello 圖示是捷徑 hello 的最上層功能表：</span><span class="sxs-lookup"><span data-stu-id="afa4c-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="afa4c-138">圖示</span><span class="sxs-lookup"><span data-stu-id="afa4c-138">Icon</span></span>                               | <span data-ttu-id="afa4c-139">詳細資料</span><span class="sxs-lookup"><span data-stu-id="afa4c-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-140">**開啟**</span><span class="sxs-lookup"><span data-stu-id="afa4c-140">**Open**</span></span> | <span data-ttu-id="afa4c-141">開啟新的檔案</span><span class="sxs-lookup"><span data-stu-id="afa4c-141">Opens a new file</span></span> |
| <span data-ttu-id="afa4c-142">**儲存**</span><span class="sxs-lookup"><span data-stu-id="afa4c-142">**Save**</span></span> | <span data-ttu-id="afa4c-143">儲存目前的檔案</span><span class="sxs-lookup"><span data-stu-id="afa4c-143">Saves current file</span></span> |
| <span data-ttu-id="afa4c-144">**設計**</span><span class="sxs-lookup"><span data-stu-id="afa4c-144">**Design**</span></span> | <span data-ttu-id="afa4c-145">便會進入設計檢視，您可以在其中建立模型</span><span class="sxs-lookup"><span data-stu-id="afa4c-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="afa4c-146">**分析**</span><span class="sxs-lookup"><span data-stu-id="afa4c-146">**Analyze**</span></span> | <span data-ttu-id="afa4c-147">顯示產生的威脅和其屬性</span><span class="sxs-lookup"><span data-stu-id="afa4c-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="afa4c-148">**新增圖表**</span><span class="sxs-lookup"><span data-stu-id="afa4c-148">**Add Diagram**</span></span> | <span data-ttu-id="afa4c-149">加入新的圖表 （類似 toonew 索引標籤在 Excel 中）</span><span class="sxs-lookup"><span data-stu-id="afa4c-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="afa4c-150">**刪除圖表**</span><span class="sxs-lookup"><span data-stu-id="afa4c-150">**Delete Diagram**</span></span> | <span data-ttu-id="afa4c-151">刪除目前的圖表</span><span class="sxs-lookup"><span data-stu-id="afa4c-151">Deletes current diagram</span></span> |
| <span data-ttu-id="afa4c-152">**複製/剪下/貼上**</span><span class="sxs-lookup"><span data-stu-id="afa4c-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="afa4c-153">複製/剪下/貼上元素</span><span class="sxs-lookup"><span data-stu-id="afa4c-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="afa4c-154">**復原/重做**</span><span class="sxs-lookup"><span data-stu-id="afa4c-154">**Undo/Redo**</span></span> | <span data-ttu-id="afa4c-155">復原/重做動作</span><span class="sxs-lookup"><span data-stu-id="afa4c-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="afa4c-156">**放大/縮小**</span><span class="sxs-lookup"><span data-stu-id="afa4c-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="afa4c-157">拉出 hello 圖表更好的檢視</span><span class="sxs-lookup"><span data-stu-id="afa4c-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="afa4c-158">**意見反應**</span><span class="sxs-lookup"><span data-stu-id="afa4c-158">**Feedback**</span></span> | <span data-ttu-id="afa4c-159">開啟 hello MSDN 論壇</span><span class="sxs-lookup"><span data-stu-id="afa4c-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="afa4c-160">畫布</span><span class="sxs-lookup"><span data-stu-id="afa4c-160">Canvas</span></span>

<span data-ttu-id="afa4c-161">hello 空間其中您拖放到的項目。</span><span class="sxs-lookup"><span data-stu-id="afa4c-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="afa4c-162">拖放是最快的 hello 和最有效率的方式 toobuild 模型。</span><span class="sxs-lookup"><span data-stu-id="afa4c-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="afa4c-163">您也可以以滑鼠右鍵按一下，並選取從 hello 功能表中，這會將泛型版本的 hello 項目使用，如下所示。</span><span class="sxs-lookup"><span data-stu-id="afa4c-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="afa4c-164">Hello 畫布上的卸除 hello 樣板</span><span class="sxs-lookup"><span data-stu-id="afa4c-164">Dropping hello stencil on hello canvas</span></span>

![畫布置放](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="afa4c-166">按一下 hello 樣板</span><span class="sxs-lookup"><span data-stu-id="afa4c-166">Clicking on hello stencil</span></span>

![元素屬性](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="afa4c-168">樣板</span><span class="sxs-lookup"><span data-stu-id="afa4c-168">Stencils</span></span>

<span data-ttu-id="afa4c-169">您可以找到其中所有樣板可用 toouse hello 選取的範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="afa4c-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="afa4c-170">如果找不到 hello 右項目，請嘗試使用其他範本，或修改一個 toofit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="afa4c-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="afa4c-171">一般而言，您應該要能夠 toofind 像 hello 的以下類別的組合：</span><span class="sxs-lookup"><span data-stu-id="afa4c-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="afa4c-172">樣板名稱</span><span class="sxs-lookup"><span data-stu-id="afa4c-172">Stencil Name</span></span>                               | <span data-ttu-id="afa4c-173">詳細資料</span><span class="sxs-lookup"><span data-stu-id="afa4c-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-174">**處理程序**</span><span class="sxs-lookup"><span data-stu-id="afa4c-174">**Process**</span></span> | <span data-ttu-id="afa4c-175">應用程式、瀏覽器外掛程式、執行緒、虛擬機器</span><span class="sxs-lookup"><span data-stu-id="afa4c-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="afa4c-176">**外部互動者**</span><span class="sxs-lookup"><span data-stu-id="afa4c-176">**External Interactor**</span></span> | <span data-ttu-id="afa4c-177">驗證提供者、瀏覽器、使用者、Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="afa4c-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="afa4c-178">**資料存放區**</span><span class="sxs-lookup"><span data-stu-id="afa4c-178">**Data Store**</span></span> | <span data-ttu-id="afa4c-179">快取、儲存體、設定檔、資料庫、登錄</span><span class="sxs-lookup"><span data-stu-id="afa4c-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="afa4c-180">**資料流程**</span><span class="sxs-lookup"><span data-stu-id="afa4c-180">**Data Flow**</span></span> | <span data-ttu-id="afa4c-181">二進位、ALPC、HTTP、HTTPS/TLS/SSL、IOCTL、IPSec、具名管道、DCOM、SMB、UDP</span><span class="sxs-lookup"><span data-stu-id="afa4c-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="afa4c-182">**信任線條/框線界限**</span><span class="sxs-lookup"><span data-stu-id="afa4c-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="afa4c-183">公司網路、網際網路、機器、沙箱、使用者/核心模式</span><span class="sxs-lookup"><span data-stu-id="afa4c-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="afa4c-184">附註/訊息</span><span class="sxs-lookup"><span data-stu-id="afa4c-184">Notes/Messages</span></span>

| <span data-ttu-id="afa4c-185">元件</span><span class="sxs-lookup"><span data-stu-id="afa4c-185">Component</span></span>                               | <span data-ttu-id="afa4c-186">詳細資料</span><span class="sxs-lookup"><span data-stu-id="afa4c-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-187">**訊息**</span><span class="sxs-lookup"><span data-stu-id="afa4c-187">**Messages**</span></span> | <span data-ttu-id="afa4c-188">每當發生錯誤時 (例如元素之間沒有資料流程) 警示使用者的內部工具邏輯</span><span class="sxs-lookup"><span data-stu-id="afa4c-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="afa4c-189">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="afa4c-189">**Notes**</span></span> | <span data-ttu-id="afa4c-190">手動加入的 toohello 檔案由工程小組整個 hello 設計，並檢閱程序</span><span class="sxs-lookup"><span data-stu-id="afa4c-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="afa4c-191">元素屬性</span><span class="sxs-lookup"><span data-stu-id="afa4c-191">Element properties</span></span>

<span data-ttu-id="afa4c-192">這些會因選取的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="afa4c-192">These vary by hello elements selected.</span></span> <span data-ttu-id="afa4c-193">除了信任界限，其他所有元素會包含 3 個一般選取項目：</span><span class="sxs-lookup"><span data-stu-id="afa4c-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="afa4c-194">元素屬性</span><span class="sxs-lookup"><span data-stu-id="afa4c-194">Element Property</span></span>                               | <span data-ttu-id="afa4c-195">詳細資料</span><span class="sxs-lookup"><span data-stu-id="afa4c-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-196">**名稱**</span><span class="sxs-lookup"><span data-stu-id="afa4c-196">**Name**</span></span> | <span data-ttu-id="afa4c-197">適用於命名易於辨識您的處理序、 儲存、 互動及流量 toobe</span><span class="sxs-lookup"><span data-stu-id="afa4c-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="afa4c-198">**超出範圍**</span><span class="sxs-lookup"><span data-stu-id="afa4c-198">**Out of Scope**</span></span> | <span data-ttu-id="afa4c-199">如果選取，hello 項目是取自 hello 威脅產生矩陣 （不建議）</span><span class="sxs-lookup"><span data-stu-id="afa4c-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="afa4c-200">**超出範圍原因**</span><span class="sxs-lookup"><span data-stu-id="afa4c-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="afa4c-201">對齊欄位 toolet 使用者知道為什麼不在範圍已選取</span><span class="sxs-lookup"><span data-stu-id="afa4c-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="afa4c-202">每個元素類別下的屬性都會變更。</span><span class="sxs-lookup"><span data-stu-id="afa4c-202">Properties are changed under each element category.</span></span> <span data-ttu-id="afa4c-203">按一下每個項目 tooinspect hello 可用的選項，或開啟多個 hello 範本 toolearn。</span><span class="sxs-lookup"><span data-stu-id="afa4c-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="afa4c-204">讓我們先進入 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="afa4c-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="afa4c-205">歡迎使用畫面</span><span class="sxs-lookup"><span data-stu-id="afa4c-205">Welcome screen</span></span>

<span data-ttu-id="afa4c-206">hello 歡迎畫面 是當您開啟 hello 應用程式時，您會看到 hello 第一件事。</span><span class="sxs-lookup"><span data-stu-id="afa4c-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="afa4c-207">開啟模型</span><span class="sxs-lookup"><span data-stu-id="afa4c-207">Open A model</span></span>

<span data-ttu-id="afa4c-208">將游標移到 [開啟模型] 按鈕會為您顯示 2 個隱藏選項：[從這部電腦開啟] 和 [從 OneDrive 開啟]。</span><span class="sxs-lookup"><span data-stu-id="afa4c-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="afa4c-209">hello 第一次開啟 hello 開啟舊檔 畫面上，雖然 hello 第二個會引導您完成 hello 登入程序為 OneDrive，可讓您 toopick 資料夾和檔案成功驗證之後。</span><span class="sxs-lookup"><span data-stu-id="afa4c-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![開啟模型](./media/azure-security-threat-modeling-tool/openmodel.png)

![從電腦或 OneDrive 開啟](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="afa4c-212">意見反應、建議和問題</span><span class="sxs-lookup"><span data-stu-id="afa4c-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="afa4c-213">選取此選項會帶您 toohello MSDN 論壇 SDL 工具。</span><span class="sxs-lookup"><span data-stu-id="afa4c-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="afa4c-214">它是很好的方法 toocheck 出看其他人對 hello 工具，包括因應措施和新的想法。</span><span class="sxs-lookup"><span data-stu-id="afa4c-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![意見反應](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="afa4c-216">設計檢視</span><span class="sxs-lookup"><span data-stu-id="afa4c-216">Design view</span></span>

<span data-ttu-id="afa4c-217">每當您開啟或建立新的模型，您將會進入 toohello [設計] 檢視。</span><span class="sxs-lookup"><span data-stu-id="afa4c-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="afa4c-218">新增元素</span><span class="sxs-lookup"><span data-stu-id="afa4c-218">Adding elements</span></span>

<span data-ttu-id="afa4c-219">有 2 種 tooadd 項目在 hello 方格上：</span><span class="sxs-lookup"><span data-stu-id="afa4c-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="afa4c-220">**將拖放**– 拖曳 hello 所需的項目 toohello 方格中，然後使用 hello 項目屬性 tooprovide 其他資訊。</span><span class="sxs-lookup"><span data-stu-id="afa4c-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="afa4c-221">**以滑鼠右鍵按一下**– hello 方格上以滑鼠右鍵按一下任何位置，然後從 hello 下拉式功能表中選取。</span><span class="sxs-lookup"><span data-stu-id="afa4c-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="afa4c-222">泛型的表示法，該元素會出現在囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="afa4c-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="afa4c-223">連線元素</span><span class="sxs-lookup"><span data-stu-id="afa4c-223">Connecting elements</span></span>

<span data-ttu-id="afa4c-224">有 2 種方式 tooconnect 項目在 hello 工具：</span><span class="sxs-lookup"><span data-stu-id="afa4c-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="afa4c-225">**將拖放**– 拖曳 hello 所需的資料流程 toohello 方格中，並連接這兩個 ends toohello 適當的項目。</span><span class="sxs-lookup"><span data-stu-id="afa4c-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="afa4c-226">**按一下 + 移位**– 按一下 hello （傳送資料） 的第一個項目，請按住 hello Shift 鍵，然後選取 hello （接收資料） 的第二個元素。</span><span class="sxs-lookup"><span data-stu-id="afa4c-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="afa4c-227">按一下滑鼠右鍵，然後選取 [連接]。</span><span class="sxs-lookup"><span data-stu-id="afa4c-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="afa4c-228">如果您使用雙向資料流程，hello 順序並不重要。</span><span class="sxs-lookup"><span data-stu-id="afa4c-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="afa4c-229">屬性</span><span class="sxs-lookup"><span data-stu-id="afa4c-229">Properties</span></span>

<span data-ttu-id="afa4c-230">顯示所有可修改的 hello 屬性放在 hello 圖表中的 hello 樣板上。</span><span class="sxs-lookup"><span data-stu-id="afa4c-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="afa4c-231">hello 樣板，只要按一下 toosee hello 屬性，並將據此擴展 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="afa4c-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="afa4c-232">hello 下面範例會顯示之前和之後樣板拖曳 hello 圖表 「 資料庫 」:</span><span class="sxs-lookup"><span data-stu-id="afa4c-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="afa4c-233">先前</span><span class="sxs-lookup"><span data-stu-id="afa4c-233">Before</span></span>

![先前](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="afa4c-235">後續</span><span class="sxs-lookup"><span data-stu-id="afa4c-235">After</span></span>

![後續](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="afa4c-237">訊息</span><span class="sxs-lookup"><span data-stu-id="afa4c-237">Messages</span></span>

<span data-ttu-id="afa4c-238">如果您建立的威脅模型，忘記 tooconnect 資料流程 tooelements hello 訊息視窗會通知您 tooact。</span><span class="sxs-lookup"><span data-stu-id="afa4c-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="afa4c-239">您可以選擇 tooignore，它或後續 hello 指示 toofix hello 問題。</span><span class="sxs-lookup"><span data-stu-id="afa4c-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![訊息](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="afa4c-241">注意事項</span><span class="sxs-lookup"><span data-stu-id="afa4c-241">Notes</span></span>

<span data-ttu-id="afa4c-242">切換索引標籤，從訊息 tooNotes 可讓您 tooadd 備忘稿 tooyour 圖表 toocapture 您的想法</span><span class="sxs-lookup"><span data-stu-id="afa4c-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="afa4c-243">分析檢視</span><span class="sxs-lookup"><span data-stu-id="afa4c-243">Analysis view</span></span>

<span data-ttu-id="afa4c-244">一旦您完成建置您的圖表，tooanalysis 檢視切換移 toohello 上方功能表選取項目，然後選擇 hello 放大鏡下一步 toohello 小畫家調色盤。</span><span class="sxs-lookup"><span data-stu-id="afa4c-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![分析檢視](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="afa4c-246">產生的威脅選取項目</span><span class="sxs-lookup"><span data-stu-id="afa4c-246">Generated threat selection</span></span>

<span data-ttu-id="afa4c-247">當您按一下威脅時，您可以利用三個唯一的函式：</span><span class="sxs-lookup"><span data-stu-id="afa4c-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="afa4c-248">功能</span><span class="sxs-lookup"><span data-stu-id="afa4c-248">Feature</span></span>                               | <span data-ttu-id="afa4c-249">資訊</span><span class="sxs-lookup"><span data-stu-id="afa4c-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="afa4c-250">**讀取指標**</span><span class="sxs-lookup"><span data-stu-id="afa4c-250">**Read Indicator**</span></span> | <p><span data-ttu-id="afa4c-251">威脅現在標示成已閱讀，輕鬆地可協助您追蹤您已經瀏覽的 hello 項目</span><span class="sxs-lookup"><span data-stu-id="afa4c-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![讀取/未讀取指標](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="afa4c-253">**互動焦點**</span><span class="sxs-lookup"><span data-stu-id="afa4c-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="afa4c-254">在屬於 toothat 威脅的 hello 圖表互動會反白顯示</span><span class="sxs-lookup"><span data-stu-id="afa4c-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![互動焦點](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="afa4c-256">**威脅屬性**</span><span class="sxs-lookup"><span data-stu-id="afa4c-256">**Threat Properties**</span></span> | <p><span data-ttu-id="afa4c-257">Hello 威脅屬性 視窗中已填入 hello 威脅的其他資訊</span><span class="sxs-lookup"><span data-stu-id="afa4c-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![威脅屬性](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="afa4c-259">優先順序變更</span><span class="sxs-lookup"><span data-stu-id="afa4c-259">Priority change</span></span>

<span data-ttu-id="afa4c-260">變更每個產生的威脅的 hello 優先權層級也會變更其色彩 toomake 它輕鬆 tooidentify 高、 中度與低優先權的威脅。</span><span class="sxs-lookup"><span data-stu-id="afa4c-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![優先順序變更](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="afa4c-262">威脅屬性可編輯欄位</span><span class="sxs-lookup"><span data-stu-id="afa4c-262">Threat properties editable fields</span></span>

<span data-ttu-id="afa4c-263">如同上面的 hello 影像，使用者可以變更 hello 工具所產生的 hello 資訊也會加入資訊 toocertain 欄位，例如對齊。</span><span class="sxs-lookup"><span data-stu-id="afa4c-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="afa4c-264">這些欄位所產生 hello 範本，因此如果您需要每個威脅的詳細資訊，您已經鼓勵的 toomake 修改。</span><span class="sxs-lookup"><span data-stu-id="afa4c-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![威脅屬性](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="afa4c-266">報告</span><span class="sxs-lookup"><span data-stu-id="afa4c-266">Reports</span></span>

<span data-ttu-id="afa4c-267">一旦您完成時變更的優先順序，且每個更新 hello 狀態產生威脅，您可以儲存 hello 檔案及/或列印報表移過 「 報告 」，然後再 「 建立完整報告。 」</span><span class="sxs-lookup"><span data-stu-id="afa4c-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="afa4c-268">系統會詢問 tooname hello 報表，一旦您這樣做，您應該會看到類似下面的 toohello 影像：</span><span class="sxs-lookup"><span data-stu-id="afa4c-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![報告](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="afa4c-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afa4c-270">Next steps</span></span>

<span data-ttu-id="afa4c-271">toocontribute hello 社群的範本，請移 tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** 頁面。</span><span class="sxs-lookup"><span data-stu-id="afa4c-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="afa4c-272">**[下載](https://aka.ms/tmtpreview)** hello 工具 tooget 立即開始使用。</span><span class="sxs-lookup"><span data-stu-id="afa4c-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
