---
layout: post
title: "Adapter pattern"
comments: true
categories: Java
---

## Adapter Design pattern
Adapter Design pattern allows the interface of an existing class to be used as another interface. In summary, an adapter helps two incompatible interfaces to work together.
![Image](../../../../static/img/adapter_pattern.png)

Here, we have two incompatible interfaces : MediaPlayer and MediaPackage. MP3 class is an implementation of the MediaPlayer interface and we have VLC and MP4 as implementations of the MediaPackage interface. We want to use MediaPackage implementations as MediaPlayer instances. So, we need to create an adapter to help to work with two incompatible classes.

The Adapter will be named FormatAdapter and must implement the MediaPlayer interface. Furthermore, the FormatAdapter class must have a reference to MediaPackage, the incompatible interface.

```
public interface MediaPlayer {
 void play(String filename);
}

public interface MediaPackage {
 void playFile(String filename);
}

public class MP3 implements MediaPlayer {
 @Override
 public void play(String filename) {
    System.out.println("Playing MP3 File " + filename);
 }
}

public class MP4 implements MediaPackage {
 @Override
 public void playFile(String filename) {
    System.out.println("Playing MP4 File " + filename);
 }
}

public class VLC implements MediaPackage {
 @Override
 public void playFile(String filename) {
    System.out.println("Playing VLC File " + filename);
 }
}
```
Here, we want to use VLC and MP4 instances as MediaPlayer instances. So, we need and adapter. This is the code of the FormatAdapter :
```
public class FormatAdapter implements MediaPlayer {
 private MediaPackage media;
 public FormatAdapter(MediaPackage m) {
    media = m;
 }
 @Override
 public void play(String filename) {
   System.out.print("Using Adapter --> ");
   media.playFile(filename);
 }
}

public class Main {
 public static void main(String[] args) {
    MediaPlayer player = new MP3();
    player.play("file.mp3");
    player = new FormatAdapter(new MP4());
    player.play("file.mp4");
    player = new FormatAdapter(new VLC());
    player.play("file.avi");
 }
}

```

Output:
```
Playing MP3 File file.mp3
Using Adapter --> Playing MP4 File file.mp4
Using Adapter --> Playing VLC File file.avi
```


Source: [**Medium.com**](https://medium.com/@ssaurel/implement-the-adapter-design-pattern-in-java-f9adb6a8828f)

