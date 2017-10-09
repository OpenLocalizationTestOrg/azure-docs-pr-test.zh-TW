#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop 並啟動雲端應用裝置

1. toostop 雲端應用裝置跳 toohello VM，您的雲端應用裝置。
    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. 在 hello 命令列中，按一下**停止**。

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. 系統提示您進行確認時，按一下 [是] 。

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. 當您停止 VM 時，它就會加以解除配置。 正在停止 hello 雲端應用裝置，其狀態即**Deallocating**。 停止 hello 雲端應用裝置之後，其狀態是**已停止 （取消配置）**。

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. 一旦停止 VM，請按一下**啟動**（按鈕會變成可用） toostart hello VM。 Hello 雲端應用裝置啟動後，其狀態是**已啟動**。

    ![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

使用下列 cmdlet toostop hello，並啟動雲端應用裝置。

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart 雲端應用裝置

toorestart 雲端應用裝置跳 toohello VM，您的雲端應用裝置。 在 hello 命令列中，按一下**重新啟動**。 出現提示時，請確認 hello 重新啟動。 供您 toouse hello 雲端應用裝置時，其狀態會是**執行**。

![StorSimple 雲端設備虛擬機器](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

使用下列 cmdlet toorestart 雲端應用裝置 hello。

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

