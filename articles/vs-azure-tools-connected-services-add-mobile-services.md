---
title: "使用 Visual Studio 中的 已連接服務 aaaAdding 行動服務 |Microsoft 文件"
description: "將行動服務使用 hello Visual Studio 加入已連接服務對話方塊"
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
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a><span data-ttu-id="eab58-103">使用 Visual Studio 已連接服務加入行動服務</span><span class="sxs-lookup"><span data-stu-id="eab58-103">Adding Mobile Services by using Visual Studio Connected Services</span></span>
<span data-ttu-id="eab58-104">您可以使用 Visual Studio 2015 中，連接 tooAzure 行動服務使用 hello**加入已連接服務**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eab58-104">With Visual Studio 2015, you can connect tooAzure Mobile Services using hello **Add Connected Service** dialog.</span></span> <span data-ttu-id="eab58-105">您可以從任何 C# 用戶端應用程式、任何 JavaScript 應用程式或跨平台 Cordova 應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="eab58-105">You can connect from any C# client app, any JavaScript app, or cross-platform Cordova app.</span></span> <span data-ttu-id="eab58-106">連接後，您可以建立和存取資料、建立自訂 API 和排程的工作，或加入推播通知的支援。</span><span class="sxs-lookup"><span data-stu-id="eab58-106">Once you connect, you can create and access data, create custom APIs and scheduled jobs, or add support for push notifications.</span></span>  <span data-ttu-id="eab58-107">hello 已連線的服務作業會將加入所有適當的參考和連線程式碼。</span><span class="sxs-lookup"><span data-stu-id="eab58-107">hello connected services operation adds all appropriate references and connection code.</span></span> <span data-ttu-id="eab58-108">您也可以利用包含各種熱門身分識別配置 (例如 Azure AD、Facebook、Twitter 和 Microsoft 帳戶) 的內建驗證支援。</span><span class="sxs-lookup"><span data-stu-id="eab58-108">You can also take advantage of built-in support for authentication with a variety of popular identity schemes, such as Azure AD, Facebook, Twitter, and Microsoft Accounts.</span></span>

## <a name="supported-project-types"></a><span data-ttu-id="eab58-109">支援的專案類型</span><span class="sxs-lookup"><span data-stu-id="eab58-109">Supported Project Types</span></span>
> [!NOTE]
> <span data-ttu-id="eab58-110">在 Visual Studio 2015 中，不支援使用 hello 加入已連接服務對話方塊以加入 Azure Mobile Services tooa 通用 Windows (Windows 10) 專案。</span><span class="sxs-lookup"><span data-stu-id="eab58-110">In Visual Studio 2015, adding Azure Mobile Services tooa Windows Universal (Windows 10) projects by using hello Add Connected Services dialog is not supported.</span></span> <span data-ttu-id="eab58-111">您可以藉由安裝 hello 適當封裝使用專案 hello NuGet 封裝管理員新增 Azure 行動服務。</span><span class="sxs-lookup"><span data-stu-id="eab58-111">You can add Azure Mobile Services by installing hello appropriate packages using hello NuGet Package Manager for your project.</span></span>
> 
> 

<span data-ttu-id="eab58-112">您可以使用 hello 已連接服務對話方塊 tooconnect tooAzure 行動服務中 hello 下列專案類型。</span><span class="sxs-lookup"><span data-stu-id="eab58-112">You can use hello Connected Services dialog tooconnect tooAzure Mobile Services in hello following project types.</span></span>

