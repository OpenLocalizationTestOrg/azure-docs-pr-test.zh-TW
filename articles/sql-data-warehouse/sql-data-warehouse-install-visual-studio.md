---
title: "安裝適用於 SQL 資料倉儲的 Visual Studio 和 SSDT | Microsoft Docs"
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
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="58a82-103">安裝適用於 SQL 資料倉儲的 Visual Studio 和 SSDT</span><span class="sxs-lookup"><span data-stu-id="58a82-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="58a82-104">若要開發 SQL 資料倉儲的應用程式，建議使用最新版本的 Visual Studio，搭配最新版本的 SQL Server Data Tools (SSDT)。</span><span class="sxs-lookup"><span data-stu-id="58a82-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="58a82-105">Visual Studio 2013 Update 5 搭配 SSDT 也支援回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="58a82-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="58a82-106">搭配使用 Visual Studio 和 SSDT 可讓您使用 SQL Server 物件總管，經由視覺化方式瀏覽資料表、檢視、預存程序和 SQL 資料倉儲中的其他許多物件，以及執行查詢。</span><span class="sxs-lookup"><span data-stu-id="58a82-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="58a82-107">SQL 資料倉儲尚未支援 Visual Studio 資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="58a82-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="58a82-108">此功能將會加入未來的版本中。</span><span class="sxs-lookup"><span data-stu-id="58a82-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="58a82-109">步驟 1：安裝 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58a82-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="58a82-110">遵循下列連結來下載並安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="58a82-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="58a82-111">如果已安裝 Visual Studio 2013 或更新版本，可以跳至步驟 2 安裝 SSDT。</span><span class="sxs-lookup"><span data-stu-id="58a82-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="58a82-112">[下載 Visual Studio][]。</span><span class="sxs-lookup"><span data-stu-id="58a82-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="58a82-113">依照 MSDN 上的[安裝 Visual Studio][Installing Visual Studio] 指南並選擇預設組態。</span><span class="sxs-lookup"><span data-stu-id="58a82-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="58a82-114">步驟 2：安裝 SSDT</span><span class="sxs-lookup"><span data-stu-id="58a82-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="58a82-115">若要安裝適用於 Visual Studio 的 SSDT，只需依照下列步驟，從 Visual Studio 檢查 SSDT 更新。</span><span class="sxs-lookup"><span data-stu-id="58a82-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="58a82-116">在 Visual Studio 中，按一下 [工具] / [擴充功能和更新]</span><span class="sxs-lookup"><span data-stu-id="58a82-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="58a82-117"> / [更新]。</span><span class="sxs-lookup"><span data-stu-id="58a82-117"> / **Updates**</span></span>
2. <span data-ttu-id="58a82-118">選取 [產品更新]，然後尋找 [適用於資料庫工具的 Microsoft SQL Server 更新]</span><span class="sxs-lookup"><span data-stu-id="58a82-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="58a82-119">如果找不到更新，表示您應該已安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="58a82-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="58a82-120">若要確認已安裝 SSDT，請按一下 [說明] / [關於 Microsoft Visual Studio]，然後在清單中尋找 SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="58a82-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="58a82-121">SSDT 的最新版本是 14.0.60525.0。</span><span class="sxs-lookup"><span data-stu-id="58a82-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="58a82-122">如果無法在 Visual Studio 中使用安裝選項，或者您也可以瀏覽 [SSDT 下載][SSDT Download]頁面，手動下載和安裝 SSDT。</span><span class="sxs-lookup"><span data-stu-id="58a82-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58a82-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58a82-123">Next steps</span></span>
<span data-ttu-id="58a82-124">既然有了最新版本的 SSDT，您可以開始 [連接][connect]到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="58a82-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="58a82-125">[下載 Visual Studio]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="58a82-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
