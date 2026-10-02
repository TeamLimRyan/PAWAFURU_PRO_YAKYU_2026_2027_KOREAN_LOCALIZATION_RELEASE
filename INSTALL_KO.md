# 파워프로 2026-2027 한국어 패치 v0.9

「パワフルプロ野球2026-2027」(Nintendo Switch) 일본판 한국어 패치입니다.

## 대상 버전

| 항목 | 값 |
|---|---|
| 게임 | パワフルプロ野球2026-2027 (Title ID `01007E8023F36000`) |
| 플랫폼 | Nintendo Switch |
| 필요 버전 | 일본판 Base 1.0.0 + 업데이트 **1.1.0 (v65536)** |
| 미지원 | 1.1.0이 아닌 버전(1.0.0 단독, 이후 업데이트), 다른 지역판 |

설치기가 원본 파일을 SHA-256으로 확인합니다. 버전이 다르면 설치가 멈춥니다.

## 꼭 알아 두세요

- **원본 게임이 필요합니다.** 이 패키지에는 원본 게임 데이터가 들어 있지 않습니다.
  - 본인이 정당하게 소유한 게임에서 추출한 파일로 설치기가 패치 파일을 직접 만듭니다.
- 패키지 내용:
  - 바뀐 부분의 차분(`patch/romfs_delta`)
  - 실행 파일 패치(`patch/exefs_patches`, IPS)
  - 설치기

## 설치

1. 본인 게임(1.1.0 업데이트 적용)의 romfs에서 `cdvdroot` 폴더를 추출합니다.
   - 필요한 파일: `RES00.RDB`(약 7.5GB), `RES00.RDI`, `RES10.RDB`
2. Python 3.10 이상을 설치하고, 이 폴더에서 다음을 실행합니다.
   ```
   pip install -r installer/requirements.txt
   ```
3. 설치기를 실행합니다(5~10분 걸립니다).
   ```
   python installer/install.py --romfs <cdvdroot 폴더> --out <출력 폴더>
   ```
   - 디스크 여유 공간이 약 2GB 필요합니다.
   - 끝나면 `<출력 폴더>/atmosphere`가 생깁니다.
4. 결과물을 설치합니다.
   - **Switch(Atmosphère):** `atmosphere` 폴더를 SD 카드 루트에 복사합니다.
   - **에뮬레이터(Eden 등):** 게임의 모드 폴더에 다음 구조로 넣습니다.
     - `exefs_patches/pp26_ko/*.ips` → `<모드>/exefs/`
     - `contents/01007E8023F36000/romfs/cdvdroot/*` → `<모드>/romfs/cdvdroot/`

## 제거

다음 파일과 폴더를 지웁니다.
- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES00.RDI`
- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES10.RDB`
- `atmosphere/exefs_patches/pp26_ko/` 폴더

## 업데이트·온라인 주의

- **게임을 새 버전으로 업데이트하기 전에 패치를 지우세요.**
  - 버전이 바뀌면 실행 파일 패치가 적용되지 않습니다.
  - 데이터 파일이 맞지 않아 오류가 날 수 있습니다.
- 온라인 기능은 수정된 게임으로 접속하게 됩니다. 사용 여부는 본인 판단에 맡깁니다.

## 문서

- `KNOWN_ISSUES.md`: 알려진 문제
- `CHANGELOG.md`: 변경 내역
- `qa_summary.md`: 검증 범위
- `checksums.sha256`: 파일 체크섬
- `licenses/`: 한국어 글꼴(Noto Sans KR, SIL OFL 1.1) 라이선스
