在此步驟中，您必須測試 hello 可用性群組接聽程式使用 hello 執行的用戶端應用程式相同的網路。

用戶端連接性具有下列需求的 hello:

* 用戶端連線 toohello 接聽程式必須來自位於不同雲端服務比其中一個 hello 主機 hello Always On 可用性複本的電腦。
* 如果 hello Alwayson 複本位於不同子網路中，用戶端必須指定*MultisubnetFailover = True* hello 連接字串中。 這個條件會導致平行連接嘗試中 hello tooreplicas 不同子網路。 此案例包含跨區域的 Always On 可用性群組部署。

其中一個範例是從一個 hello Vm 在 hello tooconnect toohello 接聽程式相同的 Azure 虛擬網路 （但不是其中裝載之複本）。 輕鬆 toocomplete 這項測試很 tootry tooconnect SQL Server Management Studio toohello 可用性群組接聽程式。 另一個簡單的方法是 toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)、，如下所示：

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> 如果 hello EndpointPort 值*1433年*，您不需要的 toospecify hello 呼叫它。 hello 前一次呼叫也會假設該 hello 用戶端電腦已聯結的 toohello 相同的網域和該 hello 呼叫者已授與權限 hello 資料庫使用 Windows 驗證。
> 
> 

當您測試 hello 接聽程式時，透過 hello 確定用戶端可以跨容錯移轉連接 toohello 接聽程式的可用性群組 toomake 確定 toofail。

