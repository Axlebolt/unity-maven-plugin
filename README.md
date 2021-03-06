# unity-maven-plugin

## Latest Version
0.2

## Description

A maven plugin that will be used to build unity projects

## Pom.xml information

In order to use this plugin, add the following to your pom.xml

```
<plugin>
	<groupId>ca.mestevens.unity</groupId>
	<artifactId>unity-maven-plugin</artifactId>
	<version>${xcode.maven.plugin.version}</version>
	<extensions>true</extensions>
</plugin>
```

where `${xcode.maven.plugin}` is the version of the plugin you want to use.

## Goals

### open

This goal will open your project with the unity game engine.

```shell
mvn unity:open
```

### open-solution

This goal will open your project's solution with your default editor.

```shell
mvn unity:open-solution
```

### unity-initialize

This goal will create a bunch of the folders that are used by other goals in the plugin

#### Properties

* unity.plugins.directory
	* A string representing where the maven dependencies will be copied to. Default value is `Assets/Runtime/Plugins`
* unity.test.plugins.directory
	* A string representing where the test maven dependencies will be copied to. Default value is `Assets/Editor/Plugins`
* unity.ios.plugins.directory
	* A string representing where the .ios-plugin files will be extracted to. Default value is `Assets/Plugins/iOS`
* unity.android.plugins.directory
	* A string representing where the .android-plugin files will be extracted to. Default value is `Assets/Plugins/Android`

### unity-library-dependencies

This goal will gather all the specified dependencies in your pom.xml file and place them under /Assets/Runtime/Plugins.

#### Properties

* unity.plugins.directory
	* A string representing where the maven dependencies will be copied to. Default value is `Assets/Runtime/Plugins`

### unity-copy-test-dependencies

This goal will gather all the specified dependencies with scope `test` in your pom.xml file and place them under /Assets/Editor/Plugins.

#### Properties

* unity.test.plugins.directory
	* A string representing where the test maven dependencies will be copied to. Default value is `Assets/Editor/Plugins`

### unity-sync-mono-project

This goal runs the sync monodevelop project command in unity. This is mainly used to make sure the .sln files exist.

### unity-android-build

Will build your unity project as a google android studio project in your target directory, as well as create a pom with any jar or aar dependencies you had in the unity pom.

#### Properties

* unity.path
	* A string representing the path to unity. Defaults to `/Applications/Unity/Unity.app/Contents/MacOS/Unity`
* scenes
	* A list of scenes you want included in the build. Defaults to an empty list, which will build all the scenes in your unity project.
* android.project.target.directory
	* The directory to put the android build in. Defaults to `target`
* unity.project.name
	* The name of your unity project. Defaults to `${project.artifactId}`

### unity-android-package-apk

Will take the build android project generated by `unity-android-build` and create an apk out of it. With parameters, you can also have this start an android emulator, and install the apk on it.

#### Properties

* unity.project.name
	* The name of your unity project. Defaults to `${project.artifactId}`
* android.emulator.name
	* The name of the avd you want to start. Defaults to `default`
* android.start.emulator
	* Whether or not the goal should start an android emulator for you. If you specify this property, you probably want to specify `android.emulator.name`. Defaults to `false`
* android.emulator.wait.time
	* The amount of time (in milliseconds), that the goal should wait for the emulator to start up. Default value is 60000 (60 seconds).
* android.deploy.to.devices
	* Whether or not the goal should deploy your apk to the currently running avds. Defaults to `false`

### unity-xcode-build

Will build your unity project as an xcode project in your target directory, as well as create a pom with any xcode-framework dependencies you had in the unity pom.

#### Properties

* unity.path
	* A string representing the path to unity. Defaults to `/Applications/Unity/Unity.app/Contents/MacOS/Unity`
* scenes
	* A list of scenes you want included in the build. Defaults to an empty list, which will build all the scenes in your unity project.
* xcode.project.target.directory
	* The directory to put the xcode build in. Defaults to `target`
* unity.project.name
	* The name of your unity project. Defaults to `${project.artifactId}`

### unity-build-dll

Will build your unity-library project as a dll using xbuild.

#### Properties

* xbuild.location
	* The location of the xbuild executable. Default value is `/Applications/Unity/Unity.app/Contents/Frameworks/MonoBleedingEdge/bin/xbuild`
* unity.solution.name
	* The name of the .sln file that will be used to build the dll. Default value is `${project.artifactId}.sln`
* unity.dll.name
	* The name of the dll that will be built. Default value is `${project.artifactId}-${project.version}`

### unity-package-dll

Packages the dll created by unity-build-dll for installation/deployment as a unity-library. This will also package the files under `Assets/Plugins/iOS` as an ios-plugin and the files under `Assets/Plugins/Android` as an android-plugin.

#### Properties
* unity.dll.name
	* The name of the dll that will be built. Default value is `${project.artifactId}-${project.version}`
	
### Release Notes

* 0.2
	* Initial release