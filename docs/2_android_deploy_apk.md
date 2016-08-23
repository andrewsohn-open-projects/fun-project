[![Build Status](https://travis-ci.org/hivelab-open-projects/fun-project.svg?branch=master)](https://travis-ci.org/hivelab-open-projects/fun-project)
스터디_2
====

## 배포버전 APK 추출

APK 파일을 추출하기 위해서는 먼저 `keytool`을 사용하여 private signing key를 생성해야한다. [참고URL](https://facebook.github.io/react-native/docs/signed-apk-android.html) 

커맨드창에서 아래와 같은 명령어를 쳐 .keystore 파일을 생성한다. 비밀번호의 유의한다.  

	$ keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

### gradle 설정 

1. my-release-key.keystore 같은 이름으로 keystore 파일이 생성 되었다면 해당 파일을 `android/app` 폴더 하위에 위치 시킨다.

2. `android/gradle.properties` 파일을 열어 아래 gradle 글로벌 변수들을 설정한다. (위 keytool로 생성한 keystore 비밀번호를 ****에 삽입한다) 

		MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
		MYAPP_RELEASE_KEY_ALIAS=my-key-alias
		MYAPP_RELEASE_STORE_PASSWORD=*****
		MYAPP_RELEASE_KEY_PASSWORD=*****

3. `android/app/build.gradle`을 열어 android 속성 내부에 아래와 같이 추가시켜준다. 

		...
		android {
		    ...
		    defaultConfig { ... }
		    signingConfigs {
		        release {
		            storeFile file(MYAPP_RELEASE_STORE_FILE)
		            storePassword MYAPP_RELEASE_STORE_PASSWORD
		            keyAlias MYAPP_RELEASE_KEY_ALIAS
		            keyPassword MYAPP_RELEASE_KEY_PASSWORD
		        }
		    }
		    buildTypes {
		        release {
		            ...
		            signingConfig signingConfigs.release
		        }
		    }
		}
		...

### release APK 추출

`android`폴더 하위에서 아래 커맨드 명령어를 통해 release APK를 추출시켜준다.  

	$ .\gradlew assembleRelease

### 추출된 APK 파일 경로 

추출이 완료되고 난 뒤, `android/app/build/outputs/apk` 하위로 `app-release.apk`의 이름으로 생성된 것을 확인 할 수 있다.