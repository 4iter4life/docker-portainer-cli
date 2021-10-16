Simple python container with installed portainer-cli for integration in CI/CD.

Example integration in GitLab to update related stack:

```
deploy:
  stage: deploy
  image: aeroplan/portainer-cli
  tags:
    - docker
  script:
    # configure the base_url
    - portainer-cli configure https://portainer.example.com/
    # prepare your user with permission to a related portainer stack and save passwort as a gitlab secret
    - portainer-cli login gitlab $PORTAINER_GITLAB_SECRET 
    # define the service_container_tag as environment variable in your portainer stack and use it (${service_container_tag}) in your docker-compose
    - portainer-cli update_stack <stack_id> <endpoint_id> --env.service_container_tag=$CI_PIPELINE_ID
```

see https://github.com/4iter4life/docker-portainer-cli/tree/main
