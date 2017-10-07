---
title: "chef aaaAzure 虛擬機器部署 |Microsoft 文件"
description: "了解 Chef toodo toouse 自動化虛擬機器部署和設定 Microsoft Azure 上的方式"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>使用 Chef 自動化 Azure 虛擬機器部署
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef 是個很棒的工具，可提供自動化和所需狀態組態。

我們最新的雲端應用程式開發介面版本中，Chef 提供 Azure 與緊密整合，讓您 hello 能力 tooprovision 及部署的組態狀態，透過單一命令。

在本文中，我們將示範如何 tooset 註冊您的 Chef 環境 tooprovision Azure 虛擬機器，並會逐步引導您建立原則或 「 操作手冊"，然後再部署這個操作手冊 tooan Azure 虛擬機器。

讓我們開始吧！

## <a name="chef-basics"></a>Chef 基本概念
在開始之前，建議您檢閱的 Chef hello 基本概念。 您可以在 <a href="http://www.chef.io/chef" target="_blank">這裡</a> 找到有用資訊，建議您在嘗試進行本逐步解說之前，先快速閱讀此內容。 我將在我們開始之前，不過複習 hello 基本概念。

hello 下列圖表描述 hello 高階 Chef 架構。

![][2]

Chef 有三個主要的架構元件：Chef 伺服器、Chef 用戶端 (節點) 和 Chef 工作站。

hello Chef Server 是我們的管理點，而且有兩個選項的 hello Chef Server： 託管的解決方案或內部部署方案。 我們將使用代管解決方案。

hello Chef 用戶端 （節點） 是位於您所管理的 hello 伺服器 hello 代理程式。

hello Chef 工作站是我們的系統管理工作站，我們建立我們的原則和執行我們的管理命令。 我們要執行 hello **knife**命令 hello Chef 工作站 toomanage 從我們的基礎結構。

另外還有 hello 概念"食譜 」 與 「 食譜 」。 這些都是有效我們定義及套用 tooour 伺服器 hello 原則。

## <a name="preparing-hello-workstation"></a>正在準備 hello 工作站
首先，可讓準備 hello 工作站。 使用標準的 Windows 工作站。 我們的組態檔和操作手冊，我們需要 toocreate 目錄 toostore。

首先，建立名為 C:\chef 的目錄。

然後建立名為 c:\chef\cookbooks 的第二個目錄。

我們現在需要 toodownload 我們的 Azure 設定檔，Chef 可以與我們的 Azure 訂用帳戶進行通訊。

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
下載您發行設定使用 PowerShell Azure hello [Get-azurepublishsettingsfile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0)命令。 

儲存 hello C:\chef 中的發行設定檔。

