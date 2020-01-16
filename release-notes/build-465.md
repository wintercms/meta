# Build 465:

## UX/UI Improvements:
-

## API Changes:
- Type hint for `registerSchedule` method in `PluginBase` updated to correctly hint the `Illuminate\Console\Scheduling\Schedule` object that is passed to it.

## Bug Fixes:
- Fixed issue with the `queueOn` and `laterOn` methods of the `Mail` facade throwing an invalid argument exception due to queue name string being defined where the queue manager is meant to be defined. The queue name is now injected into the `Mailable` object that is created, and the default queue manager is used instead.

## Security Improvements
-

## Translation Improvements:
-

## Performance Improvements:
-

## Community Improvements:
-

## Dependencies
-
