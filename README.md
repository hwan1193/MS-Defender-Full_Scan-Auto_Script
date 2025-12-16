# MS-Defender-Full_Scan-Auto_Script
Schedule Microsoft Defender full scans via Windows Task Scheduler (System). Intune-friendly PowerShell automation.

# MS-Defender Full Scan Auto Script

Windows 환경에서 Microsoft Defender Full Scan을 작업 스케줄러(SYSTEM 계정)로 등록/운영하기 위한 PowerShell 자동화 스크립트입니다.
(운영 서버/클라이언트에 동일하게 적용 가능하도록 설계)

## What it does
- 지정된 스케줄로 Defender Full Scan 실행 작업 생성
- 작업 생성 결과/검증 로그 파일 기록
- 롤백(작업 삭제 + 폴더 정리) 지원

## Requirements
- Windows 10/11, Windows Server
- Microsoft Defender 사용 환경
- 관리자 권한(작업 스케줄러 등록 필요)

## Quick Start

### 1) Run (Create Scheduled Task)
'''powershell

 C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -NoProfile -ExecutionPolicy Bypass -File C:\sec\Intune_Defender_MonthlyFullScan_v5.ps1

 ### 2) Verify Schedule

 schtasks /Query /TN "\Defender-Monthly-FullScan-FirstSat-0200" /V /FO LIST

 ### 3) Check Deploy Log

 type "C:ProgramData\DefenderScan\deploy_task_v5.log"

 ### Rollback (Clean Remove)

 schtasks /Delete /TN "\_TEST_Task" /F
 schtasks /Delete /TN "\Defender-Monthly-FullScan-FirstSat-0200" /F
 Remove-Item "C:\ProgramData\DefenderScan" -Recurse -Force
 


