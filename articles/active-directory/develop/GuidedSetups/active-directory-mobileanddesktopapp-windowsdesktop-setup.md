---
title: "Azure AD v2 Windows Desktop 快速入門 - 設定 | Microsoft Docs"
description: "Windows Desktop .NET (XAML) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="47242-103">設定專案</span><span class="sxs-lookup"><span data-stu-id="47242-103">Set up your project</span></span>

<span data-ttu-id="47242-104">本節提供逐步指示，說明如何建立新的專案來示範整合 Windows Desktop .NET 應用程式 (XAML) 與*使用 Microsoft 登入*，以便它可以查詢需要權杖的 Web API。</span><span class="sxs-lookup"><span data-stu-id="47242-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="47242-105">本指南建立的應用程式會顯示一個圖表按鈕，並在畫面上顯示結果和一個登出按鈕。</span><span class="sxs-lookup"><span data-stu-id="47242-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="47242-106">想要改為下載此範例的 Visual Studio 專案嗎？</span><span class="sxs-lookup"><span data-stu-id="47242-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="47242-107">[下載專案](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip)並跳至[設定步驟](#create-an-application-express)，以在執行之前先設定程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="47242-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="47242-108">建立您的應用程式</span><span class="sxs-lookup"><span data-stu-id="47242-108">Create your application</span></span>
1. <span data-ttu-id="47242-109">在 Visual Studio 中：`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="47242-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="47242-110">在 [範本] 底下，選取 `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="47242-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="47242-111">選取 `WPF App` (或選取 [WPF 應用程式]，需視您的 Visual Studio 版本而定)</span><span class="sxs-lookup"><span data-stu-id="47242-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="47242-112">將 Microsoft Authentication Library (MSAL) 新增至您的專案</span><span class="sxs-lookup"><span data-stu-id="47242-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="47242-113">在 Visual Studio 中：`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="47242-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="47242-114">在 [套件管理器主控台] 視窗中，複製/貼上下列內容：</span><span class="sxs-lookup"><span data-stu-id="47242-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="47242-115">上面的套件會安裝 Microsoft Authentication Library (MSAL)。</span><span class="sxs-lookup"><span data-stu-id="47242-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="47242-116">MSAL 會處理使用者權杖的取得、快取及重新整理作業，這些權杖是用來存取受 Azure Active Directory v2 保護的 API。</span><span class="sxs-lookup"><span data-stu-id="47242-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="47242-117">新增程式碼以初始化 MSAL</span><span class="sxs-lookup"><span data-stu-id="47242-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="47242-118">這個步驟將能協助您建立類別來處理和 MSAL 程式庫的互動，例如處理權杖。</span><span class="sxs-lookup"><span data-stu-id="47242-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="47242-119">開啟 `App.xaml.cs` 檔案，然後將 MSAL 程式庫參考新增到類別：</span><span class="sxs-lookup"><span data-stu-id="47242-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="47242-120">將應用程式類別更新至下面這樣：</span><span class="sxs-lookup"><span data-stu-id="47242-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="47242-121">建立您應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="47242-121">Create your application’s UI</span></span>
<span data-ttu-id="47242-122">下面的小節會說明應用程式如何查詢受保護的後端伺服器 (例如 Microsoft Graph)。</span><span class="sxs-lookup"><span data-stu-id="47242-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="47242-123">系統應會自動建立 MainWindow.xaml 檔案，作為專案範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="47242-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="47242-124">請開啟這個檔案，然後依照下面的指示操作：</span><span class="sxs-lookup"><span data-stu-id="47242-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="47242-125">用以下內容取代您應用程式的 `<Grid>`：</span><span class="sxs-lookup"><span data-stu-id="47242-125">Replace your application’s `<Grid>` with be the following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
