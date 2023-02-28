pipeline {
  agent any
 parameters {
        string(name: 'containerName', defaultValue: 'dorowu', description: 'nombre del dockerHub')
        string(name: 'imageName', defaultValue: 'dorowu/ubuntu-desktop-lxde-vnc', description: 'nombre de la imagen')
        string(name: 'imageTag', defaultValue: 'latest', description: 'tag de la imagen')
        string(name: 'webPort', defaultValue: '6080', description: 'puerto a publicar')
    }
    environment {
        finalName = "${containerName}"        
    }
    stages {
          stage('stop/rm') {

            when {
                expression { 
                    DOCKER_EXIST = sh(returnStdout: true, script: 'echo "$(docker ps -q --filter name=${name_final})"').trim()
                    return  DOCKER_EXIST != ''
                }
            }
            steps {
                script{
                    sh ''' 
                        docker stop ${finalName}
                    '''
                    }
                    
                }                    
                                  
            }
           
        stage('build') {
            steps {
                script{
                    sh ''' 
                        docker pull ${imageName}:${imageTag}
                    '''
                    }
                    
                }                    
                                  
            }
            stage('run') {
            steps {
                script{
                    sh ''' 
                        docker run -dp ${webPort}:80 --name ${finalName} ${imageName}:${imageTag}
                    '''
                    }
                    
                }                    
                                  
            }
        }   
    }