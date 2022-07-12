
pipeline{
agent any

              stages{
                stage('playbook'){
                       agent {
                          label{
                             label "built-in"
                                        }
                                        }
                       steps{
                             git "https://github.com/Amruta-Rajput/my-project.git"
                             sh "ansible-playbook playbook1.yml"
                            }
                            }
                stage('git_clone'){
                       agent {
                          label{
                              label "linux_slave"
                                }
                                }
                       steps{
                           dir ("/home/amruta/build"){
					   
                             git "https://github.com/Amruta-Rajput/game-of-life.git"
                           }
                       }                          
                            }
			stage('copy-package') {
				       agent {
                          label{
                              label "linux_slave"
                               }
                               }
						steps {
						dir("/home/amruta/build"){
						sh "sudo mvn package"
						sh "sudo mkdir -p /mnt/package"
						sh "sudo cp /home/amruta/build/gameoflife-web/target/*.war /mnt/package"
						}
                               
}						
							   
				}
				stage('deploy-to-docker'){
				agent {
                          label{
                              label "linux_slave"
                               }
                               }
							   steps {
							   sh "sudo docker run -it -d -p 8080:8080 -v /mnt/package:/usr/local/tomcat/webapps tomcat:8"
							   }
				
}
                            
              }                           
}
