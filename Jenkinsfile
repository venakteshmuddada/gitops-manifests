stage('Update GitOps Repo') {
  steps {
    script {
      def shortCommit = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
      def gitopsRepo = "https://github.com/venakteshmuddada/gitops-manifests.git"
      def gitopsDir = "gitops-manifests"

      sh """
        rm -rf ${gitopsDir}
        git clone ${gitopsRepo}
        cd ${gitopsDir}/overlays/dev
        sed -i 's|REPLACE_ME|${shortCommit}|' image-patch.yaml
        git config user.name "jenkins"
        git config user.email "jenkins@localhost"
        git add image-patch.yaml
        git commit -m "Update image tag to ${shortCommit}"
        git push origin main
      """
    }
  }
}
