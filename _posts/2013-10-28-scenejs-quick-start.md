---
layout: post
title: SceneJS Quick Start
description: "Get up and running with SceneJS in two minutes"
modified: 2013-05-31
category: articles
tags: [tutorial, quickstart, plugins]
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Contents</h3>
  </header>  
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

SceneJS is super easy to get started with, thanks to its succinct API with lots of defaults and
   training wheels. But don't let let that simplicity fool you - under that friendly facade it's optimised to death with
   serious tricks like scene compilation and GL state sorting, so it will happily scale up to thousands of
   objects. Let's get into it.

# First example
Let's create this spinning Newell teapot:
<br/><br/>

[![SceneJS First Example]({{ site.url }}/images/firstExample.png)](http://scenejs.org/examples.html?page=firstExample)

[Click here to run this example](http://scenejs.org/examples.html?page=firstExample).

### Step 1. Link to the API
Include the [SceneJS library](api/latest/scenejs.js) in the &lt;head&gt; tag of your web page:

{% highlight html %}
<script src="http://scenejs.org/api/latest/scenejs.js"></script>
{% endhighlight %}

### Step 2. Create a scene
We'll make a spinning blue teapot:

{% highlight javascript %}
var scene = SceneJS.createScene({
    nodes:[
        {
            type:"material",
            color: { r: 0.3, g: 0.3, b: 1.0 },

            nodes:[
                {
                    type: "rotate",
                    id: "myRotate",
                    y: 1.0,
                    angle: 0,

                    nodes: [
                        {
                            type:"prims/teapot"
                        }
                    ]
                }
            ]
        }
    ]
});
{% endhighlight %}

And voilà, there's your blue teapot!

### Step 3. Update the scene
Now let's start the teapot spinning:

{% highlight javascript %}
scene.getNode("myRotate", function(myRotate) {

    var angle = 0;

    scene.on("tick",
        function() {
            myRotate.setAngle(angle += 0.5);
        });
});
{% endhighlight %}

# Plugins
To keep the core library small, SceneJS dynamically loads it's non-core functionality from a directory of
plugins. In the example above, the <code>prims/teapot</code> node is a custom node type instantiated
from a <a href="https://github.com/xeolabs/scenejs/tree/V3.1/api/latest/plugins/node/prims/teapot.js">prims/teapot</a>
plugin, which SceneJS loaded on-demand from <a href="https://github.com/xeolabs/scenejs/tree/V3.1/api/latest/plugins">the
plugins directory</a> within its repository on GitHub.

## Serving your own plugins
If you'd rather serve the plugins yourself, then just copy that directory to your server and configure SceneJS to load
them from there, like this:

{% highlight javascript %}
SceneJS.setConfigs({
    pluginPath: "./foo/myPluginsDir"
});
{% endhighlight %}

Want to write your own plugins? Sweet! Please read more about the plugin API <a
 href="https://github.com/xeolabs/scenejs#plugin-api">here</a>.
