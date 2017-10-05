---
title: "什麼是 Azure 自動化 |Microsoft Docs"
description: "了解 Azure 自動化提供的價值，並取得常見問題的解答，以便您可以開始建立及使用 Runbook 和 Azure Automation DSC。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "何謂自動化, azure 自動化, azure 自動化範例"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 6b1fb9e7ae810df21cbcd592fef2b43309e2269c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-automation-overview"></a><span data-ttu-id="f0780-104">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="f0780-104">Azure Automation overview</span></span>
<span data-ttu-id="f0780-105">Microsoft Azure 自動化可讓使用者將執行於雲端和企業環境中的手動、長時間執行、易發生錯誤且重複性高的工作自動化。</span><span class="sxs-lookup"><span data-stu-id="f0780-105">Microsoft Azure Automation provides a way for users to automate the manual, long-running, error-prone, and frequently repeated tasks that are commonly performed in a cloud and enterprise environment.</span></span> <span data-ttu-id="f0780-106">它可以節省時間並提高日常管理工作的可靠性，甚至將它們排程為定期自動執行。</span><span class="sxs-lookup"><span data-stu-id="f0780-106">It saves time and increases the reliability of regular administrative tasks and even schedules them to be automatically performed at regular intervals.</span></span> <span data-ttu-id="f0780-107">您可以使用 Runbook 自動執行程序，或使用「期望狀態設定」自動進行組態管理。</span><span class="sxs-lookup"><span data-stu-id="f0780-107">You can automate processes using runbooks or automate configuration management using Desired State Configuration.</span></span> <span data-ttu-id="f0780-108">本文提供 Azure 自動化的簡短概觀，並回答一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="f0780-108">This article provides brief overview of Azure Automation and answers some common questions.</span></span> <span data-ttu-id="f0780-109">您可以參考此文件庫中的其他文件，以取得不同主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0780-109">You can refer to other articles in this library for more detailed information on the different topics.</span></span>

## <a name="automating-processes-with-runbooks"></a><span data-ttu-id="f0780-110">使用 Runbook 自動執行程序</span><span class="sxs-lookup"><span data-stu-id="f0780-110">Automating processes with runbooks</span></span>
<span data-ttu-id="f0780-111">Runbook 是可在 Azure 自動化中執行一些自動程序的一組工作。</span><span class="sxs-lookup"><span data-stu-id="f0780-111">A runbook is a set of tasks that perform some automated process in Azure Automation.</span></span> <span data-ttu-id="f0780-112">它可能是簡單的程序 (例如啟動虛擬機器及建立記錄項目)，或您可能會有一個結合其他較小的 Runbook 的複雜 Runbook，用來對多個資源或甚至是多個雲端和內部部署環境執行複雜的程序。</span><span class="sxs-lookup"><span data-stu-id="f0780-112">It may be a simple process such as starting a virtual machine and creating a log entry, or you may have a complex runbook that combines other smaller runbooks to perform a complex process across multiple resources or even multiple clouds and on-premises environments.</span></span>  

<span data-ttu-id="f0780-113">例如，當資料庫接近大小上限時，您可能有用來截斷 SQL Database 的現有手動程序，該程序包含多個步驟，例如連接到伺服器、連接到資料庫、取得目前的資料庫大小、檢查是否超過臨界值，然後進行截斷並通知使用者。</span><span class="sxs-lookup"><span data-stu-id="f0780-113">For example, you might have an existing manual process for truncating a SQL database if it’s approaching maximum size that includes multiple steps such as connecting to the server, connecting to the database, get the current size of database, check if threshold has exceeded and then truncate it and notify user.</span></span> <span data-ttu-id="f0780-114">不需手動執行每個步驟，您可以建立會以單一程序的形式執行這所有工作的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f0780-114">Instead of manually performing each of these steps, you could create a runbook that would perform all of these tasks as a single process.</span></span> <span data-ttu-id="f0780-115">您會啟動 Runbook、提供所需的資訊，例如 SQL 伺服器名稱、資料庫名稱和收件者電子郵件，然後在程序完成時在一旁休息。</span><span class="sxs-lookup"><span data-stu-id="f0780-115">You would start the runbook, provide the required information such as the SQL server name, database name, and recipient e-mail and then sit back while the process completes.</span></span> 

