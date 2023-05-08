try { 
      Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\vmmgmt\Parameters\GuardList\Path*' | Select-Object -Property Drive, GuardPath -ErrorAction 'Stop'
    }
catch { 
      "No paths were found encrypted by Vormetric"
    }
