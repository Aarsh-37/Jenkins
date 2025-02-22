pipeline { 
    agent any  // Runs on any available Jenkins agent
    
    stages { 
        stage('Checkout') { 
            steps { 
                git branch: 'main', url: 'https://github.com/Aarsh-37/Jenkins.git' // Replace with your repo
            } 
        } 

        stage('Setup Environment') { 
            steps { 
                sh ''' 
                #!/bin/bash
                python3 -m venv venv  # Create virtual environment
                source venv/bin/activate  # Activate virtual environment
                pip install --upgrade pip  # Upgrade pip
                pip install -r requirements.txt  # Install dependencies
                ''' 
            } 
        } 

        stage('Build') { 
            steps { 
                sh ''' 
                #!/bin/bash
                source venv/bin/activate  # Activate virtual environment
                python src/main.py  # Run the application
                ''' 
            } 
        } 

        stage('Test') { 
            steps { 
                sh ''' 
                #!/bin/bash
                source venv/bin/activate  # Activate virtual environment
                pytest src/test_main.py --junitxml=test-results.xml  # Run tests with JUnit report
                ''' 
            } 
        } 
    } 

    post { 
        always { 
            junit 'test-results.xml'  // Publish test results
            cleanWs()  // Clean the workspace after the pipeline finishes
        } 
    } 
}