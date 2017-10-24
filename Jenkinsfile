node ('') {
    env.OPENSHIFT_BUILD_NAMESPACE = "cakephp-dev"
    env.DEV_PROJECT = "cakephp-dev"
    env.TEST_PROJECT = "cakephp-test"

    env.APP_NAME = "app1"

    env.OCP_TOKEN = readFile('/var/run/secrets/kubernetes.io/serviceaccount/token').trim()
}

node() {
    stage('SCM Checkout') {
        checkout scm
    }

    stage('Build Image') {
        sh "oc start-build ${env.APP_NAME} --from-dir=. --follow"
    }

    stage ('Deploy to Dev') {
        input "Promote Application to Dev?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.DEV_PROJECT}", namespace: "${env.OPENSHIFT_BUILD_NAMESPACE}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.DEV_PROJECT}", namespace: "${env.OPENSHIFT_BUILD_NAMESPACE}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.DEV_PROJECT}", verifyReplicaCount: true)
    }

    stage ('Deploy to Test') {
        input "Promote Application to Test?"

        openshiftTag (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", destStream: "${env.APP_NAME}", destTag: 'latest', destinationAuthToken: "${env.OCP_TOKEN}", destinationNamespace: "${env.TEST_PROJECT}", namespace: "${env.DEV_PROJECT}", srcStream: "${env.APP_NAME}", srcTag: 'latest')

        openshiftVerifyDeployment (apiURL: "${env.OPENSHIFT_API_URL}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.TEST_PROJECT}", verifyReplicaCount: true)
    }

}
