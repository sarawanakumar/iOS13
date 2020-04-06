# iOS13

## SceneDelegate vs AppDelegate
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
