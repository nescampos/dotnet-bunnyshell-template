# Imagen base
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

# Directorio de trabajo
WORKDIR /app

# Copiar archivos de proyecto y restaurar dependencias
COPY *.csproj ./
RUN dotnet restore

# Copiar todo el c�digo fuente y compilar
COPY . ./
RUN dotnet publish -c Release -o out

# Imagen de producci�n
FROM mcr.microsoft.com/dotnet/aspnet:6.0

# Directorio de trabajo
WORKDIR /app

# Copiar archivos publicados de la etapa anterior
COPY --from=build-env /app/out .

ENV CircleAPIKey=${CircleAPIKey}

# Puerto en el que escucha la aplicaci�n
EXPOSE 80
# Comando de inicio de la aplicaci�n
ENTRYPOINT ["dotnet", "PayWave.dll"]