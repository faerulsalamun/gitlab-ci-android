# gitlab-ci-cd-testfairy-android

A simple .gitlab-ci.yml would look like this:

```
image: faerulsalamun/gitlab-ci-cd-testfairy-android

before_script:
    - export TESFAIRY_TOKEN=YOUR_TOKEN_TESTFAIRY
    - export KEYSTORE=/home/testfairy.jks
    - export STOREPASS=testfairy
    - export ALIAS=testfairy
    - chmod a+x /home/testfairy.sh

stages:
  - build

debug:
  stage: build
  except:
    - release
  script:
    - ./gradlew assembleDebug
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
    - /home/testfairy.sh app/build/outputs/apk/app-release.apk
  artifacts:
    paths:
    - app/build/outputs/apk/app-release.apk
```
