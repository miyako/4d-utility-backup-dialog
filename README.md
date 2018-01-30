# 4d-utility-backup-dialog
Example of [object notation](http://doc.4d.com/4Dv16R5/4D/16-R5/Using-object-notation-preview.300-3482109.en.html) + [Form](http://doc.4d.com/4Dv16R5/4D/16-R5/Form.301-3514321.en.html) dialog design

### Features

**Note**: minimum **16R5** is required

* Possible to configure backup settings from the client side ("execute on server" method property)

* Works as a component

* Create a default settings file (daily at midnight) if one does not exist.

### Discussion

As of v16Rx, location of the [Backup configuration file](http://doc.4d.com/4Dv16R5/4D/16-R5/Get-4D-file.301-3481844.en.html) is fixed to the [Database folder](http://doc.4d.com/4Dv16R5/4D/16-R5/Get-4D-folder.301-3481820.en.html) and can not be managed elsewhere. Updating it will break the applicadtion signature on Mac. On top of that, the default backup target (generated the first time [OPEN SETTINGS WINDOW](http://doc.4d.com/4Dv16R5/4D/16-R5/OPEN-SETTINGS-WINDOW.301-3481809.en.html) is called) is also inside the [Database folder](http://doc.4d.com/4Dv16R5/4D/16-R5/Get-4D-folder.301-3481820.en.html). This module specifies [Active 4D Folder](http://doc.4d.com/4Dv16R5/4D/16-R5/Get-4D-folder.301-3481820.en.html) which is outside the application bundle, but there is nothing that can be done about the location of the settings file itself. 

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

```
ASSERT(METHOD Get attribute(Current method path;Attribute executed on server))

C_OBJECT($0;$Backup)
$Backup:=New object

$path:=Get 4D file(Backup configuration file)

If (Test path name($path)=Is a document)
	
	C_LONGINT($intValue)
	C_TEXT($stringValue)
	C_BOOLEAN($boolValue)
	
	$dom:=DOM Parse XML source($path)
	
	$DataBase:=DOM Find XML element($dom;"Preferences4D/Backup/DataBase")
	
	If (OK=1)
		
		  //these paths all follow the same pattern
		$Backup.DataBase:=New object(\
		"DatabaseName";New object("Item";New collection);\
		"LastBackupPath";New object("Item";New collection);\
		"LastBackupLogPath";New object("Item";New collection);\
		"CurrentBackupSet";New object("Item";New collection);\
		"LastBackupDate";New object("Item";New collection);\
		"LastBackupTime";New object("Item";New collection))
		
		OB GET PROPERTY NAMES($Backup.DataBase;$names)
		
		For ($i;1;Size of array($names))
			$name:=$names{$i}
			$ItemsCount:=DOM Find XML element($DataBase;"DataBase/"+$name+"/ItemsCount")
			If (OK=1)
				  //DataBase.{$name}.ItemsCount
				  //DataBase.{$name}.Item[]
				DOM GET XML ELEMENT VALUE($ItemsCount;$intValue)
				ARRAY OBJECT($DatabaseNames;$intValue)
				$Backup.DataBase[$name].ItemsCount:=$intValue
				$Item:=DOM Get next sibling XML element($ItemsCount)
				For ($j;0;$intValue-1)  //0 based index
					DOM GET XML ELEMENT VALUE($Item;$stringValue)
					$Backup.DataBase[$name].Item[$j]:=Choose($stringValue="";Null;$stringValue)
					$Item:=DOM Get next sibling XML element($Item)
				End for 
			End if 
		End for 
		
		$Backup.Settings:=New object(\
		"Scheduler";New object(\
		"Monthly";New object("Every";Null;"Hour";Null;"Day";Null);\
		"Weekly";New object(\
		"Sunday";New object("Save";Null;"Hour";Null);\
		"Monday";New object("Save";Null;"Hour";Null);\
		"Tuesday";New object("Save";Null;"Hour";Null);\
		"Wednesday";New object("Save";Null;"Hour";Null);\
		"Thursday";New object("Save";Null;"Hour";Null);\
		"Friday";New object("Save";Null;"Hour";Null);\
		"Saturday";New object("Save";Null;"Hour";Null));\
		"Daily";New object("Every";Null;"Hour";Null);\
		"Hourly";New object("Every";Null;"StartingAt";Null);\
		"Frequency";Null);\
		"Advanced";New object(\
		"BackupFailure";New object(\
		"TryBackupAtTheNextScheduledDate";Null;\
		"TryToBackupAfter";Null;\
		"AbortIfBackupFail";Null;\
		"RetryCountBeforeAbort";Null);\
		"AutomaticRestore";Null;\
		"AutomaticLogIntegration";Null;\
		"AutomaticRestart";Null;\
		"BackupIfDataChange";Null;\
		"SetNumber";New object("Enable";Null;"Value";Null);\
		"CompressionRate";Null;\
		"Redundancy";Null;\
		"Interlacing";Null;\
		"FileSegmentation";New object("DefaultSize";Null);\
		"EraseOldBackupBefore";Null;\
		"CheckArchiveFileDuringBackup";Null;\
		"BackupJournalVerboseMode";Null);\
		"General";New object("IncludeStructureFile";Null;\
		"IncludeDataFile";Null;\
		"IncludeAltStructFile";Null;\
		"DestinationFolder";Null;\
		"IncludesFiles";New object("Item";New collection)))
		
		$General:=DOM Find XML element($dom;"Preferences4D/Backup/Settings/General")
		
		If (OK=1)
			$IncludeStructureFile:=DOM Find XML element($General;"General/IncludeStructureFile")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($IncludeStructureFile;$boolValue)
				$Backup.Settings.General.IncludeStructureFile:=$boolValue
			End if 
			$IncludeDataFile:=DOM Find XML element($General;"General/IncludeDataFile")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($IncludeDataFile;$boolValue)
				$Backup.Settings.General.IncludeDataFile:=$boolValue
			End if 
			$IncludeAltStructFile:=DOM Find XML element($General;"General/IncludeAltStructFile")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($IncludeAltStructFile;$boolValue)
				$Backup.Settings.General.IncludeAltStructFile:=$boolValue
			End if 
			$DestinationFolder:=DOM Find XML element($General;"General/DestinationFolder")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($DestinationFolder;$stringValue)
				$Backup.Settings.General.DestinationFolder:=Choose($stringValue="";Null;$stringValue)
			End if 
			$IncludesFiles:=DOM Find XML element($General;"General/IncludesFiles")
			If (OK=1)
				$ItemsCount:=DOM Find XML element($IncludesFiles;"IncludesFiles/ItemsCount")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($ItemsCount;$intValue)
					ARRAY OBJECT($DatabaseNames;$intValue)
					$Backup.Settings.General.IncludesFiles.ItemsCount:=$intValue
					$Item:=DOM Get next sibling XML element($ItemsCount)
					For ($j;0;$intValue-1)  //0 based index
						DOM GET XML ELEMENT VALUE($Item;$stringValue)
						$Backup.Settings.General.IncludesFiles.Item[$j]:=Choose($stringValue="";Null;$stringValue)
						$Item:=DOM Get next sibling XML element($Item)
					End for 
				End if 
			End if 
		End if 
		
		$Advanced:=DOM Find XML element($dom;"Preferences4D/Backup/Settings/Advanced")
		
		If (OK=1)
			$BackupFailure:=DOM Find XML element($Advanced;"Advanced/BackupFailure")
			If (OK=1)
				$TryBackupAtTheNextScheduledDate:=DOM Find XML element($BackupFailure;"BackupFailure/TryBackupAtTheNextScheduledDate")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($TryBackupAtTheNextScheduledDate;$boolValue)
					$Backup.Settings.Advanced.BackupFailure.TryBackupAtTheNextScheduledDate:=$boolValue
				End if 
				$TryToBackupAfter:=DOM Find XML element($BackupFailure;"BackupFailure/TryToBackupAfter")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($TryToBackupAfter;$stringValue)
					$Backup.Settings.Advanced.BackupFailure.TryToBackupAfter:=Choose($stringValue="";Null;$stringValue)
				End if 
				$AbortIfBackupFail:=DOM Find XML element($BackupFailure;"BackupFailure/AbortIfBackupFail")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($AbortIfBackupFail;$boolValue)
					$Backup.Settings.Advanced.BackupFailure.AbortIfBackupFail:=$boolValue
				End if 
				$RetryCountBeforeAbort:=DOM Find XML element($BackupFailure;"BackupFailure/RetryCountBeforeAbort")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($RetryCountBeforeAbort;$intValue)
					$Backup.Settings.Advanced.BackupFailure.RetryCountBeforeAbort:=$intValue
				End if 
			End if 
			$AutomaticRestore:=DOM Find XML element($Advanced;"Advanced/AutomaticRestore")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($AutomaticRestore;$boolValue)
				$Backup.Settings.Advanced.AutomaticRestore:=$boolValue
			End if 
			$AutomaticLogIntegration:=DOM Find XML element($Advanced;"Advanced/AutomaticLogIntegration")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($AutomaticLogIntegration;$boolValue)
				$Backup.Settings.Advanced.AutomaticLogIntegration:=$boolValue
			End if 
			$AutomaticRestart:=DOM Find XML element($Advanced;"Advanced/AutomaticRestart")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($AutomaticRestart;$boolValue)
				$Backup.Settings.Advanced.AutomaticRestart:=$boolValue
			End if 
			$BackupIfDataChange:=DOM Find XML element($Advanced;"Advanced/BackupIfDataChange")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($BackupIfDataChange;$boolValue)
				$Backup.Settings.Advanced.BackupIfDataChange:=$boolValue
			End if 
			$SetNumber:=DOM Find XML element($Advanced;"Advanced/SetNumber")
			If (OK=1)
				$Enable:=DOM Find XML element($SetNumber;"SetNumber/Enable")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Enable;$boolValue)
					$Backup.Settings.Advanced.SetNumber.Enable:=$boolValue
				End if 
				$Value:=DOM Find XML element($SetNumber;"SetNumber/Value")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Value;$intValue)
					$Backup.Settings.Advanced.SetNumber.Value:=$intValue
				End if 
			End if 
			$CompressionRate:=DOM Find XML element($Advanced;"Advanced/CompressionRate")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($CompressionRate;$stringValue)
				$Backup.Settings.Advanced.CompressionRate:=Choose($stringValue="";Null;$stringValue)
			End if 
			$Redundancy:=DOM Find XML element($Advanced;"Advanced/Redundancy")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($Redundancy;$stringValue)
				$Backup.Settings.Advanced.Redundancy:=Choose($stringValue="";Null;$stringValue)
			End if 
			$Interlacing:=DOM Find XML element($Advanced;"Advanced/Interlacing")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($Interlacing;$stringValue)
				$Backup.Settings.Advanced.Interlacing:=Choose($stringValue="";Null;$stringValue)
			End if 
			$FileSegmentation:=DOM Find XML element($Advanced;"Advanced/FileSegmentation")
			If (OK=1)
				$DefaultSize:=DOM Find XML element($FileSegmentation;"FileSegmentation/DefaultSize")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($DefaultSize;$intValue)
					$Backup.Settings.Advanced.FileSegmentation.DefaultSize:=$intValue
				End if 
			End if 
			$EraseOldBackupBefore:=DOM Find XML element($Advanced;"Advanced/EraseOldBackupBefore")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($EraseOldBackupBefore;$boolValue)
				$Backup.Settings.Advanced.EraseOldBackupBefore:=$boolValue
			End if 
			$CheckArchiveFileDuringBackup:=DOM Find XML element($Advanced;"Advanced/CheckArchiveFileDuringBackup")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($CheckArchiveFileDuringBackup;$boolValue)
				$Backup.Settings.Advanced.CheckArchiveFileDuringBackup:=$boolValue
			End if 
			$BackupJournalVerboseMode:=DOM Find XML element($Advanced;"Advanced/BackupJournalVerboseMode")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($BackupJournalVerboseMode;$boolValue)
				$Backup.Settings.Advanced.BackupJournalVerboseMode:=$boolValue
			End if 
		End if 
		
		$Scheduler:=DOM Find XML element($dom;"Preferences4D/Backup/Settings/Scheduler")
		
		If (OK=1)
			$Frequency:=DOM Find XML element($Scheduler;"Scheduler/Frequency")
			If (OK=1)
				DOM GET XML ELEMENT VALUE($Frequency;$stringValue)
				$Backup.Settings.Scheduler.Frequency:=Choose($stringValue="";Null;$stringValue)
			End if 
			
			$Monthly:=DOM Find XML element($Scheduler;"Scheduler/Monthly")
			If (OK=1)
				$Every:=DOM Find XML element($Monthly;"Monthly/Every")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Every;$intValue)
					$Backup.Settings.Scheduler.Monthly.Every:=$intValue
				End if 
				$Hour:=DOM Find XML element($Monthly;"Monthly/Hour")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Hour;$stringValue)
					$Backup.Settings.Scheduler.Monthly.Hour:=Choose($stringValue="";Null;$stringValue)
				End if 
				$Day:=DOM Find XML element($Monthly;"Monthly/Day")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Day;$intValue)
					$Backup.Settings.Scheduler.Monthly.Day:=$intValue
				End if 
			End if 
			
			$Weekly:=DOM Find XML element($Scheduler;"Scheduler/Weekly")
			If (OK=1)
				$Every:=DOM Find XML element($Weekly;"Weekly/Every")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Every;$intValue)
					$Backup.Settings.Scheduler.Weekly.Every:=$intValue
				End if 
				
				OB GET PROPERTY NAMES($Backup.Settings.Scheduler.Weekly;$names)
				
				For ($i;1;Size of array($names))
					$name:=$names{$i}
					$Day:=DOM Find XML element($Weekly;"Weekly/"+$name)
					If (OK=1)
						$Save:=DOM Find XML element($Day;$name+"/Save")
						If (OK=1)
							DOM GET XML ELEMENT VALUE($Save;$boolValue)
							$Backup.Settings.Scheduler.Weekly[$name].Save:=$boolValue
						End if 
						$Hour:=DOM Find XML element($Day;$name+"/Hour")
						If (OK=1)
							DOM GET XML ELEMENT VALUE($Hour;$stringValue)
							$Backup.Settings.Scheduler.Weekly[$name].Hour:=Choose($stringValue="";Null;$stringValue)
						End if 
					End if 
				End for 
			End if 
			
			$Daily:=DOM Find XML element($Scheduler;"Scheduler/Daily")
			If (OK=1)
				$Every:=DOM Find XML element($Daily;"Daily/Every")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Every;$intValue)
					$Backup.Settings.Scheduler.Daily.Every:=$intValue
				End if 
				$Hour:=DOM Find XML element($Daily;"Daily/Hour")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Hour;$stringValue)
					$Backup.Settings.Scheduler.Daily.Hour:=Choose($stringValue="";Null;$stringValue)
				End if 
			End if 
			
			$Hourly:=DOM Find XML element($Scheduler;"Scheduler/Hourly")
			If (OK=1)
				$Every:=DOM Find XML element($Hourly;"Hourly/Every")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($Every;$intValue)
					$Backup.Settings.Scheduler.Hourly.Every:=$intValue
				End if 
				$StartingAt:=DOM Find XML element($Hourly;"Hourly/StartingAt")
				If (OK=1)
					DOM GET XML ELEMENT VALUE($StartingAt;$stringValue)
					$Backup.Settings.Scheduler.Hourly.StartingAt:=Choose($stringValue="";Null;$stringValue)
				End if 
			End if 
			
		End if 
		
	End if 
	
	DOM CLOSE XML($dom)
	
End if 

$0:=$Backup
```

### Screenshot

<img width="656" alt="2017-12-27 1 05 03" src="https://user-images.githubusercontent.com/1725068/34360232-048b045a-eaa2-11e7-9514-304cf5cf1a5b.png">
