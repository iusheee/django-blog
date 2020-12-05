pipeline {
        agent any
        stages {
                stage('Code Checkout') {
                   steps{
                        git 'https://github.com/iusheee/django-blog.git'
                   }
                }

                stage('Unit Test') {
                   steps{
                        script {
                            sh '''
                                #!/bin/bash
                                if sudo docker images | grep aayushichoudhary/test 
                                then
                                       echo "Image already pulled"
                                else
                                       sudo docker pull aayushichoudhary/test:v1
                                fi 
                                if  sudo docker ps | grep test_container
                                then
                                        echo "already running"
                                        
                                        sudo docker exec test_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                        
                                        sudo docker exec test_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:4000 &
										sudo sleep 15
                                        if sudo docker exec test_container pytest -v  /unit_test/test2.py
                                        then
                                            exit 0
                                        else
                                            exit 1
											echo "Failed !"
                                        fi
                                else
                                        sudo docker run -dit -p 3000:4000 -v /var/lib/jenkins/workspace/assignment/:/sourcecode --name test_container aayushichoudhary/test:v1
                                        sudo docker exec test_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                        
                                        sudo docker exec test_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:4000 &
										sudo sleep 15
                                        if sudo docker exec test_container pytest -v  /unit_test/test2.py
                                        then
                                            exit 0
                                        else
											exit 1
                                            echo "Test Case Failed !!"
                                        fi
                                fi
                            '''
                        }
                   }
                }


                stage('App Deployment on Server') {
                   steps{
                         script {
                                sh '''
                                        #!/bin/bash
                                        if sudo docker images | grep aayushichoudhary/prod
                                        then
                                                echo "already pulled image"
                                        else
                                                sudo docker pull aayushichoudhary/prod:v1
                                        fi
                                        if  sudo docker ps -a | grep prod_container | grep Exited
                                        then
                                            sudo docker rm -f prod_container
                                        fi
                                        if sudo docker ps | grep prod_container
                                        then
                                                echo "Container running"
                                                
                                                sudo docker exec prod_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                                
                                                sudo docker exec prod_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:6000 &
                                        else
                                               sudo docker run -dit -p 5000:6000 -v /var/lib/jenkins/workspace/assignment/:/sourcecode --name prod_container aayushichoudhary/prod:v1
                                                
                                                sudo docker exec prod_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                                
                                                sudo docker exec prod_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:6000 &
                                        fi
                                '''
                                }
                   }
                }
        }
}pipeline {
        agent any
        stages {
                stage('Code Checkout') {
                   steps{
                        git 'https://github.com/iusheee/django-blog.git'
                   }
                }

                stage('Unit Test') {
                   steps{
                        script {
                            sh '''
                                #!/bin/bash
                                if sudo docker images | grep aayushichoudhary/test 
                                then
                                       echo "Image already pulled"
                                else
                                       sudo docker pull aayushichoudhary/test:v1
                                fi 
                                if  sudo docker ps | grep test_container
                                then
                                        echo "already running"
                                        
                                        sudo docker exec test_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                        
                                        sudo docker exec test_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:4000 &
                                        if sudo docker exec test_container pytest -v  /unit_test/test2.py
                                        then
                                            exit 0
                                        else
                                            exit 1
											echo "Failed !"
                                        fi
                                else
                                        sudo docker run -dit -p 3000:4000 -v /var/lib/jenkins/workspace/assignment/:/sourcecode --name test_container aayushichoudhary/test:v1
                                        sudo docker exec test_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                        
                                        sudo docker exec test_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:4000 &
                                        if sudo docker exec test_container pytest -v  /unit_test/test2.py
                                        then
                                            exit 0
                                        else
											exit 1
                                            echo "Test Case Failed !!"
                                        fi
                                fi
                            '''
                        }
                   }
                }


                stage('App Deployment on Server') {
                   steps{
                         script {
                                sh '''
                                        #!/bin/bash
                                        if sudo docker images | grep aayushichoudhary/prod
                                        then
                                                echo "already pulled image"
                                        else
                                                sudo docker pull aayushichoudhary/prod:v1
                                        fi
                                        if  sudo docker ps -a | grep prod_container | grep Exited
                                        then
                                            sudo docker rm -f prod_container
                                        fi
                                        if sudo docker ps | grep prod_container
                                        then
                                                echo "Container running"
                                                
                                                sudo docker exec prod_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                                
                                                sudo docker exec prod_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:6000 &
                                        else
                                               sudo docker run -dit -p 5000:6000 -v /var/lib/jenkins/workspace/assignment/:/sourcecode --name prod_container aayushichoudhary/prod:v1
                                                
                                                sudo docker exec prod_container sed -i "s/ALLOWED_HOSTS = [[]]/ALLOWED_HOSTS = ['*',]/g" /sourcecode/mysite/settings.py
                                                
                                                sudo docker exec prod_container python3.6 /sourcecode/manage.py runserver 0.0.0.0:6000 &
                                        fi
                                '''
                                }
                   }
                }
        }
}
