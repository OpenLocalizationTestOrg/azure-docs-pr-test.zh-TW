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
## <a name="set-up-your-project"></a>設定專案

本節提供有關如何逐步解說 toocreate 新的專案 toodemonstrate 如何 toointegrate Windows 桌面.NET 應用程式 (XAML) 與*使用 Microsoft 登入*，它才能查詢需要權杖的 Web Api。

本指南所建立的 hello 應用程式公開螢幕和登出按鈕上的按鈕 toograph 並顯示結果。

> 改為偏好 toodownload 這個範例的 Visual Studio 專案嗎？ [下載專案](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。


### <a name="create-your-application"></a>建立您的應用程式
1. 在 Visual Studio 中：`File` > `New` > `Project`<br/>
2. 在 [範本] 底下，選取 `Visual C#`
3. 選取`WPF App`(或*WPF 應用程式*視您的 Visual Studio 的 hello 版本而定)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>加入 hello Microsoft 驗證程式庫 (MSAL) tooyour 專案
1. 在 Visual Studio 中：`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. 複製/貼上下列 hello hello 封裝管理員主控台 視窗中：

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> 上述的 hello 套件會安裝 hello Microsoft 驗證程式庫 (MSAL)。 MSAL 處理取得，快取和重新整理使用者使用 toskens tooaccess Api 受到 Azure Active Directory v2。

## <a name="add-hello-code-tooinitialize-msal"></a>新增 hello 程式碼 tooinitialize MSAL
此步驟將協助您建立類別 toohandle 會互動 MSAL 程式庫，如處理語彙基元。

1. 開啟 hello`App.xaml.cs`檔案，然後加入 hello MSAL 文件庫 toohello 類別的參考：

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
更新 hello 應用程式類別 toohello 下列：
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

## <a name="create-your-applications-ui"></a>建立您應用程式的 UI
hello 一節顯示如何應用程式可以查詢 Graph 受保護的後端伺服器。 系統應會自動建立 MainWindow.xaml 檔案，作為專案範本的一部分。 開啟這個檔案的這個檔案，然後依照下列指示 hello:

取代您的應用程式`<Grid>`是 hello 下列：

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
