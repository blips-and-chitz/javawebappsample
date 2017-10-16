node {
    // not master branch
    if  (env.BRANCH_NAME != 'master') {
        checkout()
        build()
        staging()
    } // master branch
    else {
        checkout()
        build()
        production()
    }
}

def checkout () {
    stage('init') {
      checkout scm
    }
}

def build () {
    stage('build') {
      sh 'mvn clean package'
    }
}

def production {
    stage('deploy') {
      def resourceGroup = 'tomcatTesting123'
      def webAppName = 'tomcatTesting123'
      sh 'mv target/*.war target/ROOT.war'
      azureWebAppPublish azureCredentialsId: 'mySp', publishType: 'file',
                         resourceGroup: resourceGroup, appName: webAppName,
                         filePath: '*.war', sourceDirectory: 'target', targetDirectory: 'webapps'
    }
}

def staging {
    stage('deploy') {
      def resourceGroup = 'tomcatTesting123'
      def webAppName = 'tomcatTesting123-staging'
      sh 'mv target/*.war target/ROOT.war'
      azureWebAppPublish azureCredentialsId: 'mySp', publishType: 'file',
                         resourceGroup: resourceGroup, appName: webAppName,
                         filePath: '*.war', sourceDirectory: 'target', targetDirectory: 'webapps'
    }
}
