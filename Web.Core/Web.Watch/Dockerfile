FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build

WORKDIR /app

COPY . .

RUN msbuild /p:Configuration=Debug -r:False

FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
WORKDIR /inetpub/wwwroot
RUN Remove-Website -Name 'Default Web Site'
COPY --from=build /app/Web.Watch/. ./
ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]