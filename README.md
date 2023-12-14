param
(
    [string]$EnvironmentName,
    [string]$ApplicationPath
)
Import-Module webadministration
Import-Module ActiveDirectory
$AIMdbPropertiesFile= "AIMDB.properties";
$AIMdbPropertiesFilePath="$ApplicationPath\$EnvironmentName\$AIMdbPropertiesFile";
$file_raw_data=Get-Content -Path $AIMdbPropertiesFilePath  -Raw
$configuration=ConvertFrom-StringData($file_raw_data);#Transformation of property file into Hash table
$LOG_DIR= $configuration.("Log_Path");
$CertPath=$configuration.("SSLCert");
$CertPassword=$configuration.("SSL");
$Port=$configuration.("Https_Port");
$CertName=$configuration.("CertDNSName");
$HostHeader=$configuration.("HostHeader");
#Purge logs more than 15 days
Get-ChildItem $LOG_DIR -Recurse -File | Where CreationTime -lt  (Get-Date).AddDays(-15) | Remove-Item -Force
if(-not (Test-Path $LOG_DIR))
{
    New-Item -Path $LOG_DIR -ItemType Directory
}
$FileName= "$($LOG_DIR)SSLCertificateInstall_Log_$((Get-Date).ToString("yyyyMMdd-hhmmss"))-$($EnvironmentName).log"
Write-Output "FileName: $($FileName)" | Out-File -FilePath $FileName -Append
Write-Output "FileName: $($FileName)" | Out-File -FilePath $FileName -Append
try
{
     $password = $CertPassword | ConvertTo-SecureString -AsPlainText -Force
     Write-Output "Started importing the SSL on to certificate manager"| Out-File -FilePath $FileName -Append
     Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $password -Exportable -Verbose
     Write-Output "Completed importing the SSL on to certificate manager"| Out-File -FilePath $FileName -Append
     $request = Get-childitem -path cert:\localmachine\My | Where-Object { $_.Subject -match "CN=$CertName" }
     $request
     $AddSSL = $request.Thumbprint
     
     Get-WebBinding -port $Port -name "Default web site" | Remove-WebBinding
     Write-Output "Removed https Port $Port from IIS"| Out-File -FilePath $FileName -Append
    
     New-WebBinding -name "Default web site" -port $Port -Protocol https -HostHeader "$HostHeader" -SslFlags 1 
     Write-Output "Added https Port $Port on IIS"| Out-File -FilePath $FileName -Append

     Get-WebBinding -Protocol http | Remove-WebBinding -confirm:$false
     Write-Output "Removed http port:8800 on IIS"| Out-File -FilePath $FileName -Append

     Get-WebBinding -name "Default web site" -Port "8800" -Protocol http -HostHeader $null 
     Write-Output "Added http Port 8800 on IIS"| Out-File -FilePath $FileName -Append

     $(Get-WebBinding -name "Default web site" -port $Port -Protocol https -HostHeader "$HostHeader").AddSSLCertificate($AddSSL, "my") 
     Write-Output "Completed binding the SSL to https Port $Port on IIS"| Out-File -FilePath $FileName -Append
}
catch
{
    Write-Output $_.Exception|format-list -Force | Out-File -FilePath $FileName -Append
}
