# escape=`

ARG tag=1803

FROM mcr.microsoft.com/windows/servercore:$tag AS servercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ARG GRAFANA_VERSION="6.1.6"
ARG GRAFANA_SHA256="178e6fb92dfb560fa4f2871bccb93a37283a35cc8ce40a3b6962ccb92e645f33"

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
