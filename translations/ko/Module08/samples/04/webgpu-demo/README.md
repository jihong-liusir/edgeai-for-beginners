<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7a474b8e201d5316c0095cdbc3bf0555",
  "translation_date": "2025-09-24T10:45:54+00:00",
  "source_file": "Module08/samples/04/webgpu-demo/README.md",
  "language_code": "ko"
}
-->
# WebGPU + ONNX Runtime 데모

이 데모는 WebGPU를 활용한 하드웨어 가속과 ONNX Runtime Web을 사용하여 브라우저에서 AI 모델을 실행하는 방법을 보여줍니다.

## 데모의 주요 내용

- **브라우저 기반 AI**: 모델을 브라우저 내에서 완전히 실행
- **WebGPU 가속**: 가능한 경우 하드웨어 가속 추론
- **개인정보 보호 우선**: 데이터가 기기를 벗어나지 않음
- **설치 불필요**: 호환 브라우저에서 바로 작동
- **유연한 대체**: WebGPU가 없을 경우 CPU로 자동 전환

## 요구 사항

**브라우저 호환성:**
- WebGPU가 활성화된 Chrome/Edge 113+
- WebGPU 상태 확인: `chrome://gpu`
- WebGPU 활성화: `chrome://flags/#enable-unsafe-webgpu`

## 데모 실행 방법

### 옵션 1: 로컬 서버 (권장)

```cmd
# Navigate to the demo directory
cd Module08\samples\04\webgpu-demo

# Start a local server
python -m http.server 5173

# Open browser to http://localhost:5173
```

### 옵션 2: VS Code Live Server

1. VS Code에서 "Live Server" 확장 설치
2. `index.html`을 오른쪽 클릭 → "Open with Live Server" 선택
3. 브라우저에서 데모가 자동으로 열림

## 데모에서 확인할 수 있는 내용

1. **WebGPU 감지**: 브라우저 호환성 확인
2. **모델 로딩**: MNIST 분류기를 다운로드하고 초기화
3. **추론 실행**: 샘플 데이터를 기반으로 예측 실행
4. **성능 지표**: 로드 시간과 추론 속도 표시
5. **결과 표시**: 예측 신뢰도와 원시 출력값

## 예상 성능

| 실행 제공자       | 모델 로드 | 추론       | 비고               |
|-------------------|-----------|------------|--------------------|
| **WebGPU**        | ~2-5초    | ~10-50ms   | 하드웨어 가속      |
| **CPU (WASM)**    | ~2-5초    | ~50-200ms  | 소프트웨어 대체    |

## 문제 해결

**WebGPU가 사용 불가능한 경우:**
- Chrome/Edge 113+로 업데이트
- `chrome://flags`에서 WebGPU 활성화
- GPU 드라이버가 최신 상태인지 확인
- 데모는 자동으로 CPU로 전환됨

**로드 오류:**
- HTTP를 통해 제공 중인지 확인 (file:// 아님)
- 모델 다운로드를 위한 네트워크 연결 확인
- ONNX 모델이 CORS에 의해 차단되지 않았는지 확인

**성능 문제:**
- WebGPU는 CPU에 비해 상당한 속도 향상을 제공
- 첫 실행은 모델 다운로드로 인해 느릴 수 있음
- 이후 실행은 브라우저 캐시를 사용

## Foundry Local과의 통합

이 WebGPU 데모는 Foundry Local과의 통합을 통해 다음을 보여줍니다:

- **클라이언트 측 추론**으로 최상의 개인정보 보호
- **오프라인 기능**으로 인터넷이 없을 때도 작동  
- **엣지 배포**로 자원이 제한된 환경에서 활용
- **하이브리드 아키텍처**로 로컬 및 서버 추론 결합

프로덕션 애플리케이션을 위해 고려할 사항:
- 서버 측 추론을 위해 Foundry Local 사용
- 클라이언트 측 전처리/후처리를 위해 WebGPU 사용
- 로컬/원격 추론 간 지능형 라우팅 구현

## 기술적 세부 사항

**사용된 모델:**
- MNIST 숫자 분류기 (ONNX 형식)
- 입력: 28x28 그레이스케일 이미지
- 출력: 10개 클래스의 확률 분포
- 크기: ~500KB (빠른 다운로드)

**ONNX Runtime Web:**
- GPU 가속을 위한 WebGPU 실행 제공자
- CPU 대체를 위한 WASM 실행 제공자
- 자동 최적화 및 그래프 최적화

**브라우저 API:**
- 하드웨어 접근을 위한 WebGPU
- 백그라운드 처리를 위한 Web Workers (향후 개선 예정)
- 효율적인 계산을 위한 WebAssembly

## 다음 단계

- 사용자 지정 ONNX 모델로 시도
- 실제 이미지 업로드 및 분류 구현
- 더 큰 모델을 위한 스트리밍 추론 추가
- 카메라/마이크 입력과 통합

---

