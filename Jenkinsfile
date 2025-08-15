pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SJK3051/Git_task.git'
            }
        }

        stage('Debug Workspace') {
            steps {
                sh '''
                    echo "Current working directory:"
                    pwd
                    echo "Listing files:"
                    ls -lR
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "Building Docker image..."
                    
                    # Check if Dockerfile exists at root
                    if [ -f Dockerfile ]; then
                        docker build -t myapp:latest .
                    else
                        echo "Dockerfile not found in root — searching..."
                        DOCKERFILE_PATH=$(find . -name Dockerfile | head -n 1)
                        if [ -z "$DOCKERFILE_PATH" ]; then
                            echo "❌ No Dockerfile found in repository."
                            exit 1
                        fi
                        DOCKER_DIR=$(dirname "$DOCKERFILE_PATH")
                        echo "✅ Found Dockerfile at: $DOCKERFILE_PATH"
                        docker build -t myapp:latest -f "$DOCKERFILE_PATH" "$DOCKER_DIR"
                    fi
                '''
            }
        }
    }
}