## <a name="what-can-runbooks-automate"></a><span data-ttu-id="f0780-116">Runbook 可以自動化什麼？</span><span class="sxs-lookup"><span data-stu-id="f0780-116">What can runbooks automate?</span></span>
<span data-ttu-id="f0780-117">Azure 自動化中的 Runbook 是以 Windows PowerShell 或 Windows PowerShell 工作流程為基礎，因此它們會執行 PowerShell 能做的一切功能。</span><span class="sxs-lookup"><span data-stu-id="f0780-117">Runbooks in Azure Automation are based on Windows PowerShell or Windows PowerShell Workflow, so they do anything that PowerShell can do.</span></span> <span data-ttu-id="f0780-118">如果應用程式或服務具有 API，則 Runbook 處理它。</span><span class="sxs-lookup"><span data-stu-id="f0780-118">If an application or service has an API, then a runbook can work with it.</span></span> <span data-ttu-id="f0780-119">如果您有應用程式適用的 PowerShell 模組，可以將該模組載入到 Azure 自動化，並且在 Runbook 中包含這些 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f0780-119">If you have a PowerShell module for the application, then you can load that module into Azure Automation and include those cmdlets in your runbook.</span></span> <span data-ttu-id="f0780-120">Azure 自動化 Runbook 會在 Azure 雲端執行，而且可以存取任何雲端資源或可從雲端存取的外部資源。</span><span class="sxs-lookup"><span data-stu-id="f0780-120">Azure Automation runbooks run in the Azure cloud and can access any cloud resources or external resources that can be accessed from the cloud.</span></span> <span data-ttu-id="f0780-121">使用 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)，Runbook 可以在您的本機資料中心中執行以管理本機資源。</span><span class="sxs-lookup"><span data-stu-id="f0780-121">Using [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), runbooks can run in your local data center to manage local resources.</span></span> 

