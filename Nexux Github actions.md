name: Java with Nexus Repository

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: Set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: Build with Maven
      run: mvn package --file pom.xml
    - name: Nexus Repo Publish
      uses: sonatype-nexus-community/nexus-repo-github-action@master
      with:
        serverUrl: http://163c6cdd.ngrok.io
        username: admin
        password: ${{ secrets.password }}
        format: maven2
        repository: maven-releases
        coordinates: groupId=com.example artifactId=app version=1.0.0
        assets: extension=jar
        filename: ./target/app-1.0.0.jar
