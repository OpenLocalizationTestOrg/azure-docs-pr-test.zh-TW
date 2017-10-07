# 概觀
## [什麼是雲端服務？](cloud-services-choose-me.md)
## [雲端服務組態檔與封裝](cloud-services-model-and-package.md)

# 開始使用
## [.NET 雲端服務範例](cloud-services-dotnet-get-started.md)
## [Python for Visual Studio 雲端服務範例](cloud-services-python-ptvs.md)
## [使用 Microsoft HPC Pack 設定混合式 HPC 叢集](cloud-services-setup-hybrid-hpcpack-cluster.md)

# 作法
## 規劃
### [虛擬機器大小](cloud-services-sizes-specs.md)
### [更新](cloud-services-update-azure-service.md)

## 開發
### [建立 PHP Web 和背景工作角色](../cloud-services-php-create-web-role.md)
### [建置和部署 Node.js 應用程式](cloud-services-nodejs-develop-deploy-app.md)
### [使用 Express 建置 Node.js Web 應用程式](cloud-services-nodejs-develop-deploy-express-app.md)
### 儲存體和 Visual Studio
#### [Blob 儲存體和已連接的服務](../visual-studio/vs-storage-cloud-services-getting-started-blobs.md)
#### [佇列儲存體和已連接的服務](../visual-studio/vs-storage-cloud-services-getting-started-queues.md)
#### [表格儲存體和已連接的服務](../visual-studio/vs-storage-cloud-services-getting-started-tables.md)
### 設定連續建置和部署的套件
#### [TFS 和 Team Build](cloud-services-dotnet-continuous-delivery.md)
### [設定角色的流量規則](cloud-services-enable-communication-role-instances.md)
### [處理雲端服務生命週期事件](cloud-services-role-lifecycle-dotnet.md)
### [Socket.io (Node.js)](cloud-services-nodejs-chat-app-socketio.md)
### [使用 Twilio toomake 通話 (.NET)](../partner-twilio-cloud-services-dotnet-phone-call-web-role.md)
### [New Relic](../store-new-relic-cloud-services-dotnet-application-performance-management.md)

### 設定啟動工作
#### [建立啟動工作](cloud-services-startup-tasks.md)
#### [常見啟動工作](cloud-services-startup-tasks-common.md)
#### [使用工作 tooInstall.NET 雲端服務角色](cloud-services-dotnet-install-dotnet.md)

### 設定遠端桌面
#### [入口網站](cloud-services-role-enable-remote-desktop-new-portal.md)
#### [傳統入口網站](cloud-services-role-enable-remote-desktop.md)
#### [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)

## 部署
### 在入口網站中建立和部署雲端服務
#### [入口網站](cloud-services-how-to-create-deploy-portal.md)
#### [傳統入口網站](cloud-services-how-to-create-deploy.md)
### [使用 PowerShell 建立空的雲端服務容器](cloud-services-powershell-create-cloud-container.md)
### 設定自訂網域名稱
#### [入口網站](cloud-services-custom-domain-name-portal.md)
#### [傳統入口網站](cloud-services-custom-domain-name.md)
### [預備雲端服務部署 (Node.js)](cloud-services-nodejs-stage-application.md)
### [連接 tooa 自訂網域控制站](cloud-services-connect-to-custom-domain.md)

## 管理服務
### 一般管理工作
#### [入口網站](cloud-services-how-to-manage-portal.md)
#### [傳統入口網站](cloud-services-how-to-manage.md)
### 設定雲端服務
#### [入口網站](cloud-services-how-to-configure-portal.md)
#### [傳統入口網站](cloud-services-how-to-configure.md)
### [使用 Azure 自動化管理雲端服務](automation-manage-cloud-services.md)
### 設定自動調整
#### [入口網站](cloud-services-how-to-scale-portal.md)
#### [傳統入口網站](cloud-services-how-to-scale.md)
### [使用 Python toomanage Azure 資源](cloud-services-python-how-to-use-service-management.md)

