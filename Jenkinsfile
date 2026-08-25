pipeline {
    agent any

    environment {
        RELEASESDK = "5.0.0.43"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build mic') {
            steps {
                sh '''
                    TAG_NAME=$(git describe --tags --exact-match 2>/dev/null || echo "$GIT_BRANCH")
                    export VERSION=$(echo $TAG_NAME | cut -d "-" -f 2)
                    export RELEASE=$(echo $TAG_NAME | cut -d "-" -f 3)
                    export EXTRA_NAME=-$(echo $TAG_NAME | cut -d "-" -f 4-)

                    chmod a+w $PWD

                    docker run -u root --rm --privileged \
                        --mount type=bind,src=$PWD,dst=/share \
                        --env-file env.list \
                        -e VERSION -e RELEASE -e EXTRA_NAME \
                        coderus/sailfishos-platform-sdk:$RELEASESDK \
                        /bin/bash -c "/share/scripts/create-image.sh --release $RELEASE --version $VERSION"
                '''
            }
        }

        stage('Package artifact') {
            steps {
                sh '''
                    TAG_NAME=$(git describe --tags --exact-match 2>/dev/null || echo "$GIT_BRANCH")
                    export VERSION=$(echo $TAG_NAME | cut -d "-" -f 2)
                    export RELEASE=$(echo $TAG_NAME | cut -d "-" -f 3)
                    export EXTRA_NAME=$(echo $TAG_NAME | cut -d "-" -f 4-)

                    ARTIFACT=sailfish-release-halium-krypton-$RELEASE-$VERSION-$EXTRA_NAME.tar.bz2

                    tar -cvjSf $ARTIFACT -C ./build/mic/sfe*/ .
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '*.tar.bz2', fingerprint: true
        }
    }
}
