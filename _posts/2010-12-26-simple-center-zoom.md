---
layout: post
title: Simple center zoom
date: 2010-12-26 23:27:49.000000000 +00:00
categories:
- animations
- C#
- silverlight
tags:
- animation
- App Store
- Arts
- C#
- Filmmaking
- Illustration
- iPhone
- IPod Touch
- Microsoft Silverlight
- S
- Specialized
- Storyboard
- toolkit
- XAML
status: publish
type: post
published: true
meta:
  _edit_last: '17981463'
  tagazine-media: a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"17981463";s:7:"blog_id";s:8:"17351252";s:9:"mod_stamp";s:19:"2010-12-26
    23:30:58";}
author:
  login: soonstudios
  email: lukasz.madon@gmail.com
  display_name: Soon Studios
  first_name: ''
  last_name: ''
excerpt: !ruby/object:Hpricot::Doc
  options: {}
---
<p>To add simple pinch zoom (that I used in my Spirit Level) use <a href="http://silverlight.codeplex.com/releases/view/52297">the Silverlight Toolkit for WP7</a> and add the pinch GetureListener to a grid</p>
<p>[sourcecode language="xml"]<br />
&lt;toolkit:GestureService.GestureListener&gt;<br />
  &lt;toolkit:GestureListener PinchDelta=&quot;GestureListener_PinchDelta&quot; /&gt;<br />
 &lt;/toolkit:GestureService.GestureListener&gt;<br />
[/sourcecode]</p>
<p>and code in event</p>
<p>[sourcecode language="csharp"]<br />
 private void GestureListener_PinchDelta(object sender, PinchGestureEventArgs e)<br />
 {<br />
    if (e.DistanceRatio &lt; 1.0 || e.DistanceRatio &gt; 1.4)<br />
    {<br />
      return;<br />
    }<br />
 // Create the animation for pinch<br />
   Storyboard storyboard = new Storyboard();<br />
   DoubleAnimation pinchXAnimation = new DoubleAnimation();<br />
   pinchXAnimation.To = e.DistanceRatio;<br />
   pinchXAnimation.Duration = TimeSpan.FromSeconds(0.3);<br />
   storyboard.Children.Add(pinchXAnimation);<br />
   Storyboard.SetTargetProperty(pinchXAnimation, new PropertyPath(&quot;GridScaling.ScaleX&quot;));<br />
   Storyboard.SetTarget(pinchXAnimation, GridScaling);</p>
<p>   DoubleAnimation pinchYAnimation = new DoubleAnimation();<br />
   pinchYAnimation.To = e.DistanceRatio;<br />
   pinchYAnimation.Duration = TimeSpan.FromSeconds(0.3);<br />
   storyboard.Children.Add(pinchYAnimation);<br />
   Storyboard.SetTargetProperty(pinchYAnimation, new PropertyPath(&quot;GridScaling.ScaleY&quot;));<br />
   Storyboard.SetTarget(pinchYAnimation, GridScaling);</p>
<p>   storyboard.Begin();</p>
<p>}<br />
[/sourcecode]</p>