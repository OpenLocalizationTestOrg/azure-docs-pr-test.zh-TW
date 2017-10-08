---
title: "aaaGet.NET 入門 hello Azure CDN 文件庫 |Microsoft 文件"
description: "深入了解如何 toowrite.NET 應用程式 toomanage 使用 Visual Studio 的 Azure CDN。"
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
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>開始使用 Azure CDN 開發
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

您可以使用 hello[適用於.NET 的 Azure CDN 文件庫](https://msdn.microsoft.com/library/mt657769.aspx)tooautomate 建立及管理的 CDN 設定檔和端點。  這個教學課程引導 hello 建立簡單的.NET 主控台應用程式，示範數個 hello 可用的作業。  本教學課程中處於不應的 toodescribe hello Azure CDN 文件庫的所有層面.net 詳細資料。

需要 Visual Studio 2015 toocomplete 本教學課程。  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 可供免費下載。

> [!TIP]
> hello[從本教學課程已完成的專案](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c)MSDN 上的下載。
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>建立專案並新增 Nuget 封裝
既然我們已為我們的 CDN 設定檔建立資源群組，並提供我們的 Azure AD 應用程式的權限 toomanage CDN 設定檔與該群組中的端點，我們可以開始建立應用程式。

從 Visual Studio 2015 中，按一下**檔案**，**新增**，**專案...** tooopen hello 新增專案 對話方塊。  展開**Visual C#**，然後選取**Windows** hello hello 左側窗格中。  按一下**主控台應用程式**hello 中間窗格內。  為專案命名，然後按一下 [確定] 。  

![New Project](./media/cdn-app-dev-net/cdn-new-project.png)

受測專案即將的 toouse 有些 Azure 程式庫包含 Nuget 封裝中。  讓我們加入這些 toohello 專案。

1. 按一下 hello**工具**功能表上， **Nuget 套件管理員**，然後**Package Manager Console**。
   
    ![管理 Nuget 封裝](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. 在 hello Package Manager Console 中，執行下列命令 tooinstall hello hello **Active Directory 驗證程式庫 (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. 執行下列 tooinstall hello hello **Azure CDN 管理程式庫**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>指示詞、常數、主要方法和協助程式方法
讓我們協助我們撰寫的程式 hello 基本結構。

1. 在 [hello Program.cs] 索引標籤，取代 hello `using` hello 下列 hello 頂端的指示詞：
   
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
2. 我們需要 toodefine 我們方法會使用某些常數。  在 hello`Program`類別，但是在之前 hello`Main`方法，將 hello 面一行加入。  是確定 tooreplace hello 預留位置，包括 hello **&lt;角括號&gt;**，與您自己的值，視需要。
   
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
3. 也在 hello 類別層級，定義這兩個變數。  如果我們的設定檔和端點已經存在，我們會使用這些更新 toodetermine。
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. 取代 hello`Main`方法，如下所示：
   
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
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. 我們的其他方法的某些即將 tooprompt hello 使用者 」 是/否 」 問題。  新增下列方法 toomake hello，更加容易：
   
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

既然我們程式 hello 基本結構撰寫，我們應該建立 hello 方法呼叫 hello`Main`方法。

## <a name="authentication"></a>驗證
我們可以使用 hello Azure CDN 管理程式庫之前，我們需要 tooauthenticate 我們的服務主體，並取得驗證權杖。  這個方法會使用 ADAL tooretrieve hello 語彙基元。

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

如果您使用個別的使用者驗證，hello`GetAccessToken`方法看起來稍有不同。

> [!IMPORTANT]
> 如果您選擇 toohave 個別使用者驗證，而不是服務主體，只能使用此程式碼範例。
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

要確定 tooreplace `<redirect URI>` hello 與重新導向 Azure AD 中註冊 hello 應用程式時所輸入的 URI。

## <a name="list-cdn-profiles-and-endpoints"></a>列出 CDN 設定檔和端點
現在我們已經準備好 tooperform CDN 作業。  hello 我們方法會執行第一件事是清單所有 hello 設定檔和端點在資源群組中，而且如果它找到的相符項目中我們常數，指定 hello 設定檔和端點名稱會，記下稍後以便讓我們不試 toocreate 重複項目。

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>建立 CDN 設定檔和端點
接下來，我們將建立設定檔。

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

一旦建立 hello 設定檔之後，我們將建立端點。

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
> hello 上述範例中會指派給 hello 端點名為 origin *Contoso*與一個主機名稱`www.contoso.com`。  您應該變更這個 toopoint tooyour 自己來源的主機名稱。
> 
> 

## <a name="purge-an-endpoint"></a>清除端點
假設已建立 hello 端點，一項通用工作，我們可能會想 tooperform 在我們程式中已清除我們端點中的 hello 內容。

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
> Hello 上述範例中，在 hello 字串`/*`代表的是，我想 toopurge hello hello 端點路徑根目錄中的所有項目。  這是對等 toochecking**清除所有**hello 在 Azure 入口網站的 「 清除 」 對話方塊。 在 hello`CreateCdnProfile`我建立我們的設定檔的方法， **Verizon 從 Azure CDN**使用 hello 程式碼的設定檔`Sku = new Sku(SkuName.StandardVerizon)`，因此，這將會成功。  不過， **Akamai 從 Azure CDN**設定檔不支援**清除所有**，因此，如果我使用 Akamai 設定檔進行此教學課程中，我會需要 tooinclude 特定路徑 toopurge。
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>刪除 CDN 設定檔和端點
我們的端點和設定檔，將會刪除 hello 最後一個方法。

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

## <a name="running-hello-program"></a>執行 hello 程式
我們現在可以編譯並執行 hello 程式即可 hello**啟動**Visual Studio 中的按鈕。

![程式正在執行中](./media/cdn-app-dev-net/cdn-program-running-1.png)

當 hello 程式到達 hello 提示上方時，您也應該 hello Azure 入口網站中的可以 tooreturn tooyour 資源群組並查看已建立 hello 設定檔。

![成功！](./media/cdn-app-dev-net/cdn-success.png)

然後，我們可以確認 hello 提示 toorun hello 的其餘部分 hello 程式。

![正在完成程式](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>後續步驟
這個逐步解說中，從 toosee hello 完成專案[下載 hello 範例](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c)。

toofind 相關文件 hello Azure CDN Management Library for.NET，檢視 hello [MSDN 上的參考](https://msdn.microsoft.com/library/mt657769.aspx)。

使用 [PowerShell](cdn-manage-powershell.md)管理 CDN 資源。

