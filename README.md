# FrinckPod

[![CI Status](https://img.shields.io/travis/LetsNurtureGit/FrinckPod.svg?style=flat)](https://travis-ci.org/LetsNurtureGit/FrinckPod)
[![Version](https://img.shields.io/cocoapods/v/FrinckPod.svg?style=flat)](https://cocoapods.org/pods/FrinckPod)
[![License](https://img.shields.io/cocoapods/l/FrinckPod.svg?style=flat)](https://cocoapods.org/pods/FrinckPod)
[![Platform](https://img.shields.io/cocoapods/p/FrinckPod.svg?style=flat)](https://cocoapods.org/pods/FrinckPod)


## Overview
FrinckPod SDK is a wrapper library to detect beacons nearby you and present detailed information about beacons properties. It detects beacons near you and provide information like UUID, Major, Minor, Store/Mall Image/Video, Title and Description of store/mall as well as redirection url. You can analyse detected uses on the Admin Panel.

## Installing the iOS SDK
To use the FrinkPod SDK in your project, the minimum deployment target must be iOS 8.0

### CocoaPods
[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. It can be installed with the following command:
<pre>
$ gem install cocoapods
</pre>

To integrate the FrinkPod SDK into your Xcode project using CocoaPods, specify it in your Podfile:
```ruby
platform :ios, '8.0'
use_frameworks!
    
pod 'FrinckPod'
```

Then, run the following command:
<pre>
$ pod install
</pre>

## Usage


### Pod Import
To import FrinckPod, you need to define it as follows:

<pre>
import FrinckPod
</pre>

### Assign LNBeaconManagerDelegate to ViewController
To use functions, it is mandatory to define LNBeaconManagerDelegate with UIViewController.
<pre>
class ViewController: UIViewController, LNBeaconManagerDelegate {
    ..
    ..
    ..
}
</pre>

### Get Shared Instance of LNBeaconDataManager and LNBeaconManager
BeaconData returns detected beacons so it is required to define it as follows:
<pre>var arrBeacons = [BeaconData]()</pre>

Take shared instance of LNBeaconDataManager to use its methods and define as follow:
<pre>let beaconManager = LNBeaconDataManager.sharedInstance</pre>

Take shared instance of LNBeaconManager which is used to pass data of logged in user and define it as follows:
<pre>let beacondata = LNBeaconManager.sharedInstance</pre>

<pre>
var arrBeacons = [BeaconData]()
let beaconManager = LNBeaconDataManager.sharedInstance
let beacondata = LNBeaconManager.sharedInstance
</pre>

### Pass Logged-in Userdata in ViewDidLoad()
<pre>
let userData = ["client_id" : "101", "first_name" : "Tim", "last_name" : "Cook"]
beacondata.passUserData(userData: userData)
</pre>

### Mention delegate to self from ViewDidLoad()
Define delegate to self as follows:
<pre>beacondata.delegateManager = self</pre>

<pre>
override func viewDidLoad() {
    super.viewDidLoad()
    
    beacondata.delegateManager = self
    let userData = ["client_id" : "101",
                            "first_name" : "Tim",
                            "last_name" : "Cook"]
    beacondata.passUserData(userData: userData)
    
    beaconManager.foundBeacons()
    beaconManager.startTimer()
}
</pre>

### Add didReceiveBeaconData delegate method
This is the main implemented method in which gives all nearby beacons with its data. Implement this mehtod as mentioned below and get your reqired data:
<pre>
func didReceiveBeaconData(data: AnyObject?)  {
    arrBeacons = data as! [BeaconData]
}
</pre>

### Get Analysis of Beacons
If you want to show user analysis on dashboard of your Admin Panel then you need to define it and pass parameters like Beacon Id, URL and Type and then call didAnalysisClick method to post analysis data on the server which is define as follows:

Suppose If you're managing data on TableView then on click of table view cell, you can define under didSelectRowAt delegate method of TableView as follows:
<pre>
let obj = self.arrBeacons[indexPath.row]
let data = ["data": ["beacon_id":obj.id, "link":obj.link, "type":"2"]]  // type = 2 for iOS Device
beacondata.didAnalysisClick(param: data as! [String : [String : String]] )
</pre>


## Author

LetsNurtureGit, android.letsnurture@gmail.com

## License

FrinckPod is available under the MIT license. See the LICENSE file for more info.
