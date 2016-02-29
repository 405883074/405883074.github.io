##2016年2月26日

####Problem: UITableView截图
URL: https://github.com/davidman/DHSmartScreenshot

####Read
类UITraitCollection来封装水平和垂直方向的Size信息
```
- (void)willTransitionToTraitCollection:(UITraitCollection *)newCollection withTransitionCoordinator:(id )coordinator {
    [super willTransitionToTraitCollection:newCollection withTransitionCoordinator:coordinator];
    [coordinator animateAlongsideTransition:^(id  context) {
        if (newCollection.verticalSizeClass == UIUserInterfaceSizeClassCompact) {
        //To Do: modify something for compact vertical size
        } else {
        //To Do: modify something for other vertical size
        }
        [self.view setNeedsLayout];
    } completion:nil];
}
```

#2016年2月29日

####Problem: 离线缓存
URL: https://github.com/AFNetworking/AFNetworking、https://github.com/ibireme/YYWebImage

1. AFNetworking 为 Get 请求方式配置缓存策略
``` 
// 缓存策略（有缓存就用缓存，没有缓存就重新请求）    
requestSerializer.cachePolicy = NSURLRequestReturnCacheDataElseLoad;    
// 清空缓存
NSURLCache *urlCache = [NSURLCache sharedURLCache];
[urlCache removeAllCachedResponses];
```
2. YYWebImage 图片缓存
``` 
YYImageCache *cache = [YYWebImageManager sharedManager].cache;
// 获取缓存大小
cache.memoryCache.totalCost;
cache.memoryCache.totalCount;
cache.diskCache.totalCost;
cache.diskCache.totalCount;
// 清空缓存
[cache.memoryCache removeAllObjects];
[cache.diskCache removeAllObjects];
// 清空磁盘缓存，带进度回调
[cache.diskCache removeAllObjectsWithProgressBlock:^(int removedCount, int totalCount) {
    // progress
} endBlock:^(BOOL error) {
    // end
}];
```