* <span data-ttu-id="eab58-113">.NET Windows 8.1 市集、電話和通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="eab58-113">.NET Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="eab58-114">JavaScript Windows 8.1 市集、電話和通用應用程式專案</span><span class="sxs-lookup"><span data-stu-id="eab58-114">JavaScript Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="eab58-115">使用 Visual Studio Tools for Apache Cordova 建立的專案</span><span class="sxs-lookup"><span data-stu-id="eab58-115">Projects created using Visual Studio Tools for Apache Cordova</span></span>

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a><span data-ttu-id="eab58-116">連接 tooAzure 行動服務使用 hello 加入已連接服務對話方塊</span><span class="sxs-lookup"><span data-stu-id="eab58-116">Connect tooAzure Mobile Services using hello Add Connected Services dialog</span></span>
1. <span data-ttu-id="eab58-117">確定您具有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eab58-117">Make sure you have an Azure account.</span></span> <span data-ttu-id="eab58-118">如果您沒有 Azure 帳戶，您可以註冊 [免費試用](http://go.microsoft.com/fwlink/?LinkId=518146)。</span><span class="sxs-lookup"><span data-stu-id="eab58-118">If you don't have an Azure account, you can sign up for a [free trial](http://go.microsoft.com/fwlink/?LinkId=518146).</span></span>
2. <span data-ttu-id="eab58-119">開啟 hello**加入已連接服務** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eab58-119">Open hello **Add Connected Services** dialog box.</span></span>
   
   * <span data-ttu-id="eab58-120">對於.NET 應用程式中，開啟您的專案在 Visual Studio 中開啟 hello 內容功能表上的 hello**參考**在 方案總管 節點，然後選擇 **加入已連接服務**</span><span class="sxs-lookup"><span data-stu-id="eab58-120">For .NET apps, open your project in Visual Studio, open hello context menu for hello **References** node in Solution Explorer, and then choose **Add Connected Service**</span></span>
     
        ![連接 tooAzure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * <span data-ttu-id="eab58-122">Apache Cordova 應用程式專案中，開啟您的專案在 Visual Studio 中，開啟 hello hello 專案節點，在 方案總管的操作功能表，然後選擇**加入已連接服務**。</span><span class="sxs-lookup"><span data-stu-id="eab58-122">For Apache Cordova app projects, open your project in Visual Studio, open hello context menu for hello project node in Solution Explorer, and then choose **Add Connected Service**.</span></span>
3. <span data-ttu-id="eab58-123">在 hello**加入已連接服務**對話方塊方塊中，選擇**Azure Mobile Services**，然後選擇 [hello**設定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eab58-123">In hello **Add Connected Service** dialog box, choose **Azure Mobile Services**, and then choose hello **Configure** button.</span></span> <span data-ttu-id="eab58-124">如果您還沒有，您可能會提示的 toolog 至 Azure。</span><span class="sxs-lookup"><span data-stu-id="eab58-124">You may be prompted toolog into Azure if you haven't already done so.</span></span>
   
    ![加入 Azure 行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. <span data-ttu-id="eab58-126">在 hello **Azure Mobile Services**對話方塊方塊中，選擇現有行動服務，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="eab58-126">In hello **Azure Mobile Services** dialog box, choose an existing mobile service if you have one.</span></span> <span data-ttu-id="eab58-127">如果您需要 toocreate 新的 Azure 行動服務，因此遵循下方 toodo hello 程序。</span><span class="sxs-lookup"><span data-stu-id="eab58-127">If you need toocreate a new Azure mobile service, follow hello procedure below toodo so.</span></span> <span data-ttu-id="eab58-128">否則，請略過 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="eab58-128">Otherwise, skip toohello next step.</span></span>
   
    <span data-ttu-id="eab58-129">toocreate 新的行動服務帳戶：</span><span class="sxs-lookup"><span data-stu-id="eab58-129">toocreate a new mobile service account:</span></span>
   
   1. <span data-ttu-id="eab58-130">選擇 hello * * 建立服務 * * 在 hello hello 對話方塊底部的連結。</span><span class="sxs-lookup"><span data-stu-id="eab58-130">choose hello **Create Service **link at hello bottom of hello dialog box.</span></span>
       <span data-ttu-id="eab58-131">![加入新的已連接行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span><span class="sxs-lookup"><span data-stu-id="eab58-131">![Add new mobile connected service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span></span>
   2. <span data-ttu-id="eab58-132">在 hello**建立行動服務**對話方塊中，您可以選擇 JavaScript 後端行動服務或.NET 後端行動服務從 hello**執行階段**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="eab58-132">On hello **Create Mobile Service** dialog box, you can choose a JavaScript backend mobile service, or a .NET backend mobile service from hello **Runtime** drop-down list.</span></span> 
      
       ![建立行動服務](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       <span data-ttu-id="eab58-134">JavaScript 後端服務不但簡單而且功能強大。</span><span class="sxs-lookup"><span data-stu-id="eab58-134">A JavaScript backend service is simple and powerful.</span></span> <span data-ttu-id="eab58-135">如果您建立 JavaScript 後端行動服務，hello 伺服器端 JavaScript 程式碼儲存在 hello 雲端，但您可以使用伺服器總管 中或 hello Azure 管理入口網站編輯伺服器指令碼。</span><span class="sxs-lookup"><span data-stu-id="eab58-135">If you create a JavaScript backend mobile service, hello server-side JavaScript code is stored in hello cloud, but you can edit server scripts by using Server Explorer, or hello Azure management portal.</span></span> 
      
       <span data-ttu-id="eab58-136">.NET 後端行動服務可讓您 hello 完整能力及 Web API 和 Entity Framework 的彈性。</span><span class="sxs-lookup"><span data-stu-id="eab58-136">A .NET backend mobile service gives you hello full power and flexibility of Web API and Entity Framework.</span></span> <span data-ttu-id="eab58-137">如果您建立.NET 後端行動服務時，會為您建立專案，且加入 tooyour 解決方案。</span><span class="sxs-lookup"><span data-stu-id="eab58-137">If you create a .NET backend mobile service, a project is created for you and added tooyour solution.</span></span> 
   3. <span data-ttu-id="eab58-138">選擇 hello**區域**您想 hello 行動服務中，並接著輸入 hello 伺服器使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="eab58-138">Choose hello **Region** where you want hello mobile service, and then enter a user name and password for hello server.</span></span>
   4. <span data-ttu-id="eab58-139">您輸入 hello 所需的所有資訊之後，請選擇 hello**建立**按鈕 toocreate hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="eab58-139">After you've entered all hello required information, choose hello **Create** button toocreate hello mobile service.</span></span>
   5. <span data-ttu-id="eab58-140">hello 新的行動服務應該會出現在 hello hello 服務清單**Azure Mobile Services**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eab58-140">hello new mobile service should appear in hello service list on hello **Azure Mobile Services** dialog box.</span></span> <span data-ttu-id="eab58-141">在 hello 清單中選擇 hello 新的行動服務，然後選擇 hello**新增**按鈕 tooadd hello 服務 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="eab58-141">Choose hello new mobile service in hello list and then choose hello **Add** button tooadd hello service tooyour project.</span></span>
5. <span data-ttu-id="eab58-142">檢閱 hello 快速入門頁面隨即出現，並了解如何修改您的專案。</span><span class="sxs-lookup"><span data-stu-id="eab58-142">Review hello getting started page that appears and find out how your project was modified.</span></span> <span data-ttu-id="eab58-143">每當您加入已連接服務時，您的瀏覽器就會出現 [開始使用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="eab58-143">A Getting Started page appears in your browser whenever you add a connected service.</span></span> <span data-ttu-id="eab58-144">您可以檢閱 hello 建議的後續步驟與程式碼範例，或切換 toohello 發生了什麼事頁面 toosee 哪些參考已加入 tooyour 專案，且已修改您的程式碼和組態檔的方式。</span><span class="sxs-lookup"><span data-stu-id="eab58-144">You can review hello suggested next steps and code examples, or switch toohello What Happened page toosee what references were added tooyour project, and how your code and configuration files were modified.</span></span>
6. <span data-ttu-id="eab58-145">使用 hello 程式碼範例做為指南，開始撰寫程式碼 tooaccess 您的行動服務 ！</span><span class="sxs-lookup"><span data-stu-id="eab58-145">Using hello code samples as a guide, start writing code tooaccess your mobile service!</span></span>

## <a name="how-your-project-is-modified"></a><span data-ttu-id="eab58-146">您的專案修改方式</span><span class="sxs-lookup"><span data-stu-id="eab58-146">How your project is modified</span></span>
<span data-ttu-id="eab58-147">Visual Studio 如何修改您的專案相依於 hello 專案類型。</span><span class="sxs-lookup"><span data-stu-id="eab58-147">How Visual Studio modifies your project depends on hello project type.</span></span> <span data-ttu-id="eab58-148">若為 C# 用戶端應用程式，請參閱 [發生什麼情形 – C# 專案](http://go.microsoft.com/fwlink/p/?LinkId=513119)。</span><span class="sxs-lookup"><span data-stu-id="eab58-148">For C# client apps, see [What happend – C# projects](http://go.microsoft.com/fwlink/p/?LinkId=513119).</span></span> <span data-ttu-id="eab58-149">若為 JavaScript 用戶端應用程式，請參閱 [發生什麼情形 – JavaScript 專案](http://go.microsoft.com/fwlink/p/?LinkId=513120)。</span><span class="sxs-lookup"><span data-stu-id="eab58-149">For JavaScript client apps, see [What happened – JavaScript projects](http://go.microsoft.com/fwlink/p/?LinkId=513120).</span></span> <span data-ttu-id="eab58-150">若為 Cordova 應用程式，請參閱 [發生什麼情形 – Cordova 專案](http://go.microsoft.com/fwlink/p/?LinkId=513116)。</span><span class="sxs-lookup"><span data-stu-id="eab58-150">For Cordova apps, see [What happend – Cordova projects](http://go.microsoft.com/fwlink/p/?LinkId=513116).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eab58-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eab58-151">Next steps</span></span>
<span data-ttu-id="eab58-152">提出問題並取得協助︰</span><span class="sxs-lookup"><span data-stu-id="eab58-152">Ask questions and get help:</span></span> 

* [<span data-ttu-id="eab58-153">MSDN 論壇：Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="eab58-153">MSDN Forum: Azure Mobile Services</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [<span data-ttu-id="eab58-154">Azure 行動服務在 hello Microsoft Azure 團隊部落格</span><span class="sxs-lookup"><span data-stu-id="eab58-154">Azure Mobile Services at hello Microsoft Azure Team Blog</span></span>](https://azure.microsoft.com/blog/topics/mobile/)
* [<span data-ttu-id="eab58-155">azure.microsoft.com 上的 Azure 行動服務</span><span class="sxs-lookup"><span data-stu-id="eab58-155">Azure Mobile Services at azure.microsoft.com</span></span>](https://azure.microsoft.com/services/mobile-services/)
* [<span data-ttu-id="eab58-156">azure.microsoft.com 上的 Azure 行動服務文件</span><span class="sxs-lookup"><span data-stu-id="eab58-156">Azure Mobile Services Documentation at azure.microsoft.com</span></span>](https://azure.microsoft.com/documentation/services/mobile-services/)

