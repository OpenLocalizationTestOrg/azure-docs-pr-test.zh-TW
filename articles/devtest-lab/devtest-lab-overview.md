---
title: "關於 Azure DevTest Labs | Microsoft Docs"
description: "了解 DevTest Labs 如何讓您輕鬆地建立、管理和監視 Azure 虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="6dbc3-103">關於 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6dbc3-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="6dbc3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6dbc3-104">Overview</span></span>
<span data-ttu-id="6dbc3-105">開發人員和測試人員正藉由移至雲端來尋求解決在建立與管理其環境時所產生的延遲。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="6dbc3-106">Azure 解決了環境延遲的問題，並允許在具備成本效益的新結構內提供自助服務。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="6dbc3-107">不過，開發人員和測試人員仍然需要花很長的時間來設定提供自助式環境。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="6dbc3-108">此外，決策者不確定如何運用雲端來充分節省成本，而不會增加太多處理的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="6dbc3-109">Azure DevTest Labs 是一項服務，可協助開發人員和測試人員在 Azure 中建立快速環境，同時將浪費降至最低並控制成本。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="6dbc3-110">您可以利用可重複使用的範本和構件快速佈建 Windows 和 Linux 環境，來測試最新版的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="6dbc3-111">將您的部署管線與研發/測試實驗室輕鬆整合，來佈建隨選環境。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="6dbc3-112">藉由佈建多個測試代理程式來相應增加您的負載測試，並建立預先佈建的環境來進行訓練和示範。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="6dbc3-113">研發/測試實驗室在建立、設定及管理雲端中的開發人員和測試環境方面可提供下列優點</span><span class="sxs-lookup"><span data-stu-id="6dbc3-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="6dbc3-114">零煩惱的自助方式</span><span class="sxs-lookup"><span data-stu-id="6dbc3-114">Worry-free self-service</span></span>
<span data-ttu-id="6dbc3-115">研發/測試實驗室藉由讓您能夠設定實驗室的原則，更輕鬆地控制成本 - 例如，每位使用者的虛擬機器 (VM) 數目，以及每個實驗室的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="6dbc3-116">研發/測試實驗室也可讓您建立原則來自動關機並啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="6dbc3-117">快速做好測試的準備</span><span class="sxs-lookup"><span data-stu-id="6dbc3-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="6dbc3-118">研發/測試實驗室讓您能夠建立預先佈建的環境，完全滿足小組開發及測試應用程式時的一切需求。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="6dbc3-119">只要宣告已安裝您應用程式的最後一個良好組建且可立即運作的環境即可。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="6dbc3-120">或是使用容器，更快速且高效地建立環境。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="6dbc3-121">一次建立，隨處可用</span><span class="sxs-lookup"><span data-stu-id="6dbc3-121">Create once, use everywhere</span></span>
<span data-ttu-id="6dbc3-122">只需透過原始檔控制，便可在小組或組織內擷取並共用環境範本及構件，輕鬆建立開發人員和測試環境。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="6dbc3-123">與現有工具鏈整合</span><span class="sxs-lookup"><span data-stu-id="6dbc3-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="6dbc3-124">善用預製的外掛程式或我們的 API，直接從您偏好的持續整合 (CI) 工具、整合式開發環境 (IDE) 或自動化的發行管線來佈建研發/測試環境。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="6dbc3-125">您也可以使用我們全方位的命令列工具。</span><span class="sxs-lookup"><span data-stu-id="6dbc3-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6dbc3-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6dbc3-126">Next steps</span></span>
[<span data-ttu-id="6dbc3-127">研發/測試實驗室概念</span><span class="sxs-lookup"><span data-stu-id="6dbc3-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

