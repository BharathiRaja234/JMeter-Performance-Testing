pipeline{
  agent any
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main' , url: 'https://github.com/BharathiRaja234/JMeter-Performance-Testing.git'
      }
    }
    stage('Clean Previous Report'){
      steps{
        bat 'if exist html-report rmdir /S /Q html-report'
        bat 'if exist results.jtl del /Q results.jtl'
      }
    }
    
    stage('Run JMeter in Docker'){
      steps{
        bat 'docker run --rm -v %WORKSPACE%/tests:/tests -v %WORKSPACE%:/results justb4/jmeter:latest -n -t /tests/EmailJmeter.jmx -l /results/results.jtl -e -o /results/html-report'
      }
    }
    stage('Publish Report'){
    steps{
      publishHTML(target: [
        reportName: 'JMeter Report',
        reportDir: 'html-report',
        reportFiles: 'index.html',
        keepAll: true,
        alwaysLinkToLastBuild: true
        ])
    }
  }
}
}











      
        
