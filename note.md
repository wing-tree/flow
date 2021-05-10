# [why using android:configChanges is a bad practice](https://stackoverflow.com/questions/37787042/why-using-androidconfigchanges-is-a-bad-practice)
## https://stackoverflow.com/a/37787357
For example, one of these reasons is when your app is in the background and the OS decides to kill it (with your `Activity`, of course) to reclaim memory.

When you return to your app, the OS will try to recreate your `Activity` as you left it, but will fail to do so, because you decided not to bother with it, just used `android:configChanges` in your Manifest.

If you make sure your app can recover properly from a restart, `android:configChanges` might not be necessary at all. Because of this, the **need** to use `android:configChanges` might indicate some flaw in your app, that may worth to take a look at.

It's not bad practice to use `android:configChanges`, but it pretty easily can be, if you don't understand exactly what you're doing.

## https://stackoverflow.com/a/47720410
Using android:configChanges is good practice if you know what you are doing.

Just always test how your application how it behaves when it is restarted by system to stay comfortable for user so some state has to be saved all the time but not all. With config changes like this:

`android:configChanges="locale|keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"`

Your application will restart rather rarely on new devices that have a lot of memory. If it restarts it's not so unexpected for user anyway, as user had attention elsewhere and came back to app. User don't have to be in exact same state after restart if it happens by manual killing of application or application restart because of some other heavy tasks (playing game) user is doing, the user experience is important here.

If you need to refresh List just for different layouts for orientations changes or you need to hide some view elements you can call:

```
public void onConfigurationChanged(Configuration newConfig) {
    super.onConfigurationChanged(newConfig);
    _list.reloadData();
    _editorButton.visible(isPortrait());
}
```
