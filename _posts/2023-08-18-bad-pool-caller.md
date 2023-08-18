---
layout: post
title: Bad pool caller
description: Bad pool caller
summary: Bad pool caller
tags: 
minute: 1
---
윈도우키 + x 눌러서 Windows PowerShell(관리자) 실행    
C:\>Dism /online /cleanup-image /restorehealth    
C:\>sfc /scannow    

DISM /Online /Cleanup-Image /RestoreHealth 명령은 Windows 운영 체제의 이미지를 복구하여 손상된 파일을 원래의 상태로 복원하는 역할을 합니다. 이 명령은 시스템 이미지를 검사하고, 문제가 있는 경우 해당 문제를 자동으로 해결하려고 시도합니다. 주로 시스템의 안정성을 유지하거나 문제를 해결하는 데 사용됩니다.    

여기서 명령의 각 부분을 자세하게 설명하겠습니다:    

DISM: Deployment Image Servicing and Management의 약자로, Windows 이미지 관리 도구입니다.    
/Online: 작업을 온라인 시스템 이미지에 대해 수행함을 나타냅니다.    
/Cleanup-Image: 이미지를 정리하고 유지 관리하는 작업을 지정합니다.    
/RestoreHealth: 손상된 파일을 복구하고 이미지를 원래 상태로 되돌리기 위한 작업을 나타냅니다.    
/RestoreHealth 작업은 주로 두 가지 작업을 수행합니다:    

이미지 검사: 명령이 실행되면 시스템 이미지를 검사하여 손상된 파일을 찾습니다. 이미지 파일의 무결성과 일치성을 확인하며, 손상된 파일이나 문제가 발견되면 이를 해결하기 위한 작업을 준비합니다.    

자동 복구: 검사 후 손상된 파일이나 문제가 있는 경우, 가능한 경우 자동으로 해당 파일을 복구하거나 교체합니다. 이를 통해 이미지의 무결성을 복원하고 시스템의 안정성을 유지합니다.    

/RestoreHealth 명령은 시스템 이미지를 온라인으로 작업하므로, 인터넷에 연결되어 있는 상태에서 실행하는 것이 좋습니다. 또한, 관리자 권한으로 실행해야 합니다.    

이 명령은 시스템 이미지를 복구하기 위해 매우 유용하며, 시스템의 안정성 문제나 이상 동작 등을 해결하는 데 도움을 줄 수 있습니다.    