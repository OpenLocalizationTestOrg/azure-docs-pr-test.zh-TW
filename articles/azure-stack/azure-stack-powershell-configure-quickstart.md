---
title: "安裝並設定 Azure Stack 的 PowerShell 快速入門 | Microsoft Docs"
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
ms.openlocfilehash: d0fc07f20937d4867c59930b13f6aed4aa37f98d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="0e908-103">在 Azure Stack 使用 PowerShell 啟動和執行</span><span class="sxs-lookup"><span data-stu-id="0e908-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="0e908-104">本文說明如何使用 PowerShell 以快速開始安裝和設定 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="0e908-104">This article is a quick start to install and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="0e908-105">本文中提供的此指令碼僅適用於 **Azure Stack 操作員**。</span><span class="sxs-lookup"><span data-stu-id="0e908-105">This script provided in this article is scoped to by the **Azure Stack operator** only.</span></span>

<span data-ttu-id="0e908-106">本文是[安裝 PowerShell]( azure-stack-powershell-install.md)、[下載工具]( azure-stack-powershell-download.md)、[設定 Azure Stack 操作員的 PowerShell 環境]( azure-stack-powershell-configure-admin.md)文件中說明之步驟的精簡版本。</span><span class="sxs-lookup"><span data-stu-id="0e908-106">This article is a condensed version of the steps described in the [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure the Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="0e908-107">藉由使用本主題中的指令碼，您可以設定與 Azure Active Directory 或 Active Directory 同盟服務一起部署的 Azure Stack 的 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="0e908-107">By using the scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="0e908-108">針對以 AAD 為基礎的部署設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e908-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="0e908-109">如果您透過 VPN 連線，登入到 Azure Stack 開發套件或以 Windows 為基礎的外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="0e908-109">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="0e908-110">開啟提升權限的 PowerShell ISE 工作階段，然後執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="0e908-110">Open an elevated PowerShell ISE session and run the following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
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

# Download Azure Stack tools from GitHub and import the connect module
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

# Configure the cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="0e908-111">針對以 AD FS 為基礎的部署設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e908-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="0e908-112">如果您透過 VPN 連線，登入到 Azure Stack 開發套件或以 Windows 為基礎的外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="0e908-112">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="0e908-113">開啟提升權限的 PowerShell ISE 工作階段，然後執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="0e908-113">Open an elevated PowerShell ISE session and run the following script:</span></span>

```powershell

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
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

# Download Azure Stack tools from GitHub and import the connect module
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

# Configure the cloud administrator’s PowerShell environment.
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

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-the-connectivity"></a><span data-ttu-id="0e908-114">測試連線</span><span class="sxs-lookup"><span data-stu-id="0e908-114">Test the connectivity</span></span>

<span data-ttu-id="0e908-115">既然您已設定 PowerShell，您可以建立資源群組來測試設定：</span><span class="sxs-lookup"><span data-stu-id="0e908-115">Now that you’ve configured PowerShell, you can test the configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="0e908-116">建立資源群組後，Cmdlet 輸出會將佈建狀態屬性設定為「成功」。</span><span class="sxs-lookup"><span data-stu-id="0e908-116">When the resource group is created, the cmdlet output has the Provisioning state property set to "Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e908-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e908-117">Next steps</span></span>

* [<span data-ttu-id="0e908-118">安裝及設定 CLI</span><span class="sxs-lookup"><span data-stu-id="0e908-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="0e908-119">開發範本</span><span class="sxs-lookup"><span data-stu-id="0e908-119">Develop templates</span></span>](azure-stack-develop-templates.md)







