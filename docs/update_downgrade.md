# Update and Downgrade

## Update

For major version update (**`v1.6.0` -> `v2.0.0`**) you should follow `Update instructions` in [CHANGELOG.md](https://github.com/DiTsi/impulse/blob/main/CHANGELOG.md).

Another updates can be done without manual operations.

<!-- ### Python -->

### Docker

1. See `impulse.yml` update instructions in [CHANGELOG.md](https://github.com/DiTsi/impulse/blob/main/CHANGELOG.md) (**for major version update**) 
2. Set new tag in `docker-compose.yml`
3. Execute `docker-compose up -d`

<!-- ## Downgrade

Minor version downgrade can break functionality because some of them can contain incident objects updates. 

### Docker -->
