# [RecyclerView inside NestedScrollView does not give correct visible item position](https://stackoverflow.com/questions/48428793/recyclerview-inside-nestedscrollview-does-not-give-correct-visible-item-position)
## https://stackoverflow.com/a/48430598
If you put a `RecyclerView` inside a scrollable container—a `NestedScrollView` in your case—it will basically become a fancy `LinearLayout`, inflating and showing all the items at once. You get the first and last item as the first and last one visible because—to the RecyclerView—they are. All the items got inflated and added, so all of them are "visible on screen" inside the scrollable view.

The easy solution would be to just not nest the RecyclerView inside the NestedScrollView. A RecyclerView can scroll already, so you could just put whatever header or footer you need inside the RecyclerView as well. Nesting scrollable views always has drawbacks and you should try to avoid it whenever possible.
