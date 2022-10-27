def changelog(){
  //withCredentials([usernamePassword(credentialsId: 'jenkinsCredentials', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {    
        sh"curl -u admin:admin ${env.BUILD_URL}/api/xml?xpath=/*/changeSet -o file.xml"
        def file = readFile(file: "file.xml")   
        def msg = "Changes deployed through the build:"  
        if(file != "XPath /*/changeSet didn?t match"){  
                    def response = new XmlSlurper().parseText(file) 
                    for(int i=0;i<response.item.size(); i++){
                        def z= i+1
                        msg =  msg + "\n" + "${z}" + ". "  + response.item[i].msg    
                    }
        }else{
                msg = " No commits"
            } 
        return msg  
    
}


node{
 
  try {
  
    stage("check"){
        
        v = "origin/release-sprint-22"

        
    }
    stage('commiting'){
         
         withCredentials([usernamePassword(credentialsId: '2', passwordVariable: 'password', usernameVariable: 'username')])
        {
          
              
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sumitbhardwajji/new.git']]])
             
              sh"   git config --global user.name \"sumitbhardwajji\" "
              sh"   git config --global user.email \"sumitbhardwa7303@gmail.com\" "
              sh "git checkout $branch"
              sh"   echo 'testing sumit bhardwajji  is a great man ' > sumit2.txt "
              sh "git status"
              sh "ls | cat sumit2.txt"
              sh"   git add . "
              sh"   git commit -m \"intial\" "
              def l = env.Branch.tokenize("/")
              l = l[1]
              sh" git push https://${username}:${password}@github.com/sumitbhardwajji/new.git HEAD:refs/heads/$l "
             
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sumitbhardwajji/notejam.git']]])
              
          for(int i=0;i>-1;i++){
          print(i)
          }
            
        }
        }
  stage("chnagelog"){
              def change=changelog()
              print(change)
  
  }
  }catch(error){
    stage("error"){
          def change=changelog()
              print(change)
    }
  }
}
