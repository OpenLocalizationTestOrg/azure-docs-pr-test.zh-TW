---
title: "aaaHow toomigrate 邏輯應用程式 tooschema 版本 2015年-08-01-預覽 |Microsoft 文件"
description: "您可以輕鬆地移轉您的邏輯應用程式 toohello 最新結構描述版本。 請直接遵循下列步驟。"
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
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="4f937-104">如何 toomigrate 邏輯應用程式 tooschema 版本 2015年-08-01-預覽</span><span class="sxs-lookup"><span data-stu-id="4f937-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="4f937-105">toomove 現有邏輯應用程式 toohello 新結構描述中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4f937-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="4f937-106">在 hello Azure 入口網站中開啟邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="4f937-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="4f937-107">按一下 [更新結構描述]︰</span><span class="sxs-lookup"><span data-stu-id="4f937-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="4f937-108">![API 圖示][step1] </span><span class="sxs-lookup"><span data-stu-id="4f937-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="4f937-109">hello 更新結構描述 頁面會顯示，並提供連結 tooa 文件，提供 hello hello 新結構描述中的增強功能的詳細資料： ![API 圖示][step2]</span><span class="sxs-lookup"><span data-stu-id="4f937-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="4f937-110">當您選取**更新結構描述**，我們會自動執行 hello 移轉步驟，並為您提供 hello 程式碼輸出。</span><span class="sxs-lookup"><span data-stu-id="4f937-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="4f937-111">您可以使用這個 tooupdate 您定義中，不過，請確定您遵循的良好的編碼方式，例如述 hello**最佳做法**下一節。</span><span class="sxs-lookup"><span data-stu-id="4f937-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="4f937-112">移轉您的邏輯應用程式 toohello 最新結構描述的版本時的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="4f937-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="4f937-113">複製 hello 移轉指令碼 tooa 新邏輯應用程式-不會覆寫的 hello 舊的其中一個您完成移轉的應用程式的測試和確認的 hello 如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="4f937-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="4f937-114">放入生產環境 **之前** 先測試邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="4f937-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="4f937-115">移轉完成後，啟動 更新您的邏輯應用程式 toouse hello [managed Api](apis-list.md)盡可能。</span><span class="sxs-lookup"><span data-stu-id="4f937-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="4f937-116">例如，您可以在使用 DropBox v1 的地方開始使用 Dropbox v2。</span><span class="sxs-lookup"><span data-stu-id="4f937-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="4f937-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f937-117">What's next</span></span>
* [<span data-ttu-id="4f937-118">了解 toomanually 要如何移轉您的 Logic apps</span><span class="sxs-lookup"><span data-stu-id="4f937-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






