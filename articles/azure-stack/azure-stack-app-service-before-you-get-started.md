---
title: "部署 Azure 堆疊上的應用程式服務的 aaaBefore |Microsoft 文件"
description: "部署 Azure 堆疊上的應用程式服務之前的步驟 toocomplete"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a>開始使用 Azure Stack 上的 App Service 之前

您需要幾個項目 tooinstall Azure 堆疊上的 Azure 應用程式服務：

- 已完成的部署的 hello [Azure 堆疊開發套件](azure-stack-run-powershell-script.md)。
- 您的 Azure Stack 系統中有足夠空間可供 Azure Stack 上之 App Service 的小型部署使用。  hello 所需空間大約是 20 GB 的磁碟空間。
- 當您針對 Azure Stack 上的 App Service 建立虛擬機器時要使用的 Windows Server VM 映像。
- [執行 SQL Server 的伺服器](#SQL-Server)。

>[!NOTE] 
> 下列步驟 hello*所有*hello Azure 堆疊主機電腦上的進行。

toodeploy 資源提供者，您必須以系統管理員身分執行 hello PowerShell 整合式指令碼環境 (ISE)。 基於這個理由，您需要 tooallow cookie 和 JavaScript 中，您會使用 toosign tooAzure Active Directory 中的 hello Internet Explorer 設定檔。

## <a name="turn-off-internet-explorer-enhanced-security"></a>關閉 Internet Explorer 增強式安全性

1.  登入 toohello Azure 堆疊開發套件的電腦**AzureStack/系統管理員**，然後開啟**伺服器管理員**。

2.  針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。

3.  登入 toohello 身為管理員，Azure 堆疊開發套件電腦，然後開啟**伺服器管理員**。

4.  針對系統管理員和使用者關閉 [Internet Explorer 增強式安全性設定]。

## <a name="enable-cookies"></a>啟用 Cookie

1.  選取 [開始] > [所有應用程式] > [Windows 附屬應用程式]。 以滑鼠右鍵按一下 [Internet Explorer] > [更多] > [以系統管理員身分執行]。

2.  出現提示時，選取 [使用建議的安全性]，然後選取 [確定]。

3.  在 Internet Explorer 中，選取**工具**（hello 齒輪圖示） >**網際網路選項** > **隱私權** > **進階**.

4.  選取 [進階]。 確定已選取兩個 [接受] 核取方塊。 選取 [確定] 兩次。

5.  關閉 Internet Explorer，然後重新啟動 hello 身為系統管理員的 PowerShell ISE。

## <a name="install-powershell-for-azure-stack"></a>安裝適用於 Azure Stack 的 PowerShell

tooinstall PowerShell for Azure 堆疊，請依照下列中的 hello 步驟[安裝 PowerShell](azure-stack-powershell-install.md)。

## <a name="use-visual-studio-with-azure-stack"></a>搭配 Azure Stack 使用 Visual Studio

toouse Visual Studio 和 Azure 堆疊，請依照下列中的 hello 步驟[安裝 Visual Studio](azure-stack-install-visual-studio.md)。

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a>新增 Windows Server 2016 VM 映像 tooAzure 堆疊

由於 App Service 會部署一些虛擬機器，因此，它需要 Azure Stack 中的 Windows Server 2016 VM 映像。 tooinstall VM 映像，請依照下列中的 hello 步驟[新增預設虛擬機器映像](azure-stack-add-default-image.md)。

## <a name="SQL-Server"></a>SQL Server

Azure 堆疊上的應用程式服務需要存取 tooa SQL Server 執行個體 toocreate 和主機兩個資料庫 toorun hello 應用程式服務資源提供者。  您應該選擇 toodeploy hello SQL 連線層級設定得必須 Azure 堆疊上的 SQL Server VM**公用**。  當您完成 hello 應用程式服務在 Azure 堆疊安裝程式中的 hello 選項時，您可以選擇 hello SQL Server 執行個體 toouse。

## <a name="next-steps"></a>後續步驟

- [安裝應用程式服務資源提供者 hello](azure-stack-app-service-deploy.md)。

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
