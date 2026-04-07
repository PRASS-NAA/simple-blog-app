pipeline{
    agent any

    stages{
        stage('Pull Code From GitHub')
        {
            steps{
                git 'https://github.com/PRASS-NAA/simple-blog-app.git'
            }
        }

        stage('Set TAG') {
            steps {
                script {
                    env.TAG = sh(
                        script: "git rev-parse --short HEAD",
                        returnStdout: true
                    ).trim()
                }
            }
        }

        stage('Debug TAG') {
            steps {
                echo "TAG = ${TAG}"
            }
        }

        stage('Create Frontend And Backend Images Parallely')
        {
            parallel{
                stage('Create Frontend Image')
                {
                    steps{
                        sh "docker build -t prass6naa/blog-frontend:${TAG} ./frontend"
                    }
                }

                stage('Create Backend Image')
                {
                    steps{
                        sh "docker build -t prass6naa/blog-backend:${TAG} ./backend"
                    }
                }
            }
        }

        stage('Authenticate With Docker')
        {
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'docker-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Pushing Frontend And Backend Images')
        {
            parallel{
                stage('Pushing Frontend Image')
                {
                    steps{
                        sh "docker push prass6naa/blog-frontend:${TAG}"
                    }
                }

                stage('Pushing Backend Image')
                {
                    steps{
                        sh "docker push prass6naa/blog-backend:${TAG}"
                    }
                }
            }
            
        }

        stage('Update K8 manifests') {
            steps{
                dir('gitops') {
                    git 'https://github.com/PRASS-NAA/blog-app-k8-manifests.git'

                    sh """
                    sed -i 's|image: prass6naa/blog-frontend:.*|image: prass6naa/blog-frontend:${TAG}|' k8s/frontend/frontend.yaml
                    sed -i 's|image: prass6naa/blog-backend:.*|image: prass6naa/blog-backend:${TAG}|' k8s/backend/backend.yaml
                    """

                    withCredentials([usernamePassword(
                        credentialsId: 'github-creds',
                        usernameVariable: 'GIT_USER',
                        passwordVariable: 'GIT_PASS'
                    )]) {
                        sh """
                        git config user.email "prassml23@gmail.com"
                        git config user.name "PRASS-NAA"

                        git remote set-url origin https://\$GIT_USER:\$GIT_PASS@github.com/PRASS-NAA/blog-app-k8-manifests.git

                        git commit -am "update image to ${TAG}" || echo "No changes"
                        git push origin HEAD:master
                        """
                    }
                }
            }
        }

    }

    post
    {
        success{
            echo 'Build Success !! CI SUCCESS'
        }

        failure{
            echo 'Build Failure !! CI FAILED'
        }
    }
}