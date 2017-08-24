## Game Programming Patterns

1. Command pattern

The command pattern is essentially just redux.  You decouple function calls from
the functions by instead issuing a series of commands.  The interface of a
command usually has a `execute()` method associated to it.  Due to the
functional nature of JavaScript you can actually easily create Command factories
using closures like this:

```javascript
function makeMoveUnitCommand(unit, x, y) {
  var xBefore, yBefore;
  return {
    execute: function() {
      xBefore = unit.x();
      yBefore = unit.y();
      unit.moveTo(x, y);
    },
    undo: function() {
      unit.moveTo(xBefore, yBefore);
    }
  };
}
```
