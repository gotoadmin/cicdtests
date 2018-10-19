def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, yaml: """
apiVersion: v1
kind: Pod
metadata:
  name: textiq
  labels:
    some-label: some-label-value
spec:
  containers:
    - name: ubuntu
      image: ubuntu
      securityContext:
         privileged: true
         runAsUser: 0
      command: ["/bin/sh","-c"]
      args: ["sysctl -w vm.max_map_count=262144 && cat"]
      tty: true
"""
) {
    node (label) {
        stage('Launch ubuntu') {
            container('ubuntu') {
               sh """
                 ls -l /home/jenkins
                 """
            }
        }
    }
}
