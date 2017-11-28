---
title: "aaaConnect tooAzure Analysis Services 與 Power BI |Microsoft 文件"
description: "了解 tooconnect tooan Azure Analysis Services 如何使用 Power BI 的伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="03bb7-103">使用 Power BI 進行連接</span><span class="sxs-lookup"><span data-stu-id="03bb7-103">Connect with Power BI</span></span>

<span data-ttu-id="03bb7-104">在 Azure 中，建立伺服器並部署表格式模型 tooit 之後，您的組織中的使用者會準備 tooconnect，並開始瀏覽資料。</span><span class="sxs-lookup"><span data-stu-id="03bb7-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="03bb7-105">要確定 toouse hello 最新版本的[Power BI Desktop](https://powerbi.microsoft.com/desktop/)。</span><span class="sxs-lookup"><span data-stu-id="03bb7-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="03bb7-106">在 Power BI Desktop 中連線</span><span class="sxs-lookup"><span data-stu-id="03bb7-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="03bb7-107">在 Power BI Desktop 中，按一下 [取得資料] > [Azure] > [Azure Analysis Services 資料庫]。</span><span class="sxs-lookup"><span data-stu-id="03bb7-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="03bb7-108">在**伺服器**，輸入 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="03bb7-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="03bb7-109">是確定 tooinclude hello 完整 URL。</span><span class="sxs-lookup"><span data-stu-id="03bb7-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="03bb7-110">例如 asazure://westcentralus.asazure.windows.net/advworks。</span><span class="sxs-lookup"><span data-stu-id="03bb7-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="03bb7-111">在**資料庫**，如果您知道 hello hello 表格式模型資料庫或要 tooconnect 若要貼至此處的檢視方塊名稱。</span><span class="sxs-lookup"><span data-stu-id="03bb7-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="03bb7-112">否則，您可以將此欄位保留空白，然後稍後選取資料庫或檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="03bb7-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="03bb7-113">保留預設值，hello**即時連接**選項，然後按**連接**。</span><span class="sxs-lookup"><span data-stu-id="03bb7-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="03bb7-114">如果出現提示，請輸入您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="03bb7-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="03bb7-115">在**導覽**，展開 hello 伺服器，然後選取 hello 模型或您想要 tooconnect 至，然後按一下 檢視方塊**連接**。</span><span class="sxs-lookup"><span data-stu-id="03bb7-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="03bb7-116">按一下模型或檢視方塊 tooshow 適用於該檢視的所有 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="03bb7-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="03bb7-117">報表檢視中的空白報表與 Power BI Desktop 中開啟 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="03bb7-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="03bb7-118">hello 欄位清單會顯示所有非隱藏的模型物件。</span><span class="sxs-lookup"><span data-stu-id="03bb7-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="03bb7-119">連接狀態會顯示在 hello 右下角。</span><span class="sxs-lookup"><span data-stu-id="03bb7-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="03bb7-120">在 Power BI Desktop 中連線 (服務)</span><span class="sxs-lookup"><span data-stu-id="03bb7-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="03bb7-121">建立您的伺服器具有即時連接 tooyour 模型的 Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="03bb7-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="03bb7-122">在 [Power BI](https://powerbi.microsoft.com) 中，按一下 [取得資料]  >  [檔案]。</span><span class="sxs-lookup"><span data-stu-id="03bb7-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="03bb7-123">找到並選取您的檔案。</span><span class="sxs-lookup"><span data-stu-id="03bb7-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="03bb7-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="03bb7-124">See also</span></span>
<span data-ttu-id="03bb7-125">[連接 tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="03bb7-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="03bb7-126">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="03bb7-126">Client libraries</span></span>](analysis-services-data-providers.md)

