---
title: "aaaAzure 堆疊開發套件的部署快速入門 |Microsoft 文件"
description: "了解如何 toodeploy hello Azure 堆疊開發套件"
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
ms.openlocfilehash: 7f9fcd3a620e2916a24e57990d93dc9ace2b1129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-deployment-quickstart"></a><span data-ttu-id="6cb53-103">Azure Stack 開發套件部署快速入門</span><span class="sxs-lookup"><span data-stu-id="6cb53-103">Azure Stack Development Kit deployment quickstart</span></span>

<span data-ttu-id="6cb53-104">hello [Azure 堆疊開發套件](azure-stack-poc.md)是測試和開發環境，您可以部署 tooevaluate 和示範 Azure 堆疊功能和服務。</span><span class="sxs-lookup"><span data-stu-id="6cb53-104">hello [Azure Stack Development Kit](azure-stack-poc.md) is a testing and development environment that you can deploy tooevaluate and demonstrate Azure Stack features and services.</span></span> <span data-ttu-id="6cb53-105">tooget 總且正在執行，您將需要 tooprepare hello 環境的硬體，並執行某些指令碼 （這需要數小時）。</span><span class="sxs-lookup"><span data-stu-id="6cb53-105">tooget it up and running, you’ll need tooprepare hello environment hardware and run some scripts (this will take several hours).</span></span> <span data-ttu-id="6cb53-106">在這之後，您可以登入 toohello 系統管理員和租用戶入口網站 toomanage Azure 堆疊及測試優惠。</span><span class="sxs-lookup"><span data-stu-id="6cb53-106">After that, you can sign in toohello admin and tenant portals toomanage Azure Stack and test offers.</span></span> 

1. <span data-ttu-id="6cb53-107">[**規劃您的硬體、軟體及網路**](azure-stack-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="6cb53-107">[**Plan your hardware, software, and network**](azure-stack-deploy.md).</span></span> <span data-ttu-id="6cb53-108">裝載 hello 開發套件 （hello 開發套件主機） 的 hello 電腦必須符合硬體、 軟體和網路需求。</span><span class="sxs-lookup"><span data-stu-id="6cb53-108">hello computer that hosts hello development kit (hello development kit host) must meet hardware, software, and network requirements.</span></span> <span data-ttu-id="6cb53-109">此外，您還必須在使用 Azure Active Directory 或「Active Directory 同盟服務」之間做選擇。</span><span class="sxs-lookup"><span data-stu-id="6cb53-109">You must also choose between using Azure Active Directory or Active Directory Federation Services.</span></span> <span data-ttu-id="6cb53-110">啟動您的部署，以便 hello 安裝程序順暢執行之前, 是確定 toocomply 具備這些先決條件。</span><span class="sxs-lookup"><span data-stu-id="6cb53-110">Be sure toocomply with these prerequisites before starting your deployment so that hello installation process runs smoothly.</span></span> 

2. <span data-ttu-id="6cb53-111">[**下載並解壓縮 hello 部署套件**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit)。</span><span class="sxs-lookup"><span data-stu-id="6cb53-111">[**Download and extract hello deployment package**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit).</span></span> <span data-ttu-id="6cb53-112">您可以下載 hello 部署封裝 toohello 開發套件主機或 tooa 另一部電腦。</span><span class="sxs-lookup"><span data-stu-id="6cb53-112">You can download hello deployment package toohello development kit host or tooa another computer.</span></span> <span data-ttu-id="6cb53-113">hello 解壓縮檔案佔用 60 GB 的可用磁碟空間，因此使用另一部電腦，可協助降低 hello hello 開發套件主機的硬體需求的部署。</span><span class="sxs-lookup"><span data-stu-id="6cb53-113">hello extracted deployment files take up 60 GB of free disk space, so using another computer can help reduce hello hardware requirements for hello development kit host.</span></span>

3. <span data-ttu-id="6cb53-114">[**準備 hello 開發套件主機**](azure-stack-run-powershell-script.md#prepare-the-development-kit-host)使用 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6cb53-114">[**Prepare hello development kit host**](azure-stack-run-powershell-script.md#prepare-the-development-kit-host) by using hello installer.</span></span> <span data-ttu-id="6cb53-115">這個步驟之後，hello 開發套件主機將會開機 toohello Cloudbuilder.vhdx （包括可開機的作業系統和 hello Azure 堆疊的虛擬硬碟安裝檔案）。</span><span class="sxs-lookup"><span data-stu-id="6cb53-115">After this step, hello development kit host will boot toohello Cloudbuilder.vhdx (a virtual hard drive that includes a bootable operating system and hello Azure Stack install files).</span></span>

4. <span data-ttu-id="6cb53-116">[**部署 hello 開發套件**](azure-stack-run-powershell-script.md#deploy-the-development-kit) hello 開發套件主機上。</span><span class="sxs-lookup"><span data-stu-id="6cb53-116">[**Deploy hello development kit**](azure-stack-run-powershell-script.md#deploy-the-development-kit) on hello development kit host.</span></span>

5. <span data-ttu-id="6cb53-117">如果您的 Azure 堆疊部署使用 Azure Active Directory，您必須[向 Azure 註冊 Azure 堆疊](azure-stack-register.md)，讓您可以[下載 Azure marketplace 所提供的項目](azure-stack-download-azure-marketplace-item.md)tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="6cb53-117">If your Azure Stack deployment uses Azure Active Directory, you must [register Azure Stack with Azure](azure-stack-register.md) so that you can [download Azure marketplace items](azure-stack-download-azure-marketplace-item.md) tooAzure Stack.</span></span>

<span data-ttu-id="6cb53-118">完成這些步驟之後，您將會擁有一個同時具有系統管理員和租用戶入口網站的開發套件環境。</span><span class="sxs-lookup"><span data-stu-id="6cb53-118">After completing these steps, you’ll have a development kit environment with both administrator and tenant portals.</span></span> <span data-ttu-id="6cb53-119">接下來，您可以[連接和登入](azure-stack-connect-azure-stack.md)toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6cb53-119">Next, you can [connect and sign in](azure-stack-connect-azure-stack.md) toohello portal.</span></span> <span data-ttu-id="6cb53-120">您可以開始部署資源提供者、 建立[提供](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions)，並填入 hello Azure 堆疊[marketplace](azure-stack-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="6cb53-120">You can then start deploying resource providers, creating [offers](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions), and populating hello Azure Stack [marketplace](azure-stack-marketplace.md).</span></span>
