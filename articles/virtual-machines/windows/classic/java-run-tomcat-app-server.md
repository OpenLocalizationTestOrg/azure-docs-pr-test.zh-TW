---
title: "在傳統的 Azure VM 上 aaaRun Java 應用程式伺服器 |Microsoft 文件"
description: "本教學課程使用資源以 hello 傳統部署模型，並且示範如何建立 toocreate Windows 虛擬機器，並將它設定 toorun Apache Tomcat 應用程式伺服器。"
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>如何 toorun Java 應用程式伺服器的虛擬機器上建立 hello 傳統部署模型
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 資源管理員範本 toodeploy Java 8 與 Tomcat webapp，請參閱[這裡](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/)。

有了 Azure，您可以使用虛擬機器 tooprovide 伺服器功能。 例如，在 Azure 上執行的虛擬機器可以設定的 toohost Java 應用程式伺服器，例如 Apache Tomcat。

完成本指南之後, 您必須了解如何 toocreate 虛擬機器在 Azure 上執行，並將它設定 toorun Java 應用程式伺服器。 您會了解，並執行下列工作的 hello:

* 如何 toocreate 的虛擬機器，都有 Java Development Kit (JDK) 已安裝。
* Tooremotely 登入方式 tooyour 虛擬機器。
* 如何 tooinstall Java 應用程式伺服器--Apache Tomcat-虛擬機器上。
* 如何 toocreate 虛擬機器的端點。
* 如何 tooopen hello 中的連接埠的應用程式伺服器防火牆。

hello 完成安裝在 Tomcat 中虛擬機器上執行的結果。

