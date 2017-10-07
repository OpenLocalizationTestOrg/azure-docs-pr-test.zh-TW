---
title: "aaaInstall Visual Studio 和 SQL 資料倉儲的 SSDT |Microsoft 文件"
description: "安裝適用於 Azure SQL 資料倉儲的 Visual Studio 和 SQL Server Development Tools (SSDT)"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="1dbf8-103">安裝適用於 SQL 資料倉儲的 Visual Studio 和 SSDT</span><span class="sxs-lookup"><span data-stu-id="1dbf8-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="1dbf8-104">SQL 資料倉儲的 toodevelop 應用程式，我們建議使用 hello 最新版本的 SQL Server Data Tools (SSDT) 中的 hello 最新版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="1dbf8-105">Visual Studio 2013 Update 5 搭配 SSDT 也支援回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="1dbf8-106">有了 SSDT 使用 Visual Studio 可讓您 toouse hello SQL Server 物件總管 toovisually 瀏覽資料表、 檢視、 預存程序和更多您的 SQL 資料倉儲中的物件，以及執行查詢。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="1dbf8-107">SQL 資料倉儲尚未支援 Visual Studio 資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="1dbf8-108">此功能將會加入未來的版本中。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="1dbf8-109">步驟 1：安裝 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1dbf8-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="1dbf8-110">請遵循這些連結 toodownload 及安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="1dbf8-111">如果您已安裝 Visual Studio 2013 或更新版本，您可以略過 tooStep 2，則安裝 SSDT。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="1dbf8-112">[下載 Visual Studio][]。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="1dbf8-113">請遵循 hello[安裝 Visual Studio] [ Installing Visual Studio]引導 MSDN 上，並選擇 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="1dbf8-114">步驟 2：安裝 SSDT</span><span class="sxs-lookup"><span data-stu-id="1dbf8-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="1dbf8-115">tooinstall SSDT for Visual Studio 只會檢查 SSDT 更新從 Visual Studio 中遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="1dbf8-116">在 Visual Studio 中，按一下 [工具] / [擴充功能和更新]</span><span class="sxs-lookup"><span data-stu-id="1dbf8-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="1dbf8-117"> / [更新]。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-117"> / **Updates**</span></span>
2. <span data-ttu-id="1dbf8-118">選取 [產品更新]，然後尋找 [適用於資料庫工具的 Microsoft SQL Server 更新]</span><span class="sxs-lookup"><span data-stu-id="1dbf8-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="1dbf8-119">如果找不到更新，您應該有 hello 安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="1dbf8-120">tooconfirm SSDT 安裝後，按一下**協助** / **關於 Microsoft Visual Studio** hello 清單中尋找 SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="1dbf8-121">hello 最新版本的 SSDT 是 14.0.60525.0。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="1dbf8-122">如果 hello 選項 tooinstall 不從 Visual Studio 中，或者您可以瀏覽 hello [SSDT 下載][ SSDT Download] toodownload 頁面上，並手動安裝 SSDT。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dbf8-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1dbf8-123">Next steps</span></span>
<span data-ttu-id="1dbf8-124">現在您有 hello 最新版本的 SSDT，您就可以準備太[連接][ connect] tooyour SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="1dbf8-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[下載 Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
