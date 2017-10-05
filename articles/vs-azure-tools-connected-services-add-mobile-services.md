---
title: "使用 Visual Studio 的已連接服務加入行動服務 | Microsoft Docs"
description: "使用 Visual Studio 的加入已連接服務對話方塊加入行動服務"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: d185fdafebad56f8970e390b2a0672c3fb84df8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a><span data-ttu-id="4bc40-103">使用 Visual Studio 已連接服務加入行動服務</span><span class="sxs-lookup"><span data-stu-id="4bc40-103">Adding Mobile Services by using Visual Studio Connected Services</span></span>
<span data-ttu-id="4bc40-104">透過 Visual Studio 2015，您可以使用 [ **加入已連接服務** ] 對話方塊連接到 Azure 行動服務。</span><span class="sxs-lookup"><span data-stu-id="4bc40-104">With Visual Studio 2015, you can connect to Azure Mobile Services using the **Add Connected Service** dialog.</span></span> <span data-ttu-id="4bc40-105">您可以從任何 C# 用戶端應用程式、任何 JavaScript 應用程式或跨平台 Cordova 應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="4bc40-105">You can connect from any C# client app, any JavaScript app, or cross-platform Cordova app.</span></span> <span data-ttu-id="4bc40-106">連接後，您可以建立和存取資料、建立自訂 API 和排程的工作，或加入推播通知的支援。</span><span class="sxs-lookup"><span data-stu-id="4bc40-106">Once you connect, you can create and access data, create custom APIs and scheduled jobs, or add support for push notifications.</span></span>  <span data-ttu-id="4bc40-107">已連接服務作業會加入所有適當的參考和連接程式碼。</span><span class="sxs-lookup"><span data-stu-id="4bc40-107">The connected services operation adds all appropriate references and connection code.</span></span> <span data-ttu-id="4bc40-108">您也可以利用包含各種熱門身分識別配置 (例如 Azure AD、Facebook、Twitter 和 Microsoft 帳戶) 的內建驗證支援。</span><span class="sxs-lookup"><span data-stu-id="4bc40-108">You can also take advantage of built-in support for authentication with a variety of popular identity schemes, such as Azure AD, Facebook, Twitter, and Microsoft Accounts.</span></span>

## <a name="supported-project-types"></a><span data-ttu-id="4bc40-109">支援的專案類型</span><span class="sxs-lookup"><span data-stu-id="4bc40-109">Supported Project Types</span></span>
> [!NOTE]
> <span data-ttu-id="4bc40-110">在 Visual Studio 2015 中，不支援使用 [加入已連接服務] 對話方塊將 Azure 行動服務加入至 Windows 通用 (Windows 10) 專案。</span><span class="sxs-lookup"><span data-stu-id="4bc40-110">In Visual Studio 2015, adding Azure Mobile Services to a Windows Universal (Windows 10) projects by using the Add Connected Services dialog is not supported.</span></span> <span data-ttu-id="4bc40-111">使用 NuGet 封裝管理員為您的專案安裝適當的封裝，即可加入 Azure 行動服務。</span><span class="sxs-lookup"><span data-stu-id="4bc40-111">You can add Azure Mobile Services by installing the appropriate packages using the NuGet Package Manager for your project.</span></span>
> 
> 

<span data-ttu-id="4bc40-112">您可以使用 [已連接服務] 對話方塊來連接到 Azure Mobile Services 中的下列專案類型。</span><span class="sxs-lookup"><span data-stu-id="4bc40-112">You can use the Connected Services dialog to connect to Azure Mobile Services in the following project types.</span></span>

