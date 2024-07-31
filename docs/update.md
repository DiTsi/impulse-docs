# Update

IMPulse versions look like **`1.0`** where **`1`** is major version and **`0`** is minor.

For minor update (like **`1.0` -> `1.4`**) you can just download and run new version without additional modifications.

For major update (like **`1.6` -> `2.0`**) you should see instructions in [CHANGELOG.md](https://github.com/DiTsi/impulse/blob/main/CHANGELOG.md).

## Procedure

### Python

### Docker

1. (**for major version update**) See `impulse.yml` update instructions in [CHANGELOG.md](https://github.com/DiTsi/impulse/blob/main/CHANGELOG.md)
2. Set new tag in `docker-compose.yml`
3. Execute `docker-compose up -d`
