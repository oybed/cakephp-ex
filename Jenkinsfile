node ('') {
    env.OPENSHIFT_BUILD_NAMESPACE = "cakephp-dev"
    env.DEV_PROJECT = "cakephp-dev"
    env.TEST_PROJECT = "cakephp-test"
    env.STAGE1_PROJECT = "cakephp-stage1"
    env.STAGE2_PROJECT = "cakephp-stage2"
    env.STAGE3_PROJECT = "cakephp-stage3"
    env.STAGE4_PROJECT = "cakephp-stage4"
    env.STAGE5_PROJECT = "cakephp-stage5"

    env.APP_NAME = "app1"

    env.OCP_TOKEN = readFile('/var/run/secrets/kubernetes.io/serviceaccount/token').trim()
}

node() {
    stage('SCM Checkout') {
        checkout scm
    }

    stage('Build Image and Deploy to Dev') {
        sh "oc start-build ${env.APP_NAME} --from-dir=. --follow"
    }

    stage ('Deploy to Test') {
        input "Promote Application to Test?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.TEST_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.TEST_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Stage1') {
        input "Promote Application to Stage1?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.STAGE1_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.STAGE1_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Stage2') {
        input "Promote Application to Stage2?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.STAGE2_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.STAGE2_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Stage3') {
        input "Promote Application to Stage3?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.STAGE3_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.STAGE3_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Stage4') {
        input "Promote Application to Stage4?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.STAGE4_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.STAGE4_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Stage5') {
        input "Promote Application to Stage5?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.STAGE5_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.STAGE5_PROJECT}", verifyReplicaCount: true)
    }

}