### [客體 OS 修補程式](cloud-services-guestos-msrc-releases.md)
### 客體 OS 淘汰
#### [淘汰原則](cloud-services-guestos-retirement-policy.md)
#### [系列 1 淘汰通知](cloud-services-guestos-family1-retirement.md)
### [客體 OS 發佈新聞](cloud-services-guestos-update-matrix.md)
### [雲端服務角色設定 XPath 速查表](cloud-services-role-config-xpath.md)

## 管理憑證
### [雲端服務與管理憑證](cloud-services-certs-create.md)
### 設定 SSL 
#### [入口網站](cloud-services-configure-ssl-certificate-portal.md)
#### [傳統入口網站](cloud-services-configure-ssl-certificate.md)

## 監視
### [監視雲端服務](cloud-services-how-to-monitor.md)
### [測試效能](../vs-azure-tools-performance-profiling-cloud-services.md)
#### [使用 Visual Studio 分析工具進行測試](cloud-services-performance-testing-visual-studio-profiler.md)
### 啟用診斷
#### [PowerShell](cloud-services-diagnostics-powershell.md)
#### [.NET](cloud-services-dotnet-diagnostics.md)
#### [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
### [使用 Azure 診斷中的效能計數器](cloud-services-dotnet-diagnostics-performance-counters.md)
### [在 Azure 儲存體中儲存和檢視診斷資料](cloud-services-dotnet-diagnostics-storage.md)
### [使用診斷追蹤雲端服務](cloud-services-dotnet-diagnostics-trace-flow.md)
### [傳送診斷資料 tooApp Insights](cloud-services-dotnet-diagnostics-applicationinsights.md)

## 疑難排解
### 偵錯 
#### [啟用內容傳遞的遠端偵錯](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)
#### [雲端服務的選項](../vs-azure-tools-debugging-cloud-services-overview.md)
#### [使用 Visual Studio 的本機雲端服務](../vs-azure-tools-debug-cloud-services-virtual-machines.md)
#### [使用 Visual Studio 的已發佈雲端服務](../vs-azure-tools-intellitrace-debug-published-cloud-services.md)
### [雲端服務配置失敗](cloud-services-allocation-failures.md)
### [回收雲端服務角色的常見原因](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)
### [預設 TEMP 資料夾大小對角色而言太小](cloud-services-troubleshoot-default-temp-folder-size-too-small-web-worker-role.md)
### [常見部署問題](cloud-services-troubleshoot-deployment-problems.md)
### [角色無法 toostart](cloud-services-troubleshoot-roles-that-fail-start.md)
### [復原指引](cloud-services-disaster-recovery-guidance.md)
### 雲端服務常見問題集
#### [應用程式和服務可用性常見問題集](cloud-services-application-and-service-availability-faq.md)
#### [組能和管理常見問題](cloud-services-configuration-and-management-faq.md)
#### [連線和網路服務常見問題](cloud-services-connectivity-and-networking-faq.md)
#### [部署常見問題](cloud-services-deployment-faq.md)

# 參考
## [程式碼範例](https://azure.microsoft.com/en-us/resources/samples/?service=cloud-services)
## [.csdef XMLSchema](https://msdn.microsoft.com/library/azure/ee758711)
## [.cscfg XMLSchema](https://msdn.microsoft.com/library/azure/ee758710)
## [REST](https://msdn.microsoft.com/library/azure/ee460812)

# 資源
## [Azure 藍圖](https://azure.microsoft.com/roadmap/?category=compute)
## [學習路徑](https://azure.microsoft.com/documentation/learning-paths/cloud-services/)
## [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-us/home?forum=windowsazuredevelopment)
## [價格](https://azure.microsoft.com/pricing/details/cloud-services/)
## [定價計算機](https://azure.microsoft.com/pricing/calculator/)
## [服務更新](https://azure.microsoft.com/updates/?product=cloud-services&updatetype=&platform=)
## [影片](https://azure.microsoft.com/documentation/videos/index/?services=cloud-services)
