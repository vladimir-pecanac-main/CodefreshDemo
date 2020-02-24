FROM mcr.microsoft.com/dotnet/core/sdk:3.1 as build-image
WORKDIR /home/app
RUN ls
COPY ./*.sln ./
COPY ./*/*.csproj ./
RUN for file in $(ls *.csproj); do mkdir -p ./${file%.*}/ && mv $file ./${file%.*}/; done
RUN dotnet restore
COPY . .
RUN dotnet publish ./CodefreshDemo/CodefreshDemo.csproj -o /publish/
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /publish
COPY --from=build-image /publish .
ENV ASPNETCORE_URLS=https://+:5001;http://+:5000
ENTRYPOINT ["dotnet", "CodefreshDemo.dll"] 
