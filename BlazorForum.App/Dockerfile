FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BlazorForum.App/BlazorForum.App.csproj", "BlazorForum.App/"]
RUN dotnet restore "BlazorForum.App/BlazorForum.App.csproj"
COPY . .
WORKDIR "/src/BlazorForum.App"
RUN dotnet build "BlazorForum.App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorForum.App.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorForum.App.dll"]
