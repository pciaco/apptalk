FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["apptalk.csproj", "apptalk/"]
RUN dotnet restore "apptalk.csproj"
COPY . .
WORKDIR "/src/apptalk"
RUN dotnet build "apptalk.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "apptalk.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
CMD ASPNETCORE_URLS=http://*:$PORT dotnet apptalk.dll