# View Class

`VideoView`
- `setVideoPath(str path)`
- `setVideoUri(Uri uri)`
- `start()`
- `stopPlayback()`
- `pause()`
- `isPlaying()`

```kotlin
<ViewName
	Attr1 = Value1
	Attr2 = Value2
/>
```

```kotlin
val videoView = findViewById<VideoView>(blinding.testView.id)

val mediaController = MediaController(this)
mediaController.setAnchorView(videoView)

val uri: Uri = parse("android.resource://" + packageName + "/raw/" + fileName)

videoView.setMediaController(mediaController)
videoView.setVideoURI(uri)
videoView.requestFocus()
videoView.start()
```
# Layout

- LinearLayout
	- one next another
	- horizontal or vertical
- ConstraintLayout
	- define relative position
- RecyclerView
	- a ViewGroup that can be used to display sets of data that can be scrolled
		- items can be 
			- LinearLayoutManager
			- GridLayoutManager
- WebView
	- render a web view as part of the layout
- FrameLayout
	- a ViewGroup used to specify the position of View elements it contains on the ==top of each other== to display only a single View inside the FrameLayout
- TableLayout
	- ViewGroup used to display the child View elements in rows and columns

Under the layout folder, you can right click it and choose `Layout Resource File` for a template.

---

# URI
	Uniform Resource Identifier

It represents
- location
- name
for
- image
- video
- music

1. right-click the `res` folder and choose `Android Resource Directory`
2. specify the resource type
	1. mp4 is `raw`
3. move your `.mp4` to the folder
4. `val uri: Uri = parse("android.resource://" + packageName + "/" + fileName)`
	1. you don't need the extension

---

# Import

```kotlin
import android.widget.VideoView
```

`android.net.Uri`
- reference the location

`android.widget.MediaController`
- access the playback controls of the video player
	- play / pause / backward / forward

`android.widget.VideoView`
- render the video

---

# Kotlin


`var varName = value`
- `var cnt: Int = 25`
- `var country: String = "Canada"`

`val varName = value`
- immutable

```kotlin
var color: String
color = "blue"
```

	String variables can be combined by using +

`println()`



