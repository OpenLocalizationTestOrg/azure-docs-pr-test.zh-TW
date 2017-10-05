---
title: "在 Azure RemoteApp 中部署 QuickBooks | Microsoft Docs"
description: "了解如何與 Azure RemoteApp 共用 QuickBooks。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="71a95-103">您如何在 Azure RemoteApp 中部署 QuickBooks？</span><span class="sxs-lookup"><span data-stu-id="71a95-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="71a95-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="71a95-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="71a95-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="71a95-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="71a95-106">使用下列資訊在 Azure RemoteApp 中以應用程式形式共用 QuickBooks。</span><span class="sxs-lookup"><span data-stu-id="71a95-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="71a95-107">您可以在混合式或雲端集合中使用 Azure RemoteApp 來共用 QuickBooks 2015 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="71a95-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="71a95-108">公司檔案必須位於執行 QuickBooks 資料庫伺服器並且與 Azure RemoteApp 伺服器不同的 VM。</span><span class="sxs-lookup"><span data-stu-id="71a95-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="71a95-109">永遠不要將公司檔案儲存在您的 Azure RemoteApp 映像檔中 - 這麼做可能導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="71a95-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="71a95-110">只有 QuickBooks Enterprise 支援在外部共用上裝載 QuickBooks 檔案，該共用上具有可透過標準 Windows 網路存取的 QuickBooks 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="71a95-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="71a95-111">裝載公司檔案的 QuickBooks 資料庫伺服器必須位於與 Azure RemoteApp 集合相同的 VNET 內的不同 VM 上。</span><span class="sxs-lookup"><span data-stu-id="71a95-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="71a95-112">部署 QuickBooks 的步驟</span><span class="sxs-lookup"><span data-stu-id="71a95-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="71a95-113">建立 Azure VM 並安裝 QuickBooks、QuickBooks 資料庫伺服器，然後將公司檔案放在 Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="71a95-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="71a95-114">請務必正確設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="71a95-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="71a95-115">在[自訂映像檔](remoteapp-imageoptions.md)上安裝 QuickBooks，並且在與裝載 QuickBooks 資料庫伺服器 (公司檔案所在) 之 VM 完全相同的 VNET 內建立 [Azure RemoteApp 集合](remoteapp-collections.md) (無論是在雲端或混合式)。</span><span class="sxs-lookup"><span data-stu-id="71a95-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="71a95-116">[發佈](remoteapp-publish.md) QuickBooks 應用程式給使用者</span><span class="sxs-lookup"><span data-stu-id="71a95-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="71a95-117">啟動 Azure RemoteApp 裝載的 QuickBooks 用戶端，使用標準 Windows 網路瀏覽至裝載 QuickBooks 資料庫伺服器的 VM，並開啟公司檔案。</span><span class="sxs-lookup"><span data-stu-id="71a95-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="71a95-118">文件參考</span><span class="sxs-lookup"><span data-stu-id="71a95-118">Documentation references</span></span>
* <span data-ttu-id="71a95-119">QuickBooks [支援的組態](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="71a95-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="71a95-120">QuickBooks [部署選項](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="71a95-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="71a95-121">您也可以看看我的 Ignite 簡報 [Microsoft Azure RemoteApp 管理與系統管理的基礎](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - 向前快轉到 1:02:45，以跳到 QuickBooks 部分。</span><span class="sxs-lookup"><span data-stu-id="71a95-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="71a95-122">部署架構</span><span class="sxs-lookup"><span data-stu-id="71a95-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp 部署](./media/remoteapp-quickbooks/ra-quickbooks.png)

