# 概觀
## [什麼是服務匯流排傳訊？](service-bus-messaging-overview.md)
## [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
## [服務匯流排架構](service-bus-architecture.md)
## [常見問題集](service-bus-faq.md)

# 開始使用
## [建立命名空間](service-bus-create-namespace-portal.md)
## 使用佇列
### [.NET](service-bus-dotnet-get-started-with-queues.md)
### [Java](service-bus-java-how-to-use-queues.md)
### [Node.js](service-bus-nodejs-how-to-use-queues.md)
### [PHP](service-bus-php-how-to-use-queues.md)
### [Python](service-bus-python-how-to-use-queues.md)
### [Ruby](service-bus-ruby-how-to-use-queues.md)
### [REST](/rest/api/servicebus/queues)
## 使用主題及訂閱
### [.NET](service-bus-dotnet-how-to-use-topics-subscriptions.md)
### [Java](service-bus-java-how-to-use-topics-subscriptions.md)
### [Node.js](service-bus-nodejs-how-to-use-topics-subscriptions.md)
### [PHP](service-bus-php-how-to-use-topics-subscriptions.md)
### [Python](service-bus-python-how-to-use-topics-subscriptions.md)
### [Ruby](service-bus-ruby-how-to-use-topics-subscriptions.md)

# 作法

## 規劃和設計
### [受控服務識別 (預覽)](service-bus-managed-service-identity.md)
### [角色型存取控制 (預覽)](service-bus-role-based-access-control.md)
### [進階傳訊](service-bus-premium-messaging.md)
### [Azure 佇列和服務匯流排佇列的比較](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
### [效能最佳化](service-bus-performance-improvements.md)
### [異地災難復原和異地複寫](service-bus-geo-dr.md)
### [非同步傳訊模式與高可用性](service-bus-async-messaging.md)
### [處理中斷與災害](service-bus-outages-disasters.md)

## 開發
### [建置多層式服務匯流排應用程式](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)
### 訊息處理
#### [佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)
#### [訊息、 裝載和序列化](service-bus-messages-payloads.md)
#### [訊息傳輸、 鎖定和結算](message-transfers-locks-settlement.md)
#### [訊息排序以及時間戳記](message-sequencing.md)
#### [訊息到期 (存留時間)](message-expiration.md)
### [驗證和授權](service-bus-authentication-and-authorization.md)
#### [從 ACS 移轉至 SAS](service-bus-migrate-acs-sas.md)
#### [使用共用存取簽章進行驗證](service-bus-sas.md)
### [主題篩選條件和動作](topic-filters.md)
### [分割的佇列和主題](service-bus-partitioning.md)
### [訊息工作階段](message-sessions.md)
### AMQP
#### [AMQP 概觀](service-bus-amqp-overview.md)
#### [.NET](service-bus-amqp-dotnet.md)
#### [Java](service-bus-amqp-java.md)
#### [Java 訊息服務和 AMQP](service-bus-java-how-to-use-jms-api-amqp.md)
#### [AMQP 通訊協定指南](service-bus-amqp-protocol-guide.md)
#### [AMQP 以要求與回應為基礎的作業](service-bus-amqp-request-response.md)
### 進階功能
#### [無效信件佇列](service-bus-dead-letter-queues.md)
#### [預先擷取訊息](service-bus-prefetch.md)
#### [重複訊息偵測](duplicate-detection.md)
#### [訊息計數器](message-counters.md)
#### [訊息延遲](message-deferral.md)
#### [訊息瀏覽](message-browsing.md)
#### [建立實體與自動轉寄的鏈結](service-bus-auto-forwarding.md)
#### [交易處理](service-bus-transactions.md)
#### [配對的命名空間實作](service-bus-paired-namespaces.md)
### [端對端追蹤和診斷](service-bus-end-to-end-tracing.md)
## 管理
### [透過 Azure 監視器監視服務匯流排](service-bus-metrics-azure-monitor.md)
### [服務匯流排管理程式庫](service-bus-management-libraries.md)
### [診斷記錄](service-bus-diagnostic-logs.md)
### [暫停及重新啟用訊息實體](entity-suspend.md)
### [使用 Azure Resource Manager 範本](service-bus-resource-manager-overview.md)
#### [建立命名空間](service-bus-resource-manager-namespace.md)
#### [建立命名空間和佇列](service-bus-resource-manager-namespace-queue.md)
#### [建立命名空間與主題和訂用帳戶](service-bus-resource-manager-namespace-topic.md)
#### [建立命名空間和佇列的授權規則](service-bus-resource-manager-namespace-auth-rule.md)
#### [建立命名空間與主題、訂用帳戶和規則](service-bus-resource-manager-namespace-topic-with-rule.md)
#### 
### [使用 Azure PowerShell 佈建實體](service-bus-manage-with-ps.md)

# 參考
## .NET
### [Microsoft.ServiceBus.Messaging (.NET Framework)](/dotnet/api/microsoft.servicebus.messaging)
### [Microsoft.Azure.ServiceBus (.NET Standard)](/dotnet/api/microsoft.azure.servicebus)
## [Java](/java/api/overview/azure/servicebus)
## [Azure PowerShell](/powershell/module/azurerm.servicebus)
## [REST](/rest/api/servicebus)
## [例外狀況](service-bus-messaging-exceptions.md)
## [配額](service-bus-quotas.md)
## [SQLFilter 語法](service-bus-messaging-sql-filter.md)
## [SQLRuleAction 語法](service-bus-messaging-sql-rule-action.md)

# 資源
## [Azure 藍圖](https://azure.microsoft.com/roadmap/?category=enterprise-integration)
## [部落格](https://blogs.msdn.microsoft.com/servicebus/)
## [MSDN 論壇](https://social.msdn.microsoft.com/forums/home?forum=servbus)
## [價格](https://azure.microsoft.com/pricing/details/service-bus/)
## [定價計算機](https://azure.microsoft.com/pricing/calculator/)
## [價格詳細資料](service-bus-pricing-billing.md)
## [範例](service-bus-samples.md)
## [ServiceBus360](https://www.servicebus360.com/)
## [服務匯流排總管](https://github.com/paolosalvatori/ServiceBusExplorer)
## [服務更新](https://azure.microsoft.com/updates/?product=service-bus)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azureservicebus)
## [影片](https://azure.microsoft.com/documentation/videos/index/?services=service-bus)


