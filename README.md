### Setting up Concourse with local Artifactory

1. Pull the artifactory docker image:
    ```
    docker pull docker.bintray.io/jfrog/artifactory-oss
    ```
1. Run concourse and artifactory
    ```
    docker-compose up -d
    docker run --name artifactory -d -p 8081:8081 docker.bintray.io/jfrog/artifactory-oss
    ```
1. Download `fly` from the concourse ui at localhost:8080

1. Install fly, and login and set the pipeline
   ```
   install ~/Downloads/fly /usr/local/bin
   fly -t main login -c http://localhost:8080
   ```

1. Create a `generic-local` repo on artifactory through the UI at localhost:8081

1. Change the <ARTIFACTORY_IP> in the pipeline to be the IP of the local machine, then set the pipeline
   ```
   fly -t main set-pipeline -c pipeline.yml
   ```

1. Run the `upload-to-artifactory` task from the concourse ui
    - Check artifactory - `gonna-be-in-artifactory.txt` should be in the `generic-local` repo!

1. Run the `download-to-artifactory` task from the concourse ui
    - You should see `hello artifactory` in the task output!