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

## https://stackoverflow.com/a/37794947
To sum up all what i got form @user13 answer and other stackoverflow questions and blog posts i would like to share my finding to clear some very important aspects.

(user13) It's not bad practice to use android:configChanges, but it pretty easily can be, if you don't understand exactly what you're doing

Using this technique prevents you from easily using configuration specific resources. For instance, if you want your layout or drawables or strings or whatever to be different in portrait and landscapes, you have to manage it yourself if you use android:configChanges.

You need to override and use onConfigurationChanged() method to perform specific action if you decide to use android:configChanges
As user13 mentioned Activity is recreated not just due to orientation change but there are multiple reasons due to which activity can be restarted. Therefor activity restart should be handled for all causes. using android:configChanges only handles one case and there will be unhandled cases of activity restart which will cause a potential bug.
There are multiple and better ways to handle activity restart and plenty of help is also available on stactoverflow so android:configChanges should be used as a last resort according to documentation.
