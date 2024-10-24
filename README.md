# **TRACK ASIA TÍCH HỢP**

## **I)	Android**

### 1)	Triển khai thư viện vào project
#### •	Root gradle
```
buildscript {
    repositories {
        google()
        jcenter()
        mavenCentral()
        maven { url "https://oss.sonatype.org/content/repositories/snapshots"}
        maven { url 'https://jitpack.io' }
    }
}
```

```
allprojects {
    repositories {
        google()
        jcenter()
        mavenCentral()
        maven { url "https://oss.sonatype.org/content/repositories/snapshots"}
        maven { url 'https://jitpack.io' }
    }
}
```

#### •	App gradle
- Tạo thư mục libs chứa thư viện navigation.
```
dependencies {
    implementation('io.github.track-asia:android-sdk:1.0.20')
    implementation('io.github.track-asia:android-sdk-services:1.0.20')
    implementation('io.github.track-asia:android-sdk-turf:1.0.20')
    implementation('io.github.track-asia:android-plugin-annotation-v9:1.0.0')
    implementation files('../libs/libandroid-navigation-ui.aar')
    implementation files('../libs/libandroid-navigation.aar')
}
```
### 2)	Triển khai Mapview
#### - XML
```
    <com.trackasia.android.maps.MapView
        android:id="@+id/mapView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:trackasia_cameraZoom="12"
        app:trackasia_enableTilePrefetch="true"
        app:trackasia_enableZMediaOverlay="true"
        app:trackasia_renderTextureMode="true"
        app:trackasia_renderTextureTranslucentSurface="true"
        app:trackasia_uiAttribution="true"
        app:trackasia_uiCompass="true"
        app:trackasia_uiDoubleTapGestures="true"
        app:trackasia_uiLogo="true"
        app:trackasia_uiRotateGestures="true"
        app:trackasia_uiScrollGestures="true"
        app:trackasia_uiTiltGestures="true"
        app:trackasia_uiZoomGestures="true" />
```
#### - Code 
> import com.trackasia.android.maps.TrackasiaMap
```
private lateinit var mapboxMap: TrackasiaMap
private var styleUrl = "https://tiles.track-asia.com/tiles/v1/style-streets.json?key=public"
```
```
onCreateView()
Trackasia.getInstance(requireActivity()). //Khởi tạo 
onViewCreated()
mapView.onCreate(savedInstanceState)
mapView.getMapAsync { map ->
    this.mapboxMap = map
    map.setStyle(Style.Builder().fromUri(styleUrl)) { style ->
        enableLocationComponent(style)
    }
    navigationMapRoute = NavigationMapRoute(binding.mapView, map)
    var latlng = LatLng(10.728073, 106.624054)
    map.cameraPosition = CameraPosition.Builder().target(latlng).zoom(12.0).build()
}
```
### 3) Hình ảnh demo
<p align="center">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_1.JPEG" alt="Android" width="18%">   
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_2.JPEG" alt="Android" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_3.JPEG" alt="Android" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_4.JPEG" alt="Android" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_5.JPEG" alt="Android" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_6.JPEG" alt="Android" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/android_7.JPEG" alt="Android" width="18%">
</p>

### 4) Link Github Core

