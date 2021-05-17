# UsefulClasses
Classes that are useful for minecraft spigot development (at least for me)<br>
<br>
Useful Links:<br>
<ul>
    <li>DeluxeMenus Menu Creator: https://devmc.org/en/dm-constructor</li>
</ul>
<br>
<b>Current Class:</b><br>
<ul>
    <li>UpdateChecker</li>
    <li>ConfigUpdater</li>
</ul>

# UpdateChecker (by Choco)
<b>Original Link</b>: https://www.spigotmc.org/threads/an-actually-decent-plugin-update-checker.344327/ <br>
<b>Description</b>: Checking if there's a new version for specific plugin. <br>
<br>
<b>Example usage</b>:<br>
```java
// UpdateChecker.init(javaPlugin, resourceId)
UpdateChecker.init(this, 12038).requestUpdateCheck().whenComplete((result, exception) -> {
    if (result.requiresUpdate()) {
        this.getLogger().info(String.format("An update is available! VeinMiner %s may be downloaded on SpigotMC", result.getNewestVersion()));
        return;
    }

    switch(result.getReason()){
      case UP_TO_DATE:{
        this.getLogger().info(String.format("Your version of VeinMiner (%s) is up to date!", result.getNewestVersion()));
        break;
      }
      
      case UNRELEASED_VERSION:{
        this.getLogger().info(String.format("Your version of VeinMiner (%s) is more recent than the one publicly available. Are you on a development build?", result.getNewestVersion()));
        break;
      }
      
      default:{
        this.getLogger().warning("Could not check for a new version of VeinMiner. Reason: " + reason);
        break;
      }
      
    }
   
});
```

# ConfigUpdater
<b>Original Link</b>: https://www.spigotmc.org/threads/configupdater-keep-comments-and-values.398466/ <br>
<b>Description</b>: Updating configuration files and keep the comments and the value, and also you can ignore configuration section to be updated. <br>
<br>
<b>Example Usage</b>:
```java
try {

  File configFile = new File(this.getDataFolder(), "config.yml");
  List<String> ignoredSections = Arrays.asList("ignored", "section");

  // 1st parameter = plugin instance.
  // 2nd parameter = the file name on your plugin to get the comments and the values from.
  // 3rd parameter = the file on the server that want to be updated.
  // 4th parameter = the list of configuration section that want to be ignored.
  ConfigUpdater.update(plugin, "config.yml", configFile, ignoredSections);//The list is sections you want to ignore
  
} catch (IOException e) {

  System.out.println("Failed to update the config!");
  e.printStackTrace();
  
}
```
