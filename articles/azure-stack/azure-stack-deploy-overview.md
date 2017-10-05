---
title: "Azure Stack 開發套件部署快速入門| Microsoft Docs"
description: "了解如何部署 Azure Stack 開發套件"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 81b6282addd1e88e4146367c4dd9a2ee7b8c84bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-development-kit-deployment-quickstart"></a><span data-ttu-id="afadb-103">Azure Stack 開發套件部署快速入門</span><span class="sxs-lookup"><span data-stu-id="afadb-103">Azure Stack Development Kit deployment quickstart</span></span>

<span data-ttu-id="afadb-104">[Azure Stack 開發套件](azure-stack-poc.md)是一個測試和部署環境，可供您部署以評估及示範 Azure Stack 的功能和服務。</span><span class="sxs-lookup"><span data-stu-id="afadb-104">The [Azure Stack Development Kit](azure-stack-poc.md) is a testing and development environment that you can deploy to evaluate and demonstrate Azure Stack features and services.</span></span> <span data-ttu-id="afadb-105">若要讓它啟動並執行，您將需要準備環境硬體並執行一些指令碼 (這將需要數小時的時間)。</span><span class="sxs-lookup"><span data-stu-id="afadb-105">To get it up and running, you’ll need to prepare the environment hardware and run some scripts (this will take several hours).</span></span> <span data-ttu-id="afadb-106">之後，您可以登入系統管理員和租用戶入口網站，以管理 Azure Stack 和測試供應項目。</span><span class="sxs-lookup"><span data-stu-id="afadb-106">After that, you can sign in to the admin and tenant portals to manage Azure Stack and test offers.</span></span> 

1. <span data-ttu-id="afadb-107">[**規劃您的硬體、軟體及網路**](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="afadb-107">[**Plan your hardware, software, and network**](azure-stack-deploy.md).</span></span> <span data-ttu-id="afadb-108">裝載開發套件的電腦 (開發套件主機) 必須符合硬體、軟體及網路需求。</span><span class="sxs-lookup"><span data-stu-id="afadb-108">The computer that hosts the development kit (the development kit host) must meet hardware, software, and network requirements.</span></span> <span data-ttu-id="afadb-109">此外，您還必須在使用 Azure Active Directory 或「Active Directory 同盟服務」之間做選擇。</span><span class="sxs-lookup"><span data-stu-id="afadb-109">You must also choose between using Azure Active Directory or Active Directory Federation Services.</span></span> <span data-ttu-id="afadb-110">開始部署之前，請務必符合這些先決條件，如此安裝程序才能順暢執行。</span><span class="sxs-lookup"><span data-stu-id="afadb-110">Be sure to comply with these prerequisites before starting your deployment so that the installation process runs smoothly.</span></span> 

2. <span data-ttu-id="afadb-111">[**下載部署套件並解壓縮**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit)。</span><span class="sxs-lookup"><span data-stu-id="afadb-111">[**Download and extract the deployment package**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit).</span></span> <span data-ttu-id="afadb-112">您可以將部署套件下載到開發套件主機或另一部電腦。</span><span class="sxs-lookup"><span data-stu-id="afadb-112">You can download the deployment package to the development kit host or to a another computer.</span></span> <span data-ttu-id="afadb-113">解壓縮後的部署檔案會佔用 60 GB 的可用磁碟空間，因此使用另一部電腦可協助降低開發套件主機的硬體需求。</span><span class="sxs-lookup"><span data-stu-id="afadb-113">The extracted deployment files take up 60 GB of free disk space, so using another computer can help reduce the hardware requirements for the development kit host.</span></span>

3. <span data-ttu-id="afadb-114">使用安裝程式來[**準備開發套件主機**](azure-stack-run-powershell-script.md#prepare-the-development-kit-host)。</span><span class="sxs-lookup"><span data-stu-id="afadb-114">[**Prepare the development kit host**](azure-stack-run-powershell-script.md#prepare-the-development-kit-host) by using the installer.</span></span> <span data-ttu-id="afadb-115">在此步驟之後，開發套件主機會開機進入 Cloudbuilder.vhdx (一個包含可開機作業系統和 Azure Stack 安裝檔的虛擬硬碟)。</span><span class="sxs-lookup"><span data-stu-id="afadb-115">After this step, the development kit host will boot to the Cloudbuilder.vhdx (a virtual hard drive that includes a bootable operating system and the Azure Stack install files).</span></span>

4. <span data-ttu-id="afadb-116">在開發套件主機上[**部署開發套件**](azure-stack-run-powershell-script.md#deploy-the-development-kit)。</span><span class="sxs-lookup"><span data-stu-id="afadb-116">[**Deploy the development kit**](azure-stack-run-powershell-script.md#deploy-the-development-kit) on the development kit host.</span></span>

5. <span data-ttu-id="afadb-117">如果您的 Azure Stack 部署使用 Azure Active Directory，您就必須[向 Azure 註冊 Azure Stack](azure-stack-register.md)，如此您才能夠[將 Azure Marketplace 項目下載](azure-stack-download-azure-marketplace-item.md)到 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="afadb-117">If your Azure Stack deployment uses Azure Active Directory, you must [register Azure Stack with Azure](azure-stack-register.md) so that you can [download Azure marketplace items](azure-stack-download-azure-marketplace-item.md) to Azure Stack.</span></span>

<span data-ttu-id="afadb-118">完成這些步驟之後，您將會擁有一個同時具有系統管理員和租用戶入口網站的開發套件環境。</span><span class="sxs-lookup"><span data-stu-id="afadb-118">After completing these steps, you’ll have a development kit environment with both administrator and tenant portals.</span></span> <span data-ttu-id="afadb-119">接著，您可以[連線並登入](azure-stack-connect-azure-stack.md)入口網站。</span><span class="sxs-lookup"><span data-stu-id="afadb-119">Next, you can [connect and sign in](azure-stack-connect-azure-stack.md) to the portal.</span></span> <span data-ttu-id="afadb-120">然後，您可以開始部署資源提供者、建立[供應項目](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions)，以及填入 Azure Stack [市集](azure-stack-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="afadb-120">You can then start deploying resource providers, creating [offers](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions), and populating the Azure Stack [marketplace](azure-stack-marketplace.md).</span></span>