![執行 Apache Tomcat 的虛擬機器][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate 虛擬機器
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。  
2. 按一下**新增**，按一下 **計算**，然後按一下**查看所有**在 hello**熱門應用程式**。
3. 按一下**JDK**，按一下  **JDK 8**在 hello **JDK**窗格。  
   虛擬機器映像支援**JDK 6**和**JDK 7**可用，如果您有未準備好 toorun JDK 8 中的舊版應用程式。
4. 在 hello JDK 8 窗格中，選取 **傳統**，然後按一下 **建立**。
5. 在 hello**基本概念**刀鋒視窗中：
   1. 指定 hello 虛擬機器的名稱。
   2. 輸入 hello 系統管理員的名稱在 hello**使用者名**欄位。 請記住這個名稱，而且 hello 稍後 hello 下一個欄位的相關聯的密碼。 您需要在您從遠端登入 toohello 虛擬機器。
   3. 輸入密碼，hello**新密碼**欄位，並重新輸入在 hello**確認密碼**欄位。 此密碼是 hello 系統管理員帳戶。
   4. 選取適當的 hello**訂用帳戶**。
   5. Hello**資源群組**，按一下 **建立新**，然後輸入 hello 是新的資源群組的名稱。 或者，按一下**使用現有**並選取其中一個 hello 可用的資源群組。
   6. 選取的位置 hello 虛擬機器所在的位置，例如**美國中南部**。
6. 按一下 [下一步] 。
7. 在 hello**虛擬機器映像大小**刀鋒視窗中，選取**標準 A1**或另一個適當的映像。
8. 按一下 [選取] 。

9. 在 hello**設定**刀鋒視窗中，按一下 **確定**。 您可以使用 Azure 所提供的 hello 預設值。  
10. 在 hello**摘要**刀鋒視窗中，按一下 **確定**。

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely tooyour 虛擬機器中的符號
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [虛擬機器 (傳統)]。 如有需要按一下**更多服務**在 hello 左下角 hello 服務類別之下。 hello**虛擬機器 （傳統）**項目會列在 hello**計算**群組。
3. 按一下您要 toosign 中的 hello 虛擬機器的 hello 名稱。
4. Hello 虛擬機器啟動之後，在 hello hello 窗格頂端的功能表允許連線。
5. 按一下 [ **連接**]。
6. 回應 toohello 提示做為所需的 tooconnect toohello 虛擬機器。 一般而言，您儲存或開啟包含 hello 連接詳細資料的 hello.rdp 檔案。 您可能會有 toocopy hello url： 連接埠為 hello 最後一部分 hello hello.rdp 檔案第一行，並將它貼入遠端登入應用程式中。

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall 虛擬機器上的 Java 應用程式伺服器
您可以複製 Java 應用程式伺服器 tooyour 虛擬機器，或您可透過安裝程式在 Java 應用程式伺服器。

本教學課程會使用為 hello Java 應用程式伺服器 tooinstall Tomcat。

1. 當您登入 tooyour 虛擬機器時，開啟瀏覽器工作階段過[Apache Tomcat](http://tomcat.apache.org/download-80.cgi)。
2. 按兩下 hello 連結**32 位元/64 位元 Windows 服務的安裝程式**。 利用此技術，Tomcat 將以 Windows 服務形式進行安裝。
3. 出現提示時，選擇 toorun hello 安裝程式。
4. 在 hello **Apache Tomcat 安裝**精靈，後續 hello 提示 tooinstall Tomcat。 基於 hello 本教學課程中，接受 hello 預設值是正常的。 當您來到 hello **Apache Tomcat 安裝精靈的正在完成 hello**對話方塊中，您可以選擇性地檢查**執行 Apache Tomcat** toohave 現在 Tomcat 開始。 按一下**完成**toocomplete hello Tomcat 安裝程序。

## <a name="toostart-tomcat"></a>toostart Tomcat

開啟您的虛擬機器和執行 hello 命令上的命令提示字元，您可以手動啟動 Tomcat **net&nbsp;啟動&nbsp;Tomcat8**。

Tomcat 開始執行之後，您可以輸入 hello URL 來存取 Tomcat <http://localhost:8080/<> hello 虛擬機器的瀏覽器中。

toosee Tomcat 外部機器中執行，您需要 toocreate 端點，並開啟連接埠。

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate 虛擬機器的端點
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [虛擬機器 (傳統)]。
3. 按一下 hello hello 執行您的 Java 應用程式伺服器的虛擬機器名稱。
4. 按一下 [端點] 。
5. 按一下 [新增] 。
6. 在 hello**加入端點**對話方塊：
   1. 指定 hello 端點; 的名稱例如， **HttpIn**。
   2. 選取**TCP** hello 通訊協定。
   3. 指定**80** hello 公用連接埠。
   4. 指定**8080** hello 私用連接埠。
   5. 選取**已停用**hello 浮動 IP 位址。
   6. 將保留原狀 hello 存取控制清單。
   7. 按一下 hello**確定**按鈕 tooclose hello 對話方塊，並建立 hello 端點。

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen hello 防火牆中針對您的虛擬機器中的連接埠
1. 登入 tooyour 虛擬機器。
2. 按一下 Windows [開始] 。
3. 按一下 [控制台] 。
4. 依序按一下 [系統及安全性]、[Windows 防火牆] 及 [進階設定]。
5. 按一下 輸入規則，然後按一下新增規則。  
   ![新增輸入規則][NewIBRule]
6. Hello**規則類型**，選取**連接埠**，然後按一下**下一步**。  
   ![新增輸入規則連接埠][NewRulePort]
7. 在 hello**通訊協定和連接埠**畫面上，選取**TCP**，指定**8080**為 hello**特定本機連接埠**，然後按一下 **下一步**。  
  ![新增輸入規則][NewRuleProtocol]
8. 在 [hello**動作**畫面上，選取**允許 hello 連線**，然後按一下**下一步]**。
   ![新增輸入規則動作][NewRuleAction]
9. 在 [hello**設定檔**畫面上，確認**網域**，**私用**，和**公用**已選取，然後再按一下**下一步]**.
   ![新增輸入規則設定檔][NewRuleProfile]
10. 在 hello**名稱**畫面上，指定 hello 規則的名稱，例如**HttpIn** （hello 規則名稱不是必要的 toomatch hello 端點名稱，不過），然後按一下**完成**。  
    ![新增輸入規則名稱][NewRuleName]

此時，應該能從外部瀏覽器檢視您的 Tomcat 網站。 在 hello 瀏覽器的位址視窗中，輸入 hello 表單的 URL  **http://*您\_DNS\_名稱*。 cloudapp.net**，其中***您\_DNS\_名稱***是 hello hello 虛擬機器的建立時指定的 DNS 名稱。

## <a name="application-lifecycle-considerations"></a>應用程式生命週期考量
* 您無法建立您自己的 web 應用程式封存檔 (WAR)，並將它加入 toohello **webapps**資料夾。 例如，建立基本的 Java Service Page (JSP) 動態 Web 專案，並將它匯出為 WAR 檔案。 接下來，複製 hello WAR toohello Apache Tomcat **webapps** hello 虛擬機器，然後在瀏覽器中執行上的資料夾。
* 依預設安裝 hello Tomcat 服務時，它是 toostart 手動設定。 您可以切換它 toostart 自動使用 hello 服務 嵌入式管理單元。 啟動 hello 服務 嵌入式管理單元，依序按一下**Windows 啟動**，**系統管理工具**，然後**服務**。 按兩下 hello **Apache Tomcat**服務和設定**啟動類型**太**自動**。

    ![自動設定服務 toostart][service_automatic_startup]

    hello 的好處有自動啟動 Tomcat 是，它就會開始執行 hello 虛擬機器重新開機 （例如之後需要重新開機的軟體更新已安裝）, 時。

## <a name="next-steps"></a>後續步驟
您可以了解其他服務 （例如 Azure 儲存體、 服務匯流排和 SQL Database），您可能會想 tooinclude Java 應用程式。 檢視可用的 hello 資訊在 hello [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
