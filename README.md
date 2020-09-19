# DualUniverse-OreMonitor
This set of LUA scripts will help you setup screens that display ore name | quantity in L or T | % of how full a container is | status color coded based on ore % levels

## Change Log
9/19/2020 - Updated the spelling of Hematite through the T1 Scripts
9/18/2020 - Added a parameter call useL which by default is set to 1. By default the Qty value now displays the amount of ore in L rather than the total mass of the ore in tons. However, you can change the useL parameter to 0 to display the mass in tons. If you want to show mass you need to set the useL parameter to 0 in each board.

## Elements required

- 5 Screens M
- 5 Programming Boards
- 20 Item containers
- 1 Switch
- 1 Relay

## Control links Setup
These are the same type of links you use to link industries and containes in build mode. Each Programming board can support up to 10 links. You could modify the script/links to use less programming boards but I wanted to keep things organized/separated and also somewhat future proof if they add more ores per tier in the future.

** Important ** you must rename each slot to match the names in the scripts **

1. Programming Board 1 control links:
  - screen (same name in each Programming board for the slot linking to the screen)
  - bauxite ( linking to containing this particular ore )
  - coal ( linking to containing this particular ore )
  - hermatite ( linking to containing this particular ore )
  - quartz ( linking to containing this particular ore )
  - switch (sends on/off signals to the relay to turn on/off all the screens and programming boards)
  
2. Programming Board 2 - 5 control links:
- screen
- item container  ( rename to match the ores in each tier )
- item container  ( rename to match the ores in each tier )
- item container  ( rename to match the ores in each tier )
- item container  ( rename to match the ores in each tier )

3. Relay links:
link the relay to each screen and programing boards 2-5. So that by activating programming board one a signal will be sent to the switch which transmits that signal to the relay and the relay turns on/of every screen/programming board at once.

## Filters Setup
Under Unit add the following filters/code

1. start()
  `unit.setTimer("Live",1)`
  `switch.activate()` ** ONLY in Programming board 1 **
2. stop()3
  `switch.deactivate()` ** ONLY in Programming board 1 **
  `screen.clear()` ( not required but you can use to clear the html on the screen by deactivating the programming board linked to the screen )
3. tick(Live) (note that the name you enter for this tick needs to match the name of the timer entered in the start() filter above )

## Parameters
Each script containes two parameters per ore
- max<<orename>> ( This value represents the maximum mass in the container for this ore. This needs to be adjusted to account for 1. the difference on talents per player and 2. if you use different size containers per ore )
- weight<<orename>> ( Added this as a parameter just in case these values get adjusted in a future patch, it can be easily updated without touching the code )

## Script setup
In the lua editor enter the code for each script that matches the programming board. i.e programming board 1 under tick enter the code in T1 script and programing board 2 enter the code for T2 script etc
  
## Script Quick Setup
For each Tier script there is a quick setup file. The code in these files can be copied and to use simply right-click on a programming board > Advanced > Paste Lua configuration from clipboard. This will automatically name the slots, add filters and code. However, keep in mind you will still need to make the linkages and ensure each slot is linked to the correct container.
