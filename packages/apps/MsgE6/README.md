# packages/apps/MsgE6

### MsgPowerOffActivity / MsgQsgActivity

These two activities draw power off screen when device is being turned off.

Called from `frameworks/base/services/java/com/android/server/power/ShutdownThread.java`,
and this [code](https://github.com/rbx-rdm/pp1-frameworks/blob/27480b1d4244903925f4d3d94e0b6fe422b5031c/base/services/java/com/android/server/power/ShutdownThread.java#L134) decides which (PowerOff / Qsg) should be called.
