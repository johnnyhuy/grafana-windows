# escape=`

ARG tag=1803

FROM mcr.microsoft.com/windows/servercore:$tag AS servercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ARG GRAFANA_VERSION="6.0.0"
ARG GRAFANA_SHA256="8b74a18b8f467c46abcf96fbce2d8575d5a1a0e3afce6f9242c55224dd17e039"

RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest "https://dl.grafana.com/oss/release/grafana-$($env:GRAFANA_VERSION).windows-amd64.zip" -OutFile grafana.zip -UseBasicParsing; `
    if ((Get-FileHash grafana.zip -Algorithm sha256).Hash.ToLower() -ne $env:GRAFANA_SHA256) {exit 1}; `
    Expand-Archive grafana.zip -DestinationPath C:\; `
    Move-Item "grafana-$($env:GRAFANA_VERSION)" grafana; `
    Remove-Item grafana.zip

FROM mcr.microsoft.com/windows/nanoserver:$tag

COPY --from=servercore /grafana /grafana

EXPOSE 3000

WORKDIR C:\grafana\bin
CMD ["grafana-server.exe"]
