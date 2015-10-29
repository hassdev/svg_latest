<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>svg_path</title>
<style>
	html, body {
		width: 100%;
		height: 100%;
		padding: 0;
		margin: 0;
	}
	body {
		overflow: hidden;
	}

	#wrapper {
		width: 100%;
		min-height: 100%;
		margin: 0 auto;
		position: relative;
	}

	svg {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		margin: 0 auto;
		width: 100%;
		height: 100%;
		outline: 1px solid blue;
	}
</style>
</head>

<body>
	<div id="wrapper">
		<svg id="mysvg" width="300" height="300"></svg>
		<div id="status1"></div><br><br>
		<div id="status2"></div>
	</div>
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
	<script>
		$(document).ready(function() {
			var d = document;
			var mysvg = d.getElementById("mysvg");

			var mx, my, svgw, svgh, xmid, ymid, yini, angle, hyp, hyp_5, hyp_10, random, mx_c, mx_c_5, mx_c_10, my_c, point1, point2, text1, text2, angle, rot;

			//add event to svg element
			mysvg.addEventListener("mousemove", function(e) {
				//acquire mouse position relative to svg
				mx = e.clientX;
				my = e.clientY;

				render();
			});

			setInterval(function() {
				//svg size
				svgw = $("#mysvg").width();
				svgh = $("#mysvg").height();

				//mid point of svg & initial point of y
				xmid = svgw/2;
				ymid = svgh/2;
				yini = svgh - 100;

				//mouse coordinates from starting point
				mx_c = mx - xmid;
				my_c = -(my - yini);

				mx_c_5 = mx_c/5;
				mx_c_10 = mx_c/10;

				//display math status
				angle = my_c/mx_c;
				hyp = Math.sqrt(mx_c*mx_c + my_c*my_c);
				hyp_5 = hyp/5;
				hyp_10 = hyp/10;

				random = {
					a: Math.floor(Math.random()*15),
					b: Math.floor(Math.random()*15),
					c: Math.floor(Math.random()*15),
					d: Math.floor(Math.random()*15),
					e: Math.floor(Math.random()*15),
					f: Math.floor(Math.random()*15),
					g: Math.floor(Math.random()*15),
					h: Math.floor(Math.random()*15),
					i: Math.floor(Math.random()*15),
					j: Math.floor(Math.random()*15),
					k: Math.floor(Math.random()*15),
					l: Math.floor(Math.random()*15),
					m: Math.floor(Math.random()*15),
					n: Math.floor(Math.random()*15),
					o: Math.floor(Math.random()*15),
					p: Math.floor(Math.random()*50),
					q: Math.floor(Math.random()*50),
					r: Math.floor(Math.random()*50),
					s: Math.floor(Math.random()*50),
					t: Math.floor(Math.random()*50),
					u: Math.floor(Math.random()*50),
					v: Math.floor(Math.random()*50),
					w: Math.floor(Math.random()*50),
					x: Math.floor(Math.random()*50),
					y: Math.floor(Math.random()*50),
					z: Math.floor(Math.random()*50)
				};

				point1 = '<circle cx="' + xmid + '" cy="' + ymid + '" r="1" stroke="black" stroke-width="3" fill="red" />';
				text1 = '<text x="' + (xmid+5) + '" y="' + ymid + '" fill="#000">mid point</text>';
				point2 = '<circle cx="' + xmid + '" cy="' + yini	 + '" r="1" stroke="black" stroke-width="3" fill="red" />';
				text2 = '<text x="' + (xmid+5) + '" y="' + yini + '" fill="#000">starting point</text>';
				render();
			}, 100);

			rot = function todeg(angle) {
				var deg = Math.atan(angle)*180/Math.PI;
				deg = Math.abs(deg);
				if(mx_c < 0) {
					deg = ((90-deg) + 270);
				}
				return deg;
			}

			function render() {
				$("#status2").html(rot(angle));
				//display status
				$("#status1").html("mx: " + mx + "<br>my: " + my + "<br><br>mx_c: " + mx_c + "<br>my_c: " + my_c + "<br>mx_c_10: " + mx_c_10 + "<br><br>svg width: " + svgw + "<br>svg height: " + svgh + "<br><br>xmid: " + xmid + "<br>ymid: " + ymid + "<br>yini: " + yini +
					"<br><br>random a: " + random.a + "<br>random b: " + random.b + "<br>random c: " + random.c + "<br>hypotenuse: " + hyp);

				//add path to svg
				//var input = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10) + ',' + 50 + ' ' + (mx_c_5) + ',' + 0 + ' t' + (mx_c_5) + ',' + 0 + ' t' + (mx_c_5) + ',' + 0 + ' t' + (mx_c_5) + ',' + 0 + ' t' + (mx_c_5) + ',' + 0 + ' t' + (mx_c_5) + ',' + 0 + '" stroke="#ddd" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				//var input = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.b) + ',' + (random.z) + ' ' + (mx_c_5+random.c) + ',' + random.f + ' t' + (mx_c_5-random.g) + ',' + random.h + ' t' + (mx_c_5+random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + ' t' + (mx_c_5+random.m) + ',' + random.n + ' t' + (mx_c_5+random.d) + ',' + random.a + '" stroke="#ddd" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				
				var input1 = '<path d="M' + xmid + ',' + yini + ' q' + (hyp_10+random.b) + ',' + (random.z) + ' ' + (hyp_5+random.c) + ',' + random.f + ' t' + (hyp_5-random.g) + ',' + random.h + ' t' + (hyp_5+random.i) + ',' + random.j + ' t' + (hyp_5+random.k) + ',' + random.l + ' t' + (hyp_5+random.m) + ',' + random.n + ' t' + (hyp_5+random.d) + ',' + random.a + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				/*
				var input1 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.b) + ',' + (random.z) + ' ' + (mx_c_5+random.c) + ',' + random.f + ' t' + (mx_c_5-random.g) + ',' + random.h + ' t' + (mx_c_5+random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + ' t' + (mx_c_5+random.m) + ',' + random.n + ' t' + (mx_c_5+random.d) + ',' + random.a + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input2 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.b) + ',' + (-random.y) + ' ' + (mx_c_5+random.a) + ',' + random.b + ' t' + (mx_c_5-random.c) + ',' + random.d + ' t' + (mx_c_5+random.e) + ',' + random.f + ' t' + (mx_c_5+random.g) + ',' + random.h + ' t' + (mx_c_5+random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-3-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input3 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.c) + ',' + (random.x) + ' ' + (mx_c_5+random.d) + ',' + random.e + ' t' + (mx_c_5-random.f) + ',' + random.g + ' t' + (mx_c_5+random.h) + ',' + random.i + ' t' + (mx_c_5+random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-6-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input4 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.d) + ',' + (-random.w) + ' ' + (mx_c_5+random.e) + ',' + random.h + ' t' + (mx_c_5-random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + ' t' + (mx_c_5+random.m) + ',' + random.n + ' t' + (mx_c_5+random.o) + ',' + random.p + ' t' + (mx_c_5+random.q) + ',' + random.r + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-9-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input5 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.e) + ',' + (random.v) + ' ' + (mx_c_5+random.f) + ',' + random.g + ' t' + (mx_c_5-random.h) + ',' + random.i + ' t' + (mx_c_5+random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + ' t' + (mx_c_5+random.p) + ',' + random.q + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-12-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input6 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.f) + ',' + (-random.u) + ' ' + (mx_c_5+random.g) + ',' + random.i + ' t' + (mx_c_5-random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + ' t' + (mx_c_5+random.p) + ',' + random.q + ' t' + (mx_c_5+random.r) + ',' + random.s + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (-15-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input7 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.b) + ',' + (random.y) + ' ' + (mx_c_5+random.a) + ',' + random.b + ' t' + (mx_c_5-random.c) + ',' + random.d + ' t' + (mx_c_5+random.e) + ',' + random.f + ' t' + (mx_c_5+random.g) + ',' + random.h + ' t' + (mx_c_5+random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (3-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input8 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.c) + ',' + (-random.x) + ' ' + (mx_c_5+random.d) + ',' + random.e + ' t' + (mx_c_5-random.f) + ',' + random.g + ' t' + (mx_c_5+random.h) + ',' + random.i + ' t' + (mx_c_5+random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (6-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input9 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.d) + ',' + (random.w) + ' ' + (mx_c_5+random.e) + ',' + random.h + ' t' + (mx_c_5-random.i) + ',' + random.j + ' t' + (mx_c_5+random.k) + ',' + random.l + ' t' + (mx_c_5+random.m) + ',' + random.n + ' t' + (mx_c_5+random.o) + ',' + random.p + ' t' + (mx_c_5+random.q) + ',' + random.r + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (9-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input10 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.e) + ',' + (-random.v) + ' ' + (mx_c_5+random.f) + ',' + random.g + ' t' + (mx_c_5-random.h) + ',' + random.i + ' t' + (mx_c_5+random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + ' t' + (mx_c_5+random.p) + ',' + random.q + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (12-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				var input11 = '<path d="M' + xmid + ',' + yini + ' q' + (mx_c_10+random.f) + ',' + (random.u) + ' ' + (mx_c_5+random.g) + ',' + random.i + ' t' + (mx_c_5-random.j) + ',' + random.k + ' t' + (mx_c_5+random.l) + ',' + random.m + ' t' + (mx_c_5+random.n) + ',' + random.o + ' t' + (mx_c_5+random.p) + ',' + random.q + ' t' + (mx_c_5+random.r) + ',' + random.s + '" stroke="#f2f2f2" stroke-width="1" stroke-linejoin="round" fill="none" transform="rotate(' + (15-rot(angle)) + ' ' + xmid + ' ' + yini + ')" />';
				
				$("#mysvg").html(point1 + point2 + input1 + input2 + input3 + input4 + input5 + input6 + input7 + input8 + input9 + input10 + input11);
				*/
				$("#mysvg").html(point1 + point2 + input1);
				//$("#mysvg").html(point1 + point2 + input);
			}
		});
	</script>
</body>
</html>
