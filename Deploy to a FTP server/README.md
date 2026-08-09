#  Deploy to a FTP server (Get started with Jenkins, part 8)
```
https://www.youtube.com/watch?v=ZdUk3UeG8JQ
```

# Install git-ftp
Open your terminal or command prompt and install the extension based on your operating system:

- macOS (Using Homebrew):
```
brew install git-ftp
```

- Ubuntu / Debian:
```
sudo apt-get update
sudo apt-get install git-ftp
```

```
git ftp push --user $FTP_USERNAME --password $FTP_PASSWORD ftp://46.21.172.143/public_html
```
