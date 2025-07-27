on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

env:
  AZURE_WEBAPP_NAME: lavitaconnect-coreweb
  AZURE_WEBAPP_PACKAGE_PATH: '.'    # غيره لو المشروع داخل مجلد فرعي زي ./src
  NODE_VERSION: '20.x'              # مش ضروري لو المشروع DotNet بس ممكن نحذفه لاحقًا

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4

    - name: Setup .NET Core
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '8.0.x'

    - name: Restore dependencies
      run: dotnet restore

    - name: Build app
      run: dotnet build --configuration Release

    - name: Publish app
      run: dotnet publish -c Release -o publish

    - name: Upload artifact for deployment
      uses: actions/upload-artifact@v4
      with:
        name: dotnet-app
        path: publish

  deploy:
    permissions:
      contents: none
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'Production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
    - name: Download artifact
      uses: actions/download-artifact@v4
      with:
        name: dotnet-app

    - name: Deploy to Azure WebApp
      id: deploy-to-webapp
      uses: azure/webapps-deploy@v2
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: dotnet-app
