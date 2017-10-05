---
title: "使用 SSDT 部署至 Azure Analysis Services | Microsoft Docs"
description: "了解如何使用 SSDT 將表格式模型部署至 Azure Analysis Services 伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="08d7d-103">從 SSDT 部署模型</span><span class="sxs-lookup"><span data-stu-id="08d7d-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="08d7d-104">以您的 Azure 訂用帳戶建立伺服器後，您即可將表格式模型資料庫部署至該伺服器。</span><span class="sxs-lookup"><span data-stu-id="08d7d-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="08d7d-105">您可以使用 SQL Server Data Tools (SSDT) 建置與部署您正在使用的表格式模型專案。</span><span class="sxs-lookup"><span data-stu-id="08d7d-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="08d7d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="08d7d-106">Prerequisites</span></span>
<span data-ttu-id="08d7d-107">若要開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="08d7d-107">To get started, you need:</span></span>

* <span data-ttu-id="08d7d-108">Azure 中的 **Analysis Services 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="08d7d-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="08d7d-109">若要深入了解，請參閱[建立 Azure Analysis Services 伺服器](analysis-services-create-server.md)。</span><span class="sxs-lookup"><span data-stu-id="08d7d-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="08d7d-110">SSDT 中的**表格式模型專案**，或 1200 或更高相容性層級的現有表格式模型。</span><span class="sxs-lookup"><span data-stu-id="08d7d-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="08d7d-111">未曾建立過？</span><span class="sxs-lookup"><span data-stu-id="08d7d-111">Never created one?</span></span> <span data-ttu-id="08d7d-112">嘗試 [Adventure Works 網際網路銷售表格式模型教學課程](https://msdn.microsoft.com/library/hh231691.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08d7d-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="08d7d-113">**內部部署閘道** - 如果您組織的網路中有一或多個資料來源為內部部署，您必須安裝[內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="08d7d-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="08d7d-114">您在雲端中的伺服器必須有閘道，才能連線至您的內部部署資料來源，以處理和重新整理模型中的資料。</span><span class="sxs-lookup"><span data-stu-id="08d7d-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="08d7d-115">部署之前，請確定您可以在資料表中處理資料。</span><span class="sxs-lookup"><span data-stu-id="08d7d-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="08d7d-116">在 SSDT 中，按一下 [模型]  >  [程序]  >  **Process All** (全部處理)。</span><span class="sxs-lookup"><span data-stu-id="08d7d-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="08d7d-117">如果處理失敗，您就無法部署成功。</span><span class="sxs-lookup"><span data-stu-id="08d7d-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="08d7d-118">從 SSDT 部署表格式模型</span><span class="sxs-lookup"><span data-stu-id="08d7d-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="08d7d-119">部署之前，您必須先取得伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="08d7d-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="08d7d-120">在 [Azure 入口網站] > 伺服器 > [概觀]  >  [伺服器名稱] 中，複製伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="08d7d-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="08d7d-122">在 SSDT > [方案總管] 中，以滑鼠右鍵按一下專案 > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="08d7d-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="08d7d-123">接著在 [部署]  >  [伺服器] 中，貼上伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="08d7d-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![將伺服器名稱貼到部署伺服器屬性](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="08d7d-125">在 [方案總管] 中，以滑鼠右鍵按一下 [屬性]，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="08d7d-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="08d7d-126">系統會提示您登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="08d7d-126">You may be prompted to sign in to Azure.</span></span>
   
    ![部署至伺服器](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="08d7d-128">部署狀態會出現在 [輸出] 視窗和 [部署] 中。</span><span class="sxs-lookup"><span data-stu-id="08d7d-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![部署狀態](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="08d7d-130">就是這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="08d7d-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="08d7d-131">疑難排解</span><span class="sxs-lookup"><span data-stu-id="08d7d-131">Troubleshooting</span></span>
<span data-ttu-id="08d7d-132">如果在部署中繼資料時部署失敗，則可能是因為 SSDT 無法連線至您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="08d7d-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="08d7d-133">請確定您可以使用 SSMS 連線至您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="08d7d-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="08d7d-134">接著確定專案的 [部署伺服器] 屬性正確。</span><span class="sxs-lookup"><span data-stu-id="08d7d-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="08d7d-135">如果在資料表上部署失敗，則可能是因為您的伺服器無法連線至資料來源。</span><span class="sxs-lookup"><span data-stu-id="08d7d-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="08d7d-136">如果您的組織來源在您組織的網路中為內部部署，請務必安裝[內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="08d7d-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08d7d-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08d7d-137">Next steps</span></span>
<span data-ttu-id="08d7d-138">現在您的伺服器上已部署了表格式模型，您即可連線至該伺服器。</span><span class="sxs-lookup"><span data-stu-id="08d7d-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="08d7d-139">您可以[使用 SSMS 連線至該伺服器](analysis-services-manage.md)以進行管理。</span><span class="sxs-lookup"><span data-stu-id="08d7d-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="08d7d-140">此外，您可以[使用用戶端工具連線至該伺服器 ](analysis-services-connect.md) (如 Power BI、Power BI Desktop 或 Excel 等工具)，並開始建立報告。</span><span class="sxs-lookup"><span data-stu-id="08d7d-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

