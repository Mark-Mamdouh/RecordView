[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-RecordView-orange.svg?style=flat)](https://android-arsenal.com/details/1/6259)

 [ ![Download](https://api.bintray.com/packages/devlomi/maven/RecordView/images/download.svg) ](https://bintray.com/devlomi/maven/RecordView/_latestVersion)


# RecordView
A Simple Audio Recorder View with hold to Record Button and Swipe to Cancel


## Demo
<p align="center">
  <img src="etc/demo.GIF" height="500" alt="demo image" />
</p>




## Install
```gradle
dependencies {
  compile 'com.devlomi.record-view:record-view:1.2.2beta'
  //appcompat v26+ is higly recommended to support older APIs
}
```


## Usage

### XML

```xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/parent_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.devlomi.record_view.RecordView
        android:id="@+id/record_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_toLeftOf="@id/record_button"
        app:slide_to_cancel_arrow="@drawable/recv_ic_arrow"
        app:slide_to_cancel_bounds="10dp"
        app:slide_to_cancel_margin_right="10dp"
        app:slide_to_cancel_text="Slide To Cancel" />

    <com.devlomi.record_view.RecordButton
        android:id="@+id/record_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:background="@drawable/recv_bg_mic"
        android:scaleType="centerInside"
        app:mic_icon="@drawable/recv_ic_mic_white" />


</RelativeLayout>


```


### Java

```java

        RecordView recordView = (RecordView) findViewById(R.id.record_view);
        RecordButton recordButton = (RecordButton) findViewById(R.id.record_button);

        //IMPORTANT
        recordButton.setRecordView(recordView);

```

### Handling States

```java
recordView.setOnRecordListener(new OnRecordListener() {
            @Override
            public void onStart() {
                //Start Recording..
                Log.d("RecordView", "onStart");
            }

            @Override
            public void onCancel() {
                //On Swipe To Cancel
                Log.d("RecordView", "onCancel");

            }

            @Override
            public void onFinish(long recordTime) {
                //Stop Recording..
                String time = getHumanTimeText(recordTime);
                Log.d("RecordView", "onFinish");

                Log.d("RecordTime", time);
            }

            @Override
            public void onLessThanSecond() {
              //When the record time is less than One Second
                Log.d("RecordView", "onLessThanSecond");
            }
        });

```

### Handle Clicks for Record Button
```java

    recordButton.setListenForRecord(false);

 //ListenForRecord must be false ,otherwise onClick will not be called
        recordButton.setOnRecordClickListener(new OnRecordClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "RECORD BUTTON CLICKED", Toast.LENGTH_SHORT).show();
                Log.d("RecordButton","RECORD BUTTON CLICKED");
            }
        });
```

### Listen for Basket Animation End

```java

   recordView.setOnBasketAnimationEndListener(new OnBasketAnimationEnd() {
            @Override
            public void onAnimationEnd() {
                Log.d("RecordView", "Basket Animation Finished");
            }
        });

```


Change Swipe To Cancel Bounds (when the 'Slide To Cancel' Text View get before Counter).
default is 25dp

```java
recordView.setCancelBounds(30);//dp
```

### Some Customization

```java
        recordView.setSmallMicColor(Color.parseColor("#c2185b"));

        recordView.setSlideToCancelText("TEXT");

        //disable Sounds
        recordView.setSoundEnabled(false);

        //prevent recording under one Second (it's false by default)
        recordView.setLessThanSecondAllowed(false);
    
        //set Custom sounds onRecord 
        //you can pass 0 if you don't want to play sound in certain state
        recordView.setCustomSounds(R.raw.record_start,R.raw.record_finished,0);

```

### Thanks/Credits
- [NetoDevel](https://github.com/NetoDevel) for some inspiration and some code in his lib [audio-recorder-button](https://github.com/safetysystemtechnology/audio-recorder-button) 
- [alexjlockwood](https://github.com/alexjlockwood) for making this Awesome tool  [ShapeShifter](https://shapeshifter.design/) which helped me to animate vectors easily
- team-supercharge for making [ShimmerLayout](https://github.com/team-supercharge/ShimmerLayout)
