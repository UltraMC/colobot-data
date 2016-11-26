properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '30', artifactNumToKeepStr: '10']]])

node('master') {
    stage 'Pull changes'
    checkout scm

    stage 'Build data'
    sh 'mkdir -p build'
    dir('build') {
        sh '''
            cmake -DCMAKE_INSTALL_PREFIX=/install -DCOLOBOT_INSTALL_DATA_DIR=/install/data ..
            make
            rm -rf install
            DESTDIR=. make install
        '''
    }

    stage 'Archive data'
    sh 'rm -f data.zip'
    zip zipFile: 'data.zip', archive: true, dir: 'build/install'
}