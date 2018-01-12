node {
  checkout scm
  
  stage "Deploy Application"
  switch (env.BRANCH_NAME) {

    // Roll out to production
    case "master":
        // Change deployed image in staging to the one we just built
        sh("kubectl --namespace=staging apply -f zookeeper/")
        sh("kubectl --namespace=staging apply -f kafka/")
        break

    // Roll out a dev environment
    default:
        // Create namespace if it doesn't exist
        sh("kubectl get ns ${env.BRANCH_NAME} || kubectl create ns ${env.BRANCH_NAME}")
        sh("kubectl --namespace=${env.BRANCH_NAME} apply -f zookeeper/")
        sh("kubectl --namespace=${env.BRANCH_NAME} apply -f kafka/")
  }
}