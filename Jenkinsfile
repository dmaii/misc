node("applications") {
  deleteDir()
  stage('kickwheel') {
    //checkout([$class: 'GitSCM', branches: [[name: '*/sauce-connect']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'sauce-connect']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'git@github.com:metamx/frontend-scripts.git']]])
    dir('sauce-connect/scripts/deployment/kickwheel') {
      //python kickwheel.py -g e2e
      echo 172.168.1.1 > address.txt
    }
  }
  stage('sauce connect start') {
    dir('sauce-connect/scripts/deployment/sauce-connect') {
      sh GHOSTBUSTERS_DASH_HOST=`cat address.txt`
      //python sauce_connect_start.py --tunnel-domains=${GHOSTBUSTERS_DASH_HOST} --user=${GHOSTBUSTER_SAUCE_USERNAME} --api-key=${GHOSTBUSTER_SAUCE_ACCESS_KEY}
      echo ${GHOSTBUSTERS_DASH_HOST}
      echo ${GHOSTBUSTER_SAUCE_USERNAME}
      echo ${GHOSTBUSTER_SAUCE_ACCESS_KEY}
    }
  }

  stage('ghostbuster') {
    checkout([$class: 'GitSCM', branches: [[name: '*/ghostbuster']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'ghostbuster']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'git@github.com:metamx/ghostbuster.git']]])
    GHOSTBUSTER_SAUCE_TUNNEL=`cat sc_tunnel_id.txt`
    dir('ghostbuster') {
      echo ${GHOSTBUSTER_SAUCE_TUNNEL}
      //sh ./scripts/docker-build
      //sh ./scripts/docker-run-sauce
    }
  }
}
