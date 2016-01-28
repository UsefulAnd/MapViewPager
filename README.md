[ ![Download](https://api.bintray.com/packages/moreno/maven/MapViewPager/images/download.svg) ](https://bintray.com/moreno/maven/MapViewPager/_latestVersion)

# MapViewPager

Android library that connects ViewPager fragments with Google Maps markers and makes them work together.


## Features

- [x] Any amount of markers per fragment supported
- [x] Default camera position (for fragments with 0 or *more than 1* markers) automatically calculated


## Download

#### Gradle

```gradle
repositories {
    maven {
        url  "http://dl.bintray.com/moreno/maven" 
    }
}

dependencies {
    compile 'com.github.nitrico.mapviewpager:mapviewpager:0.0.1'
}
```


## Usage

Create a ViewPager adapter extending from **MapViewPager.Adapter** or **MapViewPager.MultiAdapter** and override method
`public CameraPosition getCameraPosition(int position)` or `public List<CameraPosition> getCameraPositions(int position)` returning the markers camera position for each fragment.

You can create a CameraPosition it like that: `CameraPosition.builder().target(new LatLng(latitude, longitude)).zoom(zoom).build();`

Include the view in your xml layout

```xml
<com.github.nitrico.mapviewpager.MapViewPager
        android:id="@+id/mapViewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:viewPagerWeight="1"
        app:mapWeight="1"
        app:mapGravity="1"
        app:mapOffset="56dp" />
```
and call `mapViewPager.start(this, adapter, /*optional*/callback);` passing the AppCompatActivity (or FragmentActivity) and adapter instances. You can also pass a MapViewPager.Callback instance to get notified when the GoogleMap object is created and working.

##### XML attributes

|Attribute|Format|Default|Description
|---|---|---|---|
|viewPagerWeight|integer|1|Weight of the viewpager in the layout|
|mapWeight|integer|1|Weight of the map in the layout|
|mapGravity|integer (0..3)|1|Position of the map in the layout: 0=left, 1=top, 2=right, 3=bottom|
|mapOffset|dimension|0dp||
|mapPaddingLeft|dimension|0dp|Left padding for the map|
|mapPaddingTop|dimension|0dp|Top padding for the map|
|mapPaddingRight|dimension|0dp|Right padding for the map|
|mapPaddingBottom|dimension|0dp|Bottom padding for the map|
|markersAlpha|float (0..1)|0.4|Opacity of markers when deactivated|

##### MapViewPager public methods

```java
void start(@NonNull FragmentActivity activity, @NonNull AbsAdapter mapAdapter) 
void start(@NonNull FragmentActivity activity, @NonNull AbsAdapter mapAdapter, @Nullable Callback callback)
void setCurrentItem(int currentItem)
GoogleMap getMap()
SupportMapFragment getMapFragment()
ViewPager getViewPager() 
CameraUpdate getDefaultPosition() 

// Single getters (when adapter extends MapViewPager.Adapter)
Marker getMarker(int position)
List<Marker> getMarkers()

// Multi getters (when adapter extends MapViewPager.MultiAdapter)
Marker getMarker(int page, int position)
List<Marker> getMarkers(int page) 
List<List<Marker>> getAllMarkers()
CameraUpdate getDefaultPosition(int page) 
List<CameraUpdate> getDefaultPositions()
```

#### Advanced usage

Check the examples in the app folder!


## License
```
Copyright 2016 Miguel Ángel Moreno

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
