---
title: "建立 Azure RemoteApp 映像 | Microsoft Docs"
description: "了解可用來建立 Azure RemoteApp 之映像的選項"
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
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="05e2c-103">建立 Azure RemoteApp 映像</span><span class="sxs-lookup"><span data-stu-id="05e2c-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="05e2c-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="05e2c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="05e2c-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="05e2c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="05e2c-106">Azure RemoteApp 使用映像保留與使用者共用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="05e2c-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="05e2c-107">(我們使用您的映像來建立 VM - 這是使用者登入 Azure RemoteApp 時存取的內容。)若要使用選擇的應用程式建立 Azure RemoteApp 集合 (不論是雲端還是混合式)，請從建立已安裝這些應用程式的映像開始。</span><span class="sxs-lookup"><span data-stu-id="05e2c-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="05e2c-108">接著，建立使用該映像的集合，並將使用者指派給集合，然後將應用程式發佈給那些使用者。</span><span class="sxs-lookup"><span data-stu-id="05e2c-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="05e2c-109">您有幾個選項可建立或使用映像。</span><span class="sxs-lookup"><span data-stu-id="05e2c-109">You have several options for creating or using images.</span></span> <span data-ttu-id="05e2c-110">映像的基本 [需求](remoteapp-imagereqs.md) 是它執行 Windows Server 2012 R2 並已安裝遠端桌面工作階段主機 (RDSH) 角色。</span><span class="sxs-lookup"><span data-stu-id="05e2c-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="05e2c-111">如何達成就是有趣的地方。</span><span class="sxs-lookup"><span data-stu-id="05e2c-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="05e2c-112">如果是映像，則您有下列選擇：</span><span class="sxs-lookup"><span data-stu-id="05e2c-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="05e2c-113">您可以匯入和使用 [根據 Azure 虛擬機器的映像](remoteapp-image-on-azurevm.md)。</span><span class="sxs-lookup"><span data-stu-id="05e2c-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="05e2c-114">這適用於需要自訂設定的特定業務應用程式。</span><span class="sxs-lookup"><span data-stu-id="05e2c-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="05e2c-115">您可以自訂要用於應用程式的映像。</span><span class="sxs-lookup"><span data-stu-id="05e2c-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="05e2c-116">您可以 [建立和上傳自訂映像](remoteapp-create-custom-image.md)。</span><span class="sxs-lookup"><span data-stu-id="05e2c-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="05e2c-117">如果您已經有用於內部部署遠端桌面服務部署的映像，則這十分不錯。</span><span class="sxs-lookup"><span data-stu-id="05e2c-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="05e2c-118">您可以使用 RemoteApp 訂用帳戶中所含的其中一個 [範本映像](remoteapp-images.md) 。</span><span class="sxs-lookup"><span data-stu-id="05e2c-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="05e2c-119">這些映像是由 RemoteApp 小組所建立和維護，並且包含一些可提供給您使用者的標準應用程式 (如 Office 套件)。</span><span class="sxs-lookup"><span data-stu-id="05e2c-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="05e2c-120">請注意，只有 Office 365 Pro Plus 映像才能用於生產設定中。</span><span class="sxs-lookup"><span data-stu-id="05e2c-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="05e2c-121">不論在何處取得映像或如何建立映像，您都會想要確定您了解 [應用程式需求](remoteapp-appreqs.md) ，確保您的應用程式在 RemoteApp 中運作良好。</span><span class="sxs-lookup"><span data-stu-id="05e2c-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="05e2c-122">然後，下一步是建立[雲端](remoteapp-create-cloud-deployment.md)或[混合式](remoteapp-create-hybrid-deployment.md) 集合。</span><span class="sxs-lookup"><span data-stu-id="05e2c-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

