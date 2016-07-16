---
published: true
layout: post
title: Handling blog images
categories: writing
---
Into the wee hours last night, I wasted a bunch of time wrestling with how to handle photos for my blog. My technical goals for the photos on my blog are as follows:

- **Performance**: compressed file size without sacrificing too much quality
- **Right-sized**: not thousands of pixels high and wide, more like 800x600
- **Organized**: stored in Github in a sensical way

I already knew I could use [TinyJPG][tinyjpg] for my performance goal. And I found a free iPad app called [Image Size][imagesize] that does the second. But I noticed that when I uploaded photos from the native Photos app to TinyJPG for compression, all the photos shared the same name: "image.jpeg". I frantically searched the internet for how I could rename photos in iOS. Many people said it couldn't be done, while others pointed out paid apps you could download to achieve this goal. I even tried using Github's web interface to handle the situation, but I couldn't find a rename function.

Just when I was about to give up and start using a weird workflow involving uploading photos from Photos to Dropbox, renaming them, and saving them back to Photos, I discovered that [Prose][prose]'s Markdown toolbar has a button to insert an image. You can choose an image from your photo library and specify the path and filename you want to upload it to in your Github repo. Perfect!

[Development Seed][devseed], you are an amazing team of developers, and I want to give you money.

[devseed]: https://developmentseed.org/team/
[imagesize]: https://itunes.apple.com/us/app/image-size/id670766542
[prose]: http://prose.io
[tinyjpg]: https://tinyjpg.com/