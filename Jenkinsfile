pipeline{
 agent any
 environment{
  PROJECT_ID='dhana'
  CLUSTER_NAME='cluster-1'
  CREDENTIAL_ID='credentialId'
  LOCATION='us-central1-c'
 }
 
 stages{
        stage("checkout scm"){
            steps{
                    checkout scm
                }
 
         }
       stage("Build image"){
             steps{
                    script{
                        myapp=docker.build("dhanalucky2308/hello-world:1")
                     }
             }
 
      }
     stage("Push Image"){
            steps{
                  script{
                       docker.withRegistry('https://registry.hub.docker.com','dockerId'){
	                     myapp.push("1")
	                     }
                 }
           }
 
     }
    stage("Deploy to GKE"){
           steps{
            step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialId: env.CREDENTIAL_ID, verifyDeployments: true ])
			
           }
      }
  }
}
