---
title: "aaaInstall 和設定 PowerShell 的 Azure 堆疊快速入門 |Microsoft 文件"
description: "深入瞭解 Azure Stack 的 PowerShell 的安裝和設定。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: bb0bed983a09e32dbaaa39159b1d6d8bae7ea690
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="a3c4e-103">在 Azure Stack 使用 PowerShell 啟動和執行</span><span class="sxs-lookup"><span data-stu-id="a3c4e-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="a3c4e-104">本文是快速入門 tooinstall，並使用 PowerShell 設定 Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-104">This article is a quick start tooinstall and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="a3c4e-105">本文中提供此指令碼為已設定領域的 tooby hello **Azure 堆疊運算子**只。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-105">This script provided in this article is scoped tooby hello **Azure Stack operator** only.</span></span>

<span data-ttu-id="a3c4e-106">這篇文章是壓縮的版的 hello 中所述的 hello 步驟[安裝 PowerShell]( azure-stack-powershell-install.md)，[下載工具]( azure-stack-powershell-download.md)，[設定 hello Azure 堆疊操作員的 PowerShell 環境]( azure-stack-powershell-configure-admin.md)文件。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-106">This article is a condensed version of hello steps described in hello [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure hello Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="a3c4e-107">使用本主題中的 hello 指令碼，您可以設定 Azure 堆疊環境中部署與 Azure Active Directory 或 Active Directory Federation Services PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-107">By using hello scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="a3c4e-108">針對以 AAD 為基礎的部署設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3c4e-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="a3c4e-109">登入 tooyour Azure 堆疊開發套件或 windows 的外部用戶端如果透過 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-109">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="a3c4e-110">開啟提升權限的 PowerShell ISE 工作階段，然後執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a3c4e-110">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="a3c4e-111">針對以 AD FS 為基礎的部署設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3c4e-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="a3c4e-112">登入 tooyour Azure 堆疊開發套件或 windows 的外部用戶端如果透過 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="a3c4e-112">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="a3c4e-113">開啟提升權限的 PowerShell ISE 工作階段，然後執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a3c4e-113">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.local.azurestack.external/" `
  -EnableAdfsAuthentication:$true

$TenantID = Get-AzsDirectoryTenantId `
  -ADFS `
  -EnvironmentName "AzureStackAdmin"

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-hello-connectivity"></a><span data-ttu-id="a3c4e-114">測試 hello 連線</span><span class="sxs-lookup"><span data-stu-id="a3c4e-114">Test hello connectivity</span></span>

<span data-ttu-id="a3c4e-115">既然您已設定 PowerShell，您可以藉由建立資源群組來測試 hello 組態：</span><span class="sxs-lookup"><span data-stu-id="a3c4e-115">Now that you’ve configured PowerShell, you can test hello configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="a3c4e-116">Hello cmdlet 輸出建立 hello 資源群組時，具有 hello 佈建狀態屬性設定太"成功。 」</span><span class="sxs-lookup"><span data-stu-id="a3c4e-116">When hello resource group is created, hello cmdlet output has hello Provisioning state property set too"Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3c4e-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3c4e-117">Next steps</span></span>

* [<span data-ttu-id="a3c4e-118">安裝及設定 CLI</span><span class="sxs-lookup"><span data-stu-id="a3c4e-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="a3c4e-119">開發範本</span><span class="sxs-lookup"><span data-stu-id="a3c4e-119">Develop templates</span></span>](azure-stack-develop-templates.md)







