node {
  stage('Clone sources') {
    git
        branch: 'main',
        url: 'https://github.com/eonuallain/jenkins-related.git'
  }

  stage('Cancel older builds') {
    echo "Checking for older running builds ..."
  }
}
