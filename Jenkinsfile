node {
  if (env.BRANCH_NAME != 'master') {
    stage('init') {
      checkout scm
    }

    stage('build') {
      sh 'mvn clean package'
    }

    stage('deploy') {
      def resourceGroup = 'tomcatTesting123'
      def webAppName = 'tomcatTesting123-staging'
      sh 'mv target/*.war target/ROOT.war'
      azureWebAppPublish azureCredentialsId: 'mySp', publishType: 'file',
                         resourceGroup: resourceGroup, appName: webAppName,
                         filePath: '*.war', sourceDirectory: 'target', targetDirectory: 'webapps'
    }
  }
  else {
      stage('init') {
      checkout scm
    }

    stage('build') {
      sh 'mvn clean package'
    }

    stage('deploy') {
      def resourceGroup = 'tomcatTesting123'
      def webAppName = 'tomcatTesting123'
      sh 'mv target/*.war target/ROOT.war'
      azureWebAppPublish azureCredentialsId: 'mySp', publishType: 'file',
                         resourceGroup: resourceGroup, appName: webAppName,
                         filePath: '*.war', sourceDirectory: 'target', targetDirectory: 'webapps'
    }
  }
}
