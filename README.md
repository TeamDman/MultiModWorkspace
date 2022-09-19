# MultiModWorkspace

A workspace for developing multiple mods simultaneously.

See also: [McJty's workspace](https://github.com/McJtyMods/MultiWorkspace)

## Setting up a multi-mod workspace from scratch

1. Download forge MDK from [here](https://files.minecraftforge.net/)
2. Create a dir for the multi mod workspace
3. From the MDK, copy the following files to the workspace:
    - gradle/
    - gradlew
    - gradlew.bat
    - settings.gradle
4. Create an empty `build.gradle` file in the workspace
5. Create a folder called `workspace` in the workspace
6. To the `myworkspace/workspace` folder you just created, copy from the MDK again:
    - gradle/
    - build.gradle
    - gradlew
    - gradlew.bat
7. Clone the mods you want to use into their own sub-folders in the workspace, e.g., `myworkspace/SuperFactoryManager`
8. Edit `myworkspace/settings.gradle` to add the following lines below the `pluginManagement` block provided in the MDK

   ```gradle
   include 'SuperFactoryManager' // do this for your mods
   include 'workspace'
   ```

   You should also copy and custom stuff from any of your individual mods' `settings.gradle` file, since only the root one will be loaded.
   Your individual mods should still keep the `settings.gradle` file so they can be built independently.

9. In `myworkspace/workspace/build.gradle` inside each of the `minecraft.runs.*.mods` blocks, add a reference to each of your mods.

   Example:

   ```gradle
   RFToolsStorage {
      source project(':RFToolsStorage').sourceSets.main
   }
   RFToolsBase {
      source project(':RFToolsBase').sourceSets.main
   }
   ```
   
   Optionally, also change the workingDirectory to be different for each run config.
   
   Don't forget to also remove the `examplemod` blocks.

10. Inside the same build.gradle from the previous step, go to the dependencies block and add the following:

   ```gradle
      implementation project(':SuperfactoryManager')
   ```

10. Open IntelliJ and point it to the empty build.gradle `myworkspace/build.gradle`
11. Run `genIntellijRuns` and select the `workspace` module, pick `myrootmodule.workspace.main`
12. Hit Shift-F5 (reload from disk) on the top most element in the project browser until the new run configurations show up
13. Run the `workspace runClient` runconfig, it should ask you to pick the module
14. Don't forget to set up your license, README, and git stuff for the multi workspace. Git should avoid committing the mods to the multi-repo.


### Troubleshooting


If none of your issues are listed here, check out the [MinecraftForge Discord](https://discord.gg/forge).  
Make sure to use the search box before asking for help.  
Make sure to use the correct channels when asking for help.  
Make sure to visit [dontasktoask.com](https://dontasktoask.com/) before asking for help.  


---

`Caused by: java.lang.module.InvalidModuleDescriptorException: Unsupported major.minor version 60.0`

Make sure you're using the correct java version.  
Project structure (Ctrl+Alt+Shift+S) -> SDK should be `Java 17`

---

```log
Build file 'D:\Repos\Minecraft\Forge\MultiModWorkspace\SuperFactoryManager\build.gradle' line: 12

Plugin [id: 'net.minecraftforge.gradle', version: '5.1.+'] was not found in any of the following sources:

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
```

Make sure you have the `pluginManagement` block inside the root `settings.gradle` file.

---

```log
Exception in thread "main" java.lang.IllegalStateException: Could not find forge-1.19.2-43.1.1 in classpath
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.targets.CommonUserdevLaunchHandler.lambda$findJarOnClasspath$2(CommonUserdevLaunchHandler.java:46)
	at java.base/java.util.Optional.orElseThrow(Optional.java:403)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.targets.CommonUserdevLaunchHandler.findJarOnClasspath(CommonUserdevLaunchHandler.java:46)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.targets.ForgeUserdevLaunchHandler.processStreams(ForgeUserdevLaunchHandler.java:17)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.targets.CommonUserdevLaunchHandler.getMinecraftPaths(CommonUserdevLaunchHandler.java:34)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.moddiscovery.MinecraftLocator.scanMods(MinecraftLocator.java:36)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.moddiscovery.ModDiscoverer.discoverMods(ModDiscoverer.java:74)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.FMLLoader.beginModScan(FMLLoader.java:166)
	at MC-BOOTSTRAP/fmlloader@1.19.2-43.1.2/net.minecraftforge.fml.loading.FMLServiceProvider.beginScanning(FMLServiceProvider.java:86)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.TransformationServiceDecorator.runScan(TransformationServiceDecorator.java:112)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.TransformationServicesHandler.lambda$runScanningTransformationServices$8(TransformationServicesHandler.java:100)
	at java.base/java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197)
	at java.base/java.util.HashMap$ValueSpliterator.forEachRemaining(HashMap.java:1779)
	at java.base/java.util.stream.AbstractPipeline.copyInto(AbstractPipeline.java:509)
	at java.base/java.util.stream.AbstractPipeline.wrapAndCopyInto(AbstractPipeline.java:499)
	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:575)
	at java.base/java.util.stream.AbstractPipeline.evaluateToArrayNode(AbstractPipeline.java:260)
	at java.base/java.util.stream.ReferencePipeline.toArray(ReferencePipeline.java:616)
	at java.base/java.util.stream.ReferencePipeline.toArray(ReferencePipeline.java:622)
	at java.base/java.util.stream.ReferencePipeline.toList(ReferencePipeline.java:627)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.TransformationServicesHandler.runScanningTransformationServices(TransformationServicesHandler.java:102)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.TransformationServicesHandler.initializeTransformationServices(TransformationServicesHandler.java:55)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.Launcher.run(Launcher.java:87)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.Launcher.main(Launcher.java:77)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.BootstrapLaunchConsumer.accept(BootstrapLaunchConsumer.java:26)
	at MC-BOOTSTRAP/cpw.mods.modlauncher@10.0.8/cpw.mods.modlauncher.BootstrapLaunchConsumer.accept(BootstrapLaunchConsumer.java:23)
	at cpw.mods.bootstraplauncher@1.1.2/cpw.mods.bootstraplauncher.BootstrapLauncher.main(BootstrapLauncher.java:141)

Process finished with exit code 1
```

You probably updated your Forge version without running `genIntellijRuns` again.

---

`Missing 'minecraft' dependency.`

Make sure to edit `myworkspace/settings.gradle` to include all your mods.

Make sure to view the full gradle logs, sometimes there is more information there.

---

> No errors, but some mods not being loaded

Make sure to run `genIntellijRuns` after adding new mods to the workspace.

---

```log
[17:34:15] [modloading-worker-0/ERROR] [ne.mi.fm.ja.FMLModContainer/LOADING]: Failed to create mod instance. ModID: geoscopes, class ca.teamdman.geoscopes.Geoscopes
java.lang.IllegalAccessException: class net.minecraftforge.fml.javafmlmod.FMLModContainer (in module javafmllanguage) cannot access a member of class ca.teamdman.geoscopes.Geoscopes (in module geoscopes) with modifiers "private"
	at jdk.internal.reflect.Reflection.newIllegalAccessException(Reflection.java:392) ~[?:?] {}
	at java.lang.reflect.AccessibleObject.checkAccess(AccessibleObject.java:674) ~[?:?] {}
	at java.lang.reflect.Constructor.newInstanceWithCaller(Constructor.java:489) ~[?:?] {}
	at java.lang.reflect.Constructor.newInstance(Constructor.java:480) ~[?:?] {}
	at net.minecraftforge.fml.javafmlmod.FMLModContainer.constructMod(FMLModContainer.java:68) ~[javafmllanguage-1.19.2-43.1.2.jar%23184!/:?] {}
	at net.minecraftforge.fml.ModContainer.lambda$buildTransitionHandler$10(ModContainer.java:121) ~[fmlcore-1.19.2-43.1.2.jar%23187!/:?] {}
	at java.util.concurrent.CompletableFuture$AsyncRun.run(CompletableFuture.java:1804) [?:?] {}
	at java.util.concurrent.CompletableFuture$AsyncRun.exec(CompletableFuture.java:1796) [?:?] {}
	at java.util.concurrent.ForkJoinTask.doExec(ForkJoinTask.java:373) [?:?] {}
	at java.util.concurrent.ForkJoinPool$WorkQueue.topLevelExec(ForkJoinPool.java:1182) [?:?] {}
	at java.util.concurrent.ForkJoinPool.scan(ForkJoinPool.java:1655) [?:?] {}
	at java.util.concurrent.ForkJoinPool.runWorker(ForkJoinPool.java:1622) [?:?] {}
	at java.util.concurrent.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:165) [?:?] {}
```

Make sure your `mods.toml` file uses `kotlinforforge` instead of `javafml` if it's a Kotlin mod [ref](https://github.com/thedarkcolour/KotlinForForge).

---

```log
[17:45:52] [Render thread/FATAL] [ne.mi.fm.ModLoader/CORE]: Error during pre-loading phase
net.minecraftforge.fml.ModLoadingException: Mod File main needs language provider kotlinforforge:43 or above to load
§7We have found 3.7.1
```

Make sure to edit the `mods.toml` `loaderVersion` property if using Kotlin [ref](https://github.com/thedarkcolour/KotlinForForge)

---

```log
[17:50:40] [Render thread/FATAL] [ne.mi.fm.ModLoader/CORE]: Error during pre-loading phase
net.minecraftforge.fml.ModLoadingException: Mod File main needs language provider kotlinforforge:3 or above to load
§7We have found none
	at net.minecraftforge.fml.ModLoadingException.lambda$fromEarlyException$0(ModLoadingException.java:50) ~[fmlcore-1.19.2-43.1.2.jar%23187!/:?] {}
	at java.util.stream.ReferencePipeline$3$1.accept(ReferencePipeline.java:197) ~[?:?] {}
```

Make sure `myworkspace/workspace/build.gradle` has the Kotlin plugins and stuff added as well [ref](https://github.com/thedarkcolour/KotlinForForge).

---

> Kotlin mods not building when running `workspace runClient`

Edit the run config to Build Project instead of just Build

## Starting a new mod

1. Download the Forge MDK for the version of forge your projects are using from [here](https://files.minecraftforge.net)
2. Create a [new GitHub repo](https://github.com/new) for your mod
3. Clone the new repo to the workspace root
4. Copy to the cloned repo the following files from the MDK
   - gradle/
   - src/
   - .gitattributes
   - .gitignore
   - build.gradle
   - gradle.properties
   - gradlew
   - gradlew.bat
   - settings.gradle
5. Edit `myworkspace/mynewmod/build.gradle` to have the appropriate details for the new mod (version, group, archiveBaseName)
6. Edit `myworkspace/workspace/build.gradle` `minecraft.runs` and `dependencies` blocks to include the new mod.
7. Edit `myworkspace/settings.gradle` to include the new mod
8. Run `genIntellijRuns`

## FAQ

> Do all the mods have to use the same Forge version?

I accidentally had mods using different forge patch versions, so apparently you CAN have different versions.

---

> There's a bunch of duplicate stuff in the double-shift menu when searching now, how2fix?

Looks like IDEA is indexing the mappings for each subproject separately.  
Idk how to fix.

---

> What if two mods both load JEI in their dependencies?

Make sure they're the same version I guess?  
I'm not having issues with it.