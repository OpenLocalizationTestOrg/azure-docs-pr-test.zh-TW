---
title: "hello for Java 的 Azure 程式庫封裝 aaaDisplaying 在 Eclipse 中的 Javadoc 內容"
description: "如何 toodisplay hello Javadoc 內容在 Eclipse 中的 hello Azure 程式庫。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="639d6-103">在 Eclipse 中顯示 Javadoc 內容 hello for Java 的 Azure 程式庫封裝</span><span class="sxs-lookup"><span data-stu-id="639d6-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="639d6-104">hello hello Azure Libraries for Java 的 Javadoc 內容可以透過建立 hello Javadoc 內容 toohello Azure Libraries for Java 的關聯檢視 Eclipse 環境中。</span><span class="sxs-lookup"><span data-stu-id="639d6-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="639d6-105">hello 下列步驟說明如何 toouse 這項功能在 Eclipse 內。</span><span class="sxs-lookup"><span data-stu-id="639d6-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="639d6-106">此程序假設您已經加入 hello Azure Library for Java tooyour 組建路徑。</span><span class="sxs-lookup"><span data-stu-id="639d6-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="639d6-107">toodisplay 在 Eclipse 中的 hello Azure Libraries for Java 的 Javadoc 內容</span><span class="sxs-lookup"><span data-stu-id="639d6-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="639d6-108">在 Eclipse 的專案總管中，在 hello**參考程式庫**專案的區段中，開啟 hello hello Azure Library for Java JAR 的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="639d6-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="639d6-109">例如， **microsoft windowsazure api-0.1.0.jar** （hello 版本號碼可能會不同，取決於您已安裝哪些版本）。</span><span class="sxs-lookup"><span data-stu-id="639d6-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="639d6-110">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="639d6-110">Click **Properties**.</span></span>

* <span data-ttu-id="639d6-111">在 hello**屬性**對話方塊中的，hello 左窗格中，按一下**Javadoc 位置**。</span><span class="sxs-lookup"><span data-stu-id="639d6-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="639d6-112">hello **Javadoc 位置** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="639d6-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="639d6-113">您可以指定 [Javadoc URL]或 [封存檔案中的 Javadoc]。</span><span class="sxs-lookup"><span data-stu-id="639d6-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="639d6-114">如果您選擇 toospecify **Javadoc URL**，例如使用 hello Url **http://dl.windowsazure.com/javadoc**或**http://dl.windowsazure.com/storage/javadoc**。</span><span class="sxs-lookup"><span data-stu-id="639d6-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="639d6-115">如果您選擇 toouse**封存中的 Javadoc**，您可以指定外部檔案或工作區檔案。</span><span class="sxs-lookup"><span data-stu-id="639d6-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="639d6-116">選擇後視需要進行瀏覽/驗證。</span><span class="sxs-lookup"><span data-stu-id="639d6-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="639d6-117">hello 下列範例將 hello Azure Libraries for Java 與 hello 對應 Javadoc JAR 已下載至本機資料夾 tooa **c:\MyAzureJARs**。</span><span class="sxs-lookup"><span data-stu-id="639d6-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="639d6-118">選擇性步驟：按一下 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="639d6-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="639d6-119">無法在此顯示以 hello Javadoc JAR 的潛在問題。</span><span class="sxs-lookup"><span data-stu-id="639d6-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="639d6-120">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="639d6-120">Click **OK**.</span></span>

<span data-ttu-id="639d6-121">一旦與 hello 程式庫相關聯，hello Javadoc 內容應該會顯示在您的 Eclipse IDE。</span><span class="sxs-lookup"><span data-stu-id="639d6-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="639d6-122">例如，如果`blob`定義的型別`CloudBlockBlob`您的程式碼內 hello 以下是您輸入時，會出現的 Javadoc 內容範例`blob.acquireLease`程式碼中：</span><span class="sxs-lookup"><span data-stu-id="639d6-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="639d6-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="639d6-123">See Also</span></span>
<span data-ttu-id="639d6-124">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="639d6-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="639d6-125">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="639d6-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="639d6-126">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="639d6-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="639d6-127">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="639d6-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
