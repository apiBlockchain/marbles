node {
    dir("/root/"){
    checkout scm

    env.DOCKER_API_VERSION="1.23"
    appName = "blockchain/marbles-app"
    registryHost = "finance.icp.sc.ibm.com:8500/"
    imageName = "${registryHost}${appName}:${env.BUILD_ID}"
    env.BUILDIMG=imageName
    docker.withRegistry('https://finance.icp.sc.ibm.com:8500/', 'docker'){
    stage "Build"

        def pcImg = docker.build("finance.icp.sc.ibm.com:8500/blockchain/marbles-app:${env.BUILD_ID}", "-f scripts/Dockerfile .")
       // sh "cp /root/.dockercfg ${HOME}/.dockercfg"
        pcImg.push()

    input 'Do you want to proceed with Deployment?'
    stage "Deploy"

        sh "kubectl set image deployment/demoapp-demochart demochart=${imageName}"
        sh "kubectl rollout status deployment/demoapp-demochart"
}
}
}

