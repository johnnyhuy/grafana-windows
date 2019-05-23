# escape=`

FROM mcr.microsoft.com/windows/servercore:10.0.14393.2608 AS servercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ARG GRAFANA_VERSION="6.2.0"
ARG GRAFANA_SHA256="233b6181d5c83e8ce60f364e9d63df24cd05267dd7aa67949ffa031392b6cf33"

RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    Invoke-WebRequest "https://dl.grafana.com/oss/release/grafana-$($env:GRAFANA_VERSION).windows-amd64.zip" -OutFile grafana.zip -UseBasicParsing; `
    if ((Get-FileHash grafana.zip -Algorithm sha256).Hash.ToLower() -ne $env:GRAFANA_SHA256) {exit 1}; `
    Expand-Archive grafana.zip -DestinationPath C:\; `
    Move-Item "grafana-$($env:GRAFANA_VERSION)" grafana; `
    Remove-Item grafana.zip

FROM mcr.microsoft.com/windows/nanoserver:sac2016

COPY --from=servercore /grafana /grafana

EXPOSE 3000

WORKDIR C:\grafana\bin
CMD ["grafana-server.exe"]
