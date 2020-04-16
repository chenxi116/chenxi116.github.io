---
layout: post
title:  "Compiling matcaffe on Ubuntu 16.04"
---
By default, Ubuntu 16.04 uses gcc and g++ 5.4. This is fine for Caffe installation, and in fact there is an [official guide][caffe-install] for that. However, even the latest Matlab release 2016b only supports gcc and g++ 4.9 for mex. This becomes an issue when compiling matcaffe. Apparently this problem is met by [other people][caffe-post] as well. 

I solved the issue by combining methods in [this post][post1] and [this post][post2].

- Install gcc and g++ 4.9

{% highlight shell %}
sudo apt-get install gcc-4.9 g++-4.9 gcc-4.9-multilib g++-4.9-multilib
{% endhighlight %}

- Change the `Name="g++"`, `ShortName="g++"` in `~/.matlab/R2016b/mex_C++_glnxa64.xml` to `Name="g++-4.9"`, `ShortName="g++-4.9"`. Same goes for gcc in `mex_C_glnxa64.xml`.

- Open Matlab and run

{% highlight shell %}
mex -setup C -f ~/.matlab/R2016b/mex_C_glnxa64.xml
mex -setup C++ -f ~/.matlab/R2016b/mex_C++_glnxa64.xml
{% endhighlight %}

- Compile matcaffe by 

{% highlight shell %}
make matcaffe
{% endhighlight %}

- Relink `libstdc++.so.6` in the Matlab directory

{% highlight shell %}
cd /usr/local/MATLAB/R2016b/sys/os/glnxa64
sudo rm libstdc++.so.6
sudo ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.21 libstdc++.so.6
{% endhighlight %}

- Relink OpenCV related libraries in the Matlab directory

{% highlight shell %}
cd /usr/local/MATLAB/R2016b/bin/glnxa64
sudo rm libopencv_core.so.2.4
sudo ln -s /usr/lib/x86_64-linux-gnu/libopencv_core.so.2.4.9 libopencv_core.so.2.4
sudo rm libopencv_highgui.so.2.4
sudo ln -s /usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9 libopencv_highgui.so.2.4
sudo rm libopencv_imgproc.so.2.4
sudo ln -s /usr/lib/x86_64-linux-gnu/libopencv_imgproc.so.2.4.9 libopencv_imgproc.so.2.4
{% endhighlight %}

[caffe-install]: https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide
[caffe-post]: https://groups.google.com/forum/#!topic/caffe-users/-eFEdJCGgzc
[post1]: http://www.voidcn.com/blog/eagelangel/article/p-6186882.html
[post2]: https://github.com/BVLC/caffe/issues/3934