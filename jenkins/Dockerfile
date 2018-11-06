FROM jenkins/jenkins:lts
MAINTAINER vic "bxvipsky@gmial.com"

RUN apt-get update -qq && \
    apt-get install -y --on-install-recommends git openjdk-8-jdk unzip curl && \
    apt-get clean

# DOWNLOAD ANDROID SDK
ENV USR_LOCAL /usr/local
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
RUN curl -L "${ANDROID_SDK_URL}" | tar --no-same-owner -xz -C ${USR_LOCAL}
ENV ANDROID_HOME ${USR_LOCAL}/android-sdk-linux
ENV ANDROID_SDK ${USR_LOCAL}/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo "export PATH=${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOMOE}/platform-tools" >> /etc/profile

ENV ANDROID_SDK_COMPONENTS tools,platform-tools,build-tools-26.0.2,android-26,extra-android-m2repository,extra-google-m2repository

RUN echo y | android update sdk --no-ui --all --filter "${ANDROID_SDK_COMPONENTS}"
ENV TERM dumb

# GRADLE INSTALL
WORKDIR ${USR_LOCAL}
ENV GRADLE_URL http://services.gradle.org/distributions/gradle-4.4-all.zip
ADD ${GRADLE_URL} gradle-4.4-bin.zip
RUN unzip gradle-4.4-bin.zip && ln -s gradle-4.4 gradle
ENV GRADLE_HOME ${USR_LOCAL}/gradle

#config gradle path
RUN echo "export PATH=${PATH}:${GRADLE_HOME}/bin" >> /etc/profile
ENV PATH ${PATH}:${GRADLE_HOME}/bin
