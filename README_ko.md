# TaxaScope (KRIBB-KCTC 생물정보학 툴킷)

[![Version](https://img.shields.io/badge/version-1.0-green.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![License](https://img.shields.io/badge/license-Academic%20Use-orange.svg)](LICENSE)

한국생명공학연구원(KRIBB) 한국미생물보존센터(KCTC)

TaxaScope는 Windows 환경에서 미생물 유전체 분석을 위해 설계된 통합형 GUI 기반 생물정보학 툴킷입니다. 복잡한 명령줄 워크플로우와 사용자 친화적인 연구 애플리케이션을 하나의 데스크톱 인터페이스에서 연결하며, 워크플로우 구성, 컨테이너 기반 실행, 결과 미리보기, 재현성 보고서 기능을 통합적으로 제공합니다.

## 문서

관리되는 문서는 `docs/` 디렉토리에 집중되어 있습니다.

- [문서 인덱스](docs/README.md)
- [TaxaScope 사용자 매뉴얼](docs/TaxaScope_User_Manual.md)
- [HTML 사용자 가이드 (영어/중국어/한국어, 텍스트 전용 워크플로우 버전)](docs/TaxaScope_User_Guide.html)
- [설치 가이드](docs/Installation_Guide.md)
- [소프트웨어 가용성](docs/Software_Availability.md)
- [도구 재현성](docs/Tool_Reproducibility.md)

사용자 매뉴얼은 검토자를 위한 주요 문서로, TaxaScope에 실제 구현된 데스크톱 워크플로우를 설명합니다: 최초 환경 설정, 작업 디렉토리 선택, 원클릭 데이터베이스 다운로드, 오프라인 또는 온라인 컨테이너 이미지 처리, NCBI 또는 로컬 입력 준비, 모듈 파라미터 설정, 배치 실행, 결과 검토, 출력 디렉토리 구조, 문제 해결, HTML/Markdown/JSON 재현성 보고서 생성.

## 주요 기능

- **원클릭 분석**: Prokka, BUSCO, CheckM2, dbCAN, antiSMASH, PhyloPhlAn, ANI/AAI에 대한 자동화 워크플로우.
- **NCBI 데이터 획득**: GCA/GCF 등록번호를 사용한 유전체 일괄 검색.
- **컨테이너 기반 실행**: 격리된 Podman/Docker 호환 컨테이너 환경에서 도구 실행.
- **오프라인 이미지 처리**: 네트워크 접근이 제한된 경우 사전 패키징된 컨테이너 이미지를 가져오거나 내보낼 수 있음.
- **배치 워크플로우 구성**: 여러 모듈을 순차 워크플로우로 조합 가능.
- **결과 검토**: GUI에서 출력 파일, 그래프, 보고서, 계통수를 확인 가능.
- **재현성 보고서**: 소프트웨어, 데이터베이스, 파라미터, 타임스탬프, 입력 및 출력 메타데이터를 포함한 HTML, Markdown, JSON 보고서 내보내기.

## 아키텍처

TaxaScope는 안정성과 재현성을 지원하기 위해 4계층 아키텍처를 사용합니다:

1. **프레젠테이션 계층**: CustomTkinter 기반 그래픽 사용자 인터페이스.
2. **오케스트레이션 계층**: 작업 스케줄링, 파라미터 처리, 데이터 흐름을 위한 Python 및 PowerShell 스크립트.
3. **분석 핵심 계층**: 컨테이너화된 생물정보학 도구 및 로컬 데이터베이스.
4. **인프라 계층**: WSL2와 Podman/Docker 백엔드가 있는 Windows 호스트 시스템.

<img width="1916" height="1029" alt="그림 1. TaxaScope 아키텍처" src="https://github.com/user-attachments/assets/69093f22-e0cb-4a13-b01a-d653ad878088" />

그림 1. TaxaScope 아키텍처. 시스템은 사용자 인터페이스, 오케스트레이션 엔진, 분석 핵심, 인프라의 4계층 모델로 운영됩니다. 프레젠테이션 계층은 파라미터 조정 및 결과 시각화를 위한 GUI를 제공합니다. 오케스트레이션 계층은 작업 스케줄링 및 리소스 할당을 관리합니다. 분석 핵심 계층은 격리된 컨테이너 환경에서 생물정보학 도구를 실행합니다. 인프라 계층은 Windows, WSL2, Podman/Docker, 데이터 I/O를 처리합니다.

## 포함된 도구

| 도구 | 기능 |
| :--- | :--- |
| Prokka | 유전체 빠른 주석 |
| ANI/AAI | 분류학적 동일성 및 종 구분 |
| dbCAN3 | 탄수화물 활성 효소 동정 |
| antiSMASH | 생합성 유전자 클러스터 분석 |
| CheckM2 | 머신러닝 기반 품질 평가 |
| BUSCO | 계통 특이적 완전성 평가 |
| PhyloPhlAn | 전유전체 계통발생 |
| Get Data | NCBI 유전체 일괄 다운로더 |

## GUI 워크플로우

TaxaScope GUI 워크플로우는 다음과 같이 운영됩니다:

1. `TaxaScope.exe`를 실행합니다. 최초 사용 시 `Env Setup`을 클릭하고 인터페이스에 `Env Ready`가 표시될 때까지 기다립니다.
2. `Select Work Directory`를 클릭하고 입력 파일, 데이터베이스, 중간 파일, 출력 결과 및 보고서가 저장될 프로젝트 폴더를 선택합니다.
3. `Download DBs`를 클릭하여 `TaxaScope_Databases`를 채우고 데이터베이스 출처 파일을 작성합니다.
4. GCA/GCF 등록번호를 사용하여 `Get Data`를 통해 입력 데이터를 추가하거나, 로컬 FASTA/FA/FNA/FAA/GBK/GBFF 파일을 작업 디렉토리에 배치합니다.
5. `Genome Stats`, `Prokka`, `CheckM`, `BUSCO`, `dbCAN`, `antiSMASH`, `PhyloPhlAn`, `AAI/ANI`에서 모듈 파라미터를 설정합니다.
6. `Batch`를 열고 `Data Acquisition (Optional)` 및 `Analysis Sequence Setup`을 사용하며, 필요한 경우 보고서 생성을 활성화한 상태로 `DEPLOY COMPLETE WORKFLOW`를 클릭합니다.
7. `Runtime`, `Console`, `File Browser`, `Preview`를 사용하여 진행 상황을 모니터링하고, 로그를 확인하며, 출력 결과를 검토합니다.

전체 설명은 [TaxaScope 사용자 매뉴얼](docs/TaxaScope_User_Manual.md)을 참조하십시오.

## 시스템 요구 사항

| 구성 요소 | 권장 사양 |
| :--- | :--- |
| 운영 체제 | Windows 11 64비트 |
| RAM | 64 GB |
| CPU | 16코어 x86-64 |
| 디스크 | 여유 공간 200 GB (SSD) |

> **참고:** 대규모 유전체 데이터셋에서 CheckM2, BUSCO, PhyloPhlAn 등 메모리 집약적인 모듈을 동시에 실행할 경우 64 GB RAM을 강력히 권장합니다. 50개 이상의 유전체 데이터셋의 경우, 32 GB 미만의 시스템에서는 분석 속도가 현저히 느려지거나 실패할 수 있습니다.

## 시작하기

1. 최신 TaxaScope 릴리스를 다운로드합니다.
2. `TaxaScope.exe`를 실행합니다.
3. 최초 사용 시 `Env Setup`을 클릭하여 실행 환경을 초기화합니다.
4. `Select Work Directory`를 클릭하여 프로젝트 폴더를 선택한 후 `Download DBs`를 클릭합니다.
5. 완전한 GUI 워크플로우 튜토리얼, 출력 구조 및 재현성 보고서 문서는 [TaxaScope 사용자 매뉴얼](docs/TaxaScope_User_Manual.md)을 참조하십시오.

## 논문 및 인용

연구에 TaxaScope를 사용하셨다면 다음을 인용해 주십시오:

> Peng, Y., Jiang, Y., Lee, Y. J., Lee, J. H., Kim, C. Y., & Lee, J. (2026). TaxaScope: a container-native, visualization-centric workstation for genome-based bacterial taxonomy. *Frontiers in Microbiology*, 17, 1809734.

## 라이선스

본 소프트웨어는 학술 목적으로만 제공됩니다. 사용 제한 및 저작권 표시에 관한 전체 내용은 [LICENSE](LICENSE) 파일을 참조하십시오.

KCTC 로고는 KRIBB의 상표이며 오픈소스 라이선스에 포함되지 않습니다.
