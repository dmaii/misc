node {
  deleteDir()

  stage('kickwheel') {
//    checkout([$class: 'GitSCM', branches: [[name: '*/sauce-connect']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'sauce-connect']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '473f0330-96e0-4384-83d3-0610730f1fe5', url: 'git@github.com:metamx/frontend-scripts.git']]])
    //python ./sauce-connect/scripts/deployment/kickwheel.py -g e2e
    sh 'echo 172.168.1.1 > address.txt'
  }

  stage('sauce connect start') {
    sh 'GHOSTBUSTERS_DASH_HOST=`cat address.txt`'
    sh 'echo alkdfjalkfjaklfwe > sc_tunnel_id.txt'
    //python ./sauce-connect/scripts/deployment/sauce_connect_start.py --tunnel-domains=${GHOSTBUSTERS_DASH_HOST} --user=${GHOSTBUSTER_SAUCE_USERNAME} --api-key=${GHOSTBUSTER_SAUCE_ACCESS_KEY}
    sh 'echo ${GHOSTBUSTERS_DASH_HOST}'
    sh 'echo ${GHOSTBUSTER_SAUCE_USERNAME}'
    sh 'echo ${GHOSTBUSTER_SAUCE_ACCESS_KEY}'
  }

  stage('ghostbuster') {
//    checkout([$class: 'GitSCM', branches: [[name: '*/ghostbuster']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'ghostbuster']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '473f0330-96e0-4384-83d3-0610730f1fe5', url: 'git@github.com:metamx/ghostbuster.git']]])
    sh 'mkdir ghostbuster'
    sh 'GHOSTBUSTER_SAUCE_TUNNEL=`cat sc_tunnel_id.txt`'
    dir('ghostbuster') {
      sh 'echo ${GHOSTBUSTER_SAUCE_TUNNEL}'
      //sh ./scripts/docker-build
      //sh ./scripts/docker-run-sauce
    }
  }
}
