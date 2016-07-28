# gitlab-ci-cd-testfairy-android

A simple .gitlab-ci.yml would look like this:

```
stages:
  - build

debug:
  stage: build
  except:
    - release
  script:
    - ./gradlew assembleDebug
    - export TESFAIRY_TOKEN=YOUR_TOKEN_TESTFAIRY
    - export KEYSTORE=/home/testfairy.jks
    - export STOREPASS=testfairy
    - export ALIAS=testfairy
    - chmod a+x /home/testfairy.sh
    - /home/testfairy.sh app/build/outputs/apk/app-debug.apk
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk

release:
  stage: build
  only:
    - release
  script:
    - ./gradlew assembleRelease
    - export TESFAIRY_TOKEN=YOUR_TOKEN_TESTFAIRY
    - export KEYSTORE=/home/testfairy.jks
    - export STOREPASS=testfairy
    - export ALIAS=testfairy
    - chmod a+x /home/testfairy.sh
    - /home/testfairy.sh app/build/outputs/apk/app-release.apk
  artifacts:
    paths:
    - app/build/outputs/apk/app-release.apk
```
