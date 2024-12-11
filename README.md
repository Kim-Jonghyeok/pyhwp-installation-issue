```markdown
# Windows 환경에서 `pyhwp` 설치 및 Import 문제 해결

## 문제 설명
Windows 환경에서 `pip`를 사용하여 `pyhwp` 패키지를 설치한 후, Python에서 `import pyhwp`를 시도하면 `ModuleNotFoundError`가 발생했습니다. 이는 패키지가 `.egg` 형식으로 설치되어 Python이 이를 제대로 인식하지 못했기 때문입니다.

### 관찰된 현상
1. `pip install pyhwp` 명령 실행 후, `site-packages` 디렉토리에 아래 두 폴더가 생성되었습니다:
   - `pyhwp-0.1b16.dev0.dist-info`
   - `pyhwp-0.1b16.dev0-py3.8.egg`

2. 일반적인 `pyhwp` 폴더가 없었으며, Python은 `.egg` 폴더를 패키지로 인식하지 못했습니다.

3. `.egg` 경로를 `sys.path`에 수동으로 추가하면 동작하지만, 이는 일회성 해결책으로 불편했습니다.

---

## 해결 방법
`.egg` 폴더를 일반적인 패키지 폴더로 변환하면 문제가 해결됩니다. `.egg` 폴더의 이름을 `pyhwp`로 변경한 후, Python에서 정상적으로 `pyhwp`를 import할 수 있었습니다.

---

## 해결 단계
1. `.egg` 폴더 위치 확인:
   - `site-packages` 경로에서 `pyhwp-0.1b16.dev0-py3.8.egg` 폴더를 찾습니다.
     예: 
     ```
     C:\Program Files\Spyder\Python\Lib\site-packages\pyhwp-0.1b16.dev0-py3.8.egg
     ```

2. `.egg` 폴더 이름 변경:
   - `pyhwp-0.1b16.dev0-py3.8.egg` 폴더를 `pyhwp`로 이름을 변경합니다.

3. Import 테스트:
   - Python에서 아래 코드를 실행하여 정상적으로 동작하는지 확인합니다.
     ```python
     import pyhwp
     print("pyhwp import 성공!")
     ```

---

## 추가 참고 사항
- `.egg` 형식은 최신 Python 환경에서는 비추천되며, 패키지 개발자는 `.whl` 형식으로 배포하는 것을 고려할 수 있습니다.
- 만약 위 방법으로 해결되지 않는 경우, GitHub 소스에서 직접 설치를 시도할 수 있습니다:
  1. [pyhwp GitHub 저장소](https://github.com/mete0r/pyhwp)에서 소스를 다운로드합니다.
  2. 압축을 해제한 디렉토리로 이동 후, 아래 명령을 실행합니다:
     ```bash
     python setup.py install
     ```

- 가상환경을 사용하는 것도 문제를 해결하거나 격리하는 좋은 방법입니다:
  ```bash
  python -m venv pyhwp_env
  pyhwp_env\Scripts\activate
  pip install git+https://github.com/mete0r/pyhwp.git
  ```

---

## 제안 사항
`pyhwp` 패키지 개발자에게 다음 사항을 제안할 수 있습니다:
1. `.egg` 대신 `.whl` 형식으로 배포하여 호환성을 개선.
2. README나 문서에 `.egg` 관련 문제와 해결 방법을 추가.

---

## 요약
`.egg` 폴더를 `pyhwp`로 이름을 변경한 후 문제를 해결할 수 있었습니다. 같은 문제를 겪는 사용자들에게 도움이 되길 바랍니다.
```
