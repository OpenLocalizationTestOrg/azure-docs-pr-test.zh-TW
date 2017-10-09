---
title: "aaaAzure Windows 虛擬機器 DotNet 核心教學課程 1 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a><span data-ttu-id="b60a7-103">自動化應用程式部署 tooWindows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b60a7-103">Automating application deployments tooWindows Virtual Machines</span></span>

<span data-ttu-id="b60a7-104">這個系列包含四個部分，詳細說明了如何使用 Azure Resource Manager 範本來部署及設定 Azure 資源和應用程式。</span><span class="sxs-lookup"><span data-stu-id="b60a7-104">This four-part series details deploying and configuring Azure resource and applications using Azure Resource Manager templates.</span></span> <span data-ttu-id="b60a7-105">本系列的範例範本部署和 hello 檢查部署範本。</span><span class="sxs-lookup"><span data-stu-id="b60a7-105">In this series, a sample template is deployed and hello deployment template examined.</span></span> <span data-ttu-id="b60a7-106">本系列的 hello 目標是 tooeducate hello Azure 資源，之間的關聯性，並 tooprovide 交給上部署完全整合的 Azure 資源管理員範本的經驗。</span><span class="sxs-lookup"><span data-stu-id="b60a7-106">hello goal of this series is tooeducate on hello relationship between Azure resources, and tooprovide hands on experience deploying fully integrated Azure Resource Manager templates.</span></span> <span data-ttu-id="b60a7-107">本文件假設您對 Azure Resource Manager 有基本程度的認識，開始進行本教學課程之前，請讓自己熟悉 Azure Resource Manager 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="b60a7-107">This document assumes a basic level of knowledge with Azure Resource Manager, before starting this tutorial familiarize yourself with basic Azure Resource Manager concepts.</span></span>

## <a name="music-store-application"></a><span data-ttu-id="b60a7-108">音樂市集應用程式</span><span class="sxs-lookup"><span data-stu-id="b60a7-108">Music store application</span></span>
<span data-ttu-id="b60a7-109">hello 用於這一系列的範例是.Net Core 應用程式在模擬音樂商店購買體驗。</span><span class="sxs-lookup"><span data-stu-id="b60a7-109">hello sample used in this series is a .Net Core application simulating a Music Store shopping experience.</span></span> <span data-ttu-id="b60a7-110">此應用程式可以是已部署的 tooeither Linux 或 Windows 的虛擬系統，同時已建立部署的範例。</span><span class="sxs-lookup"><span data-stu-id="b60a7-110">This application can be deployed tooeither a Linux or Windows virtual system, sample deployments have been created for both.</span></span> <span data-ttu-id="b60a7-111">hello 應用程式包含 web 應用程式和 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b60a7-111">hello application includes a web application and a SQL database.</span></span> <span data-ttu-id="b60a7-112">在閱讀本系列文章 hello 之前, 部署 hello 應用程式使用此頁面上找到的 hello 部署按鈕。</span><span class="sxs-lookup"><span data-stu-id="b60a7-112">Before reading hello articles in this series, deploy hello application using hello deployment button found on this page.</span></span> <span data-ttu-id="b60a7-113">完整部署時，hello 應用程式 / Azure 架構看起來像下列圖表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="b60a7-113">When fully deployed, hello application / Azure architecture looks like hello following diagram.</span></span> 

<span data-ttu-id="b60a7-114">hello 音樂存放區 Resource Manager 範本可以在這裡，找到[音樂存放區 Windows 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)</span><span class="sxs-lookup"><span data-stu-id="b60a7-114">hello Music Store Resource Manager template can be found here, [Music Store Windows Template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)</span></span>

![音樂市集應用程式](./media/dotnet-core-1-landing/music-store.png)

<span data-ttu-id="b60a7-116">每個元件，包括 hello JSON 會檢查下列四個發行項的 hello 範本產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b60a7-116">Each of these components, including hello associate template JSON is examined in hello following four articles.</span></span>

