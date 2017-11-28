---
title: "aaaEnable 使用 PowerShell 的 Azure 雲端服務中的角色的遠端桌面連線"
description: "如何 tooconfigure 您的 azure 雲端服務應用程式使用 PowerShell tooallow 遠端桌面連線"
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="5e924-103">使用 PowerShell 啟用 Azure 雲端服務中角色的遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="5e924-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e924-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5e924-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="5e924-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="5e924-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="5e924-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e924-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="5e924-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5e924-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="5e924-108">遠端桌面可讓您在 Azure 中執行的角色 tooaccess hello 桌面。</span><span class="sxs-lookup"><span data-stu-id="5e924-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="5e924-109">您可以使用遠端桌面連線 tootroubleshoot 後診斷問題的應用程式，在執行時。</span><span class="sxs-lookup"><span data-stu-id="5e924-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="5e924-110">本文說明如何使用 PowerShell 將雲端服務角色上的 tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="5e924-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="5e924-111">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 這個發行項所需的必要條件。</span><span class="sxs-lookup"><span data-stu-id="5e924-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="5e924-112">PowerShell 會利用 hello 遠端桌面延伸模組，因此您可以在 hello 應用程式部署之後啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="5e924-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="5e924-113">從 PowerShell 設定遠端桌面</span><span class="sxs-lookup"><span data-stu-id="5e924-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="5e924-114">hello[組 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0)指令程式可讓您指定的角色或您的雲端服務部署的所有角色上 tooenable 遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="5e924-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="5e924-115">hello cmdlet 可讓您指定 hello 遠端桌面的使用者透過 hello hello 使用者名稱和密碼*認證*參數可接受 PSCredential 物件。</span><span class="sxs-lookup"><span data-stu-id="5e924-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="5e924-116">如果您以互動方式使用 PowerShell，您可以輕鬆地設定 hello PSCredential 物件呼叫 hello[取得認證](https://technet.microsoft.com/library/hh849815.aspx)cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e924-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="5e924-117">此命令會顯示對話方塊，讓您 tooenter hello 使用者名稱和密碼 hello 遠端使用者以安全的方式。</span><span class="sxs-lookup"><span data-stu-id="5e924-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="5e924-118">因為 PowerShell 可協助自動化案例中，您也可以設定 hello **PSCredential**物件不需要使用者互動的方式。</span><span class="sxs-lookup"><span data-stu-id="5e924-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="5e924-119">首先，您需要 tooset 安全密碼。</span><span class="sxs-lookup"><span data-stu-id="5e924-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="5e924-120">您開始使用指定的純文字密碼轉換 tooa 安全字串使用[Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e924-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="5e924-121">接下來您需要 tooconvert 這個安全字串的加密標準字串使用[Convertfrom-securestring](https://technet.microsoft.com/library/hh849814.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e924-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="5e924-122">現在您可以將儲存此加密標準字串 tooa 檔案使用[Set-content](https://technet.microsoft.com/library/ee176959.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e924-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="5e924-123">您也可以建立安全密碼的檔案，所以您不需要 tootype hello 密碼在每次。</span><span class="sxs-lookup"><span data-stu-id="5e924-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="5e924-124">此外，安全的密碼檔案也比純文字檔案安全。</span><span class="sxs-lookup"><span data-stu-id="5e924-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="5e924-125">使用下列 PowerShell toocreate 安全密碼檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e924-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="5e924-126">當設定 hello 密碼，請確定您符合 hello[複雜性需求](https://technet.microsoft.com/library/cc786468.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e924-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="5e924-127">從 hello 安全密碼檔案 toocreate hello 認證物件，您必須閱讀 hello 檔案內容並將它們轉換後的 tooa 安全字串使用[Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5e924-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="5e924-128">hello[組 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet 也接受*到期*參數，指定**DateTime** hello 使用者帳戶到期。</span><span class="sxs-lookup"><span data-stu-id="5e924-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="5e924-129">例如，您可以設定 hello 帳戶 tooexpire 幾天從 hello 目前日期和時間。</span><span class="sxs-lookup"><span data-stu-id="5e924-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="5e924-130">此 PowerShell 範例將示範如何 tooset hello 雲端服務上的遠端桌面延伸模組：</span><span class="sxs-lookup"><span data-stu-id="5e924-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="5e924-131">您也可以指定 hello 部署位置和要 tooenable 遠端桌面的角色。</span><span class="sxs-lookup"><span data-stu-id="5e924-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="5e924-132">如果未指定這些參數，hello cmdlet 可讓 hello 中的所有角色的遠端桌面**生產**部署位置。</span><span class="sxs-lookup"><span data-stu-id="5e924-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="5e924-133">hello 遠端桌面延伸模組是與部署相關聯。</span><span class="sxs-lookup"><span data-stu-id="5e924-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="5e924-134">如果您建立新的部署的 hello 服務時，您有 tooenable 遠端桌面該部署。</span><span class="sxs-lookup"><span data-stu-id="5e924-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="5e924-135">如果您一定想要啟用 toohave 遠端桌面，您應該考慮您的部署工作流程整合 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5e924-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="5e924-136">從遠端桌面連接到角色執行個體</span><span class="sxs-lookup"><span data-stu-id="5e924-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="5e924-137">hello [Get-azureremotedesktopfile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0)指令程式是使用的 tooremote 桌面連接到您的雲端服務的特定角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="5e924-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="5e924-138">您可以使用 hello *LocalPath*參數 toodownload hello RDP 檔案在本機。</span><span class="sxs-lookup"><span data-stu-id="5e924-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="5e924-139">您可以使用 hello 或者*啟動*參數 toodirectly 啟動 hello 遠端桌面連線 對話方塊 tooaccess hello 雲端服務角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="5e924-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="5e924-140">檢查服務上是否已啟用遠端桌面延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e924-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="5e924-141">hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet 會顯示的遠端桌面已啟用或停用服務部署。</span><span class="sxs-lookup"><span data-stu-id="5e924-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="5e924-142">hello cmdlet 會傳回 hello hello 遠端桌面使用者與 hello 角色 hello 遠端桌面延伸模組已啟用的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5e924-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="5e924-143">根據預設，這發生在 hello 部署位置上，您可以選擇改為暫存位置 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="5e924-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="5e924-144">從服務移除遠端桌面延伸模組</span><span class="sxs-lookup"><span data-stu-id="5e924-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="5e924-145">如果您已啟用 hello 遠端桌面延伸模組的部署，而且需要 tooupdate hello 遠端桌面設定，請先移除 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e924-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="5e924-146">然後重新啟用的 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="5e924-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="5e924-147">例如，如果您想 tooset hello 遠端使用者帳戶或 hello 帳戶的新密碼過期。</span><span class="sxs-lookup"><span data-stu-id="5e924-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="5e924-148">執行此動作需要有 hello 遠端桌面啟用擴充功能的現有部署。</span><span class="sxs-lookup"><span data-stu-id="5e924-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="5e924-149">針對新的部署，您只可以直接套用 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e924-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="5e924-150">tooremove hello 遠端桌面延伸模組從 hello 部署，您可以使用 hello[移除 AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e924-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="5e924-151">您也可以選擇指定 hello 部署位置和要從中 tooremove hello 遠端桌面延伸模組的角色。</span><span class="sxs-lookup"><span data-stu-id="5e924-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="5e924-152">toocompletely 移除 hello 延伸組態，您應該呼叫 hello*移除*cmdlet 搭配 hello **UninstallConfiguration**參數。</span><span class="sxs-lookup"><span data-stu-id="5e924-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="5e924-153">hello **UninstallConfiguration**參數解除安裝任何擴充功能組態也就是套用的 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="5e924-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="5e924-154">每個延伸模組組態會與 hello 服務組態關聯。</span><span class="sxs-lookup"><span data-stu-id="5e924-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="5e924-155">呼叫 hello*移除*cmdlet 而沒有**UninstallConfiguration**解除關聯 hello<mark>部署</mark>從 hello 延伸組態，因此有效地移除hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5e924-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="5e924-156">不過，hello 延伸模組組態會保持與 hello 服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="5e924-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="5e924-157">其他資源</span><span class="sxs-lookup"><span data-stu-id="5e924-157">Additional resources</span></span>

<span data-ttu-id="5e924-158">[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="5e924-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
