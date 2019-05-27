

#!/bin/sh

#set -x

source /home/q/tools/fault_drilling/download.sh

JAVA_HOME=/home/q/java/default
FAULT_HOME=/home/q/tools/fault_drilling
AGENT_JAR_PATH=${FAULT_HOME}/agent.jar
CORE_JAR_PATH=${FAULT_HOME}/core.jar

APP_CODE=$1
APP_PORT=$2
MODE=$3
SERVER_HOSTS=$4
SERVER_PORT=$5
CLIENT_HOST=$6

pid=$(sudo netstat -anp | grep ${APP_PORT} | grep java | grep LISTEN | awk '{print $7}' | cut -d/ -f1)

echo "pid: ${pid}"

if [ "${MODE}"x = "TEST"x ]
then
    args={\"appCode\":\"${APP_CODE}\",\"serverHost\":\"${SERVER_HOSTS}\",\"serverPort\":${SERVER_PORT},\"clientHost\":\"${CLIENT_HOST}\"}
    echo "-----------args: "${args}
    sudo -utomcat ${JAVA_HOME}/bin/java -jar ${FAULT_HOME}/binder.jar ${pid} ${AGENT_JAR_PATH} ${CORE_JAR_PATH} ${args}
else
    echo "-------no server mode"
    sudo -utomcat ${JAVA_HOME}/bin/java -jar ${FAULT_HOME}/binder.jar ${APPCODE} ${pid}
fi
