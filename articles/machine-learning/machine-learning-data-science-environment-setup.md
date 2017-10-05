---
title: "在 Azure 中設定資料科學環境 | Microsoft Docs"
description: "在 Azure 上設定用於 Team Data Science Process 中的資料科學環境。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 481cfa6a-7ea3-46ac-b0f9-2e3982c37153
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: bradsev
ms.openlocfilehash: 4f2f66288428aa0aa41abb40ce0e43c4848543ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-data-science-environments-for-use-in-the-team-data-science-process"></a><span data-ttu-id="14f7a-103">設定用於 Team Data Science Process 中的資料科學環境</span><span class="sxs-lookup"><span data-stu-id="14f7a-103">Set up data science environments for use in the Team Data Science Process</span></span>
<span data-ttu-id="14f7a-104">Team Data Science Process 使用各種資料科學環境來儲存、處理和分析資料。</span><span class="sxs-lookup"><span data-stu-id="14f7a-104">The Team Data Science Process uses various data science environments for the storage, processing, and analysis of data.</span></span> <span data-ttu-id="14f7a-105">他們包含 Azure Blob 儲存體、數種類型的 Azure 虛擬機器、HDInsight (Hadoop) 叢集，以及 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="14f7a-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span></span> <span data-ttu-id="14f7a-106">要使用哪一個環境，取決於要進行模型化的資料類型和數量，以及該資料在雲端中的目標目的地。</span><span class="sxs-lookup"><span data-stu-id="14f7a-106">The decision about which environment to use depends on the type and quantity of data to be modeled and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="14f7a-107">如需進行這項決策時要考量之問題的指引，請參閱[規劃您的 Azure Machine Learning 資料科學環境](machine-learning-data-science-plan-your-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="14f7a-107">For guidance on questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="14f7a-108">如需在進行進階分析時可能會遇到的部分案例目錄，請參閱 [適用於 Team Data Science Process 的案例](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="14f7a-108">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Team Data Science Process](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="14f7a-109">此功能表所連結的主題會說明如何設定 Team Data Science Process 所用的各種資料科學環境。</span><span class="sxs-lookup"><span data-stu-id="14f7a-109">This menu links to topics that describe how to set up the various data science environments used by the Team Data Science Process.</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="14f7a-110">**Microsoft 資料科學虛擬機器 (DSVM)** 也以 Azure 虛擬機器 (VM) 映像形式提供。</span><span class="sxs-lookup"><span data-stu-id="14f7a-110">The **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span></span> <span data-ttu-id="14f7a-111">此 VM 會預先安裝並且以數個常用於資料分析和機器學習服務的熱門工具進行設定。</span><span class="sxs-lookup"><span data-stu-id="14f7a-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="14f7a-112">DSVM 可用於 Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="14f7a-112">The DSVM is available on both Windows and Linux.</span></span> <span data-ttu-id="14f7a-113">如需進一步資訊，請參閱[適用於 Linux 和 Windows 的雲端型資料科學虛擬機器簡介](machine-learning-data-science-virtual-machine-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="14f7a-113">For further information, see [Introduction to the cloud-based Data Science Virtual Machine for Linux and Windows](machine-learning-data-science-virtual-machine-overview.md).</span></span>