* <span data-ttu-id="b60a7-117">[**應用程式架構**](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – 應用程式元件，例如網站和資料庫需要 toobe 裝載於 Azure 的電腦資源，例如虛擬機器和 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b60a7-117">[**Application Architecture**](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – Application components such as web sites and databases need toobe hosted on Azure computer resources such as virtual machines and Azure SQL databases.</span></span> <span data-ttu-id="b60a7-118">本文件逐步解說對應計算需要、 tooAzure 資源，以及部署與 Azure 資源管理員範本，這些資源。</span><span class="sxs-lookup"><span data-stu-id="b60a7-118">This document walks through mapping compute need, tooAzure resources, and deploying these resources with an Azure Resource Manager template.</span></span> 
* <span data-ttu-id="b60a7-119">[**存取與安全性**](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – 裝載在 Azure 中的應用程式，時，需要 tooconsider hello 應用程式存取時，以及如何在不同的應用程式元件彼此存取。</span><span class="sxs-lookup"><span data-stu-id="b60a7-119">[**Access and Security**](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – When hosting applications in Azure, it is necessary tooconsider how hello application is accessed, and how different application components access each other.</span></span> <span data-ttu-id="b60a7-120">本文件詳述提供和保護網際網路存取 tooan 應用程式和應用程式元件之間的存取權。</span><span class="sxs-lookup"><span data-stu-id="b60a7-120">This document details providing and securing internet access tooan application and access between application components.</span></span>
* <span data-ttu-id="b60a7-121">[**可用性和延展性**](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – 延展和可用性，請參閱 toohello 基礎結構停機期間執行的應用程式的能力 toostay 和 hello 能力 tooscale 計算資源 toomeet 應用程式的需要。</span><span class="sxs-lookup"><span data-stu-id="b60a7-121">[**Availability and Scale**](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) – Availability and scale refer toohello applications ability toostay running during infrastructure downtime, and hello ability tooscale compute resources toomeet application demand.</span></span> <span data-ttu-id="b60a7-122">此文件詳細資料 hello 元件需要的 toodeploy 負載平衡和高可用性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b60a7-122">This document details hello components needed toodeploy a load balanced and highly available application.</span></span>
* <span data-ttu-id="b60a7-123">[**應用程式部署**](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) -時必須考量部署應用程式到 Azure 虛擬機器，根據哪個 hello hello 虛擬機器安裝應用程式二進位檔的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="b60a7-123">[**Application Deployment**](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) - When deploying applications onto Azure Virtual Machines, hello method by which hello application binaries are installed on hello Virtual Machine must be considered.</span></span> <span data-ttu-id="b60a7-124">此文件詳細說明如何使用「Azure 虛擬機器自訂指令碼擴充功能」來自動安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="b60a7-124">This document details automating application installation using Azure Virtual Machine Custom Script Extensions.</span></span>

<span data-ttu-id="b60a7-125">hello 開發 Azure 資源管理員範本時的目標是 tooautomate hello 部署 Azure 基礎結構和 hello 安裝和任何的設定應用程式裝載於 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b60a7-125">hello goal when developing Azure Resource Manager templates is tooautomate hello deployment of Azure Infrastructure, and hello installation and configuration of any applications being hosted on this Azure infrastructure.</span></span> <span data-ttu-id="b60a7-126">仔細閱讀這些文章將可獲得這項體驗的範例解說。</span><span class="sxs-lookup"><span data-stu-id="b60a7-126">Working through these articles provides an example of this experience.</span></span>

## <a name="deploy-hello-music-store-application"></a><span data-ttu-id="b60a7-127">部署 hello 音樂市集應用程式</span><span class="sxs-lookup"><span data-stu-id="b60a7-127">Deploy hello music store application</span></span>
<span data-ttu-id="b60a7-128">hello Music Store 應用程式可以使用這個按鈕進行部署。</span><span class="sxs-lookup"><span data-stu-id="b60a7-128">hello Music Store application can be deployed using this button.</span></span>

<span data-ttu-id="b60a7-129"><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a></span><span class="sxs-lookup"><span data-stu-id="b60a7-129"><a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a></span></span>

<span data-ttu-id="b60a7-130">hello Azure Resource Manager 範本需要 hello 下列參數值。</span><span class="sxs-lookup"><span data-stu-id="b60a7-130">hello Azure Resource Manager template requires hello following parameter values.</span></span>

| <span data-ttu-id="b60a7-131">參數名稱</span><span class="sxs-lookup"><span data-stu-id="b60a7-131">Parameter Name</span></span> | <span data-ttu-id="b60a7-132">說明</span><span class="sxs-lookup"><span data-stu-id="b60a7-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b60a7-133">ADMINUSERNAME</span><span class="sxs-lookup"><span data-stu-id="b60a7-133">ADMINUSERNAME</span></span> |<span data-ttu-id="b60a7-134">使用 hello 虛擬機器和 hello Azure SQL Database 的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b60a7-134">Admin user name that is used on hello virtual machine and hello Azure SQL Database.</span></span> |
| <span data-ttu-id="b60a7-135">ADMINPASSWORD</span><span class="sxs-lookup"><span data-stu-id="b60a7-135">ADMINPASSWORD</span></span> |<span data-ttu-id="b60a7-136">適用於 Azure 虛擬機器 hello 和 SQL Database 的密碼。</span><span class="sxs-lookup"><span data-stu-id="b60a7-136">Password that is used on hello Azure Virtual Machine and SQL Database.</span></span> |
| <span data-ttu-id="b60a7-137">NUMBEROFINSTANCES</span><span class="sxs-lookup"><span data-stu-id="b60a7-137">NUMBEROFINSTANCES</span></span> |<span data-ttu-id="b60a7-138">hello 建立的虛擬機器 toobe 數目。</span><span class="sxs-lookup"><span data-stu-id="b60a7-138">hello number of virtual machines toobe created.</span></span> <span data-ttu-id="b60a7-139">每個這些虛擬機器主機 hello Music Store web 應用程式，以及所有流量是負載平衡它們。</span><span class="sxs-lookup"><span data-stu-id="b60a7-139">Each of these virtual machines host hello Music Store web application, and all traffic is load balanced across them.</span></span> |
| <span data-ttu-id="b60a7-140">PUBLICIPADDRESSDNSNAME</span><span class="sxs-lookup"><span data-stu-id="b60a7-140">PUBLICIPADDRESSDNSNAME</span></span> |<span data-ttu-id="b60a7-141">Hello 公用 IP 位址相關聯的全域唯一 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="b60a7-141">Globally unique DNS name associated with hello Public IP address.</span></span> |

<span data-ttu-id="b60a7-142">Hello 範本部署完成後，瀏覽的 toohello 公用 IP 位址使用任何網際網路瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b60a7-142">When hello template deployment has completed, browse toohello public IP Address using any internet browser.</span></span> <span data-ttu-id="b60a7-143">hello.Net Core 音樂站台將會出現。</span><span class="sxs-lookup"><span data-stu-id="b60a7-143">hello .Net Core Music site will be presented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b60a7-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b60a7-144">Next steps</span></span>
<hr>

[<span data-ttu-id="b60a7-145">步驟 1 - 使用 Azure Resource Manager 範本的應用程式架構</span><span class="sxs-lookup"><span data-stu-id="b60a7-145">Step 1 - Application Architecture with Azure Resource Manager Templates</span></span>](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="b60a7-146">步驟 2 - Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="b60a7-146">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="b60a7-147">步驟 3 - Azure Resource Manager 範本中的可用性和規模</span><span class="sxs-lookup"><span data-stu-id="b60a7-147">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="b60a7-148">步驟 4 - 使用 Azure Resource Manager 範本進行應用程式部署</span><span class="sxs-lookup"><span data-stu-id="b60a7-148">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

