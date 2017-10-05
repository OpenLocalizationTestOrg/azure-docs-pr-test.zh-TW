---
title: "使用 PowerShell 啟用 Azure 雲端服務中角色的遠端桌面連線"
description: "如何使用 PowerShell 設定的 Azure 雲端服務應用程式以允許遠端桌面連線"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="c0417-103">使用 PowerShell 啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="c0417-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0417-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c0417-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="c0417-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c0417-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="c0417-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0417-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="c0417-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0417-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="c0417-108">遠端桌面可讓您存取 Azure 內執行中角色的桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="c0417-109">您可以使用遠端桌面連線來疑難排解和診斷執行中應用程式的問題。</span><span class="sxs-lookup"><span data-stu-id="c0417-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="c0417-110">這篇文章描述如何使用 PowerShell 在雲端服務角色上啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="c0417-111">如需這篇文章所需要的必要條件，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="c0417-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="c0417-112">PowerShell 會利用遠端桌面延伸模組，因此在應用程式部署之後，您也可以啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="c0417-113">從 PowerShell 設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="c0417-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="c0417-114">[Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) Cmdlet 可讓您在雲端服務部署的指定角色或所有角色上啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="c0417-115">此 Cmdlet 可讓您透過可接受 PSCredential 物件的 *Credential* 參數，指定遠端桌面使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c0417-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="c0417-116">如果您以互動方式使用 PowerShell，您可以呼叫 [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) Cmdlet，輕鬆地設定 PSCredential 物件。</span><span class="sxs-lookup"><span data-stu-id="c0417-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="c0417-117">此命令會顯示對話方塊，可讓您以安全的方式輸入遠端使用者的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c0417-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="c0417-118">由於 PowerShell 在自動化案例中非常實用，您也可以透過不需要使用者互動的方式設定 **PSCredential** 物件。</span><span class="sxs-lookup"><span data-stu-id="c0417-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="c0417-119">您必須先設定安全的密碼。</span><span class="sxs-lookup"><span data-stu-id="c0417-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="c0417-120">首先，指定純文字密碼，然後使用 [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx)轉換成安全字串。</span><span class="sxs-lookup"><span data-stu-id="c0417-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="c0417-121">接下來，您需要使用 [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx)，將這個安全字串轉換成加密的標準字串。</span><span class="sxs-lookup"><span data-stu-id="c0417-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="c0417-122">現在，您可以使用 [Set-Content](https://technet.microsoft.com/library/ee176959.aspx)，將此加密的標準字串儲存到檔案。</span><span class="sxs-lookup"><span data-stu-id="c0417-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="c0417-123">您也可以建立安全的密碼檔案，這樣就不需要每次都要輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="c0417-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="c0417-124">此外，安全的密碼檔案也比純文字檔案安全。</span><span class="sxs-lookup"><span data-stu-id="c0417-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="c0417-125">使用下列 PowerShell 來建立安全的密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="c0417-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="c0417-126">設定密碼時，請確定您符合 [複雜性需求](https://technet.microsoft.com/library/cc786468.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c0417-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="c0417-127">若要從安全的密碼檔案建立認證物件，您必須讀取檔案內容，並使用 [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx)將它們轉換回安全字串。</span><span class="sxs-lookup"><span data-stu-id="c0417-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="c0417-128">[Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) Cmdlet 也接受 *Expiration* 參數，它可指定使用者帳戶到期的 **日期時間** 。</span><span class="sxs-lookup"><span data-stu-id="c0417-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="c0417-129">例如，您可以設定帳戶在目前日期和時間的幾天後到期。</span><span class="sxs-lookup"><span data-stu-id="c0417-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="c0417-130">這個 PowerShell 範例示範如何在雲端服務上設定遠端桌面延伸模組：</span><span class="sxs-lookup"><span data-stu-id="c0417-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="c0417-131">您可以選擇性地指定部署位置和您想要啟用遠端桌面的角色。</span><span class="sxs-lookup"><span data-stu-id="c0417-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="c0417-132">如果未指定這些參數，此 Cmdlet 會在「生產」  部署位置中的所有角色上啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="c0417-133">遠端桌面延伸模組與部署相關聯。</span><span class="sxs-lookup"><span data-stu-id="c0417-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="c0417-134">如果您為服務建立新的部署，您必須啟用該部署上的遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="c0417-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="c0417-135">如果您想一律啟用遠端桌面，則您應該考慮將 PowerShell 指令碼整合到您的部署工作流程中。</span><span class="sxs-lookup"><span data-stu-id="c0417-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="c0417-136">從遠端桌面連接到角色執行個體</span><span class="sxs-lookup"><span data-stu-id="c0417-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="c0417-137">[Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) Cmdlet 用於從遠端桌面連接到雲端服務的特定角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="c0417-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="c0417-138">您可以使用 *LocalPath* 參數將 RDP 檔案下載到本機。</span><span class="sxs-lookup"><span data-stu-id="c0417-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="c0417-139">或您可以使用 *Launch* 參數，直接啟動 [遠端桌面連線] 對話方塊來存取雲端服務角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="c0417-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="c0417-140">檢查服務上是否已啟用遠端桌面延伸模組</span><span class="sxs-lookup"><span data-stu-id="c0417-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="c0417-141">[Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) Cmdlet 會顯示服務部署上的遠端桌面為啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="c0417-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="c0417-142">此 Cmdlet 會傳回遠端桌面使用者的使用者名稱，以及已啟用遠端桌面延伸模組的角色。</span><span class="sxs-lookup"><span data-stu-id="c0417-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="c0417-143">根據預設，這會發生在部署位置上，而您可以選擇改為使用預備位置。</span><span class="sxs-lookup"><span data-stu-id="c0417-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="c0417-144">從服務移除遠端桌面延伸模組</span><span class="sxs-lookup"><span data-stu-id="c0417-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="c0417-145">如果您已在部署上啟用遠端桌面延伸模組，且需要更新遠端桌面設定，則必須先移除延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c0417-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="c0417-146">然後使用新的設定將它再次啟用。</span><span class="sxs-lookup"><span data-stu-id="c0417-146">And enable it again with the new settings.</span></span> <span data-ttu-id="c0417-147">例如，如果您想為遠端使用者帳戶或是已到期的帳戶設定新密碼。</span><span class="sxs-lookup"><span data-stu-id="c0417-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="c0417-148">必須在已啟用遠端桌面延伸模組的現有部署上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="c0417-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="c0417-149">對於新部署，您可以直接套用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c0417-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="c0417-150">若要從部署移除遠端桌面延伸模組，您可以使用 [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c0417-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="c0417-151">您也可以選擇性地指定您想要移除遠端桌面延伸模組的部署位置和角色。</span><span class="sxs-lookup"><span data-stu-id="c0417-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="c0417-152">若要完全移除延伸模組組態，您應該在呼叫 *remove* Cmdlet 時指定 **UninstallConfiguration** 參數。</span><span class="sxs-lookup"><span data-stu-id="c0417-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="c0417-153">**UninstallConfiguration** 參數會將任何已套用到服務的延伸模組組態解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c0417-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="c0417-154">每個延伸模組組態都與服務組態相關連。</span><span class="sxs-lookup"><span data-stu-id="c0417-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="c0417-155">呼叫 remove Cmdlet 時未指定 **UninstallConfiguration** 會取消<mark>部署</mark>與擴充組態的關聯，因此實際上會移除延伸模組。</span><span class="sxs-lookup"><span data-stu-id="c0417-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="c0417-156">不過，延伸模組組態仍然與服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="c0417-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="c0417-157">其他資源</span><span class="sxs-lookup"><span data-stu-id="c0417-157">Additional resources</span></span>

<span data-ttu-id="c0417-158">[如何設定雲端服務](cloud-services-how-to-configure.md)
[雲端服務常見問題集 - 遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c0417-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
