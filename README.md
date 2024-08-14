1. 깃헙 레포 생성
2. actions > set up a workflow yourself 클릭
3. yml 파일명 수정
4. yml 파일 작성
5. commit
6. action 에서 돌아가는 것 확인

*) re-run job, 빌드하고 있는 중에 stop 가능(cancel workflow)
```yml
# 오래걸림.. action 취소하는 것 실습
- name: 파일 찾기!!
  run: find / -name 'test.py'
```

# YML 파일 작성 방법
```yml
name: Hello Github Action # github action 이름

# 어떤 이벤트(push, pull_request) 가 일어났을 때에 jobs를 실행, 다중 이벤트 처리 가능 -> 공식문서 보기
on: [push] # push 했을 때 jobs 실행

# 이벤트가 일어났을 때, 실행될 작업들
jobs:
    build : # 작업 단위
        # 어디서 실행할지 OS(Windows, MacOS, Ubuntu), 버전 -> 공식문서 보기
        runs-on: ubuntu-latest # 우분투 버전 명시 가능(latest : 최근 버전)
        steps:
            # run 뒤에는 실제 작동하는 코드 넣어야 함
            - name: Hello World 출력!!
              run: echo Hello World
            - name: 디렉토리 출력!!
              run: ls -al
            - name: 파이썬 버전 출력!!
              run: python -V
            # python 파일 실행
            # uses: 다른 사람이 만들어 놓은 액션 가지고 옴 / checkout 이라는 액션 사용
              # 없는 경우 아무것도 없는 os에서 입력한 run 만 실행
              # 있는 경우 아무것도 없는 os에서 우리 코드를 클론 다운로드 받아서 실행
            - uses: actions/checkout@v3 
            - name: 파이썬 실행!!
              run: python test.py
            # 오래걸림.. action 취소하는 것 실습
            # - name: 파일 찾기!!
            #   run: find / -name 'test.py'
```

## python 파일 실행 방법
1. py 파일 생성
2. yml 파일 > steps에 작성
   ```yml
   - uses: actions/checkout@v3 # 추가해야 함, 추가 안하면 Error, 했을 때 안했을 때 파일이 있는지 없는지 확인하기
   - name: 디렉토리 출력!!
     run: ls -al
   - name: 파이썬 실행!!
     run: python test.py
   ```
3. commit
4. action 에서 돌아가는 것 확인

## python 패키지 설치 확인
```yml
- name: 파이썬 패키지 설치 확인
 run: pip list
```

## python 패키지 설치
1. requirements.txt 생성
2. 필요한 패키지 입력하기
```txt
beautifulsoup4
requests == 버전작성
```

# 공식 문서
- yml 파일 수정에 들어가면 Commit 아래에 Workflow 옆에 있음
