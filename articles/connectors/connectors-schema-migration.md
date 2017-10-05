---
title: "如何將邏輯應用程式移轉至結構描述版本 2015-08-01-preview | Microsoft Docs"
description: "您可以輕鬆地將邏輯應用程式移轉至最新的結構描述版本。 請直接遵循下列步驟。"
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="ee37d-104">如何將邏輯應用程式移轉至結構描述版本 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="ee37d-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="ee37d-105">若要將現有的邏輯應用程式移至新的結構描述，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="ee37d-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="ee37d-106">在 Azure 入口網站中開啟邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ee37d-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="ee37d-107">按一下 [更新結構描述]︰</span><span class="sxs-lookup"><span data-stu-id="ee37d-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="ee37d-108">![API 圖示][step1] </span><span class="sxs-lookup"><span data-stu-id="ee37d-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="ee37d-109">[更新結構描述] 頁面便會出現，並提供會提供新結構描述增強功能詳細資訊之文件的連結︰![API 圖示][step2]</span><span class="sxs-lookup"><span data-stu-id="ee37d-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="ee37d-110">當您選取 [更新結構描述] 時，我們會自動執行移轉步驟，並為您提供程式碼輸出。</span><span class="sxs-lookup"><span data-stu-id="ee37d-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="ee37d-111">您可以使用此輸出更新您的定義，不過，請確定您有遵循良好的程式碼撰寫方式，例如下面的**最佳作法**一節中所說的方式。</span><span class="sxs-lookup"><span data-stu-id="ee37d-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="ee37d-112">將邏輯應用程式移轉至最新結構描述版本時的最佳作法︰</span><span class="sxs-lookup"><span data-stu-id="ee37d-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="ee37d-113">將已移轉的指令碼複製到新的邏輯應用程式 - 在完成測試並確認移轉的應用程式已如預期般運作後再覆寫舊的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee37d-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="ee37d-114">放入生產環境 **之前** 先測試邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ee37d-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="ee37d-115">移轉完成後，開始更新邏輯應用程式以盡可能使用 [Managed API](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="ee37d-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="ee37d-116">例如，您可以在使用 DropBox v1 的地方開始使用 Dropbox v2。</span><span class="sxs-lookup"><span data-stu-id="ee37d-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="ee37d-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee37d-117">What's next</span></span>
* [<span data-ttu-id="ee37d-118">了解如何手動移轉邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ee37d-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






