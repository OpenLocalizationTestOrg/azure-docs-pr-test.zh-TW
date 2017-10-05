---
title: "安裝 Emulator Express 在 Visual Studio 中偵錯雲端服務應用程式 | Microsoft Docs"
description: "說明如何安裝 C++ 可轉散發套件在 Visual Studio 中啟用 Emulator Express"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="0755a-103">在 VS 2017 中使用 Emulator Express 偵錯雲端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0755a-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="0755a-104">這篇文章說明如何在 VS 2017 中使用 Emulator Express 偵錯雲端服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="0755a-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="0755a-105">背景資訊</span><span class="sxs-lookup"><span data-stu-id="0755a-105">Background context</span></span>
<span data-ttu-id="0755a-106">Visual Studio 中依預設會使用 Emulator Express 來偵錯雲端服務 Web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="0755a-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="0755a-107">此設定是在雲端服務專案屬性頁中指定。</span><span class="sxs-lookup"><span data-stu-id="0755a-107">This setting is specified in the Cloud Services project properties page.</span></span>

![開啟專案屬性][0]

![預設已選取 Emulator Express][1]

<span data-ttu-id="0755a-110">[Visual c + + 可轉散發][ Visual C++ Redistributable]的模擬器需要 Visual Studio express。</span><span class="sxs-lookup"><span data-stu-id="0755a-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="0755a-111">目前未隨著 Azure 工作負載一起安裝。</span><span class="sxs-lookup"><span data-stu-id="0755a-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="0755a-112">按下 F5 來偵錯雲端服務應用程式時，Visual Studio 會提示安裝此元件，然後繼續偵錯。</span><span class="sxs-lookup"><span data-stu-id="0755a-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![提示安裝 C++ 可轉散發套件][2]

<span data-ttu-id="0755a-114">按一下 [是] 以安裝 C++ 可轉散發套件。</span><span class="sxs-lookup"><span data-stu-id="0755a-114">Click Yes to install C++ Redistributable.</span></span>

![安裝 C++ 可轉散發套件][3]

<span data-ttu-id="0755a-116">再按一次 F5 以啟動偵錯工作階段。</span><span class="sxs-lookup"><span data-stu-id="0755a-116">Press F5 again to launch debugging sessions.</span></span>

![開始偵錯][4]

![偵錯成功][5]

> <span data-ttu-id="0755a-119">注意︰Visual C++ 可轉散發套件只需要安裝一次。</span><span class="sxs-lookup"><span data-stu-id="0755a-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="0755a-120">如果您是從舊版的 Azure SDK 升級，且已安裝 Emulator Express，則不會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="0755a-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="0755a-121">手動因應措施</span><span class="sxs-lookup"><span data-stu-id="0755a-121">Manual workaround</span></span>
<span data-ttu-id="0755a-122">您也可以安裝[Visual c + + 可轉散發][ Visual C++ Redistributable]手動方式 Visual Studio 在您的系統上安裝它，則會套用相同的效果。</span><span class="sxs-lookup"><span data-stu-id="0755a-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="0755a-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="0755a-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="0755a-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="0755a-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="0755a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0755a-125">Next Steps</span></span>
<span data-ttu-id="0755a-126">深入了解使用 Azure 計算模擬器來偵錯您的雲端服務應用程式，Visual Studio 中：[執行和偵錯雲端服務在本機電腦上的使用 Emulator Express][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="0755a-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
