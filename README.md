# STIG-2

<#
.SYNOPSIS
    This PowerShell script ensures that Microsoft consumer experiences are turned off

.NOTES
    Author          : Htain Ney
    Date Created    : 2026-06-12
    Last Modified   : 2026-06-12
    Version         : 1.0
    CVEs            : N/A
    Plugin IDs      : N/A
    STIG-ID         : WN11-CC-000197

.TESTED ON
    Date(s) Tested  : 2026-11-14
    Tested By       : Htain Ney
    Systems Tested  : Windows 11
    PowerShell Ver. : 5.1

.USAGE
    Put any usage instructions here.
    Example syntax:
    PS C:\> .\STIG-ID-WN11-CC-000197.ps1
#>

# Define the registry path and value for WN11-CC-000197
$registryPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CloudContent"
$valueName = "DisableWindowsConsumerFeatures"
$valueData = 1 # 0x00000001 in hexadecimal

# Check if the registry path exists, if not create it
if (-not (Test-Path $registryPath)) {
    New-Item -Path $registryPath -Force
}

# Set the DisableWindowsConsumerFeatures value
Set-ItemProperty -Path $registryPath -Name $valueName -Value $valueData -Type DWord

# Output success message
Write-Host "Registry value '$valueName' set to '$valueData' at '$registryPath'."

# Confirmation of success
Get-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CloudContent" -Name "DisableWindowsConsumerFeatures"
# Expected Value: DisableWindowsConsumerFeatures = 1
