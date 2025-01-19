# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia os arquivos do projeto e restaura as dependências
COPY *.csproj ./
#COPY NuGet.Config /root/.nuget/NuGet/NuGet.Config
RUN dotnet restore

# Copia todos os arquivos restantes e compila o projeto
COPY . ./
RUN dotnet publish -c Release -o /out

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copia os arquivos publicados para o ambiente de runtime
COPY --from=build /out ./

# Define a porta exposta pelo contêiner
EXPOSE 8080

# Define o comando de inicialização
ENTRYPOINT ["dotnet", "KubernetsLab.dll"]