---
title: "Azure Analysis Services aaaManage |Microsoft 文件"
description: "了解如何 toomanage Analysis Services 在 Azure 中的伺服器。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Azure Analysis Services
一旦您已在 Azure 中建立 Analysis Services 伺服器，可能有某些管理工作，您需要立即 tooperform 或向下一段時間的 hello 路段圖。 例如，執行處理 toohello 重新整理資料，控制可以存取您的伺服器上的 hello 模型或監視伺服器之健全狀況。 有些管理工作只能在 Azure 入口網站中執行，有些只能在 SQL Server Management Studio (SSMS) 中執行，也有些工作可以在這兩個位置中執行。

## <a name="azure-portal"></a>Azure 入口網站
[Azure 入口網站](http://portal.azure.com/)是您可以建立和刪除伺服器、 監視伺服器的資源、 變更大小和位置管理誰存取 tooyour 伺服器。  如果您有一些問題，也可以提交支援要求。

![在 Azure 中取得伺服器名稱](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
在 Azure 中的 tooyour 伺服器連線，就如同連接 tooa 您組織中的伺服器執行個體。 從 SSMS，您可以執行許多相同工作，例如處理序資料或建立處理指令碼、 管理角色，以及使用 PowerShell 的 hello。
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>下載並安裝 SSMS
tooget 所有 hello 最新的功能和 hello 流暢體驗連接 tooyour Azure Analysis Services 伺服器時，請確定您使用 hello 最新版本的 SSMS。 

[下載 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。


### <a name="tooconnect-with-ssms"></a>使用 SSMS tooconnect
 當使用 SSMS 連接 tooyour 伺服器 hello 第一次之前，請確定 hello Analysis Services 系統管理員群組中包含您的使用者名稱。 詳細資訊，請參閱 toolearn [Server 系統管理員](#server-administrators)本文稍後。

1. 在連接之前，您會需要 tooget hello 伺服器名稱。 在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 伺服器名稱。
   
    ![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. 在 SSMS > [物件總管] 中，按一下 [連線]  > [分析服務] 。
3. 在 hello**連接 tooServer**對話方塊中，貼上在 hello 伺服器名稱，然後在**驗證**，選擇其中一個 hello 下列驗證類型：
   
    **Windows 驗證**toouse 您的 Windows 網域 \ 使用者名稱和密碼認證。

    **Active Directory 密碼驗證**toouse 組織帳戶。 例如，當從未加入網域的電腦連線時。

    **Active Directory 通用驗證**toouse[非互動式或多重要素驗證](../sql-database/sql-database-ssms-mfa-authentication.md)。 
   
    ![在 SSMS 中連線](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>伺服器管理員和資料庫使用者
在 Azure Analysis Services 中，有兩種類型的使用者：伺服器管理員和資料庫使用者。 這兩種類型的使用者都必須位於 Azure Active Directory 中，而且必須由組織的電子郵件地址或 UPN 指定。 詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。


## <a name="troubleshooting-connection-problems"></a>連接問題的疑難排解
如果您遇到問題，請使用 SSMS 中的 連線時，您可能需要 tooclear hello 登入快取。 沒有快取的 toodisc。 tooclear hello 快取中，關閉並重新啟動 hello 連接處理程序。 

## <a name="next-steps"></a>後續步驟
如果您未部署表格式模型 tooyour 新的伺服器，現在是很好的時間。 詳細資訊，請參閱 toolearn[部署 tooAzure Analysis Services](analysis-services-deploy.md)。

如果您已部署模型 tooyour 伺服器，您已準備好 tooconnect tooit 使用用戶端或瀏覽器。 詳細資訊，請參閱 toolearn[從 Azure Analysis Services 伺服器取得資料](analysis-services-connect.md)。

