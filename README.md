CustomMKAnnotationView
======================

A  Custom MKAnnotationView

example：



- (void)viewDidLoad
{
    [super viewDidLoad];

    self.annotations = @[@{@"latitude":@"30.281843",
                               @"longitude":@"120.102193",
                               @"title":@"test-title-1",
                               @"subtitle":@"test-sub-title-11"},
                             @{@"latitude":@"30.290144",
                               @"longitude":@"120.146696‎",
                               @"title":@"test-title-2",
                               @"subtitle":@"test-sub-title-22"},
                             @{@"latitude":@"30.248076",
                               @"longitude":@"120.164162‎",
                               @"title":@"test-title-3",
                               @"subtitle":@"test-sub-title-33"},
                             @{@"latitude":@"30.425622",
                               @"longitude":@"120.299605",
                               @"title":@"test-title-4",
                               @"subtitle":@"test-sub-title-44"}
                             ];
    
	self.mapView = [[MapView alloc] initWithDelegate:self];
    [self.view addSubview:_mapView];
    [_mapView setFrame:self.view.bounds];
    
    [_mapView beginLoad];
}


#pragma mark -
#pragma mark delegate

- (NSInteger)numbersWithCalloutViewForMapView
{
    return 0;
}

- (CLLocationCoordinate2D)coordinateForMapViewWithIndex:(NSInteger)index
{
    Item *item = [[Item alloc] initWithDictionary:[_annotations objectAtIndex:index]];
    CLLocationCoordinate2D coordinate;
	coordinate.latitude = [item.latitude doubleValue];
	coordinate.longitude = [item.longitude doubleValue];
    return coordinate;
}

- (UIImage *)baseMKAnnotationViewImageWithIndex:(NSInteger)index
{
    return [UIImage imageNamed:@"pin"];
}

- (UIView *)mapViewCalloutContentViewWithIndex:(NSInteger)index
{
    Item *item = [[Item alloc] initWithDictionary:[_annotations objectAtIndex:index]];
    TestMapCell  *cell = [[[NSBundle mainBundle] loadNibNamed:@"TestMapCell" owner:self options:nil] objectAtIndex:0];
    cell.title.text = item.title;
    cell.subtitle.text = item.subtitle;
    return cell;
}

- (void)calloutViewDidSelectedWithIndex:(NSInteger)index
{
    NSLog(@"%@",[_annotations objectAtIndex:index]);
}
