pipeline{
  agent any
  stages{
    stage('Build Docker Image'){
      steps{
        bat '"C:\\Users\\HP\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t products-jmeter .'
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
        bat ' "C:\\Users\\HP\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" run --rm -v %WORKSPACE%/tests:/tests -v %WORKSPACE%:/results justb4/jmeter:latest -n -t /tests/EmailJmeter.jmx -l /results/results.jtl -e -o /results/html-report'
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











      
        
