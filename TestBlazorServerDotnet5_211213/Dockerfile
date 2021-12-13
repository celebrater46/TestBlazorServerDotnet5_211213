FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["TestBlazorServerDotnet5_211213/TestBlazorServerDotnet5_211213.csproj", "TestBlazorServerDotnet5_211213/"]
RUN dotnet restore "TestBlazorServerDotnet5_211213/TestBlazorServerDotnet5_211213.csproj"
COPY . .
WORKDIR "/src/TestBlazorServerDotnet5_211213"
RUN dotnet build "TestBlazorServerDotnet5_211213.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestBlazorServerDotnet5_211213.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestBlazorServerDotnet5_211213.dll"]
