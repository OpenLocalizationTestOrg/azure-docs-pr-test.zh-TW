---
title: "使用 SSDT aaaDeploy tooAzure Analysis Services |Microsoft 文件"
description: "了解表格式模型 tooan toodeploy Azure Analysis Services 如何使用 SSDT 的伺服器。"
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="ddb77-103">從 SSDT 部署模型</span><span class="sxs-lookup"><span data-stu-id="ddb77-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="ddb77-104">您的 Azure 訂用帳戶中建立的伺服器之後，您已準備好 toodeploy 表格式模型資料庫 tooit。</span><span class="sxs-lookup"><span data-stu-id="ddb77-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="ddb77-105">您可以使用 SQL Server Data Tools (SSDT) toobuild 並部署您在處理表格式模型專案。</span><span class="sxs-lookup"><span data-stu-id="ddb77-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ddb77-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ddb77-106">Prerequisites</span></span>
<span data-ttu-id="ddb77-107">tooget 開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="ddb77-107">tooget started, you need:</span></span>

* <span data-ttu-id="ddb77-108">Azure 中的 **Analysis Services 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="ddb77-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="ddb77-109">詳細資訊，請參閱 toolearn[建立 Azure Analysis Services 伺服器](analysis-services-create-server.md)。</span><span class="sxs-lookup"><span data-stu-id="ddb77-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="ddb77-110">**表格式模型專案**SSDT 或現有的表格式模型在 hello 1200 或更高的相容性層級中。</span><span class="sxs-lookup"><span data-stu-id="ddb77-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="ddb77-111">未曾建立過？</span><span class="sxs-lookup"><span data-stu-id="ddb77-111">Never created one?</span></span> <span data-ttu-id="ddb77-112">再試一次 hello [Adventure Works 網際網路銷售的表格式模型教學課程](https://msdn.microsoft.com/library/hh231691.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ddb77-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="ddb77-113">**在內部部署閘道**-如果一或多個資料來源位於內部部署組織的網路中，您需要 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="ddb77-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="ddb77-114">您的伺服器 hello 雲端連線 tooyour 在內部部署資料來源 tooprocess 和重新整理模型中的資料 hello hello 閘道是必要的。</span><span class="sxs-lookup"><span data-stu-id="ddb77-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="ddb77-115">在部署之前，請確定您可以處理 hello 資料在資料表中。</span><span class="sxs-lookup"><span data-stu-id="ddb77-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="ddb77-116">在 SSDT 中，按一下 [模型]  >  [程序]  >  **Process All** (全部處理)。</span><span class="sxs-lookup"><span data-stu-id="ddb77-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="ddb77-117">如果處理失敗，您就無法部署成功。</span><span class="sxs-lookup"><span data-stu-id="ddb77-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="ddb77-118">toodeploy 從 SSDT 的表格式模型</span><span class="sxs-lookup"><span data-stu-id="ddb77-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="ddb77-119">在部署之前，您會需要 tooget hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ddb77-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="ddb77-120">在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ddb77-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="ddb77-122">在 SSDT 中 >**方案總管 中**，以滑鼠右鍵按一下 hello 專案 >**屬性**。</span><span class="sxs-lookup"><span data-stu-id="ddb77-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="ddb77-123">接著在**部署** > **伺服器**貼上 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ddb77-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![將伺服器名稱貼到部署伺服器屬性](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="ddb77-125">在 [方案總管] 中，以滑鼠右鍵按一下 [屬性]，然後按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="ddb77-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="ddb77-126">您可能會提示的 toosign tooAzure 中。</span><span class="sxs-lookup"><span data-stu-id="ddb77-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![部署 tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="ddb77-128">部署狀態會出現在這兩個 hello 輸出 視窗和部署。</span><span class="sxs-lookup"><span data-stu-id="ddb77-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![部署狀態](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="ddb77-130">這就是沒有 tooit ！</span><span class="sxs-lookup"><span data-stu-id="ddb77-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="ddb77-131">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ddb77-131">Troubleshooting</span></span>
<span data-ttu-id="ddb77-132">如果部署失敗部署中繼資料時，它可能是因為 SSDT 無法 tooyour 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="ddb77-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="ddb77-133">請確定您可以使用 SSMS 的 tooyour 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="ddb77-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="ddb77-134">請確定 hello hello 專案的 [部署伺服器] 屬性正確。</span><span class="sxs-lookup"><span data-stu-id="ddb77-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="ddb77-135">如果部署失敗的資料表上，它可能是因為您的伺服器無法連線 tooa 資料來源。</span><span class="sxs-lookup"><span data-stu-id="ddb77-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="ddb77-136">如果您的資料來源是內部部署組織的網路中，是確定 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="ddb77-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddb77-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddb77-137">Next steps</span></span>
<span data-ttu-id="ddb77-138">有您的表格式模型部署的 tooyour 伺服器之後，您準備好 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="ddb77-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="ddb77-139">您可以[使用 SSMS 連接 tooit](analysis-services-manage.md) toomanage 它。</span><span class="sxs-lookup"><span data-stu-id="ddb77-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="ddb77-140">而且，您可以[連接使用用戶端工具 tooit](analysis-services-connect.md)喜歡 Power BI、 Power BI Desktop 或 Excel 及建立報表的開始。</span><span class="sxs-lookup"><span data-stu-id="ddb77-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

