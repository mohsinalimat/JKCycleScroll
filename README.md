# JKCycleScroll
简单易用的无限轮播器. 支持横向、竖向两种滑动方式


## Usage

### 1.Installation

#### JKCycleScrollView is available through [CocoaPods](http://cocoapods.org). To install it, simply add the following line to your Podfile:

```ruby
pod 'JKCycleScrollView', '~> 0.1.0'
```

### 2.初始化JKCycleScrollView

#### 定义JKCycleScrollView对象

```objective-c
@property (nonatomic, strong) NSArray  *data;
@property (nonatomic, strong) JKCycleScrollView *scrollView;
```
#### 初始化scrollView

```objective-c
 - (JKCycleScrollView *)scrollView {
        if (!_scrollView) {
          _scrollView = [[JKCycleScrollView alloc] initWithFrame:CGRectZero scrollDirection:UICollectionViewScrollDirectionHorizontal];
          _scrollView.backgroundColor = [UIColor orangeColor];
          _scrollView.delegate = self;
          _scrollView.dataSource = self;
          _scrollView.scrollType = JKScrollTypeAutoCyclically;
          [_scrollView registerClass:[TestCell class] forCellWithReuseIdentifier:kCycleScrollViewReuseIdentifer];
          _scrollView.translatesAutoresizingMaskIntoConstraints = NO;
          [self.view addSubview:_scrollView];
          [self.view addConstraints:[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-20-[_scrollView]-20-|" options:0 metrics:nil views:NSDictionaryOfVariableBindings(_scrollView)]];
          [self.view addConstraints:[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-100-[_scrollView(204)]" options:NSLayoutFormatAlignAllTop metrics:nil views:NSDictionaryOfVariableBindings(_scrollView)]];
        }
        return _scrollView;
     }
```   
#### 初始化数据源

```objective-c
self.data = @[@"http://img.pconline.com.cn/images/upload/upc/tx/photoblog/1410/21/c4/39944979_39944979_1413878416125_mthumb.jpg",@"http://image92.360doc.com/DownloadImg/2015/12/1715/63143393_18.jpg",@"http://f.hiphotos.baidu.com/image/pic/item/b151f8198618367a9f738e022a738bd4b21ce573.jpg",@"http://img006.hc360.cn/hb/MTQ2MDc5MzQ2ODQyNy02OTQyMjQ1MjI=.jpg"];
```   
#### 刷新视图

```objective-c
[self.scrollView reloadData];
```   
    
### 3.实现JKCyclicScrollViewDataSource和JKCyclicScrollViewDelegate协议

```objective-c
    #pragma mark - JKCyclicScrollViewDataSource
    - (NSInteger)numberOfItemsInCollectionView:(JKCycleScrollView *)collectionView{
        return [self.data count];
    }
    
    - (UICollectionViewCell *)collectionView:(JKCycleScrollView *)collectionView cellForItemAtIndex:(NSInteger)index{
        TestCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:kCycleScrollViewReuseIdentifer]；
        NSString *url = self.data[index];
        [cell.imageView sd_setImageWithURL:[NSURL URLWithString:url]];
        return cell;
    }
    
    #pragma mark - JKCyclicScrollViewDelegate
    - (void)collectionView:(JKCycleScrollView *)collectionView didSelectItemAtIndex:(NSInteger)index{
        NSLog(@"didSelectItemAtIndex: %@",@(index));
    }
    - (void)collectionView:(JKCycleScrollView *)collectionView didScrollToIndex:(NSInteger)index{
        NSLog(@"didScrollToIndex: %@",@(index));
    }
```


## Author

iJecky <http://weibo.com/rubbishpicker>

## License

JKCycleScroll is available under the MIT license. See the [LICENSE](LICENSE) file for more info.
