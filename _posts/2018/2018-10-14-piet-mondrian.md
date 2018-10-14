---
layout: post
title: "D3js - Piet Mondrian"
date: '2018-10-14 19:50 +0100'
author: Fergus Findley
tags:
  - learning
  - D3js
description: 'One of my favorite painting this time in D3js'
image: 
---

<div id='chart'></div>

<script src="https://d3js.org/d3.v4.min.js"></script>
<script>
var total_width = $("#chart").width(),
	total_height = total_width;

var root = d3.select('#chart').append('svg')
	.attr('width', total_width)
	.attr('height', total_height)
	.style('border', '1px solid black');
	
var rects=[
	{x: -total_width/(480/2), y:-total_width/(480/2), w: total_width/(480/200), h:total_width/(480/270), fill: '#C53022'},
	{x: -total_width/(480/2), y:total_width/(480/270), w: total_width/(480/200), h:total_width/(480/212), fill: '#E3E0DF'},
	{x: total_width/(480/200), y:-total_width/(480/2), w: total_width/(480/282), h:total_width/(480/270), fill: '#E3E0DF'},
	{x: total_width/(480/200), y:total_width/(480/270), w: total_width/(480/244), h:total_width/(480/190), fill: '#E3E0DF'},
	{x: total_width/(480/200), y:total_width/(480/462), w: total_width/(480/128), h:total_width/(480/22), fill: '#ECBD17'},
	{x: total_width/(480/330), y:total_width/(480/462), w: total_width/(480/114), h:total_width/(480/22), fill: '#DBD6D9'},
	{x: total_width/(480/446), y:total_width/(480/270), w: total_width/(480/36), h:total_width/(480/86), fill: '#0D110F'},
	{x: total_width/(480/446), y:total_width/(480/358), w: total_width/(480/36), h:total_width/(480/174), fill: '#1B5B9E'}
];
	
root.selectAll('rect')
	.data(rects).enter()
	.append('rect')
	.attr('x', function(d) {return d.x;})
	.attr('y', function(d) {return d.y;})
	.attr('width', function(d) {return d.w;})
	.attr('height', function(d) {return d.h;})
	.attr('fill', function(d) {return d.fill || '#eef2d1';})
	.attr('stroke-width', total_width/120)
	.attr('stroke', 'black');
</script>
