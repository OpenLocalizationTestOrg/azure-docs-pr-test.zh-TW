---
title: "aaaAbout Azure DevTest Labs |Microsoft 文件"
description: "了解如何 DevTest Labs 可讓您輕鬆 toocreate、 管理和監視 Azure 虛擬機器"
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
ms.openlocfilehash: 5e5aa683f80144a2f6872c7fa328016120ea6253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="6687d-103">關於 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6687d-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="6687d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6687d-104">Overview</span></span>
<span data-ttu-id="6687d-105">開發人員和測試人員會建立及管理其環境移 toohello 雲端尋找 toosolve hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="6687d-105">Developers and testers are looking toosolve hello delays in creating and managing their environments by going toohello cloud.</span></span>  <span data-ttu-id="6687d-106">Azure 解決了在 hello 環境延遲問題，並可讓自助服務成本效率結構內。</span><span class="sxs-lookup"><span data-stu-id="6687d-106">Azure solves hello problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="6687d-107">不過，開發人員和測試人員仍然需要 toospend 相當長的時間，設定其自行提供的環境。</span><span class="sxs-lookup"><span data-stu-id="6687d-107">However, developers and testers still need toospend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="6687d-108">此外，決策者不確定如何 tooleverage hello 雲端 toomaximize 節省而不會增加其成本太多處理額外負荷。</span><span class="sxs-lookup"><span data-stu-id="6687d-108">Also, decision makers are uncertain about how tooleverage hello cloud toomaximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="6687d-109">Azure DevTest Labs 是一項服務，可協助開發人員和測試人員在 Azure 中建立快速環境，同時將浪費降至最低並控制成本。</span><span class="sxs-lookup"><span data-stu-id="6687d-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="6687d-110">您可以測試 hello 最新版本的應用程式快速佈建 Windows 和 Linux 的環境，使用可重複使用的範本和成品。</span><span class="sxs-lookup"><span data-stu-id="6687d-110">You can test hello latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="6687d-111">輕鬆地整合 DevTest Labs tooprovision 視環境中部署管線。</span><span class="sxs-lookup"><span data-stu-id="6687d-111">Easily integrate your deployment pipeline with DevTest Labs tooprovision on-demand environments.</span></span> <span data-ttu-id="6687d-112">藉由佈建多個測試代理程式來相應增加您的負載測試，並建立預先佈建的環境來進行訓練和示範。</span><span class="sxs-lookup"><span data-stu-id="6687d-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="6687d-113">DevTest Labs 提供下列優點建立、 設定及管理 hello 雲端中的開發人員和測試環境的 hello</span><span class="sxs-lookup"><span data-stu-id="6687d-113">DevTest Labs provides hello following benefits in creating, configuring, and managing developer and test environments in hello cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="6687d-114">零煩惱的自助方式</span><span class="sxs-lookup"><span data-stu-id="6687d-114">Worry-free self-service</span></span>
<span data-ttu-id="6687d-115">DevTest Labs 可讓您更輕鬆 toocontrol 成本可讓您在您的實驗室-例如，虛擬機器 (VM) 數目的 tooset 原則每位使用者和每個實驗室的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="6687d-115">DevTest Labs makes it easier toocontrol costs by allowing you tooset policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="6687d-116">DevTest Labs 也可讓您 toocreate 原則 tooautomatically 關機和啟動 Vm。</span><span class="sxs-lookup"><span data-stu-id="6687d-116">DevTest Labs also enables you toocreate policies tooautomatically shut down and start VMs.</span></span>

## <a name="quickly-get-tooready-to-test"></a><span data-ttu-id="6687d-117">快速取得 tooready-測試</span><span class="sxs-lookup"><span data-stu-id="6687d-117">Quickly get tooready-to-test</span></span>
<span data-ttu-id="6687d-118">DevTest Labs 可讓您與您的小組必須 toostart 開發及測試應用程式的所有項目 toocreate 預先佈建的環境。</span><span class="sxs-lookup"><span data-stu-id="6687d-118">DevTest Labs enables you toocreate pre-provisioned environments with everything your team needs toostart developing and testing applications.</span></span> <span data-ttu-id="6687d-119">只要宣告 hello hello 最後一個良好的組建的應用程式安裝所在的環境，並取得以立即開始運作。</span><span class="sxs-lookup"><span data-stu-id="6687d-119">Simply claim hello environments where hello last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="6687d-120">或是使用容器，更快速且高效地建立環境。</span><span class="sxs-lookup"><span data-stu-id="6687d-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="6687d-121">一次建立，隨處可用</span><span class="sxs-lookup"><span data-stu-id="6687d-121">Create once, use everywhere</span></span>
<span data-ttu-id="6687d-122">擷取共用的環境範本與您的小組或公司的所有原始檔控制中的成品 toocreate 開發人員並輕鬆地測試環境。</span><span class="sxs-lookup"><span data-stu-id="6687d-122">Capture and share environment templates and artifacts within your team or organization - all in source control - toocreate developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="6687d-123">與現有工具鏈整合</span><span class="sxs-lookup"><span data-stu-id="6687d-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="6687d-124">利用預先製作的外掛程式或我們 API tooprovision 開發/測試環境直接從您慣用的持續整合 (CI) 工具，整合式開發環境 (IDE)，或自動發行管線。</span><span class="sxs-lookup"><span data-stu-id="6687d-124">Leverage pre-made plug-ins or our API tooprovision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="6687d-125">您也可以使用我們全方位的命令列工具。</span><span class="sxs-lookup"><span data-stu-id="6687d-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6687d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6687d-126">Next steps</span></span>
[<span data-ttu-id="6687d-127">研發/測試實驗室概念</span><span class="sxs-lookup"><span data-stu-id="6687d-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

