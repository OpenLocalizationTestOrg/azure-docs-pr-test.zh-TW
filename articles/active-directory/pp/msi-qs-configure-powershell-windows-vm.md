---
title: "如何使用 PowerShell 設定 Azure VM 上的 MSI"
description: "使用 PowerShell 在 Azure VM 上設定「受控服務身分識別 (MSI)」的逐步指示。"
services: active-directory
documentationcenter: 
author: BryanLa
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: bdd797db4d5ed0676a9d4f55a0be6e779fd75105
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="configure-a-vm-managed-service-identity-msi-using-powershell"></a>使用 PowerShell 設定「VM 受控服務身分識別 (MSI)」

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

在 Azure Active Directory 中，「受控服務身分識別」會提供自動受控身分給 Azure 服務。 您可以使用此身分識別來向任何支援 Azure AD 驗證的服務進行驗證，不需要任何您程式碼中的認證。 

在本文中，您將了解如何使用 PowerShell 啟用和移除 Azure Windows VM 的 MSI。

## <a name="prerequisites"></a>必要條件

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

此外，如果您尚未安裝[最新版的 Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) (版本 4.3.1 或更新版本)，請先安裝。

## <a name="enable-msi-during-creation-of-an-azure-vm"></a>在建立 Azure VM 時啟用 MSI

若要建立啟用 MSI 的虛擬機器：

1. 請參閱下列 Azure VM 快速入門，完成必要的章節 (「登入 Azure」、「建立資源群組」、「建立網路群組」、「建立VM」)。 

   > [!IMPORTANT] 
   > 當您取得「建立VM」一節時，請稍微修改一下 [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvm) Cmdlet 語法。 請務必新增 `-IdentityType "SystemAssigned"` 參數，以佈建具有 MSI 的 VM，例如：
   >  
   > `$vmConfig = New-AzureRmVMConfig -VMName myVM -IdentityType "SystemAssigned" ...`

   - [使用 PowerShell 建立 Windows 虛擬機器](~/articles/virtual-machines/windows/quick-create-powershell.md)
   - [使用 PowerShell 建立 Linux 虛擬機器](~/articles/virtual-machines/linux/quick-create-powershell.md)



2. 在 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) Cmdlet 使用 `-Type` 參數新增 MSI VM 延伸模組。 您可以傳遞「ManagedIdentityExtensionForWindows」或「ManagedIdentityExtensionForLinux」(取決於 VM 的類型)，並使用 `-Name` 參數為其命名。 `-Settings` 參數會指定 OAuth 權杖端點所使用的連接埠，以用來取得權杖：

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```

## <a name="enable-msi-on-an-existing-azure-vm"></a>在現有的 Azure VM 上啟用 MSI

如果您要在現有的虛擬機器上啟用 MSI：

1. 使用 `Login-AzureRmAccount` 登入 Azure。 使用與包含虛擬機器的 Azure 訂用帳戶相關聯的帳戶。 此外也請確定您的帳戶屬於在 VM 上具有寫入權限的角色，例如「虛擬機器參與者」：

   ```powershell
   Login-AzureRmAccount
   ```

2. 先使用 `Get-AzureRmVM` Cmdlet 擷取 VM 屬性。 然後在 [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) Cmdlet 上使用 `-IdentityType` 參數啟用 MSI。

   ```powershell
   $vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
   Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm -IdentityType "SystemAssigned"
   ```

3. 在 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) Cmdlet 使用 `-Type` 參數新增 MSI VM 延伸模組。 您可以傳遞「ManagedIdentityExtensionForWindows」或「ManagedIdentityExtensionForLinux」(取決於 VM 的類型)，並使用 `-Name` 參數為其命名。 `-Settings` 參數會指定 OAuth 權杖端點所使用的連接埠，以用來取得權杖。 請比對現有 VM 位置，確認指定正確的 `-Location` 參數：

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```

## <a name="remove-msi-from-an-azure-vm"></a>從 Azure VM 移除 MSI

如果您的虛擬機器不再需要 MSI，您可以使用 `RemoveAzureRmVMExtension` Cmdlet 從 VM 移除 MSI：

1. 使用 `Login-AzureRmAccount` 登入 Azure。 使用與包含虛擬機器的 Azure 訂用帳戶相關聯的帳戶。 此外也請確定您的帳戶屬於在 VM 上具有寫入權限的角色，例如「虛擬機器參與者」：

   ```powershell
   Login-AzureRmAccount
   ```

2. 搭配 [Remove-AzureRmVMExtension](/powershell/module/azurerm.compute/remove-azurermvmextension) Cmdlet 來使用 `-Name` 切換，指定新增擴充功能時所使用的相同名稱：

   ```powershell
   Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -Name "ManagedIdentityExtensionForWindows" -VMName myVM
   ```

## <a name="related-content"></a>相關內容

- 
            [受控服務識別概觀](msi-overview.md)
- 如需完整的 Azure VM 建立快速入門，請參閱：
  
  - [使用 PowerShell 建立 Windows 虛擬機器](~/articles/virtual-machines/windows/quick-create-powershell.md) 
  - [使用 PowerShell 建立 Linux 虛擬機器](~/articles/virtual-machines/linux/quick-create-powershell.md) 

使用下列意見區段來提供意見反應，並協助我們改善及設計我們的內容。
















