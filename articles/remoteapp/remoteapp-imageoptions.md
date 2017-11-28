---
title: "Azure RemoteApp 映像 aaaCreate |Microsoft 文件"
description: "了解可用來建立的 Azure RemoteApp 映像的 hello 選項"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="c1433-103">建立 Azure RemoteApp 映像</span><span class="sxs-lookup"><span data-stu-id="c1433-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c1433-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="c1433-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c1433-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c1433-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c1433-106">Azure RemoteApp 使用映像 toohold hello 應用程式，您與您的使用者共用。</span><span class="sxs-lookup"><span data-stu-id="c1433-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="c1433-107">（我們接受您的映像並使用它 toocreate Vm 層的什麼 hello 當使用者存取他們登入 Azure RemoteApp。）toocreate 與您所選擇的應用程式的 Azure RemoteApp 集合，不論是雲端或混合式，開始您以建立映像與安裝這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1433-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="c1433-108">接著，建立集合，其中會使用該映像、 將使用者指派 toohello 集合和發佈應用程式 toothose 使用者。</span><span class="sxs-lookup"><span data-stu-id="c1433-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="c1433-109">您有幾個選項可建立或使用映像。</span><span class="sxs-lookup"><span data-stu-id="c1433-109">You have several options for creating or using images.</span></span> <span data-ttu-id="c1433-110">基本的 hello[需求](remoteapp-imagereqs.md)的映像的是執行 Windows Server 2012 R2 且已安裝的 hello 遠端桌面工作階段主機 (RDSH) 角色。</span><span class="sxs-lookup"><span data-stu-id="c1433-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="c1433-111">如何達成就是有趣的地方。</span><span class="sxs-lookup"><span data-stu-id="c1433-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="c1433-112">您有下列選項，當 tooimages hello:</span><span class="sxs-lookup"><span data-stu-id="c1433-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="c1433-113">您可以匯入和使用 [根據 Azure 虛擬機器的映像](remoteapp-image-on-azurevm.md)。</span><span class="sxs-lookup"><span data-stu-id="c1433-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="c1433-114">這適用於需要自訂設定的特定業務應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1433-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="c1433-115">您可以自訂 hello 映像 toowork hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1433-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="c1433-116">您可以 [建立和上傳自訂映像](remoteapp-create-custom-image.md)。</span><span class="sxs-lookup"><span data-stu-id="c1433-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="c1433-117">如果您已經有用於內部部署遠端桌面服務部署的映像，則這十分不錯。</span><span class="sxs-lookup"><span data-stu-id="c1433-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="c1433-118">您可以使用其中一個 hello[範本映像](remoteapp-images.md)納入 RemoteApp 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1433-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="c1433-119">這些映像所建立，且由 hello RemoteApp 團隊負責維護，且包含一些標準應用程式 （例如 hello Office 套件），您可以將可用的 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="c1433-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="c1433-120">請注意只有 hello Office 365 Pro Plus 映像可用於生產設定。</span><span class="sxs-lookup"><span data-stu-id="c1433-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="c1433-121">不論您用來取得您的映像，或您建立的方式，您需要確定您了解 hello toomake[應用程式需求](remoteapp-appreqs.md)您的應用程式都適用於 RemoteApp 的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="c1433-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="c1433-122">接著，hello 下一個步驟就是 toocreate[雲端](remoteapp-create-cloud-deployment.md)或[混合式](remoteapp-create-hybrid-deployment.md)集合。</span><span class="sxs-lookup"><span data-stu-id="c1433-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

