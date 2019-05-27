###

#!/bin/sh

SO_TIMEOUT=60

DOWNLOAD_URL_PREFIX="http://^^^^/nexus/service/local/repositories"

BINDER_JAR_VERSION=$7
AGENT_JAR_VERSION=$8
CORE_JAR_VERSION=$9

JAR_FILES=(
${BINDER_JAR_VERSION}
${AGENT_JAR_VERSION}
${CORE_JAR_VERSION}
)


# exit shell with err_code
# $1 : err_code
# $2 : err_msg
exit_on_err()
{
    echo "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
    [[ ! -z "${2}" ]] && echo "${2}" 1>&2
    exit ${1}
}


cd /home/q/tools/fault_drilling/
# download from nexus
for jarPath in ${JAR_FILES[@]}
do
if [ -n" ${jarPath}" ];then
    jarwithv=${jarPath##*/}
    echo "downloading... ${jarwithv}";
    url=${DOWNLOAD_URL_PREFIX}${jarPath}
    curl --connect-timeout ${SO_TIMEOUT} -# -sO ${url}
    result=$(echo $jarwithv | grep "binder")
    if [[ "$result" != "" ]]
    then
    sudo mv ./${jarwithv} binder.jar
    sudo chmod 755 binder.jar
    fi
    result=$(echo $jarwithv | grep "agent")
    if [[ "$result" != "" ]]
    then
    sudo mv ./${jarwithv} agent.jar
    sudo chmod 755 agent.jar
    fi
    result=$(echo $jarwithv | grep "core")
    if [[ "$result" != "" ]]
    then
    sudo mv ./${jarwithv} core.jar
    sudo chmod 755 core.jar
    fi \
    || exit_on_err 1 "download ${jarPath} failed!"
fi
done
