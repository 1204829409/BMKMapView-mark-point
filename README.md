# BMKMapView-mark-point
how to  mark point with BaiDu map

//  Created by KMS on 16/10/20.
//  Copyright © 2016年 KMS. All rights reserved.
//

#import <UIKit/UIKit.h>

#import <BaiduMapAPI_Base/BMKBaseComponent.h>
@interface AppDelegate : UIResponder <UIApplicationDelegate, BMKGeneralDelegate> {
    UIWindow *window;
    UINavigationController *navigationController;
}

@property (strong, nonatomic) UIWindow *window;
@property (nonatomic, retain)  UINavigationController *navigationController;

@end

___________________________________________________________________________________



//  Created by KMS on 16/10/20.
//  Copyright © 2016年 KMS. All rights reserved.
//

#import "AppDelegate.h"
#import <BaiduMapAPI_Map/BMKMapComponent.h>


#import <BaiduMapAPI_Base/BMKBaseComponent.h>//引入base相关所有的头文件

#import <BaiduMapAPI_Map/BMKMapComponent.h>//引入地图功能所有的头文件

#import <BaiduMapAPI_Search/BMKSearchComponent.h>//引入检索功能所有的头文件

#import <BaiduMapAPI_Cloud/BMKCloudSearchComponent.h>//引入云检索功能所有的头文件

#import <BaiduMapAPI_Location/BMKLocationComponent.h>//引入定位功能所有的头文件

#import <BaiduMapAPI_Utils/BMKUtilsComponent.h>//引入计算工具所有的头文件

#import <BaiduMapAPI_Radar/BMKRadarComponent.h>//引入周边雷达功能所有的头文件

#import <BaiduMapAPI_Map/BMKMapView.h>//只引入所需的单个头文件


@interface AppDelegate ()

@end

BMKMapManager* _mapManager;
@implementation AppDelegate

@synthesize window;
@synthesize navigationController;




- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    // 要使用百度地图，请先启动BaiduMapManager
    _mapManager = [[BMKMapManager alloc]init];
    BOOL success =  [_mapManager start:@"8CccLuVDFPzIv5631w249fgXB9GyY0LH" generalDelegate:nil];
    
    if (!success) {
        NSLog(@"失败");
    }
       return YES;
}



- (void)onGetNetworkState:(int)iError
{
    if (0 == iError) {
        NSLog(@"联网成功");
    }
    else{
        NSLog(@"onGetNetworkState %d",iError);
    }
    
}

- (void)onGetPermissionState:(int)iError
{
    if (0 == iError) {
        NSLog(@"授权成功");
    }
    else {
        NSLog(@"onGetPermissionState %d",iError);
    }
}
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

#import "ViewController.h"
#import <BaiduMapAPI_Map/BMKMapView.h>
#import <BaiduMapAPI_Map/BMKMapComponent.h>

#import "UIButton+ImageTitleStyle.h"
#import "KMSBMKMapView.h"
@interface ViewController ()<BMKMapViewDelegate>

{
    KMSBMKMapView* _mapView;
}
@property (weak, nonatomic) IBOutlet UIButton *imageTitleStytleButton;


@end

@implementation ViewController



- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self.imageTitleStytleButton setButtonImageTitleStyle:ButtonImageTitleStyleTop padding:3];
    //适配ios7
    if( ([[[UIDevice currentDevice] systemVersion] doubleValue]>=7.0))
    {
        //        self.edgesForExtendedLayout=UIRectEdgeNone;
        self.navigationController.navigationBar.translucent = NO;
    }
    CLLocationCoordinate2D coor;
    coor.latitude =30.307407;
    coor.longitude = 120.386266;

    _mapView = [[KMSBMKMapView alloc]initWithFrame:CGRectMake(0, self.view.frame.size.height
                                                              /2, self.view.frame.size.width
                                                             , self.view.frame.size.height
                                                              /2) location:coor];
    [self.view addSubview:_mapView];
