---
title: "Azure Active Directory 中的新 Azure 堆疊租用戶帳戶 aaaAdd |Microsoft 文件"
description: "部署 Microsoft Azure 堆疊開發套件之後, 您必須至少一個 toocreate 租用戶的使用者帳戶，好讓您可以瀏覽 hello 租用戶入口網站。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a>在 Azure Active Directory 中新增 Azure Stack 租用戶帳戶
之後[部署 hello Azure 堆疊開發套件](azure-stack-run-powershell-script.md)，讓您可以瀏覽 hello 租用戶入口網站，並測試您的優惠和方案，您將需要租用戶的使用者帳戶。 您可以建立租用戶帳戶[使用 hello Azure 入口網站](#create-an-azure-stack-tenant-account-using-the-azure-portal)或[使用 PowerShell](#create-an-azure-stack-tenant-account-using-powershell)。

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a>建立 Azure 堆疊租用戶帳戶使用 hello Azure 入口網站
您必須擁有 Azure 訂用帳戶 toouse hello Azure 入口網站。

1. 登入太[Azure](http://manage.windowsazure.com)。
2. 在 Microsoft Azure 左側的導覽列中，按一下 [Active Directory] 。
3. 在 hello 目錄清單中，按一下您想要 Azure 堆疊 toouse 或建立一個新的 hello 目錄。
4. 在此目錄頁面上，按一下 [使用者] 。
5. 按一下 [新增使用者] 。
6. 在 hello**新增使用者**精靈，hello**使用者類型**清單中，選擇**您組織中的新使用者**。
7. 在 hello**使用者名**方塊中，輸入 hello 使用者的名稱。
8. 在 hello  **@** 方塊中，選擇 hello 適當的項目。
9. 按一下 下一步箭號 hello。
10. 在 [hello**使用者設定檔**hello 精靈] 頁面輸入**名字**，**姓氏**，和**顯示名稱**。
11. 在 hello**角色**清單中，選擇**使用者**。
12. 按一下 下一步箭號 hello。
13. 在 hello**取得暫時密碼**頁面上，按一下**建立**。
14. 複製 hello**新密碼**。
15. 登入 tooMicrosoft Azure hello 新帳戶。 變更 hello 密碼提示。
16. 登入太`https://portal.local.azurestack.external`與 hello 新帳戶 toosee hello 租用戶入口網站。

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a>使用 PowerShell 建立 Azure Stack 租用戶帳戶
如果您沒有 Azure 訂用帳戶，您無法使用 hello Azure 入口網站 tooadd 租用戶的使用者帳戶。 在此情況下，您可以改為使用 hello Azure Active Directory 的 Windows PowerShell 模組。

> [!NOTE]
> 如果您使用 Microsoft 帳戶 (Live ID) toodeploy Azure 堆疊開發套件，您無法使用 AAD PowerShell toocreate 租用戶帳戶。 
> 
> 

1. 安裝 hello [Microsoft Online Services 登入小幫手的 IT 專業人員 RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950)。
2. 安裝 hello [Azure Active Directory 的 Windows PowerShell 模組 （64 位元版本）](http://go.microsoft.com/fwlink/p/?linkid=236297)並開啟它。
3. 執行下列 cmdlet 的 hello:

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. 登入 tooMicrosoft Azure hello 新帳戶。 變更 hello 密碼提示。
2. 登入太`https://portal.local.azurestack.external`與 hello 新帳戶 toosee hello 租用戶入口網站。

