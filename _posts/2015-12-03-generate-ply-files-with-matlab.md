---
layout: post
title:  "Generate PLY Files with Matlab"
---
When doing a class project, I needed to export from Matlab a bunch of 3D points (with color) to PLY files, so as to visualize the point cloud using MeshLab. With the instruction from [Konstantine Tsotsos][tsotsos], the process is as simple as: 

Write a header:

{% highlight shell %}
ply
format ascii 1.0
comment written by YOUR_NAME
element vertex NUM_POINTS
property float32 x
property float32 y
property float32 z
property uchar red
property uchar green
property uchar blue
end_header
{% endhighlight %}

Followed by the data as rows of `x y z r g b`:

{% highlight shell %}
-0.49	-0.375	0.841	0	0	0
-0.491	-0.374	0.843	0	0	0
-0.491	-0.372	0.843	0	0	11
-0.491	-0.371	0.844	0	0	7
-0.491	-0.369	0.844	0	0	12
-0.491	-0.368	0.844	0	0	0
-0.491	-0.366	0.844	12	10	18
{% endhighlight %}

Without further ado, here is a Matlab code to export PLY files:

{% highlight matlab %}
function write_ply(fname, P, C)
% Written by Chenxi cxliu@ucla.edu
% Input: fname: output file name, e.g. 'data.ply'
%        P: 3*m matrix with the rows indicating X, Y, Z
%        C: 3*m matrix with the rows indicating R, G, B

num = size(P, 2);
header = 'ply\n';
header = [header, 'format ascii 1.0\n'];
header = [header, 'comment written by Chenxi\n'];
header = [header, 'element vertex ', num2str(num), '\n'];
header = [header, 'property float32 x\n'];
header = [header, 'property float32 y\n'];
header = [header, 'property float32 z\n'];
header = [header, 'property uchar red\n'];
header = [header, 'property uchar green\n'];
header = [header, 'property uchar blue\n'];
header = [header, 'end_header\n'];

data = [P', double(C')];

fid = fopen(fname, 'w');
fprintf(fid, header);
dlmwrite(fname, data, '-append', 'delimiter', '\t', 'precision', 3);
fclose(fid);
{% endhighlight %}


[tsotsos]: https://sites.google.com/site/ktsotsos/