# iOS

## SceneDelegate vs AppDelegate in iOS 13
Part of Responsibility of AppDelegate is delegated to SceneDelegate. Now our app can have multiple scenes. By Default, our app will have one Scene called as UIWindowScene. The App's Info.plist must keep track of the number of Scenes Being used in a particular app under `Application Scene Manifest`. A window is like a Backdrop derived from Microsoft Windows.



## UITableViewDiffableDataSource
  ### The Problem
  When there is a need to partially update the tableview's contents. We use apis like 
tableView.beginUpdates()
tableView.insertRows(at: [IndexPath], options: .automatic)
tableView.endUpdates()

   to update the tableview and before that, we have to ensure to set appropriate datasource for the updation we intend to perform. This is tedious as the number of inserts/updates/deletes grow.
 
  ### Idea
  UITable Diffable datasource helps us manage the datasource with the help of snapshot. Which acts as single source of truth between our view and datasource.
  When there is a change in data source, construct new snapshot and apply it to the current snapshot.


## Static and dynamic Libraries
- Static libraries can have only the code but not assets/resources like nib, images, coredata etc. Whereas a dynamic library can have both code and resource. For a static library to have resource, it can shipped with an accompanying bundle. 
- In the build settings of a framework search for `Mach-O type` which specifies what type of library it is (dyn/stat/executable etc)
- A framework can have either static or dynamic libraries
- *Dynamic libraries* are linked at runtime using a dynamic linker while, *static libraries* are linked at compile time with static linker.
- Performance wise Static libraries are relatively faster when starting the app, because the app skips the dynamic linking phase of the app which happens at runtime.
- Static library will increase the size of the app because all the libs code is inside the binary.
- While adding a framework to the app there's an option called `Embed and sign`, `Do not embed` &, `Embed w/o sign`
- When we're importing static library to an app, it is unnecessary to embed it, because, the static library's code would already have been compiled along with original app's source code and the app executable contains the code of static library as well.
- When we're importing dynamic library to an app, it is essentila to choose `embed` otherwise at runtime, when the library is getting accessed from the app, the linker won't find it and crash the app.
- If the framework you add is already signed, we can choose, embed but don't sign. Otherwise `embed and sign`.

## Appdelegate UIWindow tip:
- It is important to understand that every time the window's root view controller is changed/modified, we should ensure that `window.makeKeyAndVisible()` is being called. If not the window will go black as you update the view controller.
