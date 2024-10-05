У CopyTask есть expand(**version**: version, **javaVersion**: javaVersion, **timeStamp**: timeStamp, **osName**: osName)
```Plain
processResources {

    filesMatching('**/constants.properties') {
        expand(version: version, javaVersion: javaVersion, timeStamp: timeStamp, osName: osName)
    }

    filesMatching('**/notice.html') {
        expand(version: version, javaVersion: javaVersion, timeStamp: timeStamp, osName: osName)
    }
}
```