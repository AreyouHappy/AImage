# JWAnimatedImage
A animated GIF engine for iOS in Swift 
##Features
- [x] Have a great performance on memory usage by using producer/consumer pattern.
- [x] Have a great performance on CPU usage by using asynchronous loading.
- [x] More flexible on display by using factor "level of Integrity" 
- [x] Using new Algorithm to choose frames.
- [x] Small but complete,easy to extend.

##How to Use
```swift
let url = NSBundle.mainBundle().URLForResource(“imagename”, withExtension: "gif")!
let imageData = NSData(contentsOfURL:url)
let imageView = JWAnimatedImageView()
imageView.addGifImage(imageData!)
imageView.frame = CGRect(x: 0.0, y: 30.0, width: 300.0, height: 200.0)
view.addSubview(imageView)
```
##Benchmark:Compare with [FLAnimatedImage](https://github.com/Flipboard/FLAnimatedImage)
> Updated:March1,2016<p>
> Measurement device:&nbsp;iPhone6 with iOS 9.2.1<p>
> Measurement tool:&nbsp;Profile in Xcode<p>
> Measurement image:&nbsp;See it in repository,all the parameters are default.<p>
> Measurement result:<p>
####1.Display just one GIF image
####1.1 CPU usgae:
######JWAnimatedImage<p>
![JW_CPU](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/JW_CPU1.png)<p>
######FLAnimatedImage<p>
![FL_CPU](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/FL_CPU1.png)<p>
####1.2 Memory usage: 
######JWAnimatedImage<p>
![JW_MEM](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/JW_MEM1.png)<p>
######FLAnimatedImage<p>
![FL_MEM](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/FL_MEM1.png)<p>
 > I've discussed the high memory usage of FLAnimatedImage with [@mitchellporter](https://github.com/mitchellporter) and confirmed this problem does exist，you can see it [here](https://github.com/wangjwchn/JWAnimatedImage/issues/1)<p>

####2.Display 30 GIF images
####Like this:
![DEMO](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/DEMO.jpg)<p>
####1.1 CPU usgae:
######JWAnimatedImage<p>
![JW_CPU](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/JW_CPU2.png)<p>
######FLAnimatedImage<p>
![FL_CPU](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/FL_CPU2.png)<p> 
 > ......
![FL_CPU](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/FL_CPU3.png)<p> 
 > For each image,FLAnimatedImage create a new thread and running independently,from the graph,we can see there are 36 thread when we load 30 GIF images,that will cause a heavy CPU usage.<p>
 > So in JWAnimatedImage,we use 'global queue' in 'GCD' to handle these tasks together.that makes the number of thread down to 10,and those threads are dynamic,from the graph,we can see some of them are just start.<p>

####1.2 Memory usage:
######JWAnimatedImage<p>
![JW_MEM](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/JW_MEM2.png)<p>
######FLAnimatedImage<p>
![FL_MEM](https://raw.githubusercontent.com/wangjwchn/JWAnimatedImage/master/BenchmarkPicture/FL_MEM2.png)<p>
 > I think JWAnimatedImage is better than FLAnimatedImage in cpu and memory usage.<p>

##Licence
 > JWAnimatedImage is released under the MIT license. See LICENSE for details.<p>
