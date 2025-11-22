FROM jenkins/jenkins:lts-jdk17

USER root

RUN apt-get update && apt-get install -y lsb-release curl gnupg

RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
    https://download.docker.com/linux/debian/gpg

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
    https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && apt-get install -y docker-ce-cli

# إنشاء docker group وإضافة jenkins إليه
RUN groupadd -g 999 docker || true \
    && usermod -aG docker jenkins

# ضبط صلاحيات مجلد workspace إذا تحتاج
RUN mkdir -p /var/jenkins_home/.go_cache \
    && chown -R jenkins:jenkins /var/jenkins_home/.go_cache

USER jenkins
