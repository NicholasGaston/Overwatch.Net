# Overwatch.Net

An unofficial player stats API for the Blizzard game "Overwatch". **Currently only supports PC players.**

## What is it?

It's a simple wrapper that grabs player stats from a users PlayOverwatch.com profile and parses it into a nice set of objects to be used however you like. It's written entirely in C# using AngleSharp to parse the data from the page. The only limiting factor is the speed at which the PlayOverwatch profile can be loaded.

## Current Features
* Entirely async operation
* Auto-generated objects - No need to compare strings, just use the statically typed objects.
* Serializable - No complex data.
* Region detection - Easily find the correct region for the pl

## Planned Features
Currently this is a very early working version with very few features beyond the ability to get and store data.
* JSON Serialisation out of the box courtesy of JSON.NET
* Events for refreshing cached data after a given amount of time
* Full proper error and exception handling
* Investigate the possibility of adding support for console players

## Dependencies

* AngleSharp - Used to parse the data from the PlayOverwatch page as no other data source is available from Blizzard.

## Usage

After you've added the necessary references to your project, using the library is incredibly simple.

The below code will create a new Overwatch player with the given Battletag, it will then detect the players region and update the users stats entirely asynchronously.
```csharp
OverwatchPlayer player = new OverwatchPlayer("SirDoombox#2603");
await player.DetectRegion();
await UpdateStats();
TimeSpan timePlayed = player.Stats.AllHeroes.Game.TimePlayed
```
You can cut down on some of the requests you need to make (and the time that those requests take up) by specifying the region at creation (if known). This snippet also uses `.GetAwaiter().GetResult()` to make the method run in a synchronous fashion.
```csharp
OverwatchPlayer player = new OverwatchPlayer("SirDoombox#2603", Region.eu);
player.UpdateStats().GetAwaiter().GetResult();
TimeSpan timePlayed = player.Stats.AllHeroes.Game.TimePlayed
````
There are also some helper methods available for use to simplify some common operations
```csharp
bool validTag = OverwatchAPIHelpers.IsValidBattletag("SomePlayer#1234"); // Returns true.
string profileUrl = OverwatchAPIHelpers.ProfileUrl("SomePlayer#1234", Region.eu); // Returns a PlayOverwatch profile URL.
```

## Contact
If you wish to contact me about contributing to the project, or have any questions / suggestions please feel free to come find me on the [C# discord server.](https://discord.gg/0np62rq4o8GnQO9l "C# Discord")

Please report any issues or bugs that you may find at your earliest convenience so I can get them fixed ASAP.
