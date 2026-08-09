```
Jenkins -> New Item

Enter an item name

Select an item type -> Freestyle project

Type name -> Flutter Android Build
```

# Config Project Folder

```
Configure -> General -> Advanced -> Use Custom Workspace -> 

C:\Users\windows_rig3\StudioProjects\flutter_project
```

# Build Steps

```
Configure -> Build Steps -> Execute Windows batch command
```

```
git config --global --add safe.directory C:/flutter_windows_3.32.2-stable/flutter
flutter pub get
```

```
flutter build appbundle
```
