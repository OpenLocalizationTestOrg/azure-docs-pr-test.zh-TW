---
title: "aaaOptions 偵錯 Azure 雲端服務 |Microsoft 文件"
description: "進行 Azure 雲端服務的偵錯"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a><span data-ttu-id="0338f-103">了解各種 hello toodebug Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="0338f-103">Learn hello various ways toodebug an Azure cloud service</span></span>
<span data-ttu-id="0338f-104">本文章提供連結 toohello 各種方式 toodebug Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0338f-104">This article provides links toohello various ways toodebug an Azure cloud service.</span></span> 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a><span data-ttu-id="0338f-105">在 Visual Studio 中進行 Azure 雲端服務的偵錯</span><span class="sxs-lookup"><span data-stu-id="0338f-105">Debugging an Azure cloud service in Visual Studio</span></span>
<span data-ttu-id="0338f-106">您可以儲存時間和金錢使用 hello Azure 計算模擬器 toodebug 您的雲端服務在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="0338f-106">You can save time and money by using hello Azure compute emulator toodebug your cloud service on a local machine.</span></span> <span data-ttu-id="0338f-107">透過在部署服務之前於本機偵錯服務，您可以改善可靠性和效能，而不需支付運算時間。</span><span class="sxs-lookup"><span data-stu-id="0338f-107">By debugging a service locally before you deploy it, you can improve reliability and performance without paying for compute time.</span></span> <span data-ttu-id="0338f-108">不過，某些錯誤可能只有當您在 Azure 中執行雲端服務時才會發生。</span><span class="sxs-lookup"><span data-stu-id="0338f-108">However, some errors might occur only when you run a cloud service in Azure.</span></span> <span data-ttu-id="0338f-109">在 Azure 中執行雲端服務時，才會發生的錯誤可以藉由啟用遠端偵錯時您發行服務，並再將 hello 偵錯工具 tooa 角色執行個體附加偵錯。</span><span class="sxs-lookup"><span data-stu-id="0338f-109">Errors that occur only when you run a cloud service in Azure can be debugged by enabling remote debugging when you publish your service, and then attaching hello debugger tooa role instance.</span></span> <span data-ttu-id="0338f-110">如需詳細資訊，請參閱 [在您的本機電腦上偵錯您的雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)。</span><span class="sxs-lookup"><span data-stu-id="0338f-110">For more information, see [Debug your cloud service on your local computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).</span></span>

## <a name="using-azure-diagnostics"></a><span data-ttu-id="0338f-111">使用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="0338f-111">Using Azure Diagnostics</span></span> 
<span data-ttu-id="0338f-112">您可以使用 Azure 診斷 toolog 是否在 hello 開發環境中，或在 Azure 中執行 hello 角色的詳細資訊從角色中的程式碼執行。</span><span class="sxs-lookup"><span data-stu-id="0338f-112">You can use Azure Diagnostics toolog detailed information from code running within roles, whether hello roles are running in hello development environment or in Azure.</span></span> <span data-ttu-id="0338f-113">如需詳細資訊，請參閱 [在 Azure 雲端服務中啟用 Azure 診斷](http://go.microsoft.com/fwlink/p/?LinkId=400450)。</span><span class="sxs-lookup"><span data-stu-id="0338f-113">For more information, see [Enabling Azure Diagnostics in Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).</span></span>

## <a name="using-intellitrace"></a><span data-ttu-id="0338f-114">使用 IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="0338f-114">Using IntelliTrace</span></span> 
<span data-ttu-id="0338f-115">如果您使用 Visual Studio Enterprise toowrite 角色目標.NET Framework 4.5，您可以啟用 IntelliTrace，在您部署 Azure 雲端服務從 Visual Studio 的 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="0338f-115">If you are using Visual Studio Enterprise toowrite roles targeted .NET Framework 4.5, you can enable IntelliTrace at hello time that you deploy an Azure cloud service from Visual Studio.</span></span> <span data-ttu-id="0338f-116">IntelliTrace 會提供記錄檔，您可以使用 Visual Studio toodebug 與您的應用程式在 Azure 中執行一樣。</span><span class="sxs-lookup"><span data-stu-id="0338f-116">IntelliTrace provides a log that you can use with Visual Studio toodebug your application as if it were running in Azure.</span></span> <span data-ttu-id="0338f-117">如需詳細資訊，請參閱 [使用 IntelliTrace 和 Visual Studio 進行已發佈的雲端服務偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623016)。</span><span class="sxs-lookup"><span data-stu-id="0338f-117">For more information, see [Debugging a published cloud service with IntelliTrace and Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="0338f-118">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="0338f-118">Remote debugging</span></span> 
<span data-ttu-id="0338f-119">您可以啟用遠端偵錯雲端服務在 hello 階段，當您部署 hello 雲端服務，從 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0338f-119">You can enable remote debugging on your cloud services at hello time when you deploy hello cloud service from Visual Studio.</span></span> <span data-ttu-id="0338f-120">如果您選擇 tooenable 遠端偵錯部署，執行每個角色執行個體的 hello 虛擬機器上安裝遠端偵錯服務。</span><span class="sxs-lookup"><span data-stu-id="0338f-120">If you choose tooenable remote debugging for a deployment, remote debugging services are installed on hello virtual machines that run each role instance.</span></span> <span data-ttu-id="0338f-121">這些服務 (例如 `msvsmon.exe`) 不會影響效能或造成額外成本。</span><span class="sxs-lookup"><span data-stu-id="0338f-121">These services - such as `msvsmon.exe` - do not affect performance or result in extra costs.</span></span> <span data-ttu-id="0338f-122">如需詳細資訊，請參閱 [在 Azure 中偵錯雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="0338f-122">For more information, see [Debug a cloud service in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0338f-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0338f-123">Next steps</span></span>
- <span data-ttu-id="0338f-124">[偵錯 Azure 雲端服務或在 Visual Studio 中的 VM](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -了解如何 toodebug Azure 雲端服務的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0338f-124">[Debugging an Azure cloud service or VM in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Learn hello details of how toodebug Azure cloud services.</span></span>
