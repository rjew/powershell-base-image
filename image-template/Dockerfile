ARG BASE_IMAGE
FROM ${BASE_IMAGE}

WORKDIR /root

ARG SYSTEM_PACKAGES_FILE=system-packages.txt
COPY ${SYSTEM_PACKAGES_FILE} .

RUN packages=$(cat ${SYSTEM_PACKAGES_FILE} | sed 's/ /-/' | uniq | paste -d' ' -); \
    if [ -n "${packages}" ]; then tdnf install -y ${packages}; fi

ARG PACKAGES_FILE=packages.txt
COPY ${PACKAGES_FILE} requirements.psd1

RUN pj=$(cat requirements.psd1); if [ -n "${pj}" ]; then \
    pwsh -command '$ErrorActionPreference="Stop"; Invoke-PSDepend -Path "/root/requirements.psd1" -Confirm:$false'; fi
