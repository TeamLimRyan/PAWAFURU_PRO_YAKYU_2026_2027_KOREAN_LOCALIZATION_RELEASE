# 파워풀 프로야구 2026-2027 한국어 패치 v1.01 — xdelta판

Nintendo Switch 일본판 **Base 1.0.0 + Update 1.1.0 (v65536)** 전용입니다.
Title ID: `01007E8023F36000`. 다른 지역판·게임 버전은 지원하지 않습니다.

v1.0 이후 접수된 번역·연출·설정 이름·경기 안정성 피드백과 패치 로딩 최적화를 반영했습니다.
이전 패치 사용자는 **수정하지 않은 1.1.0 원본에서 새로 적용**해 주세요.
이전 한국어 패치 결과물을 xdelta의 원본 입력으로 사용하면 안 됩니다.

## 준비

본인 소유 게임에서 추출한 업데이트 적용 원본 `cdvdroot`가 필요합니다.
`RES00.RDI`, `RES00.RDB`, `RES10.RDB`의 크기와 SHA-256을 `manifest.json`으로 검사합니다.
NSP/XCI에 직접 적용하는 패치가 아닙니다. 원본 게임·키·펌웨어·세이브는 포함하지 않습니다.

ZIP 전체를 새 폴더에 풀어 주세요. ZIP 보관 공간 외에 압축 해제 약 1.6GB,
출력 드라이브 약 2GB의 여유 공간이 필요합니다.

## Windows 자동 적용

Windows x64용 xdelta3를 포함하며 Python은 필요하지 않습니다.
압축을 푼 폴더에서 PowerShell을 열고 실행합니다.

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\apply_xdelta.ps1 -Romfs "C:\게임원본\cdvdroot" -Out "C:\한국어패치결과"
```

`-Out`에는 아직 존재하지 않는 새 폴더를 지정합니다. 원본·패치·완성 파일을 SHA-256으로
검증하며, **PASS가 표시된 뒤** 결과물을 설치합니다. 원본을 재압축하지 않습니다.

- Switch(Atmosphère): 출력 폴더의 `atmosphere`를 SD 카드 루트에 복사합니다.
- Eden 등 에뮬레이터: 출력의 `atmosphere/exefs_patches/pp26_ko/*.ips`를 모드의 `exefs/`에,
  `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/` 아래 두 파일을 모드의 `romfs/cdvdroot/`에 복사합니다.

**RDI·RDB·IPS 세 파일을 함께 교체**하고, 이전 한국어 모드를 중복 활성화하지 마세요.
기존 세이브를 삭제할 필요는 없습니다. 사용자 지정 이름은 유지됩니다.

## 수동 적용

| 원본 입력 | 패치 | 별도 폴더에 만들 출력 |
|---|---|---|
| 원본 `RES00.RDI` | `patch/RES00.RDI.xdelta` | `RES00.RDI` |
| 원본 `RES10.RDB` | `patch/RES10.RDB.xdelta` | `RES10.RDB` |

```text
xdelta3 -d -s ORIGINAL/RES00.RDI patch/RES00.RDI.xdelta OUTPUT/RES00.RDI
xdelta3 -d -s ORIGINAL/RES10.RDB patch/RES10.RDB.xdelta OUTPUT/RES10.RDB
```

먼저 `OUTPUT` 폴더를 만들고 원본을 덮어쓰지 마세요. `manifest.json`의 원본 3파일과
출력 2파일의 크기·해시를 확인합니다. 원본 `RES00.RDB`는 변경하거나 모드에 복사하지 않습니다.
**`patch/FBE18F31CCBD0BFA4247F8A870B6E300BE16889D.ips`도 반드시 설치**해야 합니다.
Windows 이외 환경에서는 해당 운영체제의 xdelta3를 사용합니다.

## 제거 및 복구

Switch에서는 다음 3파일만 제거합니다. 원본 게임과 세이브는 삭제하지 않습니다.

- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES00.RDI`
- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES10.RDB`
- `atmosphere/exefs_patches/pp26_ko/FBE18F31CCBD0BFA4247F8A870B6E300BE16889D.ips`

에뮬레이터에서는 한국어 모드를 비활성화합니다. 설치가 실패했다면 불완전한 결과물을
복사하지 말고, 원본 경로를 확인한 뒤 새 `-Out` 폴더로 재실행합니다.
게임 버전을 업데이트하기 전에는 패치를 제거하세요.

## 검증 및 라이선스

2026-10-10 사용자 확인과 배포 승인을 반영했습니다. 로컬 검사와 사용자 확인 범위는
`qa_summary.md`, 설치 검증은 `xdelta_verification.json`에 기록합니다.
`checksums.sha256`은 패키지 파일 체크섬입니다. 알려진 범위는 `KNOWN_ISSUES.md`를 참고하세요.

한국어 글꼴은 Noto Sans CJK(OFL), 동봉 xdelta3는 Joshua MacDonald의 공식 v3.2.0
Windows x64 바이너리(Apache-2.0)입니다. `licenses/` 및 `tools/PROVENANCE.md`에
라이선스와 출처를 포함합니다. 원작의 권리는 각 권리자에게 있습니다.
