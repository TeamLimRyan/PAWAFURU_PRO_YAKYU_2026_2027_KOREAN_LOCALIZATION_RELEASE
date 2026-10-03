# 파워풀 프로야구 2026-2027 한국어 패치 v1.0

Nintendo Switch 일본판 **Base 1.0.0 + Update 1.1.0 (v65536)**용입니다. Title ID는 `01007E8023F36000`입니다. 다른 지역판·게임 버전에는 적용하지 마세요.

2026-10-04 제작 의뢰자가 최종 빌드의 실기 검증 완료와 1.0 배포를 승인했습니다. 설치기는 그 승인본과 동일한 파일을 복원합니다.

## 준비

본인 소유 게임에서 추출한, 1.1.0 업데이트가 적용된 원본 `cdvdroot`가 필요합니다. 필요한 파일은 `RES00.RDI`, `RES00.RDB`, `RES10.RDB`입니다. 원본 게임·키·펌웨어·세이브는 패키지에 포함하지 않습니다.

**ZIP 전체를 새 폴더에 풀어 주세요.** v0.9·v0.91 설치기나 차분과 섞지 마세요. 기존 사용자도 새 번역·이미지 수정이 포함된 1.0으로 다시 설치해야 합니다. 원본 입력에는 이전 패치 결과물이 아닌 게임 원본을 사용하세요.

Python 3.10 이상이 필요합니다. Windows Python 3.12와 3.14에서 전체 설치를 확인했습니다. ZIP·압축 해제 공간 외에 출력 드라이브 여유 공간 약 2GB를 확보하세요.

## 설치

압축을 푼 폴더에서 실행합니다.

```powershell
python -m pip install -r installer/requirements.txt
python installer/install.py --romfs "C:\게임원본\cdvdroot" --out "C:\한국어패치결과"
```

설치기는 원본·차분·복원 결과를 SHA-256으로 확인하며 재압축하지 않습니다. **완료 메시지가 나온 뒤** 결과물을 복사하세요.

- Switch(Atmosphère): 출력 폴더의 `atmosphere`를 SD 카드 루트에 복사합니다.
- Eden 등 에뮬레이터: 게임 모드 폴더 안에 `exefs`와 `romfs`를 만듭니다. `atmosphere/exefs_patches/pp26_ko/*.ips`를 `<모드>/exefs/`로, `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/`를 `<모드>/romfs/cdvdroot/`로 복사합니다. 이전 한국어 패치 모드와 중복 적용하지 마세요.

설치 실패 시 출력 폴더의 `install_report.json`에 단계와 해시가 기록됩니다.

## 제거

Switch에서는 다음 패치 파일만 삭제합니다. 게임 원본과 세이브는 삭제하지 않습니다.

- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES00.RDI`
- `atmosphere/contents/01007E8023F36000/romfs/cdvdroot/RES10.RDB`
- `atmosphere/exefs_patches/pp26_ko/FBE18F31CCBD0BFA4247F8A870B6E300BE16889D.ips`

에뮬레이터에서는 해당 한국어 패치 모드를 비활성화하거나 제거합니다.

## 업데이트와 알려진 범위

게임을 다른 버전으로 업데이트하기 전에 패치를 제거하세요. 온라인 연결 항목은 기존 에뮬레이터 QA의 외부 연결 제한으로 별도 검증되지 않았습니다. 원본 유지 이미지와 기타 범위는 `KNOWN_ISSUES.md`, 검증 근거는 `qa_summary.md`를 참고하세요.

한국어 글꼴의 SIL OFL 라이선스는 `licenses/`에 포함합니다. 원작의 권리는 각 권리자에게 있습니다.
