---
title: "aaaAzure AD v2 Windows 桌面快速入門-安裝 |Microsoft 文件"
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
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="a44e0-103">設定專案</span><span class="sxs-lookup"><span data-stu-id="a44e0-103">Set up your project</span></span>

<span data-ttu-id="a44e0-104">本節提供有關如何逐步解說 toocreate 新的專案 toodemonstrate 如何 toointegrate Windows 桌面.NET 應用程式 (XAML) 與*使用 Microsoft 登入*，它才能查詢需要權杖的 Web Api。</span><span class="sxs-lookup"><span data-stu-id="a44e0-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="a44e0-105">本指南所建立的 hello 應用程式公開螢幕和登出按鈕上的按鈕 toograph 並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="a44e0-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="a44e0-106">改為偏好 toodownload 這個範例的 Visual Studio 專案嗎？</span><span class="sxs-lookup"><span data-stu-id="a44e0-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="a44e0-107">[下載專案](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。</span><span class="sxs-lookup"><span data-stu-id="a44e0-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="a44e0-108">建立您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a44e0-108">Create your application</span></span>
1. <span data-ttu-id="a44e0-109">在 Visual Studio 中：`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="a44e0-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="a44e0-110">在 [範本] 底下，選取 `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="a44e0-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="a44e0-111">選取`WPF App`(或*WPF 應用程式*視您的 Visual Studio 的 hello 版本而定)</span><span class="sxs-lookup"><span data-stu-id="a44e0-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="a44e0-112">加入 hello Microsoft 驗證程式庫 (MSAL) tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="a44e0-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="a44e0-113">在 Visual Studio 中：`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="a44e0-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="a44e0-114">複製/貼上下列 hello hello 封裝管理員主控台 視窗中：</span><span class="sxs-lookup"><span data-stu-id="a44e0-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="a44e0-115">上述的 hello 套件會安裝 hello Microsoft 驗證程式庫 (MSAL)。</span><span class="sxs-lookup"><span data-stu-id="a44e0-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="a44e0-116">MSAL 處理取得，快取和重新整理使用者使用 toskens tooaccess Api 受到 Azure Active Directory v2。</span><span class="sxs-lookup"><span data-stu-id="a44e0-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="a44e0-117">新增 hello 程式碼 tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="a44e0-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="a44e0-118">此步驟將協助您建立類別 toohandle 會互動 MSAL 程式庫，如處理語彙基元。</span><span class="sxs-lookup"><span data-stu-id="a44e0-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="a44e0-119">開啟 hello`App.xaml.cs`檔案，然後加入 hello MSAL 文件庫 toohello 類別的參考：</span><span class="sxs-lookup"><span data-stu-id="a44e0-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="a44e0-120">更新 hello 應用程式類別 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="a44e0-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="a44e0-121">建立您應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="a44e0-121">Create your application’s UI</span></span>
<span data-ttu-id="a44e0-122">hello 一節顯示如何應用程式可以查詢 Graph 受保護的後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="a44e0-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="a44e0-123">系統應會自動建立 MainWindow.xaml 檔案，作為專案範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="a44e0-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="a44e0-124">開啟這個檔案的這個檔案，然後依照下列指示 hello:</span><span class="sxs-lookup"><span data-stu-id="a44e0-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="a44e0-125">取代您的應用程式`<Grid>`是 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a44e0-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
