# Docker Android Build Box

[![Build Status](https://travis-ci.org/P1-Ro/docker-android-build-box.svg?branch=master)](https://travis-ci.org/P1-Ro/docker-android-build-box) [![](https://images.microbadger.com/badges/version/theglow666/android-build-box.svg)](https://microbadger.com/images/theglow666/android-build-box "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/theglow666/android-build-box.svg)](https://microbadger.com/images/theglow666/android-build-box "Get your own image badge on microbadger.com")

[![docker icon](https://dockeri.co/image/theglow666/android-build-box)](https://hub.docker.com/r/theglow666/android-build-box/)



## Introduction

A **docker** image build with **Android** build environment.


## What Is Inside

It includes the following components:

* ~~Ubuntu 18.04~~ [Alpine with OpenJDK](https://hub.docker.com/r/adoptopenjdk/openjdk8/tags?page=1&name=alpine-slim&ordering=-name)
* Android SDK ~~16 17 18 19 20 21 22 23 24 25~~ 26 27 28 29
* Android build tools:
  * ~~17.0.0~~
  * ~~18.1.1~~
  * ~~19.1.0~~
  * ~~20.0.0~~
  * ~~21.1.2 22.0.1~~
  * ~~23.0.1 23.0.2 23.0.3~~
  * ~~24.0.0 24.0.1 24.0.2 24.0.3~~
  * ~~25.0.0 25.0.1 25.0.2 25.0.3~~
  * ~~26.0.0 26.0.1 26.0.2~~
  * 27.0.1 27.0.2 27.0.3
  * 28.0.1 28.0.2 28.0.3
  * 29.0.2
* ~~Android NDK r20~~
* extra-android-m2repository
* extra-google-m2repository
* extra-google-google\_play\_services
* Google API add-ons
* ~~Android Emulator~~
* Constraint Layout
* ~~TestNG~~
* ~~Python 2, Python 3~~
* ~~Node.js, npm, React Native~~
* ~~Ruby, RubyGems~~
* ~~fastlane~~
* ~~Kotlin 1.3~~
* ~~Flutter 1.5.4~~


## Docker Pull

The docker image is publicly automated build on [Docker Hub](https://hub.docker.com/r/theglow666/android-build-box/) based on the Dockerfile in this repo, so there is no hidden stuff in it. To pull the latest docker image:

    docker pull theglow666/android-build-box:release

**Importannt:** Use actual tag to sepecific a stable version instead of `release`.  Checkout **[Releases](releases)** to see all the available tags.

## Usage

### Use the image to build an Android project

You can use this docker image to build your Android project with a single docker command:

    cd <android project directory>  # change working directory to your project root directory.
    docker run --rm -v `pwd`:/project theglow666/android-build-box bash -c 'cd /project; ./gradlew build'

Run docker image with interactive bash shell:

    docker run -v `pwd`:/project -it theglow666/android-build-box bash


### Use the image for a Bitbucket pipeline

If you have an Android project in a Bitbucket repository and want to use its pipeline to build it, you can simply specify this docker image.
Here is an example of `bitbucket-pipelines.yml`

    image: theglow666/android-build-box:tagname

    pipelines:
      default:
        - step:
            caches:
              - gradle
              - gradlewrapper
              - androidavd
            script:
              - bash ./gradlew assemble
    definitions:
      caches:
        gradlewrapper: ~/.gradle/wrapper
        androidavd: $ANDROID_HOME/.android/avd

The caches are used to [store downloaded dependencies](https://confluence.atlassian.com/bitbucket/caching-dependencies-895552876.html) from previous builds, to speed up the next builds.

## Docker Build Image

If you want to build the docker image by yourself, you can use following command.
The image itself is around 2 GB, check your free disk space before building it.

    docker build -t android-build-box .

## Tags
Check releases for tags



## Contribution

If you want to enhance this docker image or fix something, feel free to send [pull request](https://github.com/P1-Ro/docker-android-build-box/pull/new/master).


## References

* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
* [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* [Build your own image](https://docs.docker.com/engine/getstarted/step_four/)
* [uber android build environment](https://hub.docker.com/r/uber/android-build-environment/)
* [Refactoring a Dockerfile for image size](https://blog.replicated.com/refactoring-a-dockerfile-for-image-size/)

