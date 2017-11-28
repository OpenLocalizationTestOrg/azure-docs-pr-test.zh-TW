---
title: "aaaSetup emulator express toodebug Visual Studio 中的雲端服務應用程式 |Microsoft 文件"
description: "說明如何 tooinstall hello Emulator Express 在 Visual Studio 中的 c + + 可轉散發套件 tooenable"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="64b48-103">使用中 VS 2017 Emulator Express toodebug 雲端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="64b48-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="64b48-104">這篇文章說明如何 toouse Emulator Express toodebug 雲端服務中的應用程式與 2017年。</span><span class="sxs-lookup"><span data-stu-id="64b48-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="64b48-105">背景資訊</span><span class="sxs-lookup"><span data-stu-id="64b48-105">Background context</span></span>
<span data-ttu-id="64b48-106">Visual Studio 中依預設會使用 Emulator Express 來偵錯雲端服務 Web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="64b48-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="64b48-107">此設定指定在 hello 雲端服務專案屬性頁面中。</span><span class="sxs-lookup"><span data-stu-id="64b48-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![開啟專案屬性][0]

![預設已選取 Emulator Express][1]

<span data-ttu-id="64b48-110">hello [Visual c + + 可轉散發][ Visual C++ Redistributable]的模擬器需要 Visual Studio express。</span><span class="sxs-lookup"><span data-stu-id="64b48-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="64b48-111">目前並未安裝以 hello Azure 的工作負載。</span><span class="sxs-lookup"><span data-stu-id="64b48-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="64b48-112">在 F5 時軌跡 toodebug 雲端服務應用程式，Visual Studio 會提示 tooinstall 此元件，並繼續進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="64b48-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![提示安裝 C++ 可轉散發套件][2]

<span data-ttu-id="64b48-114">按一下 [是] tooinstall c + + 可轉散發套件。</span><span class="sxs-lookup"><span data-stu-id="64b48-114">Click Yes tooinstall C++ Redistributable.</span></span>

![安裝 C++ 可轉散發套件][3]

<span data-ttu-id="64b48-116">按 F5 再次 toolaunch 偵錯工作階段。</span><span class="sxs-lookup"><span data-stu-id="64b48-116">Press F5 again toolaunch debugging sessions.</span></span>

![開始偵錯][4]

![偵錯成功][5]

> <span data-ttu-id="64b48-119">注意︰Visual C++ 可轉散發套件只需要安裝一次。</span><span class="sxs-lookup"><span data-stu-id="64b48-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="64b48-120">如果您是從舊版的 Azure SDK 升級，且已安裝 Emulator Express，則不會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="64b48-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="64b48-121">手動因應措施</span><span class="sxs-lookup"><span data-stu-id="64b48-121">Manual workaround</span></span>
<span data-ttu-id="64b48-122">您也可以安裝 hello [Visual c + + 可轉散發][ Visual C++ Redistributable]手動方式 Visual Studio 在您的系統上安裝它，則會套用相同的效果。</span><span class="sxs-lookup"><span data-stu-id="64b48-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="64b48-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="64b48-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="64b48-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="64b48-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="64b48-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64b48-125">Next Steps</span></span>
<span data-ttu-id="64b48-126">深入了解使用 Azure 計算模擬器 toodebug 您在 Visual Studio 中的雲端服務應用程式：[使用 Emulator Express toorun 和偵錯在本機電腦上的雲端服務][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="64b48-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
