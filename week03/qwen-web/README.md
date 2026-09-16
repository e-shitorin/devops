# Week 03 - Shell Scripting

## 1. 실습 환경

- Ubuntu (WSL)
- Python 3
- Ollama
- Qwen3 0.6B

## 2. Qwen w/ Ollama

### Ollama 설치 확인

```bash
ollama --version
python3 --version
````

### Qwen 모델 다운로드

```bash
ollama pull qwen3:0.6b
ollama list
```

### Ollama API 확인

```bash
curl -fsS http://127.0.0.1:11434/api/tags
```

Qwen 모델의 API 응답을 확인하였다.

## 3. Python Web Application

`chat.py`를 실행하여 로컬 웹 애플리케이션을 확인하였다.

```bash
python3 chat.py
```

실행 결과:

```text
웹 접속: http://localhost:8000
사용 모델: qwen3:0.6b
```

## 4. Shell Script

### start.sh

```bash
#!/bin/bash
cd "$(dirname "$0")" || exit 1

if ! command -v python3 >/dev/null 2>&1; then
    echo "Python3를 먼저 설치하세요." >&2
    exit 1
fi

exec python3 chat.py
```

실행 권한을 설정하였다.

```bash
chmod u+x start.sh
```

### 실행

```bash
./start.sh
```

실행 결과:

```text
웹 접속: http://localhost:8000
사용 모델: qwen3:0.6b
```

## 5. 환경 변수

### start_with_export.sh

```bash
export MODEL="qwen3:0.6b"
exec ./start.sh
```

`MODEL` 환경 변수를 설정하여 실행하였다.

### start_with_export_2.sh

```bash
export WEB_PORT="8080"
exec ./start.sh
```

`WEB_PORT` 환경 변수를 설정하여 8080 포트에서 실행하였다.

실행 결과:

```text
웹 접속: http://localhost:8080
사용 모델: qwen3:0.6b
```

## 6. 수업 내용 정리

* 셸 스크립트의 기본 구조
* shebang (`#!/bin/bash`)
* 실행 권한 (`chmod`)
* `$0`와 `dirname`
* 명령어 치환 `$(...)`
* 환경 변수 `export`
* 종료 상태 코드 `$?`
* `||`를 이용한 오류 처리
* `if` 조건문
* `command -v`를 이용한 명령어 존재 여부 확인
* `exec`를 이용한 프로세스 실행

## 7. 실습 결과

* Ollama 설치 및 실행 확인
* `qwen3:0.6b` 모델 다운로드 완료
* Python 웹 애플리케이션 실행 확인
* `start.sh` 작성 및 실행 확인
* `MODEL` 환경 변수 적용 확인
* `WEB_PORT=8080` 환경 변수 적용 확인
* HTTP 200 응답 확인
