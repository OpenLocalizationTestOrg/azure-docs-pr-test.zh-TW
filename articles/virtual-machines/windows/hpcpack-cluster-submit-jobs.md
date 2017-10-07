---
title: "在 Azure 中的 aaaSubmit 作業 tooan HPC Pack 叢集 |Microsoft 文件"
description: "了解如何註冊內部部署電腦 toosubmit tooset 作業 tooan Azure 中的 HPC Pack 叢集"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>提交從內部部署電腦 tooan HPC Pack 叢集中部署在 Azure 中的 HPC 工作
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

設定內部部署用戶端電腦 toosubmit 作業 tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)在 Azure 中的叢集。 本文示範 tooset 本機電腦與用戶端如何透過在 Azure 中 HTTPS toohello 叢集工具 toosubmit 作業。 如此一來，數個叢集使用者可以提交作業 tooa 雲端 HPC Pack 叢集中，但不會直接連接 toohello 前端節點 VM，或存取 Azure 訂用帳戶。

![提交 Azure 中的工作 tooa 叢集][jobsubmit]

## <a name="prerequisites"></a>必要條件
* **在 Azure VM 中部署 HPC Pack 前端節點**-我們建議您使用自動化的工具例如[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)或[Azure PowerShell 指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toodeploy hello 前端節點和叢集。 您需要 hello 的 hello 前端節點的 DNS 名稱 」 和 「 叢集管理員來完成這篇文章中的 hello 步驟 hello 認證。
* **用戶端電腦** - 您必須要有可執行 HPC Pack 用戶端公用程式的 Windows 或 Windows Server 用戶端電腦 (請參閱[系統需求](https://technet.microsoft.com/library/dn535781.aspx))。 如果您只想 toouse hello HPC Pack web 入口網站或 REST API toosubmit 作業，您可以使用您選擇的任何用戶端電腦。
* **HPC Pack 安裝媒體**-tooinstall hello HPC Pack 用戶端公用程式，hello 可用的安裝套件，可從 HPC Pack (HPC Pack 2012 R2) 的最新版本為[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024)。 請確定您下載 hello 相同的 hello 前端節點 VM 上安裝 HPC Pack 版本。

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>步驟 1： 安裝及設定 hello 前端節點上的 hello web 元件
tooenable REST 介面 toosubmit 作業 toohello 叢集透過 HTTPS，請確定 hello HPC Pack web 元件進行設定 hello HPC Pack 前端節點上。 如果它們尚未安裝，先執行 HpcWebComponents.msi 安裝檔案以 hello 安裝 hello web 元件。 然後，執行 hello HPC PowerShell 指令碼設定 hello 元件**Set-hpcwebcomponents.ps1**。

如需詳細的程序，請參閱[安裝 hello Microsoft HPC Pack Web 元件](http://technet.microsoft.com/library/hh314627.aspx)。

> [!TIP]
> 某些 Azure 快速入門範本為 HPC Pack 安裝和自動設定 hello web 元件。 如果您使用 hello [HPC Pack IaaS 部署指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toocreate hello 叢集中，您可以選擇性地安裝和設定 hello web 元件為 hello 部署的一部分。
> 
> 

**tooinstall hello web 元件**

1. 使用叢集系統管理員認證 hello 連接 toohello 前端節點 VM。
2. Hello HPC Pack 安裝程式資料夾中，請在 hello 前端節點上執行 HpcWebComponents.msi。
3. Hello 精靈 tooinstall hello web 元件中的 hello 步驟

**tooconfigure hello web 元件**

1. Hello 前端節點上，系統管理員身分啟動 HPC PowerShell。
2. toochange 目錄 toohello hello 組態指令碼，下列命令的型別 hello 的位置：
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure hello REST 介面，並啟動 hello HPC Web 服務，下列命令的型別 hello:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. 當提示的 tooselect 憑證時，選擇 hello 憑證對應 toohello 公開 DNS 名稱的 hello 前端節點。 例如，如果您部署的 hello 前端節點 VM 使用 hello 傳統部署模型，hello 憑證名稱看起來像 CN =&lt;*HeadNodeDnsName*&gt;。.cloudapp.net。 如果您使用 hello Resource Manager 部署模型，hello 憑證名稱看起來像 CN =&lt;*HeadNodeDnsName*&gt;。&lt;*區域*&gt;。 cloudapp.azure.com。
   
   > [!NOTE]
   > 您選取此憑證，稍後當您提交從內部部署電腦作業 toohello 前端節點。 請勿選取或設定對應 toohello hello Active Directory 網域中的 hello 前端節點電腦名稱的憑證 (例如，CN =*MyHPCHeadNode.HpcAzure.local*)。
   > 
   > 
5. tooconfigure hello 入口網站提交作業，下列命令的型別 hello:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Hello 指令碼完成之後，停止並重新啟動請輸入下列命令的 hello hello HPC 工作排程器服務：
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>步驟 2： 在內部部署電腦上安裝 hello HPC Pack 用戶端公用程式
如果您想 tooinstall hello HPC Pack 用戶端公用程式在您的電腦上，下載 HPC Pack 安裝檔案 （完整安裝） 從 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024)。 當您開始 hello 安裝時，請選擇 hello hello 安裝選項**HPC Pack 用戶端公用程式**。

toouse hello HPC Pack 用戶端工具 toosubmit 作業 toohello 前端節點 VM，您也需要 tooexport hello 前端節點的憑證，並在 hello 用戶端電腦上安裝它。 hello 憑證必須位於中。CER 格式。

**tooexport hello 憑證從 hello 前端節點**

1. Hello 前端節點上，新增 hello 憑證嵌入式管理單元 tooa Microsoft Management Console hello 本機電腦帳戶。 如需 tooadd hello 嵌入式管理單元的步驟，請參閱[新增憑證嵌入式管理單元 tooan hello MMC](https://technet.microsoft.com/library/cc754431.aspx)。
2. 在 hello 主控台樹狀目錄中，展開**憑證-本機電腦** > **個人**，然後按一下**憑證**。
3. 找出您設定 hello HPC Pack web 元件中的 hello 憑證[步驟 1： 安裝及設定 hello 前端節點上的 hello web 元件](#step-1:-install-and-configure-the-web-components-on-the-head-node)(例如，CN =&lt;*HeadNodeDnsName* &gt;。.cloudapp.net)。
4. 以滑鼠右鍵按一下 hello 憑證，然後按一下**所有工作** > **匯出**。
5. 在 [hello 憑證匯出精靈] 中，按一下 [**下一步]**，並確定**否，不要匯出 hello 私密金鑰**已選取。
6. 後續 hello 剩餘步驟，以 DER hello 精靈 tooexport hello 憑證編碼的二進位 X.509 (。CER) 格式。

**hello 用戶端電腦上的 tooimport hello 憑證**

1. 複製 hello hello 用戶端電腦上的 hello 前端節點 tooa 資料夾從匯出的憑證。
2. Hello 用戶端電腦上，執行 certmgr.msc。
3. 在 憑證管理員 中，展開 憑證 - 目前的使用者  >  受信任的根憑證授權單位，在 憑證 上按一下滑鼠右鍵，然後按一下所有工作  >  匯入。
4. 在 hello 憑證匯入精靈，按一下 **下一步**和後續 hello 步驟 tooimport hello 憑證從信任的根憑證授權單位存放區的 hello 前端節點 toohello 匯出。

> [!TIP]
> 您可能會看到安全性警告，因為 hello 用戶端電腦不辨識 hello hello 前端節點上的憑證授權單位。 為了測試用途，您可以忽略此警告和完整 hello 憑證匯入。
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Hello 叢集上的步驟 3： 執行測試工作
您的設定，再試一次執行中的作業上 hello 叢集在 Azure 中從 hello tooverify 內部部署電腦。 例如，您可以使用 HPC Pack GUI 工具或命令列命令 toosubmit 作業 toohello 叢集。 您也可以使用網頁型入口網站 toosubmit 作業。

**hello 用戶端電腦上的 toorun 作業提交命令**

1. 用戶端電腦上安裝 hello HPC Pack 用戶端公用程式，啟動 命令提示字元。
2. 輸入範例命令。 例如，toolist hello 叢集上的所有工作都輸入 hello 接下來，根據 hello 前端節點的 hello 完整 DNS 名稱的命令類似 tooone:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    或
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Hello 排程器的 URL 中使用 hello 前端節點之後，不 hello IP 位址，hello 完整 DNS 的名稱。 如果您指定 hello IP 位址，錯誤會出現類似太"hello 伺服器憑證必須 tooeither 具有有效信任或 toobe 放入 hello 受信任的根存放區的鏈結。 」
   > 
   > 
3. 出現提示時，輸入 hello 使用者名稱 (hello 形式&lt;DomainName&gt;\\&lt;UserName&gt;) 和 hello HPC 叢集管理員或另一個您所設定之叢集使用者的密碼。 您可以選擇 toostore hello 認證，在本機供更多作業。
   
    工作清單隨即出現。

**hello 用戶端電腦上的 toouse HPC 作業管理員**

1. 如果您先前沒有儲存叢集使用者的網域認證提交作業時，您可以加入 hello 認證在認證管理員。
   
    a. 在控制台中 hello 用戶端電腦上啟動認證管理員。
   
    b. 按一下 [Windows 認證] >  [新增一般認證]。
   
    c. 指定 hello 網際網路位址 (例如 https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler 或 https://&lt;HeadNodeDnsName&gt;。&lt;區域&gt;.cloudapp.azure.com/HpcScheduler)，和 hello 使用者名稱 (&lt;DomainName&gt;\\&lt;UserName&gt;) 和密碼的 hello 叢集系統管理員或另一個您所設定之叢集使用者。
2. Hello 用戶端電腦上，啟動 HPC 作業管理員。
3. 在 hello**選取前端節點**對話方塊中，型別 hello URL toohello Azure 前端節點 (例如 https://&lt;HeadNodeDnsName&gt;。.cloudapp.net 或 https://&lt;HeadNodeDnsName&gt;.&lt;區域&gt;。 cloudapp.azure.com)。
   
    HPC 作業管理員隨即開啟，並顯示 hello 前端節點上的 工作清單。

**hello 前端節點上執行的 toouse hello web 入口網站**

1. Hello 用戶端電腦上，啟動 web 瀏覽器並輸入下列位址，根據 hello 完整 DNS 名稱的 hello 前端節點的 hello 的其中一個：
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    或
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. 在出現 hello 安全性對話方塊中，輸入 hello hello HPC 叢集管理員的網域認證。 (您也可以在不同的角色中新增其他叢集使用者。 請參閱[管理叢集使用者](https://technet.microsoft.com/library/ff919335.aspx)。)
   
    hello web 入口網站開啟 toohello 工作清單 檢視。
3. 按一下 toosubmit hello 叢集中，從傳回 hello 字串"Hello World"的範例作業**新工作**hello 左側功能窗格中。
4. 在 hello**新工作**頁面的 **從提交頁面**，按一下  **HelloWorld**。 hello 作業提交頁面隨即出現。
5. 按一下 [提交] 。 如果出現提示，提供 hello hello HPC 叢集管理員的網域認證。 送出 hello 作業，且 hello 作業識別碼會顯示在 hello**我的工作**頁面。
6. 您送出的 hello 工作 tooview hello 結果按一下 hello 作業識別碼，然後按一下**檢視工作**tooview hello 命令輸出 (下**輸出**)。

## <a name="next-steps"></a>後續步驟
* 您也可以提交作業 toohello Azure 叢集概略以 hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)。
* 如果您想從 Linux 用戶端 toosubmit 叢集作業，請參閱 hello Python hello 範例[HPC Pack 2012 R2 SDK 和範例程式碼](https://www.microsoft.com/download/details.aspx?id=41633)。

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
