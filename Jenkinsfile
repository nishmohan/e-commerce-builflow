pipeline {
    agent  any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('mlal-dockerhub-cred')
        AWS_ACCESS_KEY_ID = credentials('mlal-aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('mlal-aws-secret-key')
        AWS_REGION = 'us-west-2'
        CLUSTER_NAME = 'munish-ecommerce-cluster-3'
    }
    stages {
        stage('Build Docker Images') {
            steps {
                script {
                    def services = ['user-service', 'product-service', 'cart-service', 'order-service']
                    for (svc in services) {
                        sh "docker build -t $MLAL_DOCKERHUB_USER/${svc}:latest ./backend/${svc}"
                    }
                    // Separate for frontend
                    sh "docker build -t $MLAL_DOCKERHUB_USER/frontend:latest ./frontend"
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    sh """
                      echo \$MLAL_DOCKERHUB_PASS | docker login -u \$MLAL_DOCKERHUB_USER --password-stdin
                        """
                    def services = ['user-service', 'product-service', 'cart-service', 'order-service', 'frontend']
                    for (svc in services) {
                        sh "docker push \$MLAL_DOCKERHUB_USER/${svc}:latest"
                    }
                }
            }
        }
        /*
    stage('Provision EKS Cluster') {
      steps {
        sh '''
        eksctl create cluster \
          --name $CLUSTER_NAME \
          --region $AWS_REGION \
          --nodegroup-name standard-workers \
          --node-type t3.medium \
          --nodes 2
        '''
      }
    }
*/
        stage('Check Tools') {
            steps {
                sh 'which kubectl || echo "kubectl not found"'
                sh 'kubectl version --client || echo "kubectl broken"'
                sh 'env'
            }
        }
        stage('Configure kubeconfig') {
            steps {
                sh '''
                aws eks update-kubeconfig --region $AWS_REGION --name $CLUSTER_NAME
                    '''
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh "kubectl apply -f k8s/"
            }
        }
    }
    post {
        failure {
            echo 'Build Failed!'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
