---
title: "進行 Azure 雲端服務偵錯的選項 | Microsoft Docs"
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
ms.openlocfilehash: cdcd4ca1fbc7e0a2f24122b32148cbda3d6951a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a><span data-ttu-id="b341e-103">了解進行 Azure 雲端服務偵錯的各種方式</span><span class="sxs-lookup"><span data-stu-id="b341e-103">Learn the various ways to debug an Azure cloud service</span></span>
<span data-ttu-id="b341e-104">本文提供進行 Azure 雲端服務偵錯的各種方法連結。</span><span class="sxs-lookup"><span data-stu-id="b341e-104">This article provides links to the various ways to debug an Azure cloud service.</span></span> 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a><span data-ttu-id="b341e-105">在 Visual Studio 中進行 Azure 雲端服務的偵錯</span><span class="sxs-lookup"><span data-stu-id="b341e-105">Debugging an Azure cloud service in Visual Studio</span></span>
<span data-ttu-id="b341e-106">使用 Azure 計算模擬器在本機電腦上偵錯您的雲端服務可以節省時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="b341e-106">You can save time and money by using the Azure compute emulator to debug your cloud service on a local machine.</span></span> <span data-ttu-id="b341e-107">透過在部署服務之前於本機偵錯服務，您可以改善可靠性和效能，而不需支付運算時間。</span><span class="sxs-lookup"><span data-stu-id="b341e-107">By debugging a service locally before you deploy it, you can improve reliability and performance without paying for compute time.</span></span> <span data-ttu-id="b341e-108">不過，某些錯誤可能只有當您在 Azure 中執行雲端服務時才會發生。</span><span class="sxs-lookup"><span data-stu-id="b341e-108">However, some errors might occur only when you run a cloud service in Azure.</span></span> <span data-ttu-id="b341e-109">只有當您在 Azure 中執行雲端服務時才會發生的錯誤，可藉由在您發佈服務時啟用遠端偵錯，然後將偵錯工具附加至角色執行個體來進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="b341e-109">Errors that occur only when you run a cloud service in Azure can be debugged by enabling remote debugging when you publish your service, and then attaching the debugger to a role instance.</span></span> <span data-ttu-id="b341e-110">如需詳細資訊，請參閱 [在您的本機電腦上偵錯您的雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)。</span><span class="sxs-lookup"><span data-stu-id="b341e-110">For more information, see [Debug your cloud service on your local computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).</span></span>

## <a name="using-azure-diagnostics"></a><span data-ttu-id="b341e-111">使用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="b341e-111">Using Azure Diagnostics</span></span> 
<span data-ttu-id="b341e-112">不論角色是在開發環境中或在 Azure 中執行，您都可以使用 Azure 診斷來記錄在角色內執行的程式碼中的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b341e-112">You can use Azure Diagnostics to log detailed information from code running within roles, whether the roles are running in the development environment or in Azure.</span></span> <span data-ttu-id="b341e-113">如需詳細資訊，請參閱 [在 Azure 雲端服務中啟用 Azure 診斷](http://go.microsoft.com/fwlink/p/?LinkId=400450)。</span><span class="sxs-lookup"><span data-stu-id="b341e-113">For more information, see [Enabling Azure Diagnostics in Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).</span></span>

## <a name="using-intellitrace"></a><span data-ttu-id="b341e-114">使用 IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="b341e-114">Using IntelliTrace</span></span> 
<span data-ttu-id="b341e-115">如果您使用 Visual Studio Enterprise 來撰寫適用目標為 .NET Framework 4.5 的角色，您可以在從 Visual Studio 部署 Azure 雲端服務時啟用 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="b341e-115">If you are using Visual Studio Enterprise to write roles targeted .NET Framework 4.5, you can enable IntelliTrace at the time that you deploy an Azure cloud service from Visual Studio.</span></span> <span data-ttu-id="b341e-116">IntelliTrace 提供您可搭配 Visual Studio 使用於偵錯應用程式 (如同在 Azure 中執行) 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b341e-116">IntelliTrace provides a log that you can use with Visual Studio to debug your application as if it were running in Azure.</span></span> <span data-ttu-id="b341e-117">如需詳細資訊，請參閱 [使用 IntelliTrace 和 Visual Studio 進行已發佈的雲端服務偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623016)。</span><span class="sxs-lookup"><span data-stu-id="b341e-117">For more information, see [Debugging a published cloud service with IntelliTrace and Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="b341e-118">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="b341e-118">Remote debugging</span></span> 
<span data-ttu-id="b341e-119">您可以在從 Visual Studio 部署雲端服務時，啟用雲端服務的遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="b341e-119">You can enable remote debugging on your cloud services at the time when you deploy the cloud service from Visual Studio.</span></span> <span data-ttu-id="b341e-120">如果您選擇對部署啟用遠端偵錯，則會在執行每個角色執行個體的虛擬機器上安裝遠端偵錯服務。</span><span class="sxs-lookup"><span data-stu-id="b341e-120">If you choose to enable remote debugging for a deployment, remote debugging services are installed on the virtual machines that run each role instance.</span></span> <span data-ttu-id="b341e-121">這些服務 (例如 `msvsmon.exe`) 不會影響效能或造成額外成本。</span><span class="sxs-lookup"><span data-stu-id="b341e-121">These services - such as `msvsmon.exe` - do not affect performance or result in extra costs.</span></span> <span data-ttu-id="b341e-122">如需詳細資訊，請參閱 [在 Azure 中偵錯雲端服務](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="b341e-122">For more information, see [Debug a cloud service in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b341e-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b341e-123">Next steps</span></span>
- <span data-ttu-id="b341e-124">[在 Visual Studio 中進行 Azure 雲端服務或 VM 的偵錯](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - 了解如何進行 Azure 雲端服務偵錯的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b341e-124">[Debugging an Azure cloud service or VM in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - Learn the details of how to debug Azure cloud services.</span></span>