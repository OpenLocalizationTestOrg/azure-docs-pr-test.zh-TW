---
title: "aaaTroubleshoot Azure rbac 進行 |Microsoft 文件"
description: "取得有關角色型存取控制資源問題或疑問的協助。"
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>角色型存取控制疑難排解

文件本文會回答有關 hello 特定存取權限的角色，授與的常見問題，好讓您知道哪些 tooexpect 時使用 hello hello Azure 入口網站中的角色，並可以對存取問題進行疑難排解。 這三種角色涵蓋了所有資源類型︰

* 擁有者  
* 參與者  
* 讀取者  

擁有者和參與者都具有完整存取 toohello 管理體驗，但參與者無法提供存取 tooother 使用者或群組。 變得更有趣 hello 讀取者角色，使用，因此我們可以在其中花一些時間。 請參閱 hello[角色型存取控制取得啟動文章](role-based-access-control-configure.md)如 toogrant 的存取方式的詳細資訊。

## <a name="app-service-workloads"></a>應用程式服務工作負載
### <a name="write-access-capabilities"></a>寫入存取功能
如果您授與使用者唯讀存取 tooa 單一 web 應用程式，您可能會不預期會停用某些功能。 下列管理功能的 hello 需要**寫入**存取 tooa web 應用程式 （參與者或擁有者），並在任何唯讀案例中無法使用。

* 命令 (像是開始、停止等)
* 變更像是一般組態的設定、調整設定、備份設定與監視設定
* 存取發佈認證與其他機密，像是應用程式設定與連接字串
* 串流記錄
* 診斷記錄組態
* 主控台 (命令提示字元)
* 有效的近期部署項目 (以便本機 git 持續部署)
* 預估的花費
* Web 測試
* 虛擬網路 （只顯示 tooa 讀取器如果先前已由具有寫入權限的使用者設定的虛擬網路）。

如果您無法存取任何這些圖格，您需要 tooask 您的系統管理員參與者存取 toohello web 應用程式。

### <a name="dealing-with-related-resources"></a>處理相關資源
Web 應用程式被複雜的幾個不同的資源，相互作用 hello 存在。 以下是具有多個網站的典型資源群組：

![Web 應用程式資源群組](./media/role-based-access-control-troubleshooting/website-resource-model.png)

如此一來，如果您授與其他人存取 toojust hello web 應用程式，大部分的 hello hello hello Azure 入口網站中的網站] 刀鋒視窗的功能已停用。

這些項目需要**寫入**存取 toohello **App Service 方案**對應 tooyour 網站：  

* 檢視 hello web 應用程式的定價層 （免費或標準）  
* 調整組態 (執行個體數量、虛擬機器大小、自動調整設定)  
* 配額 (儲存容量、頻寬、CPU)  

這些項目需要**寫入**存取 toohello 整個**資源群組**，其中包含您的網站：  

* SSL 憑證和繫結 (可以在 hello 的站台間共用的 SSL 憑證相同的資源群組和地理位置)  
* 警示規則  
* 自動調整設定  
* 應用程式見解元件  
* Web 測試  

## <a name="virtual-machine-workloads"></a>虛擬機器工作負載
更像透過 web 應用程式，hello 虛擬機器刀鋒視窗上的某些功能需要寫入權限 toohello 虛擬機器或 tooother hello 資源群組中的資源。

虛擬機器是相關的 tooDomain 名稱、 虛擬網路、 儲存體帳戶和警示規則。

這些項目需要**寫入**存取 toohello**虛擬機器**:

* 端點  
* IP 位址  
* 磁碟  
* 擴充功能  

這些都需要**寫入**存取 tooboth hello**虛擬機器**，和 hello**資源群組**（hello 網域名稱），就會在：  

* 可用性集合  
* 負載平衡集合  
* 警示規則  

如果您無法存取任何這些圖格，詢問您的參與者存取 toohello 資源群組系統管理員。

## <a name="see-more"></a>更多資訊
* [Role Based Access Control](role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。
* [內建角色](role-based-access-built-in-roles.md)： 取得標準中 RBAC 的 hello 角色的相關詳細資料。
* [在 Azure rbac 進行的自訂角色](role-based-access-control-custom-roles.md)： 了解 toocreate 自訂角色 toofit 您存取需要的方式。
* [建立存取權變更歷程記錄報告](role-based-access-control-access-change-history-report.md)︰追蹤 RBAC 中的角色指派變更。

