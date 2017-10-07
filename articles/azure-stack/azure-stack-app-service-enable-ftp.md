---
title: "Azure 堆疊上的 App Service 中的 FTP aaaEnable |Microsoft 文件"
description: "Azure 堆疊上的 App Service 中的步驟 toocomplete tooenable FTP"
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
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a>在 Azure Stack 上的 App Service 中啟用 FTP

一旦您已成功部署 Azure 堆疊上的應用程式服務如果您想 tooenable FTP 發行，以便您的租用戶可以上傳其應用程式檔案和內容，有一些額外的步驟需要 toobe 完成。  在未來的版本中，這些步驟將自動執行。

> [!NOTE]
> 這些步驟適用於在 Azure Stack 資源提供者上設定 App Service 的服務或企業系統管理員。

## <a name="enable-ftp"></a>啟用 FTP

1.  Hello 服務系統管理員身分登入 toohello 堆疊 Azure 入口網站。
2.  瀏覽過**網路介面**和選取 hello **FTP NIC**下**資源群組** - **AppService 本機**。 ![Azure Stack 網路介面][1]
3.  請注意 hello**公用 IP 位址**的 hello **FTP NIC**。 
![Azure Stack 網路介面詳細資料][2]
4.  下一步瀏覽過**虛擬機器**和選取 hello **FTP0 VM**。 ![Azure Stack 虛擬機器][3]
5.  開啟 遠端桌面工作階段 toohello VM 使用 hello**連接**按鈕與登入 toohello 工作階段，使用您在應用程式服務部署期間設定的 hello 系統管理員認證。  
![Azure Stack 虛擬機器詳細資料][4]
6.  開啟**網際網路資訊服務 (IIS) 管理員**hello FTP VM (FTP0 VM) 上。
7.  在 [網站] 下，選取 [裝載 FTP 網站]。
8.  開啟 [FTP 防火牆支援]。 ![App Service FTP0-VM 上的 IIS Manager][5]
9.  輸入 hello hello FTP NIC 的公用 IP 位址，然後按一下**套用** ![IIS Manager FTP 防火牆支援][6]

## <a name="validate-hello-enabling-of-ftp"></a>驗證 hello 啟用 FTP 的

1.  登入 toohello 堆疊 Azure 入口網站為 hello 服務管理員或租用戶身分。
2.  瀏覽過**應用程式服務**並選取 Web、 行動裝置或您已建立的應用程式開發介面應用程式。 ![應用程式服務][7]
3.  在 hello 應用程式詳細資料請注意 hello **FTP 主機名稱**和**FTP/部署使用者名稱**。 ![App Service 應用程式詳細資料][8]
> [!NOTE]
> 如果看不到下的一個項目**FTP/部署使用者名稱**，您必須先使用 hello tooset hello 部署認證**部署認證**刀鋒視窗。

4.  開啟 Windows 檔案總管中，輸入 hello 檔案網址列，例如 ftp://ftp.appservice.azurestack.local hello FTP 主機名稱
5.  出現提示時輸入 hello**部署認證**您記下在步驟 3 中，如果已啟用 hello 功能您會看到 hello 應用程式服務應用程式的內容的目錄清單。 ![FTP 檔案清單][9]
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
