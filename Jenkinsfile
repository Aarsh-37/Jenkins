pipeline {
agent any

stages {
stage('Checkout') {
steps {
git branch: 'main', url: 'https://github.com/your_repo/jenkins_demo.git' // Replace with your repo

}
}
stage('Setup Environment') {
steps {
// Use Bash for the entire stage
sh '''
#!/bin/bash
python3 -m venv venv
. venv/bin/activate
pip install -r requirements.txt
'''
}
}
stage('Build') {
steps {
// Use Bash for the entire stage
sh '''
#!/bin/bash
. venv/bin/activate
python src/main.py
'''
}
}
stage('Test') {
steps {
// Use Bash for the entire stage
sh '''
#!/bin/bash
. venv/bin/activate
pytest src/test_main.py
'''

}
}
}
post {
always {
cleanWs() // Clean the workspace after the pipeline is finished
}
}
}
