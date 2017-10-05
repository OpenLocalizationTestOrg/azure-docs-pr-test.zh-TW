---
title: "開始使用適用於 .NET 的 Azure CDN 程式庫 | Microsoft Docs"
description: "了解如何使用 Visual Studio，撰寫 .NET 應用程式來管理 Azure CDN。"
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="facdc-103">開始使用 Azure CDN 開發</span><span class="sxs-lookup"><span data-stu-id="facdc-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="facdc-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="facdc-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="facdc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="facdc-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="facdc-106">您可以使用 [適用於 .NET 的 Azure CDN 程式庫](https://msdn.microsoft.com/library/mt657769.aspx) ，自動建立和管理 CDN 設定檔與端點。</span><span class="sxs-lookup"><span data-stu-id="facdc-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="facdc-107">本教學課程會逐步建立簡單的 .NET 主控台應用程式，示範數個可用的作業。</span><span class="sxs-lookup"><span data-stu-id="facdc-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="facdc-108">本教學課程的目的不是詳細說明適用於 .NET 的 Azure CDN 程式庫的所有層面。</span><span class="sxs-lookup"><span data-stu-id="facdc-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="facdc-109">您需要 Visual Studio 2015，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="facdc-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="facdc-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 可供免費下載。</span><span class="sxs-lookup"><span data-stu-id="facdc-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="facdc-111">您可以在 MSDN 上下載 [本教學課程中完成的專案](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) 。</span><span class="sxs-lookup"><span data-stu-id="facdc-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="facdc-112">建立專案並新增 Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="facdc-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="facdc-113">現在，我們已為 CDN 設定檔建立資源群組，並為 Azure AD 應用程式授與權限來管理該群組內的 CDN 設定檔和端點，我們可以開始建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="facdc-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="facdc-114">從 Visual Studio 2015 中，依序按一下 [檔案]、[新增] 和 [專案...]，以開啟 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="facdc-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="facdc-115">展開 [Visual C#]，然後選取左側窗格中的 [Windows]。</span><span class="sxs-lookup"><span data-stu-id="facdc-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="facdc-116">按一下中央窗格的 [主控台應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="facdc-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="facdc-117">為專案命名，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="facdc-117">Name your project, then click **OK**.</span></span>  

![New Project](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="facdc-119">我們的專案將使用 Nuget 封裝內含的一些 Azure 程式庫。</span><span class="sxs-lookup"><span data-stu-id="facdc-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="facdc-120">讓我們先將它們新增至專案。</span><span class="sxs-lookup"><span data-stu-id="facdc-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="facdc-121">依序按一下 [工具] 功能表、[Nuget 封裝管理員] 及 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="facdc-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![管理 Nuget 封裝](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="facdc-123">在 [封裝管理員主控台] 中，執行下列命令來安裝 **Active Directory Authentication Library (ADAL)**：</span><span class="sxs-lookup"><span data-stu-id="facdc-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="facdc-124">執行下列命令來安裝 **Azure CDN 管理程式庫**：</span><span class="sxs-lookup"><span data-stu-id="facdc-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="facdc-125">指示詞、常數、主要方法和協助程式方法</span><span class="sxs-lookup"><span data-stu-id="facdc-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="facdc-126">讓我們開始撰寫程式的基本結構。</span><span class="sxs-lookup"><span data-stu-id="facdc-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="facdc-127">回到 [Program.cs] 索引標籤，使用下列內容取代頂端的 `using` 指示詞：</span><span class="sxs-lookup"><span data-stu-id="facdc-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. <span data-ttu-id="facdc-128">我們必須定義一些我們的方法將用到的常數。</span><span class="sxs-lookup"><span data-stu-id="facdc-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="facdc-129">在 `Program` 類別中，但在 `Main` 方法之前，新增下列內容。</span><span class="sxs-lookup"><span data-stu-id="facdc-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="facdc-130">務必視需要使用您自己的值來取代預留位置，包括 **&lt;角括號&gt;**。</span><span class="sxs-lookup"><span data-stu-id="facdc-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="facdc-131">此外，也要在類別層級設定這兩個變數。</span><span class="sxs-lookup"><span data-stu-id="facdc-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="facdc-132">稍後將使用這些項目來判斷我們的設定檔和端點是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="facdc-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="facdc-133">取代 `Main` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="facdc-133">Replace the `Main` method as follows:</span></span>
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="facdc-134">在我們的其他方法中有一些會透過「是/否」問題來提示使用者。</span><span class="sxs-lookup"><span data-stu-id="facdc-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="facdc-135">新增下列方法，以使其更加容易：</span><span class="sxs-lookup"><span data-stu-id="facdc-135">Add the following method to make that a little easier:</span></span>
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

<span data-ttu-id="facdc-136">現在已撰寫了程式的基本結構，我們應該建立 `Main` 方法所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="facdc-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="facdc-137">驗證</span><span class="sxs-lookup"><span data-stu-id="facdc-137">Authentication</span></span>
<span data-ttu-id="facdc-138">在可以使用 Azure CDN 管理庫之前，需要先驗證服務主體，並取得驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="facdc-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="facdc-139">這個方法會使用 ADAL 來擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="facdc-139">This method uses ADAL to retrieve the token.</span></span>

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

<span data-ttu-id="facdc-140">如果您使用個別使用者驗證， `GetAccessToken` 方法看起來就會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="facdc-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="facdc-141">如果您選擇使用個別使用者驗證，而不是服務主體，只需使用這個程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="facdc-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

<span data-ttu-id="facdc-142">務必使用您在 Azure AD 中註冊應用程式時所輸入的重新導向 URI 來取代 `<redirect URI>` 。</span><span class="sxs-lookup"><span data-stu-id="facdc-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="facdc-143">列出 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="facdc-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="facdc-144">現在我們已經準備好執行 CDN 作業。</span><span class="sxs-lookup"><span data-stu-id="facdc-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="facdc-145">方法的首要任務就是列出資源群組中的所有設定檔和端點，而且如果找到與常數中指定的設定檔和端點名稱相符的項目，請記下該項目以供後續使用，如此一來我們就不用嘗試建立重複的項目。</span><span class="sxs-lookup"><span data-stu-id="facdc-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="facdc-146">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="facdc-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="facdc-147">接下來，我們將建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="facdc-147">Next, we'll create a profile.</span></span>

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

<span data-ttu-id="facdc-148">建立設定檔之後，我們將建立端點。</span><span class="sxs-lookup"><span data-stu-id="facdc-148">Once the profile is created, we'll create an endpoint.</span></span>

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> <span data-ttu-id="facdc-149">上述範例會為端點指派一個名為*Contoso* 的來源且主機名稱為 `www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="facdc-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="facdc-150">您應該變更此項以指向您自己來源的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="facdc-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="facdc-151">清除端點</span><span class="sxs-lookup"><span data-stu-id="facdc-151">Purge an endpoint</span></span>
<span data-ttu-id="facdc-152">假設端點已建立，我們可能想要在程式中執行的一個常見工作是清除此端點中的內容。</span><span class="sxs-lookup"><span data-stu-id="facdc-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> <span data-ttu-id="facdc-153">在上述範例中，字串 `/*` 代表我想要清除端點路徑根目錄中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="facdc-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="facdc-154">這相當於在 Azure 入口網站的 [清除] 對話方塊中勾選 [全部清除]。</span><span class="sxs-lookup"><span data-stu-id="facdc-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="facdc-155">在 `CreateCdnProfile` 方法中，我已經使用程式碼 `Sku = new Sku(SkuName.StandardVerizon)` 來建立設定檔做為**來自 Verizon 的 Azure CDN** 設定檔，因此這將會成功。</span><span class="sxs-lookup"><span data-stu-id="facdc-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="facdc-156">不過，**來自 Akamai 的 Azure CDN** 設定檔不支援 [全部清除]，因此，如果我在本教學課程中使用 Akamai 設定檔，就必須包含要清除的特定路徑。</span><span class="sxs-lookup"><span data-stu-id="facdc-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="facdc-157">刪除 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="facdc-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="facdc-158">最後一個方法會刪除我們的端點和設定檔。</span><span class="sxs-lookup"><span data-stu-id="facdc-158">The last methods will delete our endpoint and profile.</span></span>

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="facdc-159">執行程式</span><span class="sxs-lookup"><span data-stu-id="facdc-159">Running the program</span></span>
<span data-ttu-id="facdc-160">我們現在可以按一下 Visual Studio 中的 [開始]  按鈕來編譯及執行程式。</span><span class="sxs-lookup"><span data-stu-id="facdc-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![程式正在執行中](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="facdc-162">當程式達到上述提示時，您應該能夠回到您在 Azure 入口網站中的資源群組，並看見設定檔已建立。</span><span class="sxs-lookup"><span data-stu-id="facdc-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![成功！](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="facdc-164">接著，可確認提示來執行程式的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="facdc-164">We can then confirm the prompts to run the rest of the program.</span></span>

![正在完成程式](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="facdc-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="facdc-166">Next Steps</span></span>
<span data-ttu-id="facdc-167">若要查看此逐步解說中已完成的專案，請 [下載範例](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c)。</span><span class="sxs-lookup"><span data-stu-id="facdc-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="facdc-168">若要尋找適用於 .NET 的 Azure CDN 管理程式庫的其他相關文件，請檢視 [MSDN 上的參考](https://msdn.microsoft.com/library/mt657769.aspx)。</span><span class="sxs-lookup"><span data-stu-id="facdc-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="facdc-169">使用 [PowerShell](cdn-manage-powershell.md)管理 CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="facdc-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

