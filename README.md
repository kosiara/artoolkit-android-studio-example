## ARToolkit example "SimpleAR" project in Android Studio

This example project was ported from an Eclipse project to gradle & Android Studio

#### Versions:
Android Studio: 1.5.1
ARToolKit v5.3.1

Tested on:
Android 4.x, Android 5.x, Android 6.0 (should work on Android 2.3 as well)

#### Links:
ARtoolkit SDK: http://artoolkit.org/download-artoolkit-sdk

ARtoolkit SDK source: https://github.com/artoolkit/artoolkit5

#### Sample marker:

![Marker1](https://raw.githubusercontent.com/kosiara/artoolkit-android-studio-example/master/sampleMarker/patt2.jpg)

https://www.hitl.washington.edu/artoolkit/documentation/devmulti.htm

#### Sample usage:

```java
/**
 * A very simple Renderer that adds a marker and draws a cube on it.
 */
public class SimpleRenderer extends ARRenderer {

	private int markerID = -1;
	private Cube cube = new Cube(40.0f, 0.0f, 0.0f, 20.0f);

	@Override
	public boolean configureARScene() {
		markerID = ARToolKit.getInstance().addMarker("single;Data/patt.hiro;80");
		if (markerID < 0) return false;

		return true;
	}

	public void draw(GL10 gl) {

		gl.glClear(GL10.GL_COLOR_BUFFER_BIT | GL10.GL_DEPTH_BUFFER_BIT);

		gl.glMatrixMode(GL10.GL_PROJECTION);
		gl.glLoadMatrixf(ARToolKit.getInstance().getProjectionMatrix(), 0);

		gl.glEnable(GL10.GL_CULL_FACE);
		gl.glShadeModel(GL10.GL_SMOOTH);
		gl.glEnable(GL10.GL_DEPTH_TEST);
		gl.glFrontFace(GL10.GL_CW);

		gl.glMatrixMode(GL10.GL_MODELVIEW);

		if (ARToolKit.getInstance().queryMarkerVisible(markerID)) {

			gl.glLoadMatrixf(ARToolKit.getInstance().queryMarkerTransformation(markerID), 0);

			gl.glPushMatrix();
			cube.draw(gl);
			gl.glPopMatrix();
		}
	}
}
```

#### Screenshots

![Screenshot1](https://raw.githubusercontent.com/kosiara/artoolkit-android-studio-example/master/screenshots/device-2015-12-09-102231.png)
![Screenshot2](https://raw.githubusercontent.com/kosiara/artoolkit-android-studio-example/master/screenshots/device-2015-12-09-102300.png)

#### Videos

[![ARToolkit Android Studio sample](http://img.youtube.com/vi/g2z9acgPVHw/0.jpg)](https://youtu.be/g2z9acgPVHw "ARToolkit Android Studio sample")


port author: Bartosz Kosarzycki