## <a name="creating-a-managed-chef-account"></a>建立受管理的 Chef 帳戶
在 [這裡](https://manage.chef.io/signup)註冊代管的 Chef 帳戶。

在 hello 註冊過程中，您將會詢問 toocreate 新的組織。

![][3]

一旦建立您的組織，下載 hello 入門套件。

![][4]

> [!NOTE]
> 如果您收到提示，警告您，將會重設您的金鑰，因為我們不有尚未設定任何現有基礎結構，所以 tooproceed [確定]。
> 
> 

此入門套件 zip 檔案包含您的組織組態檔和金鑰。

## <a name="configuring-hello-chef-workstation"></a>設定 hello Chef 工作站
擷取 hello chef starter.zip tooC:\chef hello 內容。

複製儲存 starter\chef chef 機制底下的所有檔案\.chef tooyour c:\chef 目錄。

您的目錄現在應該看起來類似下列範例中的 hello。

![][5]

您現在應該有四個檔案，包括 c:\chef hello 根目錄中的 hello Azure 發行檔案。

hello PEM 檔案包含您的組織和管理私密金鑰進行通訊，而 hello knife.rb 檔案包含 knife 組態。 我們需要 tooedit hello knife.rb 檔案。

在您選擇的編輯器中開啟 hello 檔案，並藉由移除 hello 修改 hello"cookbook_path"/...從中 hello 路徑，讓它出現如下所示。

    cookbook_path  ["#{current_dir}/cookbooks"]

也新增 hello 下列程式行會將 hello 名稱反映您的 Azure 發行設定檔。

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Knife.rb 檔現在看起來應該類似下列範例的 toohello。

![][6]

Knife 參考 hello 下 c:\chef\cookbooks 的操作手冊目錄，而且也會使用我們的 Azure 發佈設定檔的 Azure 作業期間，可確保這些線條。

## <a name="installing-hello-chef-development-kit"></a>安裝 hello Chef 開發套件
下一步[下載並安裝](http://downloads.getchef.com/chef-dk/windows)hello ChefDK （Chef 開發套件） tooset Chef 工作站。

![][7]

安裝 c:\opscode hello 預設位置中。 此安裝大約需要 10 分鐘的時間。

確認您的 PATH 變數包含 C:\opscode\chefdk\bin、C:\opscode\chefdk\embedded\bin、c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin 等項目

如果沒有，請確定您已加入這些路徑 ！

*請注意 hello 順序的 hello 路徑重要 ！* 如果 opscode 路徑不正確的順序 hello 會出現問題。

在繼續之前，請重新啟動您的工作站。

接下來，我們將會安裝 hello Knife Azure 延伸模組。 這提供 Knife hello"Azure Plugin"。

執行下列命令的 hello。

    chef gem install knife-azure ––pre

> [!NOTE]
> hello – 前置引數可確保您收到 hello RC 新版 hello Knife Azure 外掛程式可提供存取 toohello 一組最新的 Api。
> 
> 

很少的相依性也會安裝在 hello 相同的時間。

![][8]

tooensure 一切都已正確設定，執行下列命令的 hello。

    knife azure image list

如果一切都已正確設定，您會在捲動時看到可用的 Azure 映像清單。

恭喜！ 設定工作站 hello ！

## <a name="creating-a-cookbook"></a>建立 Cookbook
使用 Chef toodefine 操作手冊的一組命令，您會希望 tooexecute 您受管理的用戶端上。 建立操作手冊很簡單，我們 hello **chef 產生 cookbook**命令 toogenerate 我們 Cookbook 的範本。 我將呼叫我的 Cookbook Web 伺服器，因為我需要可自動部署 IIS 的原則。

C:\Chef 目錄執行下列命令的 hello。

    chef generate cookbook webserver

這會產生一組 hello 目錄 C:\Chef\cookbooks\webserver 下的檔案。 我們現在需要 toodefine hello 組我們受管理的虛擬機器上，我們都希望我們 Chef 用戶端 tooexecute 命令。

hello 命令會儲存在 hello 檔案 default.rb。 在此檔案中，我會定義一組命令來安裝 IIS，啟動 IIS，並將範本檔案 toohello wwwroot 資料夾複製到。

修改 hello C:\chef\cookbooks\webserver\recipes\default.rb 檔案，並新增下列幾行 hello。

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

完成後，請儲存 hello 檔案。

## <a name="creating-a-template"></a>建立範本
如先前所述，我們需要 toogenerate 用作我們 default.html 頁面的範本檔案。

執行下列命令 toogenerate hello 範本 hello。

    chef generate template webserver Default.htm

現在您可以瀏覽 toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb 檔案。 編輯 hello 檔案加入一些簡單的"Hello World"HTML 程式碼，並儲存 hello 檔案。

## <a name="upload-hello-cookbook-toohello-chef-server"></a>上傳 hello Cookbook toohello Chef Server
在此步驟中，我們會 hello 我們建立了我們在本機電腦的操作手冊的複製，並將它上傳 toohello Chef 託管伺服器。 Hello 操作手冊上傳之後，會出現在 hello**原則** 索引標籤。

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>使用 Knife Azure 部署虛擬機器
我們現在將會部署 Azure 虛擬機器，並套用 hello 」 網頁伺服器 」 操作手冊，如此可安裝我們 IIS web 服務和預設 web 網頁。

在此順序 toodo，使用 hello **knife azure 伺服器建立**命令。

在 [hello 命令的範例則顯示下一步]。

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

hello 參數都一目了然。 替換特定變數並執行。

> [!NOTE]
> 透過 hello hello 命令列，我也使用 hello – tcp 端點參數自動化端點網路篩選規則。 我已經開啟通訊埠 80 與 3389 tooprovide 存取 toomy 網頁以及 RDP 工作階段。
> 
> 

一旦您執行 hello 命令，請移 toohello Azure 入口網站，您會看到您的電腦開始 tooprovision。

![][13]

hello 命令提示字元會顯示下一步。

![][10]

Hello 部署完成之後，我們應該是可以 tooconnect toohello web 服務透過連接埠 80 我們佈建以 hello Knife Azure 指令 hello 虛擬機器時，我們已開啟 hello 連接埠。 因為此虛擬機器 hello 只有虛擬機器在我的雲端服務，我會將與 hello 雲端服務 url 來進行連接。

![][11]

如您所見，我的 HTML 程式碼開始有點意思。

別忘了我們也可以透過從 hello Azure 入口網站連接埠 3389 透過 RDP 工作階段連接。

我希望這對您有所幫助！ 現在就開始使用 Azure 來體驗基礎結構即程式碼！

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
