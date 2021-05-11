# [Recyclerview onscrolllistener not working when setNestedScrollingEnabled to false](https://stackoverflow.com/questions/38179847/recyclerview-onscrolllistener-not-working-when-setnestedscrollingenabled-to-fals)
## https://stackoverflow.com/a/61155062
If you are recyclerView is embedded in any of the **NestedScrollView**, then you are supposed to attach the onScrollListener to NestedScrollView.
```
if (recyclerView.getLayoutManager() instanceof GridLayoutManager) {
    final GridLayoutManager gridLayoutManager = (GridLayoutManager) recyclerView.getLayoutManager();
    nestedScrollView.setOnScrollChangeListener(new NestedScrollView.OnScrollChangeListener() {
        @Override
        public void onScrollChange(NestedScrollView v, int scrollX, int scrollY, int oldScrollX, int oldScrollY) {
            if (scrollY == (v.getChildAt(0).getMeasuredHeight() - v.getMeasuredHeight()))  {
                totalItemCount = gridLayoutManager.getItemCount();
                lastVisibleItem = gridLayoutManager.findLastVisibleItemPosition();
                if (!loading
                        && totalItemCount <= (lastVisibleItem + visibleThreshold)) {
                    // End has been reached
                    // Do something
                    if (onLoadMoreListener != null) {
                        onLoadMoreListener.onLoadMore();
                    }
                    loading = true;
                }
            }
        }
    });
}
```
## https://stackoverflow.com/a/51493870
Do add setOnScrollChangeListner to your NestedScrollView
```
nestedScrollview.setOnScrollChangeListener(new NestedScrollView.OnScrollChangeListener() {
    @Override
    public void onScrollChange(NestedScrollView v, int scrollX, int scrollY, int oldScrollX, int oldScrollY) {
        if (scrollY == (v.getChildAt(0).getMeasuredHeight() - v.getMeasuredHeight()))  {
            if(loading)
                onClick();
            loading=false;
        }
    }
});
```

## https://stackoverflow.com/a/43062184
