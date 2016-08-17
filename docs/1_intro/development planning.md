[![Build Status](https://travis-ci.org/hivelab-open-projects/fun-project.svg?branch=master)](https://travis-ci.org/hivelab-open-projects/fun-project)
스터디_1
====

## Windows OS에서 Android 개발환경 구축

먼저는 Node.js와 Python2가 설치되어 있어야 React Native를 정상적으로 구동/사용 할 수 있다. 다음은 [Chocolatey](https://chocolatey.org)를 사용하여 Node.js와 Python2를 설치한다.

	$ choco install nodejs.install
	$ choco install python2

Node.js를 설치하였다면 Node.js 패키지 매니저 NPM 명령어를 사용하여 React Native를 설치한다.

	$ npm install -g react-native-cli

위 설치를 마쳤다면 실제로 React Native 어플리케이션을 생성해 볼 수 있다. 원하는 어플리케이션 경로에 커멘드창으로 접근하여 아래와 같은 명령어를 본다.

	$ react-native init apps
	$ cd apps

생성을 마쳤다면 React Native Android App을 개발환경에서 실행해 본다. 

	$ react-native run-android 

> `run-android` 명령어를 실행하기 전에 AVD 매니저를 통해 안드로이드 가상 디바이스를 먼저 실행시킨 후에 진행해야 한다. 

###주의 사항 

구축 시에 몇가지 문제점을 발견 할 수 있었는데 아래와 같은 경우를 참고하여 오류를 
 
1. install된 SDK 폴더에 ADB 실행 파일이 없는 경우
	- /platform-tools/ 내 위치하고 있다. 없는 경우 수동 설치를 해줘야 함
2. SDK에서 해당 개발환경의 android 버전이 없을 경우 (default 버전은 API 23)
	- SDK 매니저에서 해당 버전을 설치해줘야함
3.  Android Studio가 실행되어 있어 adb 및 다른 중요 기능들의 포트를 중복 사용하는 경우
	- Android Studio를 닫은 상태에서 JS 소스는 에디터(sublime text) 실행 및 디버깅은 CMD 커멘트창에서 진행한다. `run-android` 명령어를 실행하기 전에 AVD 매니저를 통해 안드로이드 가상 디바이스를 먼저 실행시킨 후에 진행해야 한다. 
