# Projects
This folder contains 3 project which essentially deploy the same application. Here are the differences:
- `guestbook-redis` and `guestbook-redis-ha` both require the user to replace `your-docker-username` with their Docker Hub username (see README `0. Replace Docker Image`) 
- `guestbook-redis-ha-helm` does not require the username replacement because it deploys the PHP container with a Helm chart which allows for parameterization
- `guestbook-redis-ha` and `guestbook-redis-ha-helm` deploy a HA redis instance while `guestbook-redis` just deploys a single redis container which serves for read and write operations.