# 4d-utility-backup-dialog
Example of object notation (Form command) based dialog design

### Features

**Note**: 16R4 [object notation](http://doc.4d.com/4Dv16R5/4D/16-R5/Using-object-notation-preview.300-3482109.en.html) is required

* Possible to configure backup settings from the client side ("execute on server" method property)

* XML to JSON converter implemented

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<!--#4dcode
	C_OBJECT:C1216($1;$Backup)
	$Backup:=$1
	C_LONGINT:C283($i)
 -->
<Preferences4D xmlns="http://www.4d.com/namespace/reserved/2004/backup">

  <Backup>
    <DataBase>
      <DatabaseName>
        <ItemsCount><!--#4dtext $Backup.DataBase.DatabaseName.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.DatabaseName.ItemsCount>$i)-->
				<Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.DatabaseName.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </DatabaseName>
      <LastBackupPath>
        <ItemsCount><!--#4dtext $Backup.DataBase.LastBackupPath.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.LastBackupPath.ItemsCount>$i)-->
        <Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.LastBackupPath.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </LastBackupPath>
      <LastBackupLogPath>
        <ItemsCount><!--#4dtext $Backup.DataBase.LastBackupLogPath.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.LastBackupLogPath.ItemsCount>$i)-->
				<Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.LastBackupLogPath.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </LastBackupLogPath>
      <CurrentBackupSet>
        <ItemsCount><!--#4dtext $Backup.DataBase.CurrentBackupSet.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.CurrentBackupSet.ItemsCount>$i)-->
				<Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.CurrentBackupSet.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </CurrentBackupSet>
      <LastBackupDate>
        <ItemsCount><!--#4dtext $Backup.DataBase.LastBackupDate.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.LastBackupDate.ItemsCount>$i)-->
				<Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.LastBackupDate.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </LastBackupDate>
      <LastBackupTime>
        <ItemsCount><!--#4dtext $Backup.DataBase.LastBackupTime.ItemsCount--></ItemsCount>
				<!--#4deval $i:=0-->
				<!--#4dloop ($Backup.DataBase.LastBackupTime.ItemsCount>$i)-->
				<Item$4dtext($i+1)><!--#4dtext $Backup.DataBase.LastBackupTime.Item[$i]--></Item$4dtext($i+1)>
				<!--#4deval $i:=$i+1-->
				<!--#4dendloop-->
      </LastBackupTime>
    </DataBase>
    <Settings>
      <Advanced>
        <BackupFailure>
          <TryBackupAtTheNextScheduledDate><!--#4dtext String:C10($Backup.Settings.Advanced.BackupFailure.TryBackupAtTheNextScheduledDate;"True;;False")--></TryBackupAtTheNextScheduledDate>
          <TryToBackupAfter><!--#4dtext $Backup.Settings.Advanced.BackupFailure.TryToBackupAfter--></TryToBackupAfter>
          <AbortIfBackupFail><!--#4dtext String:C10($Backup.Settings.Advanced.BackupFailure.AbortIfBackupFail;"True;;False")--></AbortIfBackupFail>
          <RetryCountBeforeAbort><!--#4dtext $Backup.Settings.Advanced.BackupFailure.RetryCountBeforeAbort--></RetryCountBeforeAbort>
        </BackupFailure>
        <AutomaticRestore><!--#4dtext String:C10($Backup.Settings.Advanced.AutomaticRestore;"True;;False")--></AutomaticRestore>
        <AutomaticLogIntegration><!--#4dtext String:C10($Backup.Settings.Advanced.AutomaticLogIntegration;"True;;False")--></AutomaticLogIntegration>
        <AutomaticRestart><!--#4dtext String:C10($Backup.Settings.Advanced.AutomaticRestart;"True;;False")--></AutomaticRestart>
        <BackupIfDataChange><!--#4dtext String:C10($Backup.Settings.Advanced.BackupIfDataChange;"True;;False")--></BackupIfDataChange>
        <SetNumber>
          <Enable><!--#4dtext String:C10($Backup.Settings.Advanced.SetNumber.Enable;"True;;False")--></Enable>
          <Value><!--#4dtext $Backup.Settings.Advanced.SetNumber.Value--></Value>
        </SetNumber>
        <CompressionRate><!--#4dtext $Backup.Settings.Advanced.CompressionRate--></CompressionRate>
        <Redundancy><!--#4dtext $Backup.Settings.Advanced.Redundancy--></Redundancy>
        <Interlacing><!--#4dtext $Backup.Settings.Advanced.Interlacing--></Interlacing>
        <FileSegmentation>
          <DefaultSize><!--#4dtext $Backup.Settings.Advanced.FileSegmentation.DefaultSize--></DefaultSize>
        </FileSegmentation>
        <EraseOldBackupBefore><!--#4dtext String:C10($Backup.Settings.Advanced.EraseOldBackupBefore;"True;;False")--></EraseOldBackupBefore>
        <CheckArchiveFileDuringBackup><!--#4dtext String:C10($Backup.Settings.Advanced.CheckArchiveFileDuringBackup;"True;;False")--></CheckArchiveFileDuringBackup>
        <BackupJournalVerboseMode><!--#4dtext String:C10($Backup.Settings.Advanced.BackupJournalVerboseMode;"True;;False")--></BackupJournalVerboseMode>
      </Advanced>
      <General>
        <IncludeStructureFile><!--#4dtext String:C10($Backup.Settings.General.IncludeStructureFile;"True;;False")--></IncludeStructureFile>
        <IncludeDataFile><!--#4dtext String:C10($Backup.Settings.General.IncludeDataFile;"True;;False")--></IncludeDataFile>
        <IncludeAltStructFile><!--#4dtext String:C10($Backup.Settings.General.IncludeAltStructFile;"True;;False")--></IncludeAltStructFile>
        <DestinationFolder><!--#4dtext $Backup.Settings.General.DestinationFolder--></DestinationFolder>
        <IncludesFiles>
          <ItemsCount><!--#4dtext $Backup.Settings.General.IncludesFiles.ItemsCount--></ItemsCount>
					<!--#4deval $i:=0-->
					<!--#4dloop ($Backup.Settings.General.IncludesFiles.ItemsCount>$i)-->
					<Item$4dtext($i+1)><!--#4dtext $Backup.Settings.General.IncludesFiles.Item[$i]--></Item$4dtext($i+1)>
					<!--#4deval $i:=$i+1-->
					<!--#4dendloop-->
        </IncludesFiles>
      </General>
      <Scheduler>
        <Frequency><!--#4dtext $Backup.Settings.Scheduler.Frequency--></Frequency>
        <Hourly>
          <Every><!--#4dtext $Backup.Settings.Scheduler.Hourly.Every--></Every>
          <StartingAt><!--#4dtext $Backup.Settings.Scheduler.Hourly.StartingAt--></StartingAt>
        </Hourly>
        <Daily>
          <Every><!--#4dtext $Backup.Settings.Scheduler.Daily.Every--></Every>
          <Hour><!--#4dtext $Backup.Settings.Scheduler.Daily.Hour--></Hour>
        </Daily>
        <Weekly>
          <Every><!--#4dtext $Backup.Settings.Scheduler.Weekly.Every--></Every>
          <Monday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Monday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Monday.Hour--></Hour>
          </Monday>
          <Tuesday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Tuesday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Tuesday.Hour--></Hour>
          </Tuesday>
          <Wednesday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Wednesday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Wednesday.Hour--></Hour>
          </Wednesday>
          <Thursday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Thursday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Thursday.Hour--></Hour>
          </Thursday>
          <Friday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Friday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Friday.Hour--></Hour>
          </Friday>
          <Saturday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Saturday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Saturday.Hour--></Hour>
          </Saturday>
          <Sunday>
            <Save><!--#4dtext String:C10($Backup.Settings.Scheduler.Weekly.Sunday.Save;"True;;False")--></Save>
            <Hour><!--#4dtext $Backup.Settings.Scheduler.Weekly.Sunday.Hour--></Hour>
          </Sunday>
        </Weekly>
        <Monthly>
          <Every><!--#4dtext $Backup.Settings.Scheduler.Monthly.Every--></Every>
          <Hour><!--#4dtext $Backup.Settings.Scheduler.Monthly.Hour--></Hour>
          <Day><!--#4dtext $Backup.Settings.Scheduler.Monthly.Day--></Day>
        </Monthly>
      </Scheduler>
    </Settings>
  </Backup>

</Preferences4D>
```


<img width="695" alt="2017-12-27 0 20 46" src="https://user-images.githubusercontent.com/1725068/34359610-a9aedf48-ea9c-11e7-8839-369bab65ae8c.png">
