| 資源 | 免費 | 共用 (預覽) | 基本 | 標準 | 高階 (預覽)</th> |
| --- | --- | --- | --- | --- | --- |
| 每個 [App Service 方案](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)<sup>1</sup>的 [Web、Mobile 或 API Apps](https://azure.microsoft.com/services/app-service/) |10 |100 |無限制<sup>2</sup> |無限制<sup>2</sup> |無限制<sup>2</sup> |
| 每個 [App Service 方案](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</a><sup>1</sup>的[邏輯應用程式](https://azure.microsoft.com/services/app-service/logic/) |10 |10 |10 |每個核心 20 個 |每個核心 20 個 |
| [App Service 計劃](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |每個區域 1 個 |每個資源群組 10 個 |每個資源群組 100 個 |每個資源群組 100 個 |每個資源群組 100 個 |
| 計算執行個體類型 |共用 |共用 |專用<sup>3</sup> |專用<sup>3</sup> |專用<sup>3</sup></p> |
| [相應放大](../articles/app-service-web/web-sites-scale.md) (執行個體上限) |1 個共用 |1 個共用 |3 個專用<sup>3</sup> |10 個專用<sup>3</sup> |20 個專案 (ASE 中 50 個)<sup>3、4</sup> |
| 儲存體<sup>5</sup> |1 GB<sup>5</sup> |1 GB<sup>5</sup> |10 GB<sup>5</sup> |50 GB<sup>5</sup> |500 GB<sup>4,5</sup></p> |
| CPU 時間 (5 分鐘)<sup>6</sup> |3 分鐘 |3 分鐘 |無限制，以標準[費率](https://azure.microsoft.com/pricing/details/app-service/)付費</a> |無限制，以標準費率付費 |無限制，以標準費率付費 |
| CPU 時間 (天)<sup>6</sup> |60 Minuten |240 Minuten |無限制，以標準[費率](https://azure.microsoft.com/pricing/details/app-service/)付費</a> |無限制，以標準費率付費 |無限制，以標準費率付費 |
| 記憶體 (1 小時) |每個 App Service 方案 1024 MB |每個應用程式 1024 MB |N/A |N/A |N/A |
| 頻寬 |165 MB |無限制，套用 [資料傳輸費率](https://azure.microsoft.com/pricing/details/data-transfers/) |無限制，套用資料傳輸費率 |無限制，套用資料傳輸費率 |無限制，套用資料傳輸費率 |
| 應用程式架構 |32 位元 |32 位元 |32 位元/64 位元 |32 位元/64 位元 |32 位元/64 位元 |
| 每個執行個體的 Web 通訊端<sup>7</sup> |5 |35 |350 |無限制 |無限制 |
| 並行 [偵錯工具連接數](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) (每個應用程式) |1 |1 |1 |5 |5 |
| [搭配 FTP/S 和 SSL 的 azurewebsites.net 子網域](../articles/app-service-web/web-sites-configure-ssl-certificate.md) |X |X |X |X |X |
| [自訂網域](../articles/app-service-web/web-sites-custom-domain-name.md) 支援 | |X |X |X |X |
| 自訂網域 [SSL 支援](../articles/app-service-web/web-sites-configure-ssl-certificate.md) | | |無限制 |無限制，包含 5 個 SNI SSL 和 1 個 IP SSL 連接 |無限制，包含 5 個 SNI SSL 和 1 個 IP SSL 連接 |
| 整合式負載平衡器 | |X |X |X |X |
| [永遠開啟](../articles/app-service-web/web-sites-configure.md) | | |X |X |X |
| [排定的備份](../articles/app-service-web/web-sites-backup.md) | | | |一天一次 |每 5 分鐘一次<sup>8</sup> |
| [自動調整](../articles/app-service-web/web-sites-scale.md) | | |X |X |X |
| [WebJobs](../articles/app-service-web/web-sites-create-web-jobs.md)<sup>9</sup> |X |X |X |X |X |
| [Azure 排程器](https://azure.microsoft.com/services/scheduler/) 支援 | |X |X |X |X |
| [端點監視](../articles/app-service-web/web-sites-monitor.md) | | |X |X |X |
| [預備位置](../articles/app-service-web/web-sites-staged-publishing.md) | | | |5 |20 |
| 每個應用程式的自訂網域</a> | |500 |500 |500 |500 |
| SLA | |<p> |99.9% |99.95%<sup>10</sup> |99.95%<sup>10</sup> |

<sup>1</sup>應用程式和儲存體配額是依每個 App Service 方案為準，除非另有指示。  
<sup>2</sup>hello 您可以在這些電腦上裝載的應用程式的實際數目取決於 hello hello 應用程式的活動、 hello 大小 hello 機器執行個體，以及 hello 對應的資源使用率。  
<sup>3</sup>專用的執行個體可有不同的大小。 如需詳細資訊，請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/data-transfers/pricing/details/app-service/) 。  
<sup>4</sup>premium 層設定允許 500 GB 的磁碟空間時使用應用程式服務環境和 20 計算執行個體 250 GB 的儲存體否則並 too50 計算執行個體 (主體 tooavailability)。  
<sup>5</sup>hello 儲存體限制在相同的應用程式服務計劃中跨所有應用程式是 hello 總內容大小。 [App Service 環境](../articles/app-service-web/app-service-web-configure-an-app-service-environment.md#storage)中有多個儲存體選項  
<sup>6</sup>這些資源都會受到 hello 專用執行個體 （hello 執行個體大小和執行個體的 hello 數目） 上的實體資源。  
<sup>7</sup>，但是您調整應用程式中 hello 基本層 tootwo 執行個體時，如果您有 350 的並行連線，每個 hello 兩個執行個體。  
<sup>8</sup>premium 層可讓備份間隔向下向上 tooevery 5 分鐘時使用應用程式服務環境中，與 50 次每天否則。  
<sup>9</sup>在您的 App Service 執行個體中，以背景工作的方式隨選、依照排程或連續執行自訂可執行檔和/或指令碼。 若要連續執行 WebJobs，「永遠開啟」是必要選項。 若是排程 WebJobs，則 Azure 排程器免費或標準版本是必要項目。 沒有預先定義的限制，可以在應用程式服務執行個體中執行的 Webjob 的 hello 數目，但有相依於哪些 hello 應用程式程式碼嘗試 toodo 的實際限制。   
<sup>10</sup>為部署提供的 99.95% 的 SLA，適用於使用專為容錯移轉設定 Azure 流量管理員的多個執行個體。  

