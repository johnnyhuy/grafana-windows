# Grafana for Windows

This is a repository with Grafana servers in Windows Docker containers.

## Usage

Run the following command to get this container running! There is also support for previous Windows versions.

```bash
# Windows Server 1809
docker run --rm -p 3000:3000 johnnyhuy/grafana-windows:latest

# OR

# Windows Server 1803
docker run --rm -p 3000:3000 johnnyhuy/grafana-windows:1803

# OR

# Windows Server 2016
docker run --rm -p 3000:3000 johnnyhuy/grafana-windows:win2016
```

## Prerequisites

- Docker & Windows (duhh!)

## Contribution

- Project derived from [DockerSamples/AspNet-Monitoring](https://github.com/dockersamples/aspnet-monitoring)
- **Johnny Huynh** - Initial changes in this repository

## License

This project is licensed under the MIT license, see [LICENSE](https://github.com/johnnyhuy/grafana-windows/blob/master/LICENSE) for more information.

- **dockersamples/aspnet-monitoring** is licensed under the [Apache License 2.0](https://github.com/dockersamples/aspnet-monitoring/blob/master/LICENSE)
