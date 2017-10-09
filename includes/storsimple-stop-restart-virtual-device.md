#### <a name="toostop-and-start-a-virtual-device"></a>toostop 並啟動虛擬裝置
toostop 是虛擬裝置，請按一下其名稱，然後按一下**關機**。 Hello 虛擬裝置正在關機而關閉，其狀態即**停止**。 停止 hello 虛擬裝置之後，其狀態是**已停止**。

使用下列 cmdlet toostop hello 和啟動虛擬裝置。

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart 虛擬裝置
虛擬裝置正在執行，而且您想 toorestart 時，按一下其名稱，然後按一下**重新啟動**。 Hello 虛擬裝置重新啟動時，其狀態即**正在重新啟動**。 Hello 虛擬裝置就緒可供您 toouse 時，其狀態會是**執行**。

使用下列 cmdlet toorestart 虛擬裝置 hello。

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

