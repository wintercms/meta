# Build 450 (IN PROGRESS):

## UX/UI Improvements:
-

## API Changes:
- `input()`, `get()`, & `post()` now pull values from the `Request` app container instead of directly from the PHP superglobals
- Execution context is now handled in the application container
- All uses of of `exit()` or `die()` removed to support being run under a concurrent server (i.e. Swoole)

## Bug Fixes:
-

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