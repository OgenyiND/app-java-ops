pipeline {
    agent any
    tools {
        // Use the JDK version named "Java" configured in Jenkins
        jdk 'Java'
    }

    environment {
        // Defining JAVA_HOME may be optional, depending on your Jenkins configuration
        JAVA_HOME = tool 'Java'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/OgenyiND/app-java.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                // Create a directory for compiled classes
                sh 'mkdir -p build/classes'
                // Compile Main.java
                sh '"$JAVA_HOME/bin/javac" -d build/classes Main.java'
            }
        }

        stage('Prepare Manifest') {
            steps {
                // Create the manifest file in the build/classes directory
                sh 'echo "Main-Class: Main" > build/classes/MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                // Create a directory for the JAR file
                sh 'mkdir -p build/jar'
                // Package compiled classes into a JAR file with the manifest file
                sh 'cd build/classes && "$JAVA_HOME/bin/jar" cvmf MANIFEST.MF ../jar/MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                // Run the application from the JAR file
                sh '"$JAVA_HOME/bin/java" -jar build/jar/MyApplication.jar'
            }
        }
    }
}