[⭐️ TrackAsia Java - Chứa các thư viện hỗ trợ Map](https://github.com/track-asia/trackasia-java)

[⭐️ TrackAsia Native - Chứa các thư viện core deploy chính của Map Chọn Android](https://github.com/track-asia/trackasia-native)

[⭐️ TrackAsia Navigation - Chứa các thư viện Navigation, Directions của Map](https://github.com/track-asia/trackasia-navigation-android)

### 5) Chứa bản demo map
[⭐️ TrackAsia Sample Demo - Chứa source demo map](https://git.advn.vn/sangnguyen/trackasia-demo)

### 6) Chứa thư viện đã deploy tích hợp
[⭐️ TrackAsia Libs - Chứa libs để tích hợp](https://git.advn.vn/sangnguyen/trackasia-document/-/tree/master/Android/libs)


## **II)	IOS**
### 1)	Triển khai thư viện vào project
#### •	Add package

`    https://github.com/track-asia/trackasia-gl-native-distribution chọn branch -> 1.0.2`
<img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_add_1.png" alt="ios"> 
#### •	Add libs

+ Copy thư mục libs vào project 
+ vào project -> targets ->  general -> Frameworks, libraries, and embedded content -> add 
<img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_add_2.png" alt="ios"> 

### 2)	Triển khai Mapview
#### •	Code
```
import MapboxCoreNavigation
import MapboxNavigation
import MapboxDirections

var mapView: NavigationMapView? {
    didSet {
        oldValue?.removeFromSuperview()
        if let mapView = mapView {
            configureMapView(mapView)
            view.insertSubview(mapView, belowSubview: longPressHintView)
        }
     }
}
```

```
override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    self.mapView = NavigationMapView(frame: view.bounds, styleURL: URL(string: "https://tiles.track-asia.com/tiles/v1/style-streets.json?key=public"))
}
```

### 3) Hình ảnh demo
<p align="center">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_1.png" alt="IOS" width="18%">   
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_2.png" alt="IOS" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_3.png" alt="IOS" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_4.png" alt="IOS" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_5.png" alt="IOS" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_6.png" alt="IOS" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/ios_7.png" alt="IOS" width="18%">
</p>

### 4) Link Github Core

[⭐️ TrackAsia Navigation IOS  - Chứa các thư viện navigation map](https://github.com/track-asia/trackasia-navigation-ios)

[⭐️ TrackAsia Native - Chứa các thư viện core deploy chính của Map chọn IOS](https://github.com/track-asia/trackasia-native)

[⭐️ TrackAsia Directions - Chứa các thư viện Mapbox của Map](https://github.com/track-asia/trackasia-directions-swift)

[⭐️ TrackAsia Polyline - Chứa các thư viện các point của Map](https://github.com/track-asia/trackasia-polyline)

[⭐️ TrackAsia Extension - Chứa các thư viện các extension của Map](https://github.com/track-asia/trackasia-annotation-extension)

### 5) Chứa bản demo map

[⭐️ TrackAsia Sample Demo - Chứa source demo map](https://git.advn.vn/sangnguyen/trackasia-ios-demo)

### 6) Chứa thư viện đã deploy tích hợp

## **III)	FLUTTER**
### 1)	Triển khai thư viện vào project
```
  trackasia_gl_platform_interface: ^1.0.5
  trackasia_gl_web: ^1.0.1
  trackasia_gl: ^1.0.12
```

### 2)	Triển khai Mapview
```
import 'package:trackasia_gl/trackasia_gl.dart';

TrackasiaMapController? mapController;
@override
  Widget build(BuildContext context) {
    return new Scaffold(
        body: TrackasiaMap(
      onMapCreated: _onMapCreated,
      styleString: "https://tiles.track-asia.com/tiles/v3/style-streets.json?key=public",
      initialCameraPosition: const CameraPosition(target: LatLng(0.0, 0.0)),
      onStyleLoadedCallback: _onStyleLoadedCallback,
    ));
  }
```

### 3) Hình ảnh demo

<p align="center">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/flutter_1.png" alt="FLUTTER" width="18%">   
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/flutter_2.png" alt="FLUTTER" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/flutter_3.png" alt="FLUTTER" width="18%">
  <img src="https://git.advn.vn/sangnguyen/trackasia-document/-/raw/master/images/flutter_4.png" alt="FLUTTER" width="18%">
</p>

### 4) Link Github Core

### 4) Link Github Core

[⭐️ TrackAsia Navigation Flutter  - Hiện đang phát triển]

[⭐️ TrackAsia Cocoapods - Chứa các đường dẫn install IOS](https://github.com/track-asia/trackasia-cocoapods)

[⭐️ TrackAsia Flutter Podspecs - Chứa cài đặt podspect](https://github.com/track-asia/trackasia-flutter-podspecs)

[⭐️ TrackAsia Flutter GL - Thư viện chính để chạy Flutter](https://github.com/track-asia/trackasia-flutter-gl)

### 5) Chứa bản demo map

[⭐️ TrackAsia Sample Demo - Chứa source demo map](https://git.advn.vn/sangnguyen/trackasia-flutter-demo)

### 6) Chứa thư viện đã deploy tích hợp