## <a name="getting-runbooks-from-the-community"></a><span data-ttu-id="f0780-122">從社群取得 Runbook</span><span class="sxs-lookup"><span data-stu-id="f0780-122">Getting runbooks from the community</span></span>
<span data-ttu-id="f0780-123">[Runbook 資源庫](automation-runbook-gallery.md#runbooks-in-runbook-gallery) 包含來自 Microsoft 和社群的 Runbook，您可以在您的環境中原樣使用或根據您的用途加以自訂。</span><span class="sxs-lookup"><span data-stu-id="f0780-123">The [Runbook Gallery](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contains runbooks from Microsoft and the community that you can either use unchanged in your environment or customize them for your own purposes.</span></span> <span data-ttu-id="f0780-124">它們也可做為參考以了解如何建立您自己的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f0780-124">They are also useful to as references to learn how to create your own runbooks.</span></span> <span data-ttu-id="f0780-125">您甚至可以將您認為其他使用者可能覺得很有用的自己的 Runbook 貢獻到資源庫中。</span><span class="sxs-lookup"><span data-stu-id="f0780-125">You can even contribute your own runbooks to the gallery that you think other users may find useful.</span></span> 

## <a name="creating-runbooks-with-azure-automation"></a><span data-ttu-id="f0780-126">利用 Azure 自動化建立 Runbook</span><span class="sxs-lookup"><span data-stu-id="f0780-126">Creating Runbooks with Azure Automation</span></span>
<span data-ttu-id="f0780-127">您可以從頭[建立您自己的 Runbook](automation-creating-importing-runbook.md) 或根據您的需求修改來自 [Runbook 資源庫](http://msdn.microsoft.com/library/azure/dn781422.aspx)的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f0780-127">You can [create your own runbooks](automation-creating-importing-runbook.md) from scratch or modify runbooks from the [Runbook Gallery](http://msdn.microsoft.com/library/azure/dn781422.aspx) for your own requirements.</span></span> <span data-ttu-id="f0780-128">有四個不同的 [Runbook 類型](automation-runbook-types.md)，您可以依據需求和 PowerShell 經驗自行選擇。</span><span class="sxs-lookup"><span data-stu-id="f0780-128">There are four different [runbook types](automation-runbook-types.md) that you can choose from based on your requirements and PowerShell experience.</span></span> <span data-ttu-id="f0780-129">如果您想要直接使用 PowerShell 程式碼，則可以使用離線編輯的 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 或 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)，或是使用 Azure 入口網站中的[文字編輯器](http://msdn.microsoft.com/library/azure/dn879137.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f0780-129">If you prefer to work directly with the PowerShell code, then you can use a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks) that you edit offline or with the [textual editor](http://msdn.microsoft.com/library/azure/dn879137.aspx) in the Azure portal.</span></span> <span data-ttu-id="f0780-130">如果您想要編輯 Runbook 而不要看到基礎程式碼，則可以使用 Azure 入口網站中的[圖形化編輯器](automation-runbook-types.md#graphical-runbooks)建立[圖形化 Runbook](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="f0780-130">If you prefer to edit a runbook without being exposed to the underlying code, then you can create a [Graphical runbook](automation-runbook-types.md#graphical-runbooks) using the [graphical editor](automation-graphical-authoring-intro.md) in the Azure portal.</span></span> 

<span data-ttu-id="f0780-131">寧可觀賞也不要閱讀？</span><span class="sxs-lookup"><span data-stu-id="f0780-131">Prefer watching to reading?</span></span> <span data-ttu-id="f0780-132">看看以下在 2015 年 5 月的 Microsoft Ignite 活動影片。</span><span class="sxs-lookup"><span data-stu-id="f0780-132">Have a look at the below video from Microsoft Ignite session in May 2015.</span></span> <span data-ttu-id="f0780-133">附註：雖然這個影片中討論的概念和功能是正確的，但自從這個影片錄製以來，Azure 自動化已經有很大的進展，現在它在 Azure 入口網站中具有更豐富的 UI，並支援其他的功能。</span><span class="sxs-lookup"><span data-stu-id="f0780-133">Note: While the concepts and features discussed in this video are correct, Azure Automation has progressed a lot since this video was recorded, it now has a more extensive UI in the Azure portal, and supports additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a><span data-ttu-id="f0780-134">使用「預期狀態設定」自動進行組態管理</span><span class="sxs-lookup"><span data-stu-id="f0780-134">Automating configuration management with Desired State Configuration</span></span>
<span data-ttu-id="f0780-135">[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) 是一個管理平台，可讓您使用宣告式 PowerShell 語法來管理、部署及強制設定實體主機和虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f0780-135">[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) is a management platform that allows you to manage, deploy and enforce configuration for physical hosts and virtual machines using a declarative PowerShell syntax.</span></span> <span data-ttu-id="f0780-136">您可以在中央 DSC 提取伺服器上定義組態，該伺服器是以可自動擷取和套用的電腦為目標。</span><span class="sxs-lookup"><span data-stu-id="f0780-136">You can define configurations on a central DSC Pull Server that target machines can automatically retrieve and apply.</span></span> <span data-ttu-id="f0780-137">DSC 提供一組 PowerShell Cmdlet，讓您用來管理組態和資源。</span><span class="sxs-lookup"><span data-stu-id="f0780-137">DSC provides a set of PowerShell cmdlets that you can use to manage configurations and resources.</span></span>  

<span data-ttu-id="f0780-138">[Azure Automation DSC](automation-dsc-overview.md) 是針對 PowerShell DSC 的雲端架構解決方案，可提供企業環境所需的服務。</span><span class="sxs-lookup"><span data-stu-id="f0780-138">[Azure Automation DSC](automation-dsc-overview.md) is a cloud based solution for PowerShell DSC that provides services required for enterprise environments.</span></span>  <span data-ttu-id="f0780-139">您可以在 Azure 自動化中管理 DSC 資源，並將組態套用至虛擬或實體機器，以便它們從 Azure 雲端中的 DSC 提取伺服器擷取組態。</span><span class="sxs-lookup"><span data-stu-id="f0780-139">You can manage your DSC resources in Azure Automation and apply configurations to virtual or physical machines that retrieve them from a DSC Pull Server in the Azure cloud.</span></span>  <span data-ttu-id="f0780-140">它也提供報告服務，以通知您重要的事件，例如當節點偏離其指派的組態時以及已套用新的組態時。</span><span class="sxs-lookup"><span data-stu-id="f0780-140">It also provides reporting services that inform you of important events such as when nodes have deviated from their assigned configuration and when a new configuration has been applied.</span></span> 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a><span data-ttu-id="f0780-141">使用 Azure 自動化建立自己的 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="f0780-141">Creating your own DSC configurations with Azure Automation</span></span>
<span data-ttu-id="f0780-142">[DSC 組態](automation-dsc-overview.md) 可指定節點的預期狀態。</span><span class="sxs-lookup"><span data-stu-id="f0780-142">[DSC configurations](automation-dsc-overview.md) specify the desired state of a node.</span></span>  <span data-ttu-id="f0780-143">多個節點可以套用相同的組態，以確保它們全都維持相同的狀態。</span><span class="sxs-lookup"><span data-stu-id="f0780-143">Multiple nodes can apply the same configuration to assure that they all maintain an identical state.</span></span>  <span data-ttu-id="f0780-144">您可以在本機電腦上使用任何文字編輯器來建立組態，然後將它匯入至 Azure 自動化加以編譯並套用至節點。</span><span class="sxs-lookup"><span data-stu-id="f0780-144">You can create a configuration using any text editor on your local machine and then import it into Azure Automation where you can compile it and apply it nodes.</span></span>

## <a name="getting-modules-and-configurations"></a><span data-ttu-id="f0780-145">取得模組和組態</span><span class="sxs-lookup"><span data-stu-id="f0780-145">Getting modules and configurations</span></span>
<span data-ttu-id="f0780-146">您可以從 [PowerShell 資源庫](automation-runbook-gallery.md#modules-in-powershell-gallery)取得 [PowerShell 模組](http://www.powershellgallery.com/) (其中包含您可以在 Runbook 中使用的 Cmdlet) 和 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="f0780-146">You can get [PowerShell modules](automation-runbook-gallery.md#modules-in-powershell-gallery) containing cmdlets that you can use in your runbooks and DSC configurations from the [PowerShell Gallery](http://www.powershellgallery.com/).</span></span> <span data-ttu-id="f0780-147">您可以從 Azure 入口網站啟動這個資源庫，並且將模組直接匯入 Azure 自動化，或者您可以手動下載及匯入。</span><span class="sxs-lookup"><span data-stu-id="f0780-147">You can launch this gallery from the Azure portal and import modules directly into Azure Automation, or you can download and import them manually.</span></span> <span data-ttu-id="f0780-148">您無法直接從 Azure 入口網站安裝模組，但是您可以下載及安裝它們，就像任何其他模組一樣。</span><span class="sxs-lookup"><span data-stu-id="f0780-148">You cannot install the modules directly from the Azure portal, but you can download them install them as you would any other module.</span></span> 

## <a name="example-practical-applications-of-azure-automation"></a><span data-ttu-id="f0780-149">Azure 自動化的實際應用範例</span><span class="sxs-lookup"><span data-stu-id="f0780-149">Example practical applications of Azure Automation</span></span>
<span data-ttu-id="f0780-150">以下是一些使用 Azure 自動化之自動化案例種類的範例。</span><span class="sxs-lookup"><span data-stu-id="f0780-150">Following are just a few examples of what are the kinds of automation scenarios with Azure Automation.</span></span> 

* <span data-ttu-id="f0780-151">在不同的 Azure 訂用帳戶中建立和複製虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f0780-151">Create and copy virtual machines in different Azure subscriptions.</span></span> 
* <span data-ttu-id="f0780-152">本機電腦中的檔案複本排程到 Azure Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="f0780-152">Schedule file copies from a local machine to an Azure Blob Storage container.</span></span> 
* <span data-ttu-id="f0780-153">在偵測到阻斷服務攻擊時自動執行安全性功能，例如來自用戶端的拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="f0780-153">Automate security functions such as deny requests from a client when a denial of service attack is detected.</span></span> 
* <span data-ttu-id="f0780-154">確定機器持續依循設定的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="f0780-154">Ensure machines continually align with configured security policy.</span></span>
* <span data-ttu-id="f0780-155">跨雲端和內部部署基礎結構來管理應用程式程式碼的連續部署。</span><span class="sxs-lookup"><span data-stu-id="f0780-155">Manage continuous deployment of application code across cloud and on premises infrastructure.</span></span> 
* <span data-ttu-id="f0780-156">在 Azure 中針對您的實驗室環境建置 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="f0780-156">Build an Active Directory forest in Azure for your lab environment.</span></span> 
* <span data-ttu-id="f0780-157">如果資料庫已接近大小上限，請截斷 SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="f0780-157">Truncate a table in a SQL database if DB is approaching maximum size.</span></span> 
* <span data-ttu-id="f0780-158">遠端更新 Azure 網站的環境設定。</span><span class="sxs-lookup"><span data-stu-id="f0780-158">Remotely update environment settings for an Azure website.</span></span> 

## <a name="how-does-azure-automation-relate-to-other-automation-tools"></a><span data-ttu-id="f0780-159">Azure 自動化與其他自動化工具如何產生關聯？</span><span class="sxs-lookup"><span data-stu-id="f0780-159">How does Azure Automation relate to other automation tools?</span></span>
<span data-ttu-id="f0780-160">[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) 旨在自動化私人雲端中的管理工作。</span><span class="sxs-lookup"><span data-stu-id="f0780-160">[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) is intended to automate management tasks in the private cloud.</span></span> <span data-ttu-id="f0780-161">它會安裝在您的本機資料中心，做為 [Microsoft Azure 套件](https://www.microsoft.com/en-us/server-cloud/)的元件。</span><span class="sxs-lookup"><span data-stu-id="f0780-161">It is installed locally in your data center as a component of [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/).</span></span> <span data-ttu-id="f0780-162">SMA 和 Azure 自動化使用以 Windows PowerShell 和 Windows PowerShell 工作流程為基礎的相同 Runbook 格式，但 SMA 不支援 [圖形化 Runbook](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="f0780-162">SMA and Azure Automation use the same runbook format based on Windows PowerShell and Windows PowerShell Workflow, but SMA does not support [graphical runbooks](automation-graphical-authoring-intro.md).</span></span>  

<span data-ttu-id="f0780-163">[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) 旨在自動化內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="f0780-163">[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) is intended for automation of on-premises resources.</span></span> <span data-ttu-id="f0780-164">它會使用與 Azure 自動化和服務管理自動化不同的 Runbook 格式，並具有圖形化介面，用來建立 Runbook，而不需要編寫任何指令碼。</span><span class="sxs-lookup"><span data-stu-id="f0780-164">It uses a different runbook format than Azure Automation and Service Management Automation and has a graphical interface to create runbooks without requiring any scripting.</span></span> <span data-ttu-id="f0780-165">其 Runbook 是由來自專門為 Orchestrator 編寫的整合套件的活動組成。</span><span class="sxs-lookup"><span data-stu-id="f0780-165">Its runbooks are composed of activities from Integration Packs that are written specifically for Orchestrator.</span></span> 

## <a name="where-can-i-get-more-information"></a><span data-ttu-id="f0780-166">我可以在哪裡取得詳細資訊？</span><span class="sxs-lookup"><span data-stu-id="f0780-166">Where can I get more information?</span></span>
<span data-ttu-id="f0780-167">您可利用各種資源，深入了解 Azure 自動化，並建立自己的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f0780-167">A variety of resources are available for you to learn more about Azure Automation and creating your own runbooks.</span></span> 

* <span data-ttu-id="f0780-168">**Azure 自動化程式庫** 是您目前的所在位置。</span><span class="sxs-lookup"><span data-stu-id="f0780-168">**Azure Automation Library** is where you are right now.</span></span> <span data-ttu-id="f0780-169">本文件庫中的文章提供完整的文件，說明如何設定和管理 Azure 自動化，以及撰寫自己的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f0780-169">The articles in this library provide complete documentation on the configuration and administration of Azure Automation and for authoring your own runbooks.</span></span> 
* <span data-ttu-id="f0780-170">[Azure PowerShell Cmdlet](http://msdn.microsoft.com/library/jj156055.aspx) 提供使用 Windows PowerShell 自動執行 Azure 作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="f0780-170">[Azure PowerShell cmdlets](http://msdn.microsoft.com/library/jj156055.aspx) provides information for automating Azure operations using Windows PowerShell.</span></span> <span data-ttu-id="f0780-171">Runbook 會使用這些 Cmdlet 來處理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f0780-171">Runbooks use these cmdlets to work with Azure resources.</span></span> 
* <span data-ttu-id="f0780-172">[管理部落格](https://azure.microsoft.com/blog/tag/azure-automation/) 提供 Azure 自動化的最新資訊，以及 Microsoft 的其他管理技術。</span><span class="sxs-lookup"><span data-stu-id="f0780-172">[Management Blog](https://azure.microsoft.com/blog/tag/azure-automation/) provides the latest information on Azure Automation and other management technologies from Microsoft.</span></span> <span data-ttu-id="f0780-173">您應該訂閱此部落格，隨時掌握 Azure 自動化團隊的最新消息。</span><span class="sxs-lookup"><span data-stu-id="f0780-173">You should subscribe to this blog to stay up to date with the latest from the Azure Automation team.</span></span> 
* <span data-ttu-id="f0780-174">[自動化論壇](http://go.microsoft.com/fwlink/p/?LinkId=390561) 可讓您張貼有關要由 Microsoft 和自動化社群解決的 Azure 自動化問題。</span><span class="sxs-lookup"><span data-stu-id="f0780-174">[Automation Forum](http://go.microsoft.com/fwlink/p/?LinkId=390561) allows you to post questions about Azure Automation to be addressed by Microsoft and the Automation community.</span></span> 
* <span data-ttu-id="f0780-175">[Azure 自動化 Cmdlet](https://msdn.microsoft.com/library/mt244122.aspx) 提供自動執行管理工作的資訊。</span><span class="sxs-lookup"><span data-stu-id="f0780-175">[Azure Automation Cmdlets](https://msdn.microsoft.com/library/mt244122.aspx) provides information for automating administration tasks.</span></span> <span data-ttu-id="f0780-176">它包含各種 Cmdlet 來管理自動化帳戶、資產、Runbook、DSC。</span><span class="sxs-lookup"><span data-stu-id="f0780-176">It contains cmdlets to manage Automation accounts, assets, runbooks, DSC.</span></span>

## <a name="can-i-provide-feedback"></a><span data-ttu-id="f0780-177">可以提供意見嗎？</span><span class="sxs-lookup"><span data-stu-id="f0780-177">Can I provide feedback?</span></span>
<span data-ttu-id="f0780-178">**請不吝提供意見！**</span><span class="sxs-lookup"><span data-stu-id="f0780-178">**Please give us feedback!**</span></span> <span data-ttu-id="f0780-179">如果您要尋找 Azure 自動化 Runbook 解決方案或整合模組，請在指令碼中心提出指令碼要求。</span><span class="sxs-lookup"><span data-stu-id="f0780-179">If you are looking for an Azure Automation runbook solution or an integration module, post a Script Request on Script Center.</span></span> <span data-ttu-id="f0780-180">如果您有關於 Azure 自動化的任何意見或功能要求，請張貼在 [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback)上。</span><span class="sxs-lookup"><span data-stu-id="f0780-180">If you have feedback or feature requests for Azure Automation, post them on [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback).</span></span> <span data-ttu-id="f0780-181">感謝您！</span><span class="sxs-lookup"><span data-stu-id="f0780-181">Thanks!</span></span> 
