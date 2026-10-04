@DF:tropa, aquí va el código nuevo. ↓
name: Windows Cloud PC - Anydesk Mejorado
on:
workflow_dispatch:
jobs:
build:
name: Iniciando Sistema Reforzado
runs-on: windows-latest
timeout-minutes: 10080
env:
PROCESSOR_COUNT: 8
OPENGL: "1"
GITHUB_PRESERVE_WORKFLOW: true
MEMORY_GB: 16
steps:
- name: Descargar e instalar lo esencial
run: |
Invoke-WebRequest -Uri "https://www.dropbox.com/scl/fi/7eiczvgil84czu55dxep3/Downloads.bat?rlkey=wzdc1wxjsph2b7r0atplmdz3p&dl=1" -OutFile "Downloads.bat" -UseBasicParsing
cmd /c Downloads.bat
- name: Iniciar AnyDesk
run: |
if (Test-Path "start.bat") {
cmd /c start.bat
Start-Sleep -Seconds 10
} else {
Write-Host "ERRO: Arquivo start.bat não encontrado — verifique o download."
exit 1
}
- name: Monitoreo continuo y reinicio automático
run: |
while ($true) {
$anydesk = Get-Process -Name "AnyDesk" -ErrorAction SilentlyContinue
if (-not $anydesk -or $anydesk.HasExited) {
Write-Host "Reiniciando AnyDesk..."
cmd /c start.bat
}
Start-Sleep -Seconds 60
}
- name: Mantener el sistema activo
run: |
Start-Sleep -Seconds 604800
- name: Limpieza segura
if: always()
run: |
Remove-Item Downloads.bat -Force -ErrorAction SilentlyContinue
Write-Host "Limpieza finalizada."
