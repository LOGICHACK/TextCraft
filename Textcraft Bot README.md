# **Textcraft Discord Bot**

A text-based survival, crafting, and exploration game played within Discord, inspired by Minecraft. Explore different biomes, gather resources, fight mobs, discover recipes, and even add your own content through mods\!

## **Features**

* **World Exploration:** Navigate a grid-based world using \!walk \<direction\>.  
* **Biomes:** Procedurally generated world using different biome types defined in JSON files.  
* **Resource Gathering:** Use \!mine \[item\] to gather general resources or target specific items in locations found via \!look.  
* **Crafting System:**  
  * Craft items by specifying the result (\!craft \<item\_name\>).  
  * Experiment by combining ingredients (\!craft \<ingredient1\> \<ingredient2\> ...).  
* **Recipe Discovery:** Be the first in your world to craft an item to discover its recipe\! Use \!recipes to see all discovered recipes.  
* **Combat:** Encounter mobs while walking or mining. Basic combat resolution based on equipped weapon (from toolbelt) and mob stats.  
* **Toolbelt & Inventory:** Manage tools/weapons separately from general items. Tools have durability.  
* **Basic Needs:** Track health (\!health) and restore it by eating food (\!eat \<food\_item\>).  
* **Mod Support:** Easily add new biomes, items, and recipes by creating new subdirectories and JSON files.  
* **Server Configuration:** Admins can configure event channels, leaderboards, enabled mods, and regenerate worlds (\!config, \!mods, \!regenworld).  
* **Leaderboards:** Per-server leaderboards tracking configurable stats (default: diamonds\_mined).  
* **Utilities:** \!give (with confirmation), \!ping, \!invite, \!support.

### **Per-Server (\!config command \- Admin Only)**

* \!config use\_global\_world \<true|false\>: Sets whether the server uses the shared global world or its own unique world file. Player data storage follows this setting.  
* \!config events\_channel\_id \<\#channel|ID|none\>: Sets the channel for important announcements (deaths, diamond finds).  
* \!config enable\_leaderboard \<true|false\>: Toggles the per-server leaderboard.  
* \!config leaderboard\_stat \<stat\_name\>: Sets the stat used for the per-server leaderboard. Allowed: health, diamonds\_mined, chunks\_discovered, recipes\_discovered.

## **Commands**

*(See \!help in Discord for a dynamically generated list)*

**Player Commands:** walk, look, mine, craft, give, inventory, health, eat, recipes, ping, invite, support

**Admin Commands:** config, mods, regenworld

**Owner Commands:** damage, serverranks

## **Modding Guide**

Create new gameplay experiences by adding your own content\!

### **Directory Structure**

Place your mod's files in subdirectories named after your mod within the base data folders:

* biomes/YourModName/some\_biome.json  
* items/YourModName/your\_items.json  
* recipes/YourModName/your\_recipes.json

### **Creating Files**

* **Use JSON format.** Ensure files are valid JSON (no comments inside, correct brackets/commas/quotes).  
* Use the provided template files (mod\_example\_biome, mod\_example\_items, mod\_example\_recipes) as a starting point. **Remember to remove the // comments from the templates before saving your .json files\!** Refer to the separate files for detailed field explanations without invalidating comments.

### **Key Concepts**

* **Items:** Define all new materials, tools, weapons, food, loot, etc., in items/YourModName/your\_items.json.  
  * Use type to categorize (e.g., material, tool, weapon, food).  
  * Use tags for tools/weapons (e.g., \["axe", "basic\_tool"\]) so the game knows their function. The first tag is often the primary type used in requirements (e.g., "axe"). Add "basic\_tool" or "standard\_tool" etc., for potential priority logic.  
  * Use heal for food items.  
* **Biomes:** Define environments in biomes/YourModName/your\_biome.json.  
  * Set description, optional name and image\_url.  
  * Define generally items\_mineable and the required\_tool\_tag (or null).  
  * Define specific locations with their own items and required\_tool\_tag.  
  * Define mobs with stats (damage), resistances/weaknesses (default\_effectiveness, weapon\_effectiveness), encounter difficulty (escape\_threshold, kill\_threshold), and loot.  
* **Recipes:** Define crafting recipes in recipes/YourModName/your\_recipes.json.  
  * The key is the result item name.  
  * ingredients list items consumed from inventory (counts matter).  
  * Set durability and type (tool, weapon, material, etc.) for the crafted item. The type determines if it goes to the toolbelt or inventory.

*(Note: Items and Recipes from all mods are loaded globally by the bot, but they will only be obtainable or craftable if the necessary biomes/ingredients are present in a specific world).*