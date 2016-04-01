FROM menglj/docker-imrad-dev:gst

MAINTAINER meng lingjie"meng.lj@gmail.com"

# Install java7
RUN apt-get install -y software-properties-common && add-apt-repository -y ppa:webupd8team/java && apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java7-installer

# Install Deps
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes expect git wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 python curl

# Setup environment
ENV ANDROID_SDK_URL="https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz" \
    ANDROID_BUILD_TOOLS_VERSION=23.0.2 \
    ANDROID_APIS="android-10,android-15,android-16,android-17,android-18,android-19,android-20,android-21,android-22,android-23,android-N" \
    ANDROID_HOME="/opt/android-sdk-linux"

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:/opt/tools

# Install Android SDK
RUN cd /opt && wget --output-document=android-sdk.tgz --quiet ${ANDROID_SDK_URL} && tar xzf android-sdk.tgz && rm -f android-sdk.tgz && chown -R root.root android-sdk-linux

# Install sdk elements
#COPY tools /opt/tools
#ENV PATH ${PATH}:/opt/tools
#RUN ["/opt/tools/android-accept-licenses.sh", "android update sdk --all --force --no-ui --filter platform-tools,tools,build-tools-23.0.2,build-tools-21,build-tools-21.0.1,build-tools-21.0.2,build-tools-21.1,build-tools-21.1.1,build-tools-21.1.2,build-tools-22,build-tools-22.0.1,android-21,android-22,android-23,addon-google_apis_x86-google-21,addon-google_apis_x86-google-23,extra-android-support,extra-android-m2repository,extra-google-m2repository,extra-google-google_play_services,sys-img-armeabi-v7a-android-21,sys-img-armeabi-v7a-android-23"]
#RUN echo "y\ny" | android update sdk --all --no-ui --filter platform-tools,${ANDROID_APIS},build-tools-${ANDROID_BUILD_TOOLS_VERSION},sys-img-armeabi-v7a-android-15,sys-img-armeabi-v7a-android-23


# --- Install Android SDKs and other build packages

# Other tools and resources of Android SDK
#  you should only install the packages you need!
# To get a full list of available options you can use:
#  android list sdk --no-ui --all --extended
# (!!!) Only install one package at a time, as "echo y" will only work for one license!
#       If you don't do it this way you might get "Unknown response" in the logs,
#         but the android SDK tool **won't** fail, it'll just **NOT** install the package.
RUN echo y | android update sdk --no-ui --all --filter platform-tools
RUN echo y | android update sdk --no-ui --all --filter extra-android-support

# SDKs
# Please keep these in descending order!
RUN echo y | android update sdk --no-ui --all --filter ${ANDROID_APIS}

# google apis
# Please keep these in descending order!
RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-23
RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-22
RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-21

# build tools
# Please keep these in descending order!
RUN echo y | android update sdk --no-ui --all --filter build-tools-24.0.0-preview
RUN echo y | android update sdk --no-ui --all --filter build-tools-${ANDROID_BUILD_TOOLS_VERSION}

# Android System Images, for emulators
# Please keep these in descending order!
RUN echo y | android update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-23
RUN echo y | android update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-15

# Extras
RUN echo y | android update sdk --no-ui --all --filter extra-android-m2repository
RUN echo y | android update sdk --no-ui --all --filter extra-google-m2repository
RUN echo y | android update sdk --no-ui --all --filter extra-google-google_play_services

