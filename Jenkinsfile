stage('Deploy to Kubernetes') {
    steps {
        script {
            // Define your Kubernetes credentials and Docker image details
            def kubeCredsId = 'k8scred'
            def dockerImage = 'my-node-app'
            def deploymentName = 'my-node-app'
            def registry = 'jeevac33'
            def namespace = 'default' // Change if you're using a different namespace

            // Use Kubernetes credentials
            withCredentials([file(credentialsId: kubeCredsId, variable: 'KUBECONFIG')]) {
                sh '''
                # Switch to the appropriate Kubernetes context
                kubectl config use-context my-cluster

                # Update the Kubernetes deployment with the new Docker image
                kubectl set image deployment/${deploymentName} ${dockerImage}=${registry}/${dockerImage}:${BUILD_NUMBER} --namespace=${namespace}

                # Wait for the rollout to complete
                kubectl rollout status deployment/${deploymentName} --namespace=${namespace}
                '''
            }
        }
    }
}
