http://localhost:7000 -> dashboard -> New Item -> Pipeline

Give your pipeline a name and click “OK.”

```groovy
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

# https://www.youtube.com/watch?v=RsD2nzPY0is