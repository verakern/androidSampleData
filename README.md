# androidSampleData
Sample data to be used with Android Studio Preview

It can be included through Android Studio as outlined in this article: https://proandroiddev.com/android-remote-sample-data-cd87b4da590b

Just add
```
clean.doFirst {
    def samplesDir = new File(projectDir.absolutePath, "sampledata")
    if (samplesDir.exists()) {
        samplesDir.deleteDir()
    }
}

preBuild.doFirst {
    def samplesDir = new File(projectDir.absolutePath, "sampledata")
    if (samplesDir.exists()) {
        return
    }
    samplesDir.mkdir()

    def files = ["names.json"] //list of sample files that need to be downloaded
    for(fileName in files) {
        def names = new File(samplesDir, fileName)

        new URL("https://raw.githubusercontent.com/verakern/androidSampleData/master/$fileName").withInputStream { i ->
            names.withOutputStream {
                it << i
            }
        }
    }
}
```
to your app.gradle file and use them in layout files with

```
tools:text="@sample/names.json/data/name"
tools:text="@sample/names.json/data/bio"
```
