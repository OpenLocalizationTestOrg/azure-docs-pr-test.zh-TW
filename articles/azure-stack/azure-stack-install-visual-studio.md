---
title: "aaaInstall Visual Studio 並連接 tooAzure 堆疊 |Microsoft 文件"
description: "了解 hello 步驟所需 tooinstall Visual Studio 並連接 tooAzure 堆疊"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a>安裝 Visual Studio 並連接 tooAzure 堆疊

使用 Visual Studio tooauthor 和部署 Azure 資源管理員[範本](azure-stack-arm-templates.md)Azure 堆疊中。 您可以使用 hello 或是此發行項 tooinstall Visual Studio 中所述的步驟從[Azure 堆疊開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果透過連接[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。 這些逐步執行將會全新安裝 Visual Studio 2015 Community 版本。 深入了解關於在其他 Visual Studio 版本之間的[共存](https://msdn.microsoft.com/library/ms246609.aspx)。

## <a name="install-visual-studio"></a>安裝 Visual Studio
1. 下載並執行 hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)。             
2. 搜尋**Visual Studio Community 2015 與 Microsoft Azure SDK - 2.9.6**；按一下 [新增]，然後 [安裝]。

    ![WebPI 安裝逐步執行的螢幕擷取畫面](./media/azure-stack-install-visual-studio/image1.png) 

3. 解除安裝 hello **Microsoft Azure PowerShell** hello Azure SDK 的一部分安裝。

    ![Azure PowerShell 新增/移除程式介面的螢幕擷取畫面](./media/azure-stack-install-visual-studio/image2.png) 

4. [安裝 Azure Stack 適用的 PowerShell](azure-stack-powershell-install.md)

5. Hello 安裝完成之後，請重新啟動 hello 作業系統。

## <a name="connect-tooazure-stack"></a>連接 tooAzure 堆疊

1. 啟動 Visual Studio。

2. 從 hello**檢視**功能表上，選取**Cloud Explorer**。

3. 在 hello 新窗格中，選取 **新增帳戶**並以您的 Azure Active Directory 認證登入。  
    ![Cloud Explorer 螢幕擷取畫面一次登入，而且連接 tooAzure 堆疊](./media/azure-stack-install-visual-studio/image6.png)

登入之後，您可以[部署範本](azure-stack-deploy-template-visual-studio.md)或瀏覽可用的資源類型和資源群組 toocreate 您自己的範本。  

## <a name="next-steps"></a>後續步驟

 - [開發適用於 Azure Stack 的範本](azure-stack-develop-templates.md)
