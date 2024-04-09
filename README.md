Конечно, вот пример MainActivity.java с добавленными кнопками и разметкой XML:

public class MainActivity extends AppCompatActivity {
    private MediaPlayer mediaPlayer;
    private boolean isPaused = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button playButton = findViewById(R.id.playButton);
        Button stopButton = findViewById(R.id.stopButton);
        Button pauseButton = findViewById(R.id.pauseButton);
        Button backButton = findViewById(R.id.backButton);
        Button forwardButton = findViewById(R.id.forwardButton);

        mediaPlayer = MediaPlayer.create(this, R.raw.song); // загрузка песни из файла RAW

        playButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (isPaused) {
                    mediaPlayer.start();
                    isPaused = false;
                } else {
                    mediaPlayer.start();
                }
            }
        });

        stopButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                mediaPlayer.stop();
                mediaPlayer = MediaPlayer.create(MainActivity.this, R.raw.song);
            }
        });

        pauseButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (mediaPlayer.isPlaying()) {
                    mediaPlayer.pause();
                    isPaused = true;
                }
            }
        });

        backButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                int currentPosition = mediaPlayer.getCurrentPosition();
                if (currentPosition - 5000 > 0) {
                    mediaPlayer.seekTo(currentPosition - 5000);
                }
            }
        });

        forwardButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                int currentPosition = mediaPlayer.getCurrentPosition();
                if (currentPosition + 5000 < mediaPlayer.getDuration()) {
                    mediaPlayer.seekTo(currentPosition + 5000);
                }
            }
        });
    }
}


А вот пример activitymain.xml для макета с кнопками управления:

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layoutwidth="matchparent"
    android:layoutheight="matchparent">

    <Button
        android:id="@+id/playButton"
        android:layoutwidth="wrapcontent"
        android:layoutheight="wrapcontent"
        android:text="Play"
        android:layoutcenterInParent="true"/>

    <Button
        android:id="@+id/stopButton"
        android:layoutwidth="wrapcontent"
        android:layoutheight="wrapcontent"
        android:text="Stop"
        android:layoutbelow="@id/playButton"
        android:layoutmarginTop="16dp"
        android:layoutcenterHorizontal="true"/>

    <Button
        android:id="@+id/pauseButton"
        android:layoutwidth="wrapcontent"
        android:layoutheight="wrapcontent"
        android:text="Pause"
        android:layoutbelow="@id/stopButton"
        android:layoutmarginTop="16dp"
        android:layoutcenterHorizontal="true"/>

    <Button
        android:id="@+id/backButton"
        android:layoutwidth="wrapcontent"
        android:layoutheight="wrapcontent"
        android:text="Back"
        android:layoutbelow="@id/pauseButton"
        android:layoutmarginTop="16dp"
        android:layoutcenterHorizontal="true"/>

    <Button
        android:id="@+id/forwardButton"
        android:layoutwidth="wrapcontent"
        android:layoutheight="wrapcontent"
        android:text="Forward"
        android:layoutbelow="@id/backButton"
        android:layout_marginTop="16dp"
        android:layout_centerHorizontal="true"/>

</RelativeLayout>
```

Не забудьте добавить значения ID для каждой кнопки в XML разметке и связать их с соответствующими кнопками в коде MainActivity.
