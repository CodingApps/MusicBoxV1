<h1 align="center"> Music Box </h1> <br>

<h4 align="center">Load audio from RAW file, using Java MediaPlayer with adjustable scroll and button UI.</h4> <br>
 

## Intro

This plays audio from a file, which shows an updated playback meter scrolling left to right. The scroll bar can be adjusted to playback at any time within the song. Function called from the Java MediaPlayer. 

<p align="center">
  <img alt="musicbox" title="musicbox" src="http://androidflow.github.io/screens/mbox1b.gif" width=300>
</p>
<br>

## Functions 

* Loading RAW audio file.
* Adding scroll bar to allow adjusted play time. 
* Displaying play time based on seconds playing and remaining. 

<br>

## Updating Time on Scrollbar

While the MediaPlayer function played the audio, the Scrollbar would move according remaining seconds. It was interesting to see how the Scrollbar adjusted from values input from MediaPlayer.    

``` java
    public void updateThread() {

        thread = new Thread() {
            @Override
            public void run() {

                try {
                    while (mediaPlayer != null && mediaPlayer.isPlaying()) {


                        Thread.sleep(50);
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                int newPosition = mediaPlayer.getCurrentPosition();
                                int newMax = mediaPlayer.getDuration();
                                seekbar.setMax(newMax);
                                seekbar.setProgress(newPosition);

                                //Update the text

                                leftTime.setText(String.valueOf(new java.text.SimpleDateFormat("mm:ss").format(new Date(mediaPlayer.getCurrentPosition()))));

                                rightTime.setText(String.valueOf(new java.text.SimpleDateFormat("mm:ss").format(new Date(mediaPlayer.getDuration() - mediaPlayer.getCurrentPosition()))));

                            }

                        });

                    }
```
<br>
