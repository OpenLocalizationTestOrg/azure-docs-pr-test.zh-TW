---
title: "在 Azure RemoteApp QuickBooks aaaDeploy |Microsoft 文件"
description: "深入了解如何 tooshare QuickBooks 與 Azure RemoteApp。"
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="7afa5-103">您如何在 Azure RemoteApp 中部署 QuickBooks？</span><span class="sxs-lookup"><span data-stu-id="7afa5-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7afa5-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7afa5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7afa5-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7afa5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7afa5-106">使用下列資訊 tooshare QuickBooks 成 Azure RemoteApp 中的應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="7afa5-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="7afa5-107">您可以在混合式或雲端集合中使用 Azure RemoteApp 來共用 QuickBooks 2015 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="7afa5-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="7afa5-108">hello 公司檔案必須位於執行 QuickBooks 資料庫伺服器與 hello Azure RemoteApp 伺服器位於不同的 VM。</span><span class="sxs-lookup"><span data-stu-id="7afa5-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="7afa5-109">永遠不會儲存在您的 Azure RemoteApp 映像上的 hello 公司檔案-如果您這麼做預期資料遺失。</span><span class="sxs-lookup"><span data-stu-id="7afa5-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="7afa5-110">只有 QuickBooks Enterprise 支援在外部共用 QuickBooks 可透過標準 Windows 網路存取的資料庫伺服器上裝載 hello QuickBooks 檔案。</span><span class="sxs-lookup"><span data-stu-id="7afa5-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="7afa5-111">hello QuickBooks 裝載 hello 公司檔案的資料庫伺服器必須位於不同的 VM 內 hello 相同 VNET 與 hello Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="7afa5-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="7afa5-112">步驟 toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="7afa5-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="7afa5-113">建立 Azure VM 和安裝 QuickBooks 等 QuickBooks 資料庫伺服器，並放在 Azure VM 上的 hello 公司檔案。</span><span class="sxs-lookup"><span data-stu-id="7afa5-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="7afa5-114">請確定 tooproperly 設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7afa5-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="7afa5-115">在上安裝 QuickBooks[自訂映像](remoteapp-imageoptions.md)並建立[Azure RemoteApp 集合](remoteapp-collections.md)，雲端或混合式 hello 內完全相同的 VNET，其中 VM 所裝載的 hello hello 與 QuickBooks 資料庫伺服器位於公司檔案。</span><span class="sxs-lookup"><span data-stu-id="7afa5-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="7afa5-116">[發行](remoteapp-publish.md)QuickBooks 應用程式 toousers</span><span class="sxs-lookup"><span data-stu-id="7afa5-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="7afa5-117">啟動 hello Azure RemoteApp 裝載 QuickBooks 用戶端，使用標準 Windows 網路 toohello VM 主控 hello QuickBooks 資料庫伺服器瀏覽並開啟 hello 公司檔案。</span><span class="sxs-lookup"><span data-stu-id="7afa5-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="7afa5-118">文件參考</span><span class="sxs-lookup"><span data-stu-id="7afa5-118">Documentation references</span></span>
* <span data-ttu-id="7afa5-119">QuickBooks [支援的組態](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="7afa5-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="7afa5-120">QuickBooks [部署選項](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="7afa5-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="7afa5-121">您也可以查看 Ignite 簡報，[基礎的 Microsoft Azure RemoteApp 管理和管理](https://channel9.msdn.com/Events/Ignite/2015/BRK3868)-向前快轉 too1:02:45 tooget toohello QuickBooks 組件。</span><span class="sxs-lookup"><span data-stu-id="7afa5-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="7afa5-122">部署架構</span><span class="sxs-lookup"><span data-stu-id="7afa5-122">Deployment architecture</span></span>
![QuickBooks + Azure RemoteApp 部署](./media/remoteapp-quickbooks/ra-quickbooks.png)