* <span data-ttu-id="4bc40-113">.NET Windows 8.1 市集、電話和通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="4bc40-113">.NET Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="4bc40-114">JavaScript Windows 8.1 市集、電話和通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="4bc40-114">JavaScript Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="4bc40-115">使用 Visual Studio Tools for Apache Cordova 建立的專案</span><span class="sxs-lookup"><span data-stu-id="4bc40-115">Projects created using Visual Studio Tools for Apache Cordova</span></span>

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a><span data-ttu-id="4bc40-116">使用 [加入已連接服務] 對話方塊連接到 Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="4bc40-116">Connect to Azure Mobile Services using the Add Connected Services dialog</span></span>
1. <span data-ttu-id="4bc40-117">確定您具有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bc40-117">Make sure you have an Azure account.</span></span> <span data-ttu-id="4bc40-118">如果您沒有 Azure 帳戶，您可以註冊 [免費試用](http://go.microsoft.com/fwlink/?LinkId=518146)。</span><span class="sxs-lookup"><span data-stu-id="4bc40-118">If you don't have an Azure account, you can sign up for a [free trial](http://go.microsoft.com/fwlink/?LinkId=518146).</span></span>
2. <span data-ttu-id="4bc40-119">開啟 [加入已連接服務]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4bc40-119">Open the **Add Connected Services** dialog box.</span></span>
   
   * <span data-ttu-id="4bc40-120">若為 .NET 應用程式，請在 Visual Studio 中開啟您的專案，開啟 [方案總管] 中 [參考] 節點的內容功能表，然後選擇 [加入已連接服務]</span><span class="sxs-lookup"><span data-stu-id="4bc40-120">For .NET apps, open your project in Visual Studio, open the context menu for the **References** node in Solution Explorer, and then choose **Add Connected Service**</span></span>
     
        ![連線至 Azure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * <span data-ttu-id="4bc40-122">若為 Apache Cordova 應用程式專案，請在 Visual Studio 中開啟您的專案，開啟 [方案總管] 中專案節點的內容功能表，然後選擇 [加入已連接服務] 。</span><span class="sxs-lookup"><span data-stu-id="4bc40-122">For Apache Cordova app projects, open your project in Visual Studio, open the context menu for the project node in Solution Explorer, and then choose **Add Connected Service**.</span></span>
3. <span data-ttu-id="4bc40-123">在 [加入已連接服務] 對話方塊中，選擇 [Azure 行動服務]，然後選擇 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4bc40-123">In the **Add Connected Service** dialog box, choose **Azure Mobile Services**, and then choose the **Configure** button.</span></span> <span data-ttu-id="4bc40-124">如果您尚未登入 Azure，系統可能會提示您這麼做。</span><span class="sxs-lookup"><span data-stu-id="4bc40-124">You may be prompted to log into Azure if you haven't already done so.</span></span>
   
    ![加入 Azure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. <span data-ttu-id="4bc40-126">在 [Azure 行動服務]  對話方塊中，選擇現有的行動服務 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="4bc40-126">In the **Azure Mobile Services** dialog box, choose an existing mobile service if you have one.</span></span> <span data-ttu-id="4bc40-127">如果您需要建立新的 Azure 行動服務，請遵循下面的程序。</span><span class="sxs-lookup"><span data-stu-id="4bc40-127">If you need to create a new Azure mobile service, follow the procedure below to do so.</span></span> <span data-ttu-id="4bc40-128">否則請跳到下一步。</span><span class="sxs-lookup"><span data-stu-id="4bc40-128">Otherwise, skip to the next step.</span></span>
   
    <span data-ttu-id="4bc40-129">若要建立新的行動服務帳戶︰</span><span class="sxs-lookup"><span data-stu-id="4bc40-129">To create a new mobile service account:</span></span>
   
   1. <span data-ttu-id="4bc40-130">選擇 * * 建立服務 * * 在對話方塊底部的連結。</span><span class="sxs-lookup"><span data-stu-id="4bc40-130">choose the **Create Service **link at the bottom of the dialog box.</span></span>
       <span data-ttu-id="4bc40-131">![加入新的已連接行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span><span class="sxs-lookup"><span data-stu-id="4bc40-131">![Add new mobile connected service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span></span>
   2. <span data-ttu-id="4bc40-132">在 [建立行動服務] 對話方塊上，您可以選擇 JavaScript 後端行動服務，或選擇 [執行階段] 下拉式清單中的 .NET 後端行動服務。</span><span class="sxs-lookup"><span data-stu-id="4bc40-132">On the **Create Mobile Service** dialog box, you can choose a JavaScript backend mobile service, or a .NET backend mobile service from the **Runtime** drop-down list.</span></span> 
      
       ![建立行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       <span data-ttu-id="4bc40-134">JavaScript 後端服務不但簡單而且功能強大。</span><span class="sxs-lookup"><span data-stu-id="4bc40-134">A JavaScript backend service is simple and powerful.</span></span> <span data-ttu-id="4bc40-135">如果您建立 JavaScript 後端行動服務，伺服器端 JavaScript 程式碼會儲存在雲端中，但您可以使用 [伺服器總管] 或 Azure 管理入口網站來編輯伺服器指令碼。</span><span class="sxs-lookup"><span data-stu-id="4bc40-135">If you create a JavaScript backend mobile service, the server-side JavaScript code is stored in the cloud, but you can edit server scripts by using Server Explorer, or the Azure management portal.</span></span> 
      
       <span data-ttu-id="4bc40-136">.NET 後端行動服務讓您擁有 Web API 和 Entity Framework 的完整功能與彈性。</span><span class="sxs-lookup"><span data-stu-id="4bc40-136">A .NET backend mobile service gives you the full power and flexibility of Web API and Entity Framework.</span></span> <span data-ttu-id="4bc40-137">如果您建立 .NET 後端行動服務，則系統會為您建立專案並加入至您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4bc40-137">If you create a .NET backend mobile service, a project is created for you and added to your solution.</span></span> 
   3. <span data-ttu-id="4bc40-138">選擇您想要行動服務的 [區域]  ，然後輸入伺服器的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4bc40-138">Choose the **Region** where you want the mobile service, and then enter a user name and password for the server.</span></span>
   4. <span data-ttu-id="4bc40-139">在您輸入所有必要的資訊之後，選擇 [建立]  按鈕以建立行動服務。</span><span class="sxs-lookup"><span data-stu-id="4bc40-139">After you've entered all the required information, choose the **Create** button to create the mobile service.</span></span>
   5. <span data-ttu-id="4bc40-140">新行動服務應該會顯示在 [Azure 行動服務]  對話方塊的服務清單中。</span><span class="sxs-lookup"><span data-stu-id="4bc40-140">The new mobile service should appear in the service list on the **Azure Mobile Services** dialog box.</span></span> <span data-ttu-id="4bc40-141">選擇清單中的新行動服務，然後選擇 [新增]  按鈕將服務加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="4bc40-141">Choose the new mobile service in the list and then choose the **Add** button to add the service to your project.</span></span>
5. <span data-ttu-id="4bc40-142">檢閱所顯示的 [開始使用] 頁面並了解您的專案修改方式。</span><span class="sxs-lookup"><span data-stu-id="4bc40-142">Review the getting started page that appears and find out how your project was modified.</span></span> <span data-ttu-id="4bc40-143">每當您加入已連接服務時，您的瀏覽器就會出現 [開始使用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4bc40-143">A Getting Started page appears in your browser whenever you add a connected service.</span></span> <span data-ttu-id="4bc40-144">您可以檢閱建議的後續步驟和程式碼範例，或切換到 [發生什麼情形] 頁面以查看哪些參考已加入至您的專案，以及您的程式碼和組態檔的修改方式。</span><span class="sxs-lookup"><span data-stu-id="4bc40-144">You can review the suggested next steps and code examples, or switch to the What Happened page to see what references were added to your project, and how your code and configuration files were modified.</span></span>
6. <span data-ttu-id="4bc40-145">使用程式碼範例做為指南，開始撰寫程式碼以存取您的行動服務！</span><span class="sxs-lookup"><span data-stu-id="4bc40-145">Using the code samples as a guide, start writing code to access your mobile service!</span></span>

## <a name="how-your-project-is-modified"></a><span data-ttu-id="4bc40-146">您的專案修改方式</span><span class="sxs-lookup"><span data-stu-id="4bc40-146">How your project is modified</span></span>
<span data-ttu-id="4bc40-147">Visual Studio 修改您的專案的方式視專案類型而定。</span><span class="sxs-lookup"><span data-stu-id="4bc40-147">How Visual Studio modifies your project depends on the project type.</span></span> <span data-ttu-id="4bc40-148">若為 C# 用戶端應用程式，請參閱 [發生什麼情形 – C# 專案](http://go.microsoft.com/fwlink/p/?LinkId=513119)。</span><span class="sxs-lookup"><span data-stu-id="4bc40-148">For C# client apps, see [What happend – C# projects](http://go.microsoft.com/fwlink/p/?LinkId=513119).</span></span> <span data-ttu-id="4bc40-149">若為 JavaScript 用戶端應用程式，請參閱 [發生什麼情形 – JavaScript 專案](http://go.microsoft.com/fwlink/p/?LinkId=513120)。</span><span class="sxs-lookup"><span data-stu-id="4bc40-149">For JavaScript client apps, see [What happened – JavaScript projects](http://go.microsoft.com/fwlink/p/?LinkId=513120).</span></span> <span data-ttu-id="4bc40-150">若為 Cordova 應用程式，請參閱 [發生什麼情形 – Cordova 專案](http://go.microsoft.com/fwlink/p/?LinkId=513116)。</span><span class="sxs-lookup"><span data-stu-id="4bc40-150">For Cordova apps, see [What happend – Cordova projects](http://go.microsoft.com/fwlink/p/?LinkId=513116).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bc40-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bc40-151">Next steps</span></span>
<span data-ttu-id="4bc40-152">提出問題並取得協助︰</span><span class="sxs-lookup"><span data-stu-id="4bc40-152">Ask questions and get help:</span></span> 

* [<span data-ttu-id="4bc40-153">MSDN 論壇：Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="4bc40-153">MSDN Forum: Azure Mobile Services</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [<span data-ttu-id="4bc40-154">Microsoft Azure 團隊部落格上的 Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="4bc40-154">Azure Mobile Services at the Microsoft Azure Team Blog</span></span>](https://azure.microsoft.com/blog/topics/mobile/)
* [<span data-ttu-id="4bc40-155">azure.microsoft.com 上的 Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="4bc40-155">Azure Mobile Services at azure.microsoft.com</span></span>](https://azure.microsoft.com/services/mobile-services/)
* [<span data-ttu-id="4bc40-156">azure.microsoft.com 上的 Azure 行動服務文件</span><span class="sxs-lookup"><span data-stu-id="4bc40-156">Azure Mobile Services Documentation at azure.microsoft.com</span></span>](https://azure.microsoft.com/documentation/services/mobile-services/)

