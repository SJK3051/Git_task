pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/Git_task.git'
            }
        }

        stage('Build Step') {
            steps {
                echo "✅ Build steps go here (e.g., compile, test, docker build, etc.)"
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                echo "🚀 Running Ansible Playbook..."
                
                # Ensure ansible is installed
                if ! command -v ansible-playbook &> /dev/null
                then
                    echo "⚠️ Installing Ansible..."
                    sudo apt update -y
                    sudo apt install -y ansible
                fi

                # Run playbook with inventory
                ansible-playbook -i inventory.ini playbook.yml
                '''
            }
        }
    }
}

