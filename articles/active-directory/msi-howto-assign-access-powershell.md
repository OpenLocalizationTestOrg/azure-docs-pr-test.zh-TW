---
title: "如何使用 PowerShell 將 MSI 存取權指派給 Azure 資源"
description: "使用 PowerShell 在一個資源上指派 MSI，並存取另一個資源的逐步解說指示。"
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/14/2017
ms.author: bryanla
ms.openlocfilehash: 2211146dec8ea1f460785af9efd801780c46df60
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="assign-a-managed-service-identity-msi-access-to-a-resource-using-powershell"></a>使用 PowerShell 將受控服務識別 (MSI) 存取權指派給資源

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]

一旦已透過 MSI 設定 Azure 資源，您便可以將 MSI 存取權提供給另一個資源，就像任何安全性主體。 此範例將示範如何使用 PowerShell 將 Azure 虛擬機器的 MSI 存取權提供給 Azure 儲存體帳戶。

## <a name="prerequisites"></a>必要條件

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

此外，如果您尚未安裝 [Azure PowerShell 4.3.1 版本](https://www.powershellgallery.com/packages/AzureRM/4.3.1)，則請先安裝。

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a>使用 RBAC 將 MSI 存取權指派給另一個資源

您在 Azure 資源上啟用 MSI 之後，[例如 Azure VM](msi-qs-configure-powershell-windows-vm.md)：

1. 請使用 `Login-AzureRmAccount` Cmdlet 登入 Azure。 使用您已設定 MSI 且與 Azure 訂用帳戶相關聯的帳戶：

   ```powershell
   Login-AzureRmAccount
   ```
2. 在此範例中，我們會將 Azure VM 存取權給予儲存體帳戶。 首先我們使用 [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm) 取得 VM 名為 "myVM" 的服務主體，這是我們在啟用 MSI 時所建立的。 然後，我們使用 [New-AzureRmRoleAssignment](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment) 將 VM 「讀取」存取權提供給稱為「myStorageAcct」的儲存體帳戶：

    ```powershell
    $spID = (Get-AzureRMVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzureRmRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```

## <a name="troubleshooting"></a>疑難排解

如果資源的 MSI 沒有顯示在可用的身分識別清單中，請確認已正確啟用 MSI。 在我們的案例中，我們可以返回 [Azure 入口網站](https://portal.azure.com)中的 Azure VM，並且：

- 查看 [設定] 頁面，並確定已啟用的 MSI = "Yes"。
- 查看 [延伸模組] 頁面，並確定已成功部署 MSI 延伸模組。

如果其中一者不正確，您可能需要再次在資源上重新部署 MSI，或針對部署失敗進行疑難排解。

## <a name="related-content"></a>相關內容

- 如需 MSI 的概觀，請參閱[受控服務識別概觀](msi-overview.md)。
- 若要在 Azure VM 上啟用 MSI，請參閱[使用 PowerShell 設定 Azure VM 受控服務身分識別 (MSI)](msi-qs-configure-powershell-windows-vm.md)。

使用下列意見區段來提供意見反應，並協助我們改善及設計我們的內容。

